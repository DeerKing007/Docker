# DockerHub

###上传镜像到dockerhub：

终端输入：

$ ~ docker login --username=zhangpeng0v0

输入密码

查看镜像：

$ ~ docker images

对将推送的镜像进行标记

$ docker tag e0373ff33a19 zhangpeng0v0/pnc_venv:venv

现在推送镜像：

$ ~  docker push zhangpeng0v0/pnc_venv

推送指向的是 docker.io/zhangpeng0v0/pnc_venv 仓库：

​		一旦完成，打开 DockerHub，登录账户，就能看到Docker 镜像。任何人都可以部署你的镜像。这是开发软件和发布软件最简单，最快速的方式。无论你何时更新镜像，用户都可以简单地运行：

$ ~ docker pull zhangpeng0v0/pnc_venv:venv

$ ~ docker run zhangpeng0v0/pnc_venv


