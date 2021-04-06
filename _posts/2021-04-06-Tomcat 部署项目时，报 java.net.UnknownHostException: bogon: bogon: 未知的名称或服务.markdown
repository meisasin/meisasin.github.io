---

layout: post

title:  "Tomcat 部署项目时，报 java.net.UnknownHostException: bogon: bogon: 未知的名称或服务(基于 linux 系统)"

date:   2021-04-06 14:00:00 +0800

categories: tomcat

---

<br>

#### 清明放假，公司服务器停机备份，上班后，服务器的主机名不知道为何从 localhost 改为了 bogon，导致 tomcat 启动时找不到相关主机映射。
错误提示：
```
java.net.UnknownHostException: bogon: bogon: 未知的名称或服务
```
 
##### 解决方案
在 hosts 文件中配置 bogon 的主机映射
##### 配置步骤
编辑 `/etc/hosts` 文件，添加 bogon 与主机的映射
```
127.0.0.1   bogon
```
保存退出

---

参考

- [https://blog.csdn.net/weixin_38250126/article/details/69950302](https://blog.csdn.net/weixin_38250126/article/details/69950302)
