---
layout: post
cid: 136
title: C++大作业 高性能计算器
slug: 136
date: 2022/11/11 14:04:00
updated: 2022/11/11 14:15:59
status: publish
author: mi0e
categories: 
  - C/C++
tags: 
customSummary: 
mathjax: auto
noThumbInfoEmoji: 
noThumbInfoStyle: default
outdatedNotice: no
parseWay: auto
reprint: forbidden
thumb: 
thumbChoice: default
thumbDesc: 
thumbSmall: 
thumbStyle: default
---


#### 暂时bug/问题

* 无法计算负数
* 只能整数
* 减法只能前者大于后者
* 无法判断表达式的准确性
* ~~复数实部不能小于0~~
  ***......***
  ~~头秃~~

```cpp
// 标准:GNU C++ 14
// 编译器:GNU GCC 8.1.0 64-bit Debug
#include <bits/stdc++.h>
#define MAX 10000
using namespace std;
stack <char> opt;		// 操作数
stack <string> num;		// 符号位

// 长度判断
int CompareLength(string a, string b) {
	return a.length() >= b.length() ? 1 : 0;
}

// 高精数大小判断
int CompareSize(string a, string b){
	if(a.length() > b.length()) return 1;
	if(a.length() < b.length()) return -1;
	for(int i = 0; i < a.length(); i++){
		if(a[i] > b[i]) return 1;
		if(a[i] < b[i]) return -1;
	}
	return 0;
}

// 高精度加法
string BigAdd(string a, string b) {
	int la, lb, up = 0, temp;	// up进位数
	string n;
	la = a.length();
	lb = b.length();
	if (CompareLength(a, b)) {		// 判断长度，短字符串前端补零
		for (int i = 0; i < la - lb; i++)
			b = "0" + b;
	} else {
		for (int i = 0; i < lb - la; i++)
			a = "0" + a;
	}
	for (int i = max(la, lb) - 1; i >= 0; i--) {
		temp = a[i] - '0' + b[i] - '0' + up;	// 目标 = 被加数 + 加数 + 进位数
		up = temp / 10;			// 进位数
		temp %= 10;
		n += char(temp) + '0';
	}
	if (up != 0) n += char(up) + '0';		// 99 + 1
	reverse(n.begin(), n.end());
	
	return n;
}

// 高精度减法
// 被减数需大于减除
string BigSub(string a, string b) {
	int na[MAX] = {0}, nb[MAX] = {0}, an[MAX] = {0}, la, lb;			// 初始化
	string n;
	la = a.length();
	lb = b.length();
	for (int i = 0; i < la; i++) na[la - i - 1] = a[i] - '0';		// 反转操作数，写入整形数组方便运算
	for (int i = 0; i < lb; i++) nb[lb - i - 1] = b[i] - '0';
	for (int i = 0; i < la; i++) {
		if (na[i] < nb[i]) {			// 借位操作
			na[i] += 10;
			na[i + 1]--;
		}
		an[i] = na[i] - nb[i];
	}
	for (int i = 0; i < la; i++)			// 写入输出
		n += an[i] + '0';
	reverse(n.begin(), n.end());			// 反转目标
	n.erase(0, n.find_first_not_of('0'));			// 去除前导0
	if (n == "") n = "0";			// 100-100
	
	return n;
}

// 高精度乘法
string BigMul(string a, string b) {
	int la, lb, temp_int, up = 0;
	string temp_str, n = "0";
	la = a.length();
	lb = b.length();
	reverse(a.begin(), a.end());			// 反转方便操作
	reverse(b.begin(), b.end());
	for (int i = 0; i < la; i++) {
		for (int j = 0; j < lb; j++) {
			temp_int = (a[i] - '0') * (b[j] - '0') + up;			// 加法同理，进位操作
			up =  temp_int / 10;
			temp_int %= 10;
			temp_str += temp_int + '0';				// 按位写入临时字符串
			if (up && j == lb - 1) temp_str += (char)(up + '0');			// 防止2*5无法进位
		}
		reverse(temp_str.begin(), temp_str.end());
		up = 0;			// 	置空进位符
		for (int j = 0; j < i; j++)	temp_str += "0";			// 移位处理，n+10*i同理
		//		cout << temp_str << endl;
		n = BigAdd(temp_str, n);
		temp_str = "";			// 置空按位乘
	}
	n.erase(0, n.find_first_not_of('0'));			// 0*1
	if (n == "") n = "0";
	
	return n;
}

// 高精度除法
string BigDiv(string a, string b, int flag = 1) {
	string temp = b, n;
	int l = a.length() - b.length();			// 商预操作
	for(int i = 0; i < a.length(); i++) n += "0";			// 商预操作
	for(int i = l; i >= 0; i--){
		for(int j = 0; j < i; j++){			// 被除数添零
			temp += "0";
		}
		while(CompareSize(a, temp) >= 0){
			n[i]++;
			a = BigSub(a, temp);			// 减法模拟
		}
		temp = b;
	}
	reverse(n.begin(), n.end());
	n.erase(0, n.find_first_not_of("0"));
	if (n == "") n = "0";
	
	if(flag) return n;
	else return a;			// a为余数
}

string BigMod(string a, string b) {	
	return BigDiv(a, b, 0); 
}

// 高精快速幂
string BigQuickPow(string a, string b){
	string ans = "1";
	while (b != "0"){
		if(BigDiv(b, "2", 0) == "1"){
			ans = BigMul(ans, a);
		}
		a = BigMul(a, a);
		b = BigDiv(b, "2", 1);
	}
	return ans;
}

// 中缀
int Priority(char a) {		// 符号优先级
	if (a == '+' || a == '-') return 1;
	else if (a == '*' || a == '/' || a == '^') return 2;
	else return -1;
}

void Clc(char tag) {
	string a = num.top();
	num.pop();
	string b = num.top();
	num.pop();
	// 注意出栈顺序
	if (tag == '+') num.push(BigAdd(a, b));
	else if (tag == '-') num.push(BigSub(b, a));
	else if (tag == '*') num.push(BigMul(a, b));
	else if (tag == '/') num.push(BigDiv(b, a));
	else if (tag == '%') num.push(BigMod(b, a));
	else if (tag == '^') num.push(BigQuickPow(b, a));
}

// 整数运算
string InitNum(string str){
	string temp;
	bool flag = false;
	for (int i = 0; i < str.length(); i++) {
		if (str[i] >= '0' && str[i] <= '9') {
			temp += str[i];
			flag = true;			// 为后续判断是否有剩余未入栈，如 1+1
		} else if (flag) {
			num.push(temp);
			temp = "";
			flag = false;
		}
		if (str[i] == '(') opt.push(str[i]);
		if (str[i] == '+' || str[i] == '-' || str[i] == '*' || str[i] == '/' || str[i] == '%' || str[i] == '^') {
			if (opt.empty())	opt.push(str[i]);			// 栈空直接入栈
			else {
				if (Priority(opt.top()) >= Priority(str[i])) {			// 判断优先级，当栈顶大于等于当前操作符，当前操作符不入栈直接运算
					Clc(opt.top());
					opt.pop();
					opt.push(str[i]);			// 运算结束，高优先级出栈，当前操作符入栈
				} else opt.push(str[i]);			// 反之出栈
			}
		}
		if (str[i] == ')') {			// 右括号全出栈，直至栈顶为左括号相匹配结束出栈
			while (opt.top() != '(') {
				Clc(opt.top());
				opt.pop();
			}
			opt.pop();			// 弹出左括号
		}
	}
	if (flag) num.push(temp);			// 标记判断是否有剩余为入栈
	// 操作符平级
	while (!opt.empty()) {			// 循环结束到操作栈为空
		Clc(opt.top());
		opt.pop();
	}
	//	cout << num.top();
	
	return num.top();
}

// 复数运算
complex<long int> Clc_complex(char tag, complex<long int> c1, complex<long int> c2) {
	if (tag == '+')	return c1+c2;
	else if (tag == '-') return c1-c2;
	else if (tag == '*') return c1*c2;
	else if (tag == '/') return c1/c2;
}

string InitComplex(string str){
	string com = "", tempReal = "", tempComplex = "";		// 临时复数、临时实部、临时虚部
	char complexOpt;			// 虚部符号位
	int indexRight, indexLeft;	// 记录括号
	int complexCount;			// 复数个数
	for (int i = 0; i < str.length(); i++)		// 判断复数个数，一个i为一个复数
		if(str[i] == 'i') complexCount++;
	complex<long int> c[complexCount];
	complexCount = 0;
	while(str != ""){
		// 提取复数
		indexRight = str.find('(');
		indexLeft = str.find(')');
		com = str.substr(indexRight, indexLeft + 1);			// 提取复数
		complexOpt = com.find('+')!=string::npos?'+':'-';		// 提取虚部操作符
		tempReal = com.substr(1, com.find(complexOpt) - 1);		// 提取实部
		tempComplex = com.substr(com.find(complexOpt) + 1, com.length() - 4 - tempReal.length());		// 提取虚部，复数总长度 - 括号数 - 符号数 - 实部长度 - 1(i)
//		cout << com.length() << " " <<tempReal << " " << tempComplex << endl;
		c[complexCount] = {stol(tempReal), stol(complexOpt+tempComplex)};
		// 提取完成后擦除
		str.erase(indexRight, indexLeft + 1);
		// 四则运算判断优先级
		if (str[0] == '+' || str[0] == '-' || str[0] == '*' || str[0] == '/') {
			if (opt.empty())	opt.push(str[0]);			// 栈空直接入栈
			else {
				if (Priority(opt.top()) >= Priority(str[0])) {			// 判断优先级，当栈顶大于等于当前操作符，当前操作符不入栈直接运算
					c[complexCount - 1] = Clc_complex(opt.top(), c[complexCount - 1], c[complexCount]);		// 模拟出栈
//					cout << c[complexCount - 1];
					complexCount -= 1;
					opt.pop();
					opt.push(str[0]);			// 运算结束，高优先级出栈，当前操作符入栈
				} else opt.push(str[0]);			// 反之入栈
			}
			str.erase(0, 1);			// 擦除操作符
		}
		complexCount++;
	}
	// 操作符平级依次出栈运算
	while (!opt.empty()) {
		c[complexCount - 2] = Clc_complex(opt.top(), c[complexCount - 2], c[complexCount - 1]);
		complexCount--;
		opt.pop();
	}
//	complexOpt = (c[0].imag() < 0)?'\0':'+';				// 虚部符号位
//	com = to_string(c[0].real()) + complexOpt + to_string(c[0].imag()) + 'i';
	com = to_string(c[0].real()) + ((c[0].imag() < 0) ? to_string(c[0].imag()) + 'i' : complexOpt + to_string(c[0].imag()) + 'i');			// 处理虚部符号位，格式化输出
	
	return com;
}

// 判断复数、实数
string Complex_Or_Real(string str){
	for(int i = 0; i < str.length(); i++){
		if(str[i] == 'i') return InitComplex(str);
	}
	return InitNum(str);
}

int main() {
	string str, a;
	cin >> str;
	a = Complex_Or_Real(str);
	cout << a;
	
	return 0;
}
```
