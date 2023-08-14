---
layout: post
cid: 21
title: ArrayList列表集合
slug: 21
date: 2020/12/24 20:57:00
updated: 2021/03/21 16:04:39
status: publish
author: mi0e
categories: 
  - 编程
  - Java
tags: 
customSummary: 
noThumbInfoStyle: default
outdatedNotice: no
reprint: standard
thumb: 
thumbChoice: default
thumbDesc: 
thumbSmall: 
thumbStyle: default
---

```java
    List<Type> variable = new ArrayList<>([size]);

// Type：int String method ...
// size：可省 

    class user{
    	private String name;
    	private int age;
    	public user(String string, int i) {
    		this.name = string;
    		this.age = i;
    	}
    	public String getName() {
    		return name;
    	}
    	public int getAge() {
    		return age;
    	}
    }

    	List<user> list = new ArrayList<>();
    	list.add(new user("张三",15));
```

----------


集合的遍历：

方法一

```java
    for (int i = 0; i < list.size(); i++) {
    	System.out.print(list.get(i).getName());
    	System.out.println(list.get(i).getAge());
    }
```

方法二

```java
    for (user user : list) {
        System.out.println(user.getAge() + user.getName());
    }
```

