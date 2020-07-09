# cmd：

### 1、检测是否安装： 

如mysql -V**（V要大写）**



------

# Linux：

### 1、**command not found...**

![img](https://img-blog.csdnimg.cn/20200709103113415.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==) 

linux中出现基本命令找不到的问题，经过查找发现是/etc/profile文件出现了问题，解决方案如下：

添加（注意路径，一般都是如下默认的）：

```
[root@master~]:#export PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



------

# Maven：

### 1、maven配置问题：![img](https://img-blog.csdnimg.cn/20200709103243220.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

https://blog.csdn.net/Michael_Shin/article/details/103745238?utm_medium=distribute.pc_relevant.none-task-blog-baidujs-4



------

# 数据库软件：

### 1、导入sql文件（五种链接都相似）

https://www.php.cn/tool/navicat/428550.html

https://blog.csdn.net/qq_37306670/article/details/85604063

https://jingyan.baidu.com/article/a24b33cd2de7e219ff002b6b.htmlhttps://jingyan.baidu.com/article/a24b33cd2de7e219ff002b6b.html



### 2、[**ERROR 1044 (42000): Access denied for user 'root'@'localhost'**](https://www.cnblogs.com/kerrycode/p/9198566.html)

原因一：卸载MySQL5.7后，装上8.0需要新建MySQL：

![img](https://img-blog.csdnimg.cn/2020070910361038.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTA0MjU2OQ==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

解决办法：新建MySQL

![img](https://img-blog.csdnimg.cn/20200709103647275.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)  ![img](https://img-blog.csdnimg.cn/2020070910365070.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)  ![img](https://img-blog.csdnimg.cn/20200709103653652.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

