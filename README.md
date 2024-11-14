### 安装
```
docker run -d \
--name watchtower \
-v /var/run/docker.sock:/var/run/docker.sock \
--restart=always \
containrrr/watchtower
```

### 按照特定名更新
```
docker run -d \
--name watchtower \
-v /var/run/docker.sock:/var/run/docker.sock \
--restart=always \
containrrr/watchtower 容器名1 容器名1
```

### 指定时间更新 
```
docker run -d \
--name watchtower \
-v /var/run/docker.sock:/var/run/docker.sock \
--restart=always \
containrrr/watchtower --interval 3600
```
以上为3600秒更新一次，可叠加特定名称

### 按照文本内名单更新
```
docker run -d \
  --name watchtower \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /path/to/5.txt:/config/5.txt \
  containrrr/watchtower --label-enable
```
watch.txt为文件名， -file为文件路径。需把文件名单放在5.txt内
