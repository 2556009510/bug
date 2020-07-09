### 1、**安装mysql Install/Remove of the Service Denied!错误的解决办法**

```
报错：

Install/Remove of the Service Denied

解决办法：

打开cmd.exe程序的时候选择“用管理员身份打开”
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

### 2、MySQL5.7配置

**方式一**

**https://www.jianshu.com/p/18762ddb6060**

\1. 安装

```
#1. 检查mariadb包

rpm -qa|grep mariadb

#2. #将检查到mariadb卸载

rpm -e --nodeps mariadb-libs-5.5.64-1.el7.x86_64

#3. 授权

chmod -R 777 /tmp

#4. 安装，注意安装顺序

rpm -ivh mysql-community-common-5.7.29-1.el7.x86_64.rpm

rpm -ivh mysql-community-libs-5.7.29-1.el7.x86_64.rpm

rpm -ivh mysql-community-client-5.7.29-1.el7.x86_64.rpm

rpm -ivh mysql-community-server-5.7.29-1.el7.x86_64.rpm

#安装server报Failed dependencies:libnuma.so......，则安装numactl

yum install -y numactl
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

\2. 初始化与修改密码

```
#1. 初始化

mysqld --initialize --user=mysql

#2. 启动服务

systemctl start mysqld.service

#3. 查看初始化密码，一共12位

grep 'temporary password'  /var/log/mysqld.log

#4. 登陆

mysql -uroot -p

#5. 修改密码

ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

\3. 授予MySQL远程连接

```
#1. 授权

grant all privileges on *.* to root@'%' identified by 'root';

#2. 刷新权限

flush privileges;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

\4. 关闭防火墙

```
# 本次关闭

systemctl stop firewalld.service

# 永久关闭

systemctl disable firewalld.service
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

\5. 卸载

```
#1. 检查

rpm -qa|grep -i mysql

#2. 关闭服务

systemctl stop mysqld.service

#3. 卸载，注意顺序

rpm -ev --nodeps mysql-community-client-5.7.29-1.el7.x86_64

rpm -ev --nodeps mysql-community-server-5.7.29-1.el7.x86_64

rpm -ev --nodeps mysql-community-common-5.7.29-1.el7.x86_64

rpm -ev --nodeps mysql-community-libs-5.7.29-1.el7.x86_64

#4. 查找目录

find / -name mysql

#5. 删除查到的目录

rm -rf ...

#6. 再次检查确认

rpm -qa|grep -i mysql
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**方式二：（暴力删除）**

**参考以下两个链接：**

https://blog.csdn.net/TD520314/article/details/80461545

http://www.cppcns.com/shujuku/mysql/220587.html

### **3、mysql忘记密码解决方案及三种方式修改密码**

https://blog.csdn.net/xl_1803/article/details/82503781?utm_medium=distribute.pc_relevant.none-task-blog-baidujs-3

mysql用户分为root用户（超级管理员，拥有所有权限）和普通用户，mysql服务器通过权限表来控制用户对数据库的访问,这些权限表存于root用户下的mysql数据库中。



在使用mysql数据库过程中，往往需要修改密码的操作，下面介绍三种修改密码的方式：

1、使用mysqladmin命令在命令行指定新密码

```
mysqladmin -u root -p password ‘新密码’
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

回车，将提醒你输入原密码：

![img](https://img-blog.csdnimg.cn/20200709104402210.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NTA0MjU2OQ==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2、使用set语句

```
set password=password(“新密码”)
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

这时需要重启mysql服务器或使用flush privileges语句刷新权限表,使新密码生效

3、修改user表

```
update mysql.user set authentication_string=PASSWORD("123456") where user="root" and host="localhost"
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

注意，mysql新版本用于存用户密码的字段名为authentication_string而不是 password，且新密码必须使用password函数进行加密

4、mysql8.0修改密码语句

```
ALTER USER 'root'@'localhost' IDENTIFIED BY 'ok';
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

如遇报错，先执行flush privileges

**========================================================****=====================================**

另外，不知道小伙伴们有没有遇到过忘记密码的情况呢？其实忘记密码很容易解决，下面就介绍忘记密码时的解决方案：

**第一步：**在命令行输入net stop mysql命令关闭mysql服务

**第二步：**使用--skip-grant-tables选项启动mysql服务（服务器将不加载权限判断，任何用户 都能访问数据库）

​              在命令行输入 

```
mysqld --skip-grant-tables
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

​              命令运行之后，用户无法再输入指令，此时如果在任务管理器中可以看到名称为 mysqld的进程，则表示可以用root用户                登录服务器了

**第三步：**打开另一个命令行窗口，输入不加密码的登录命令

```
mysql -u root
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

​              登录成功后可以使用update语句修改密码

​              修改完成后，必须使用flush privileges语句刷新权限表，这样新的密码才能生效

**第四步：**将输入mysqld --skip-grant-tables命令的命令行窗口关闭，接下来就可以使用新密码登录mysql服务器了

```
mysqld --skip-grant-tables
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

