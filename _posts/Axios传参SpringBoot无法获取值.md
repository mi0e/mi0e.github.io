---
title: Axios传参SpringBoot无法获取值
date: 2023-05-21 15:43:43
tags:
---

学习SpringBoot时发现前端Axios发送的data无法被后端接收

后端

```java
@PostMapping("/user/bot/add/")
public Map<String, String> add(@RequestParam Map<String, String> map) {
    System.out.println(map);
    return addService.add(map);
}
```

前端

```
const headers = {
     'Authorization': 'Bearer ' + localStorage.getItem('jwt_token'),
};

let postUrl = (url: string, data: any, headers: any) => {
     return new Promise((resolve, reject) => {
          axios.post(url, data, { headers })
              .then(response => {
                   resolve(response.data);
              })
              .catch(error => {
                   reject(error);
              });
     });
};
```

## 解决方法

axios默认发送的 `header.Content-Type`为 `json`格式，即 `Content-Type:application/json`，

如果需要后端处理数据，需添加header：`Content-Type:application/x-www-form-urlencoded`