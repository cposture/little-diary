[TOC]

# yum 安装 Node.js

以 root 身份安装 Node.js

在 Linux 下如何切换用户可以参考：https://blog.csdn.net/qq_32211827/article/details/54292304

在 Linux 下如何安装软件可以参考：https://www.cnblogs.com/qiujun/p/6840984.html

```shell
[erin@VM_29_163_centos ~]$ su root
Password: 
[root@VM_29_163_centos /home/erin]# yum install nodejs
```

最后显示，表示安装成功
```log
Installed:
  nodejs.x86_64 0:0.10.48-3.el6                                                                                                      

Dependency Installed:
  libuv.x86_64 1:0.10.34-1.el6                                                                                                      

Complete!
```

# 源码安装 Node.js

源码安装教程的官方文档：`https://github.com/nodejs/node/blob/master/BUILDING.md#building-nodejs-on-supported-platforms`

## 下载源码

到官网上查看最新版本 Node.js 的下载地址：`https://nodejs.org/dist/v8.11.1/node-v8.11.1.tar.gz`
在 Linux 下下载源码：`wget https://nodejs.org/dist/v8.11.1/node-v8.11.1.tar.gz`

## 依赖

1. gcc and g++ 4.9.4 or newer, or
2. clang and clang++ 3.4.2 or newer (macOS: latest Xcode Command Line Tools)
3. Python 2.6 or 2.7
4. GNU Make 3.81 or newer

## 遇到问题

升级 gcc 版本到 4.9.4：http://robbiefeng.iteye.com/blog/2163305，其中报错：

1. `centos zlib.h: No such file or directory` 时需要安装 `zlib-devel`，命令如下：

```
yum install zlib-devel
```

2. 编译 gcc 时，遇到 `make[3]: *** [s-attrtab] Killedmake[3]: *** Waiting for unfinished jobs....`，原因时内存不足，centos 有没有设置 swap file，导致没有虚拟内存，参考文档：http://www.cjjjs.com/paper/czxt/20173320112942.aspx

nodejs ：make install 报 `libstdc++.so.6 GLIBCXX 错误`

```
[root@VM_29_163_centos /usr/lib64]# rm libstdc++.so.6
rm: remove symbolic link `libstdc++.so.6'? y
[root@VM_29_163_centos /usr/lib64]# ln -s /usr/local/gcc/lib64/libstdc++.so.6 libstdc++.so.6
```














