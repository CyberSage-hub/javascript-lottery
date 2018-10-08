### mysql国内源
> http://mirrors.ustc.edu.cn/mysql-ftp/Downloads/MySQL-8.0/
> 例如： http://mirrors.ustc.edu.cn/mysql-ftp/Downloads/MySQL-8.0/mysql-community-server-8.0.12-1.el7.x86_64.rpm


### 各系统安装vm-tools

> CentOS6:

> enable EPEL repository

> yum -y install open-vm-tools

> service vmtoolsd start


> CentOS7:

> yum -y install open-vm-tools

> systemctl start vmtoolsd

> Ubuntu 14.04:

> aptitude update

> aptitude -y install open-vm-tools

### CentOS 7 - 最小化安装后，解决无法使用yum命令问题
1，在shell里面输入：yum --help ，结果显示yum已经正常安装了，但是用不了
2，确保是root账号进行下面操作，如果不是root身份，首先要以root身份登入当前的CentOS 7 
3，在shell里面输入命令：cd /etc/sysconfig/network-scripts ，随后回车，进入这个目录。随后在shell里面输入：ls -a ，随后回车，会显示这个目录里面的所有文件。
4，修改网卡配置文件。“ifcfg-ens33”就是我的网卡配置文件，我用vi编辑它，在shell里面输入：vi ifcfg-ens33 ，随后回车，按"i"键，进入vi编辑模式，现在就可以编辑此文件了！
5，把“ONBOOT”的值修改为"yes"，CentOS最小化安装的网卡默认不跟随系统启用，所以这项的默认值为“no”。修改成"yes"后，直接输入":wq"保存当前修改，退出vi。
6，重启操作系统，在shell里面输入：reboot，随后回车，重启操作系统。
7，验证yum是否可以正常工作了，登入系统后，在shell里面输入：yum grouplist，如果网卡设置正确，那么yum就应该可以正常工作了

### yum install gcc gcc-c++
### Cent OS 安装MySQL-Service警告：... DSA/SHA1 Signature, 密钥 ID 5072e1f5: NOKEY
> 这是由于yum安装了旧版本的GPG keys造成的 解决办法：后面加上  --force --nodeps 
> rpm -ivh mysql-community-server-8.0.12-1.el7.x86_64.rpm --force --nodeps
> 默认mysqld安装在：/usr/sbin/mysqld
> 执行：grep "A temporary password" /var/log/mysqld.log查看初始密码: txoasUGjk0:v
> 安装完成后 sudo mysql_secure_installation 修改密码，密码要设置的很复杂:abcd1234:Aivin.Zhang

> 执行systemctl enable nginx.service报错
> 因为是源码编译安装的nginx，所以需要手动创建：vi /lib/systemd/system/nginx.service
> 设置开机启动：systemctl enable nginx.service
> 提示找不到bzip2，但是明明有安装bzip2  则yum install -y bzip2-devel
> 解压php7源码，在解压后的目录里执行
> 参见文档：https://my.oschina.net/u/144160/blog/540301
> 参见文档：https://www.prosinger.net/compile-php-7-on-centos/
> 参见文档：https://segmentfault.com/a/1190000004123048

> centos7安装mysql8或者mysql5.7参考：https://linuxize.com/post/install-mysql-on-centos-7/

> 下载mysql8.0 rpm包 http://repo.mysql.com/yum/mysql-8.0-community/el/7/x86_64/mysql80-community-release-el7-1.noarch.rpm
> 解压后执行

```bash
./configure --prefix=/usr/local/php7 --with-config-file-path=/usr/local/php7/etc --enable-inline-optimization --disable-debug --disable-rpath --enable-shared --enable-opcache --enable-fpm --with-fpm-user=www --with-fpm-group=www --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd --with-gettext --enable-mbstring --with-iconv --with-openssl --with-mhash --with-openssl --enable-bcmath --enable-soap --with-libxml-dir --enable-pcntl --enable-shmop --enable-sysvmsg --enable-sysvsem --enable-sysvshm --enable-sockets --enable-calendar --enable-wddx --with-gmp --with-curl --with-zlib --enable-zip --with-bz2 --with-gd --enable-exif --with-readline

make && make install
```


> mysql8.0修改密码

> 1，vi /etc/my.cnf,在末尾添加skip-grant-tables

> 2，重启mysql systemctl restart mysqld.service

> 3,登录mysql mysql -u root 注意这里不要加-p

> 4,登录进去后，执行下面语句，重置mysql密码

> ALTER USER 'root'@'localhost' IDENTIFIED BY '23985A.sUg';

> 5,vi /etc/my.cnf,将第一步在末尾添加的skip-grant-tables去掉，重启mysql systemctl restart mysqld.service

> 6,mysql -u root -p 回车，输入刚设置的新密码即可登录

### 安装 GNOME 桌面
<pre>
1、安装命令： yum groupinstall  "GNOME Desktop"  -y
在图形界面使用 ctrl+alt+F2切换到dos界面  
dos界面 ctrl+alt+F2切换回图形界面
在命令上 输入 init 3 命令 切换到dos界面 
输入 init 5命令 切换到图形界面
如果想系统默认以某种方式启动， 使用systemd创建符号链接指向默认运行级别。
修改方法为：
1.首先删除已经存在的符号链接：
rm /etc/systemd/system/default.target 
2.默认级别转换为3(文本模式)： 
ln -sf /lib/systemd/system/multi-user.target /etc/systemd/system/default.target 
或者默认级别转换为5(图形模式)：
ln -sf /lib/systemd/system/graphical.target /etc/systemd/system/default.target 
3.重启：reboot 
</pre>
