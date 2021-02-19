**docker的镜像管理**

```
查看镜像列表:
docker images
docker image ls

导出镜像:
docker image save centos > docker-centos6.9.tar.gz
导入镜像:
docker image load -i docker-centos6.9.tar.gz
删除镜像:
docker image rm centos:latest

docker image rm 578c3

搜索镜像 	docker search + 镜像名字

给源中镜像打标签:

docker tag nginx:latest 10.0.0.11:80/nginx:latest

推送指定镜像到docker镜像源服务器

docker push 10.0.0.11:80/nginx:latest

获取镜像 (下载)	docker pull image_name

官方pull	docker pull centos:6.8（没有指定版本，默认会下载最新版） 私有仓库pull	docker pull daocloud.io/huangzhichong/alpine-cn:latest

docker history image_name   显示一个镜像的历史

docker build -t <image-name> .   *(点一定不能去掉)#使用当前目录下的Dockerfile构建镜像
```

**docker的容器管理**

```
docker -v         #查看版本

docker info     #查看docker信息

运行容器

docker run --name 容器名 -d -p 3306:3306 mysql  docker 启动容器
docker run image_name
docker run -d -p 80:80 nginx:latest
run（创建并运行一个容器） 
-d 放在后台 
-p 端口映射 :docker的容器端口
-P 随机分配端口
-v 源地址(宿主机):目标地址(容器)
docker run -it --name centos6 centos:6.9 /bin/bash 
-it 分配交互式的终端 
--name 指定容器的名字 
/bin/sh覆盖容器的初始命令

docker run image_name  启动容器***

docker stop container_id  停止容器

docker kill container_name   杀死容器

docker ps (-a -l -q)    查看容器列表

docker container rm  'docker ps -a -q'   删除所有容器

docker rm -f  'docker ps -a -q`      #删除所有容器

docker ps -a  #查看容器列表

docker exec -it 77cd6bef4dc9 /bin/bash   #进容器

docker start/stop container-id||container-name 开启/停止 指定容器id或者容器名称的容器

docker run -d -p 80:80 -v /opt/xiaoniao:/usr/share/nginx/html nginx:latest

docker logs container-name/container-id     #查看容器日志

docker ps | grep ${CONTAINER_ID}    #查看容器状态

docker commit ID new_image_name     #镜像打包 (保存对容器的修改)
docker commit -m="提交的描述信息" -a="作者" 容器id  要创建的目标镜像名:[标签名]

docker inspect <id/container_name>   #查看容器内部详情细节

docker login #登录

Ctrl+P+Q     #退出而不关闭容器
```