2022.10.11 所有组件都是最新的
0.关闭防火墙 service firewalld stop

1.创建mysql数据库并执行sql下的文件 ry-seta (ry_seata_20210128.sql) ry-config(ry_config_20220929.sql) ry-cloud(ry_20220814.sql|quartz.sql)

2.下载nacos(项目中已下载) 用docker.nacos.conf 下的 application.properties 替代 nacos/conf/application.properties
   修改 mysql 的ip和密码
   直接启动nacos即可 

3.进入nacos修改各服务redis及mysql的ip和密码

4.下载sentinel控制台的jar包(项目中已下载) https://github.com/alibaba/spring-cloud-alibaba/wiki/Sentinel
   直接启动sentinel即可 
   启动命令已放在bin/run-sentinel.bat中  java -Dserver.port=8718 -Dcsp.sentinel.dashboard.server=localhost:8718 -Dproject.name=sentinel-dashboard -jar sentinel-dashboard.jar

5.bin包下的bat命令逐个启动

6.项目地址 http://localhost:80/  账号密码: admin admin123
  sentinel地址 http://127.0.0.1:8718/  账号密码: sentinel sentinel
  nacos地址 http://172.168.10.108:8848/nacos 账号密码: nacos nacos
  springBootAdmin地址 http://localhost:9100/wallboard 账号密码: ruoyi 123456

与原项目相比的改动点：
    0.修复了 docker/docker-compose.yml/ruoyi-nacos.links 缺失 ruoyi-mysql 问题
    1.新增了 nacos-server-2.1.1.zip
    2.新增了 bin/run-sentinel.bat
    3.新增了 bin/sentinel-dashboard.jar
    4.各个dockerfile更新nacos域名参数
    5.修改nacos镜像版本为v2.0.4，其它版本可能不兼容
问题点记录：
    第一次 ./deploy.sh base 时nacos可能启动失败，生成mysql成功的话需要重启nacos