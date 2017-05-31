---
layout:     post
title:      "SpringMVCDemo"
date:       2016-05-23
---

<style type="text/css">
p{
	text-indent: 2em;
}
.post img {
  margin-bottom: 0rem;
}
</style>

--------


### 项目来源[使用IntelliJ IDEA开发SpringMVC网站](https://github.com/gaussic/SpringMVCDemo).

### 详细步骤[SpringMVCDemo](http://my.oschina.net/gaussik/blog/385697).

###相关环境配置

* Intellij IDEA 15.0.4 Ultimate
* Tomcat 7.0.68
* JDK 1.7.0_80
* Spring 3.2.0
* MySql 5.7
* Maven 3.3.9
* Bootstrap 3.3.5

### 遇到问题
* 数据库连不通问题：com.mysql.jdbc.exceptions.jdbc4.MySQLNonTransientConnectionException: Could not create connection to database server

-在persistent.xml配置文件中的数据库连接的URL地址中的端口是**3306**，而不是web环境中的8080.
>     <property name="hibernate.connection.url" value="jdbc:mysql://localhost:3306/springdemo"/>


* 在用户**修改**操作功能时，点击提交无反应。
![update-pic.jpg]({{ '/assets/img/SpringMVCDemo/update-pic.jpg' | prepend: site.baseurl }})

>      可能是在updateUser.jsp页面中缺少添加语句：   <%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>

*更新时间2016-05-24 16：43*




