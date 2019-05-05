图片资源
--


## 1、php

* **版本**

> 7.2.15，具体的版本信息如下

```
	PHP 7.2.15 (cli) (built: Feb  9 2019 03:10:54) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
    with Zend OPcache v7.2.15, Copyright (c) 1999-2018, by Zend Technologies
```

* **扩展**

> 额外的PECL扩展为
> 
>  * redis ~ 版本需要 4.3.0 及以上（集群密码）
>  * yaf ~ 版本 3.0.0 及以上（php7需要）
>  * protobuf ~ 版本需要 3.6.0 及以上（新版的PB类）  
> 


* **配置**

> 对应默认配置的修改项如下
> 对应的 YAF 配置必须增加
> 默认的 YAF 配置不支持namespace方式

```
date.timezone = Asia/Shanghai
post_max_size = 8M
upload_max_filesize = 8M

[yaf]

yaf.use_namespace = 1
yaf.lowcase_path = 1
yaf.use_spl_autoload = 1
```

	SESSION对应的配置根据服务器的需求配置！

# 2、nginx

	无特殊要求，对应dcoker中的版本信息如下：

```
nginx version: nginx/1.15.8
built by gcc 8.2.0 (Alpine 8.2.0) 
built with OpenSSL 1.1.1a  20 Nov 2018
TLS SNI support enabled
```

# 3、MySQL

	5.6 之上的版本，  
	开发环境中使用了mysql最新的版本，  
	对应docker中的MySQL版本信息如下：
```
mysql  Ver 8.0.15 for Linux on x86_64 (MySQL Community Server - GPL)
```

# 4、REDIS

	3.0 以上版本（配置集群）  
	开发环境中使用了redis最新的版本，  
	对应docker中的redis版本信息如下：

```
Redis server v=5.0.3 sha=00000000:0 malloc=jemalloc-5.1.0 bits=64 build=6b31184a90f362f2
--
redis-cli 5.0.3
```

# 二、配置中心

	配置中心的文件跟之前一样，对应使用到的文件如下：

## 1、网站域名相关配置

	/data/configs/domain/php/xxxx.php

## 2、日志目录

	配配置对应日志目录相关路径，对应配置的目录需要有读写权限！

* /data/configs/log/php/web.php

## 3、appid 相关配置

	用于调用bip接口做签名验证，对应文件路径如下

* /data/configs/appid/php/{APPID}.php  



# 三、代码发布

> 对应的 nginx 配置的重写规则如下：

```
location / {
    try_files $uri $uri/ /index.php$is_args$args;
}
```



```

# 四、注意事项

## 1、php.ini 里的 yaf 配置

```
[yaf]

yaf.use_namespace = 1
yaf.lowcase_path = 1
yaf.use_spl_autoload = 1
```

## 2、日志目录的创建

	对应文件日志目录由
	/data/configs/log/php/web.php  
	文件中的配置决定，  
	发布时需要管理员创建对应的目录  
	并赋于对应的写入权限！  

## 3、关于 redis 集群

	phpredis扩展使用设置了密码的集群需要 4.3.0 及以上的版本；  
	redis对应的配置文件中，集群的服务器需要加上 type 值配置！  
```
	type = cluster-master | cluster-slaver  
```
	否则，程序用普通方式连接上redis集群的服务器时，连接成功，但写入数据失败！

## 4、php.ini 中的 session 配置

	使用了SESSION项目，对应的php.ini里需要修改session配置，  
	目前 使用 phpredis 做 session 的存储与共享！  
	如下：  
```
session.save_handler = "redis"
session.save_path = "tcp://host1:6379?weight=1, tcp://host2:6379?weight=2&timeout=2.5, tcp://host3:6379?weight=2&read_timeout=2.5"
```


## 5、php 的软链接

	增加 php 的软链接到 /usr/bin/php  
	对应 shell 的任务可以直接使用 php 命令
