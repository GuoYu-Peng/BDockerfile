**镜像 uid, gid**
有些 dockerfile 添加了 GROUP_ID, USER_ID, USER_NAME 变量，在构建镜像时传入指定 gid, uid 和用户名  
```bash
docker build -t tag_name --build-arg USER_ID=$(id -u) --build-arg GROUP_ID=$(id -g) --build-arg USER_NAME=user_name .
```

这样创建的镜像跟主机 gid, uid 相同，避免一些文件权限问题。
