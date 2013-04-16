0、安装DSS
==========
可选，方便操作

1、下载安装ERLANG
=================
http://www.erlang.org/download.html

2、下载安装TSUNG
================
http://tsung.erlang-projects.org/dist/

3、安装依赖
===========
http://www.template-toolkit.org/download/index.html

tar zxvf Templat......
perl Makefile.PL
make
make install

yum install gnuplot gd libpng zlib


4、在多台服务器上重复以上步骤
=============================
RT

5、下载配置XML文件，并修改配置
==============================
github上有

6、开始分布式压测
=================
tsung -f http_distrubed.xml start

7、说明：
========
每个机器用2个IP，每个IP理论上可以产生65535个请求，实际上不可能那么多，而且也会被封禁...

最终的方式是，修改本机的/etc/hosts文件，将要测试的地址导向一个自己的服务器，在内网中使用尽可能多的私有IP地址，去模拟大量请求...

这样每台服务器最多可以产生数十万的用户请求（别在1U服务器上使用），并且随机分布效果很好....

配置文件为集群测试，可以配置数百台机器瞬时产生上千万的流量都是可能的...

我测试的时候使用了3台机器，瞬时模拟了请求并同步监控了嵌入服务器的负载情况...

具体配置见XML...文件

8、报告
=======
cd /root/.tsung/log/20120329-2234
/usr/local/lib/tsung/bin/tsung_stats.pl

生成的report.html即为报告文件...