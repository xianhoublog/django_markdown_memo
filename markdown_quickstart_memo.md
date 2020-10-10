# Markdown 快速入门(typora)

## 1.代码块

```java
//代码块语法：
​```java
    
​```shell
```

**1.java**

```java

package com.yrp.po;

import javax.persistence.*;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

@Entity
@Table(name = "t_user")
public class User {

    @Id
    @GeneratedValue
    private Long id;
    private String nickname;
    private String username;
    private String password;
    private String email;
    private String avatar;
    private Integer type;
    @Temporal(TemporalType.TIMESTAMP)
    private Date createTime;
    @Temporal(TemporalType.TIMESTAMP)
    private Date updateTime;

    @OneToMany(mappedBy = "user")
    private List<Blog> blogs = new ArrayList<>();

    public User() {
    }

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getNickname() {
        return nickname;
    }

    public void setNickname(String nickname) {
        this.nickname = nickname;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getAvatar() {
        return avatar;
    }

    public void setAvatar(String avatar) {
        this.avatar = avatar;
    }

    public Integer getType() {
        return type;
    }

    public void setType(Integer type) {
        this.type = type;
    }

    public Date getCreateTime() {
        return createTime;
    }

    public void setCreateTime(Date createTime) {
        this.createTime = createTime;
    }

    public Date getUpdateTime() {
        return updateTime;
    }

    public void setUpdateTime(Date updateTime) {
        this.updateTime = updateTime;
    }


    public List<Blog> getBlogs() {
        return blogs;
    }

    public void setBlogs(List<Blog> blogs) {
        this.blogs = blogs;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", nickname='" + nickname + '\'' +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", email='" + email + '\'' +
                ", avatar='" + avatar + '\'' +
                ", type=" + type +
                ", createTime=" + createTime +
                ", updateTime=" + updateTime +
                '}';
    }
}

```

**2.shell**

```shell
//Linux下sprint项目的启动命令
# java -jar blog start
```



## 2.标题

```java
//标题语法
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
    
    

```

# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题



## 3.字体

```java
// 加粗
**等不到天了黑**
// 代码高亮显示
==我是仙==
// 删除线
~~被删除了~~
// 斜体
*斜体内容*

```

// 加粗
**等不到天了黑**
// 代码高亮显示
    ==我是仙==
// 删除线
    ~~被删除了~~
// 斜体
    *斜体内容*



## 4.引用：

```java
//引用语法：
> author: nduan
>> author : nduan
>>> author : nduan
     

```

> author: nduan
> > author : nduan
> >
> > > author : nduan

## 5. 分割线

```java
//分割线
---
//分割线2
***
```

---

***

## 6. 图片插入

```java
//在线图片/本地图片
![图片名称](/image/me.png) --图片路径
```

![我的图片](C:\Users\nduan\Pictures\Camera Roll\b.jpg)



## 7.超链接

```java
//超链接语法
[我的github](https://github.com/yerenping)

```

[我的github](https://github.com/yerenping)

## 8. 列表

```java
//无序列表
- 目录1
- 目录2
- 目录3

//有序列表 //1. + 名称
    1. 首页
    2. 分类
    3. 标签

```

- 目录1

- 目录2

- 目录3

  

  1. 首页
  2. 分类
  3. 标签

  

## 9.表格

| 性别 | 名字  | 年龄 |
| ---- | ----- | ---- |
| 女   | alis  | 18   |
| 男   | lucy  | 18   |
| 男   | aldon | 20   |

