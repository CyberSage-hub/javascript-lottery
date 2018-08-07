### mysql国内源
http://mirrors.ustc.edu.cn/mysql-ftp/Downloads/MySQL-8.0/
例如：
http://mirrors.ustc.edu.cn/mysql-ftp/Downloads/MySQL-8.0/mysql-community-server-8.0.12-1.el7.x86_64.rpm

### 各系统安装vm-tools
CentOS6:
enable EPEL repository
yum -y install open-vm-tools
service vmtoolsd start

CentOS7:
yum -y install open-vm-tools
systemctl start vmtoolsd

Ubuntu 14.04:
aptitude update
aptitude -y install open-vm-tools

### CentOS 7 - 最小化安装后，解决无法使用yum命令问题
1，在shell里面输入：yum --help ，结果显示yum已经正常安装了，但是用不了
2，确保是root账号进行下面操作，如果不是root身份，首先要以root身份登入当前的CentOS 7 
3，在shell里面输入命令：cd /etc/sysconfig/network-scripts ，随后回车，进入这个目录。随后在shell里面输入：ls -a ，随后回车，会显示这个目录里面的所有文件。
4，修改网卡配置文件。“ifcfg-ens33”就是我的网卡配置文件，我用vi编辑它，在shell里面输入：vi ifcfg-ens33 ，随后回车，按"i"键，进入vi编辑模式，现在就可以编辑此文件了！
5，把“ONBOOT”的值修改为"yes"，CentOS最小化安装的网卡默认不跟随系统启用，所以这项的默认值为“no”。修改成"yes"后，直接输入":wq"保存当前修改，退出vi。
6，重启操作系统，在shell里面输入：reboot，随后回车，重启操作系统。
7，验证yum是否可以正常工作了，登入系统后，在shell里面输入：yum grouplist，如果网卡设置正确，那么yum就应该可以正常工作了

### yum install gcc gcc-c++
