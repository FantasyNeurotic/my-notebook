the way for docker
# 运行docker 镜像
* 拉取镜像
`docker pull postgres`
* 查看镜像
`docker images postgres`
* 启动镜像 并指定端口
`docker run --name postgresql-server -e POSTGRES_PASSWORD=mysecretpassword -e POSTGRES_USER=bwu -d -p 5432:5432 postgres`
``
* 进入镜像
`docker exec -it postgresql-server bash`
`sudo docker attach imagesId`