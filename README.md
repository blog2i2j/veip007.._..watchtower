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

### 已运行状态下更新
```
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower -c --run-once 容器名1 容器名2
```
`--run - once`运行一次，若设置时间间隔使用`--interval`

### 群辉推荐
创建一个txt文件，例如：/volume1/docker/watchtower/5.txt  将镜像名称写进目录，一行一个
创建一个sh文件，例如：up.sh
```bash
#!/bin/bash

# 读取容器名称列表
containers=$(cat /volume1/docker/watchtower/5.txt)

# 调用 Watchtower 更新指定的容器
for container in $containers; do
  docker run --rm \
    -v /var/run/docker.sock:/var/run/docker.sock \
    docker.lefu.men/containrrr/watchtower $container
```
设置定时运行up.sh即可
