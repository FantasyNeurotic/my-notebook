# docker 实战

## 关于Dockerfile

## 实战

### docker 安装node.js
* 创建文件夹
```cmd
mkdir ~/docker-node-hello && cd $_
```

* 创建index.js
```js
var express = require('express')
var app = express()

app.get('/', function (req, res) {
 res.send('Hello World!')
})

var server = app.listen(3001, function () {

 var host = server.address().address
 var port = server.address().port

 console.log('Example app listening at http://%s:%s', host, port)

})
```

* 创建package.json
```json
{
 "name": "docker-node-hello",
 "private": true,
 "version": "0.0.1",
 "description": "Node.js Hello world app on Ubuntu using docker",
 "dependencies": {
   "express": "4.x.x"
 }
}
```

* 创建dockerfile
```json
# 设置基础镜像
FROM ubuntu:14.10

# 如果上个步骤已经更新软件源，这步可以忽略
RUN apt-get update

# 安装 NodeJS 和 npm
RUN apt-get install -y nodejs npm

# 将目录中的文件添加至镜像的 /srv/hello 目录中
ADD . /srv/hello

# 设置工作目录
WORKDIR /srv/hello

# 安装 Node 依赖库
RUN npm install

# 暴露 3001 端口，便于访问
EXPOSE 3001

# 设置启动时默认运行命令
CMD ["nodejs", "/srv/hello/index"]
```

* 构建镜像
```cmd
  # 通过该命令，按照 Dockerfile 所配置的信息构建出镜像
  # -t 镜像的名称
  # --rm 构建成功后，删除临时镜像（每执行一行 Dockerfile 中的命令，就会创建一个临时镜像）
  docker build --rm -t node-hello .

  # 检查镜像是否创建成功
  docker images
```

* 运行docker
```cmd
docker run -p 3001:3001 --name nodejs1 node-hello
```

## 关于pg
* 拉取镜像
```cmd
docker pull postgres
```
* 查看镜像
```cmd
docker images postgres
```
* 启动镜像 并指定端口
```cmd
docker run --name postgresql-server -e POSTGRES_PASSWORD=mysecretpassword -e POSTGRES_USER=bwu -d -p 5432:5432 postgres
```
* 进入镜像
```cmd
docker exec -it postgresql-server bash
sudo docker attach imagesId
```
