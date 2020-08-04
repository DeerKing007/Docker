# 一、安装

https://docs.docker.com/engine/install/ubuntu/

### 1.卸载旧版

```
sudo apt-get remove docker docker-engine docker.io containerd runc
```

### 2.install packages to allow apt to use a repository over HTTPS:

```
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
```

### 3.Add Docker’s official GPG key:

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

#####验证：

```
sudo apt-key fingerprint 0EBFCD88
```

### 4.set up the stable repository

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

### 5.Install Docker Engine

```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

#####验证：

```
sudo docker run hello-world
```

##### 更新：

```
sudo apt-get update
```

# 二、使用-上传自己的镜像

https://docs.docker.com/docker-hub/

### 1.注册Docker Hub

### 2.创一个仓库

### 3.在Ubuntu上登录

```
sudo docker login
```

### 4.创一个Dockerfile

```
cat > Dockerfile <<EOF
FROM busybox
CMD echo "Hello world! This is my first Docker image."
EOF
```

### 5.build your Docker image

```
sudo docker build -t <your_username>/my-first-repo .
```

最后那个点是Dockerfile的路径

### 6.查看本地有哪些镜像

```
sudo docker image ls
```

### 7.Test your docker image locally

```
sudo docker run <your_username>/my-first-repo
```

### 8. push your Docker image to Docker Hub

```
docker push <your_username>/my-first-repo
```

### 9.退出登录

```
docker logout
```

# 三、使用-使用镜像

https://github.com/docker/labs/blob/master/beginner/chapters/alpine.md

```
sudo docker pull alpine
sudo docker run alpine ls -l
sudo docker run alpine echo "hello from alpine"
sudo docker run -it alpine /bin/sh
exit
sudo docker ps
sudo docker ps -a
```

