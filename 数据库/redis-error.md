# 2019-8-21-redis-error（一）

window 下出现[14748] 17 Jul 21:15:54.400 # Creating Server TCP listening socket 127.0.0.1:6379: bind: NO ERROR

如下按顺序输入如下命令就可以连接成功

```
1. Redis-cli.exe
2. shutdown
3. exit
4. redis-server.exe redis.windows.conf
   
```

