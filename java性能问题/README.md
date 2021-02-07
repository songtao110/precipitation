# 线上问题排查 
[一套完整的 Java 线上故障排查技巧](https://mp.weixin.qq.com/s/03qoBFLpvkRVhaorwCNJ5Q)

arthas安装使用
```
 [root ~]# mkdir arthas
 [root ~]# cd arthas/
 [root ~]#  wget https://maven.aliyun.com/repository/public/com/taobao/arthas/arthas-packaging/3.1.4/arthas-packaging-3.1.4-bin.zip
 [root ~]# rm -rf /home/admin/.arthas/lib/*
 [root ~]# cd arthas
 [root ~]# ./install-local.sh
 [root ~]# java -jar arthas-boot.jar

```
