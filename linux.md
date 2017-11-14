# linux

### shell的环境变量相关

#### 查看环境变量: env

#### 设置和删除变量：export unset,这些环境变量只在当前shell有效

#### 环境变量加载顺序

1./etc/profile:此文件为系统的每个用户设置环境信息,当用户第一次登录时,该文件被执行

2./etc/bashrc:为每一个运行bash shell的用户执行此文件.当bash shell被打开时,该文件被读取.

3.~/.bash_profile:每个用户都可使用该文件输入专用于自己使用的shell信息,当用户登录时,该文件仅仅执行一次!默认情况下,他设置一些环境变量,执行用户的.bashrc文件.

4.~/.bashrc:该文件包含专用于你的bash shell的bash信息,当登录时以及每次打开新的shell时,该文件被读取.

5.~/.bash_logout:当每次退出系统(退出bash shell)时,执行该文件.
