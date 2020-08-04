

```markdown
* 1.拉取镜像
docker pull gitlab/gitlab-ce

* 2.启动gitlab
sudo docker run -d \
--hostname gitlab \
--name gitlab \
--restart always \
--publish 30001:22 --publish 30000:80 --publish 30002:443 \
--volume $HOME/gitlab/data:/var/opt/gitlab \
--volume $HOME/gitlab/logs:/var/log/gitlab \
--volume $HOME/gitlab/config:/etc/gitlab \
gitlab/gitlab-ce

# -d：后台运行
# -p：将容器内部端口向外映射 --->publish
# --name：命名容器名称
# -v：将容器内数据文件夹或者日志、配置等文件夹挂载到宿主机指定目录 --->volume

* 3.进入gitlab容器修改配置
按上面的方式，gitlab容器运行没问题，但在gitlab上创建项目的时候，生成项目的URL访问地址是按容器的hostname来生成的，也就是容器的id。作为gitlab服务器，我们需要一个固定的URL访问地址，于是需要配置gitlab.rb

# 进入gitlab容器
docker exec -it gitlab /bin/bash

# 修改gitlab配置，gitlab.rb文件内容默认全是注释
$ vim /etc/gitlab/gitlab.rb

# 配置http协议所使用的访问地址,不加端口号默认为80
external_url 'http://172.24.184.248:30000'
gitlab_rails['yime_zone'] = 'Asia/Shanghai'
# 配置ssh协议所使用的访问地址和端口
gitlab_rails['gitlab_ssh_host'] = '172.24.184.248'
gitlab_rails['gitlab_shell_ssh_port'] = 222 # 此端口是run时22端口映射的222端口
:wq #保存配置文件并退出
修改gitlab.rb文件

#退出时候报here are stopped jobs是应为有进程未退
jobs -l #查看进程
kill -9 xxxx #杀掉

# 重启gitlab容器
$ docker restart gitlab

此时项目的仓库地址就变了。如果ssh端口地址不是默认的22，就会加上ssh:// 协议头
打开浏览器输入ip地址(因为我的gitlab端口为80，所以浏览器url不用输入端口号，如果端口号不是80，则打开为：ip:端口号)

* 4.访问
http://localhost:30000/

```





