
# 服务器
```
centos8 配置4核4G以上 硬盘最好大一点为了放日志 100G以上

```
#  软件
```
Node 版本 v16.13.1  

Redis  版本 6.2.6

```
# 项目配置修改

### 打开conf/config.js 文件修改对应的配置项

```
web_api_trx_domain = "http://aaaa.xxx.com/rsync/trx_trans.php" //注意这个域名主要是为了接收trx交易异步通知

web_api_usdt_domain = "http://aaaa.xxx.com/rsync/usdt_trans.php" //注意这个域名主要是为了接收usdt的异步通知


montor_contract_address = 'TR7NHqjeKQxGTCi8q8ZY4pL8otSzgjLj6t' ;//监控的合约地址 改成你要监控的合约地址哈 

Environmental  =   1   // 0：测试网络 1：正式网络环境,只需要修改这个即可  一般使用正式网络 一般使用1 这个就用1

tronWebAPiKey = '707521d2-5831-4b71-85cd-a82a327c377a' //请去官网申请  https://www.trongrid.io/



```

# 命令行切换到项目目录

```
cd   server_trx

npm install //安装依赖包

npm install -g pm2 //安装pm2守护 

node server.js //测试是否正常

pm2 start startServer.json   //让服务在后台保持运行
```


# 监控

#### 启动trx监控
```
pm2 start monitor_block_trx.js

```


#### 启动合约代币监控
```
pm2 start monitor_block_usdt.js

```

###注意事项
```
1：如果改了代码 ，请重启node服务 可以使用 pm2 restart all 启动
2：pm2 如果不知道咋使用的 请百度下 这个请学习下

```

##异步回调接收
####php代码参考
```
<?php 
$str = file_get_contents("php://input");
file_put_contents("/tmp/log.txt" , $str , FILE_APPEND );//写入日志
```
