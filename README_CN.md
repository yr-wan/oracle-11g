[English](README.md) | 中文
用于运行Oracle Database 11g Standard / Enterprise的镜像。 由于oracle许可证限制，镜像本身不包含数据库，因此将在第一次从运行时安装。

``此镜像仅供开发使用``

# 使用方法
从[Oracle官网](http://www.oracle.com/technetwork/database/in-memory/downloads/index.html)下载数据库安装文件，并将其解压到 **install_folder**

运行容器，自动安装oracle并创建数据库：

```sh
docker run --privileged --name oracle11g -p 1521:1521 -v <install_folder>:/install jaspeen/oracle-11g
```
此外，你可以提交此容器以便后续安装和配置oracle数据库：
```sh
docker commit oracle11g oracle11g-installed
```

数据库的安装路径为： **/opt/oracle** 

系统用户：
* root/install
* oracle/install

数据库用户：
* SYS/oracle

（可选）可以在创建容器时映射dpdump文件夹，以便更容易地上传dump文件：
```sh
docker run --privileged --name oracle11g -p 1521:1521 -v <install_folder>:/install -v <local_dpdump>:/opt/oracle/dpdump jaspeen/oracle-11g
```
如需执行impdp/expdp命令，需使用如下docker exec命令：
```sh
docker exec -it oracle11g impdp ..
```
