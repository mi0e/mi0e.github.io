---
layout: post
cid: 151
title: C++ 提取小数
slug: 151
date: 2022/12/06 17:45:00
updated: 2022/12/06 18:09:59
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
reprint: standard
thumb: 
thumbChoice: default
thumbDesc: 
thumbSmall: 
thumbStyle: default
---


OpenAi写的一段代码，太值得学习了

~~自己写for循环提取小数实在是太蠢了~~

## copy

```cpp
std::copy(start, end, std::back_inserter(container));

std::copy(iterator source_first, iterator source_end, iterator target_start);
```

因为第三个参数要接受一个迭代器，所以需要使用`back_inserter(container)`

## regex

pass

```cpp
string expression = "4.12*3.14";
regex pattern("([\\d.]+)|([+\\-*/()])");
vector<string> words;
copy(
	sregex_token_iterator(expression.begin(), expression.end(), pattern),
	sregex_token_iterator(),
	back_inserter(words));

for(int i = 0; i < words.size(); i++)
	cout << words[i] << endl;

```
