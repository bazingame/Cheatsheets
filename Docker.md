##  Docker


#### 列出所有image文件

```shell
docker image ls
```

#### 删除 image 文件

```shell
docker image rm [imageName]
```

#### 抓取image

```shell
docker image pull [imageLocation]
```

#### 列出容器

```shell
docker container ls        ##runing container

docker container ls -all   ##all container including stop one
```

#### 运行容器

```shell
docker run -itd container /bin/bash  # 每次生成新建一个新的容器

docker start container   ## 启动已经存在的容器
```

#### 进入docker容器

```shell
docker exec -it containerId bash # -it 参数:容器shell映射到当前shell
```

#### 运行容器并挂载目录	

```shell
docker run -dit -P \
--name scrapy \
--mount type=bind,source=/g/Project/XTUSearch,target=/code \
scrapy 
```

#### 创建image文件

创建dockerfile文件后

```shell
docker image build -t ImageName:tag .  # 最后的.代表dockerfile在当前目录内
```

#### 标注标签和版本

```shell
docker image tag tag [imageName] [username]/[repository]:[tag]
```

#### 终止容器

```shell
docker container kill [containerId]  # 会向容器内发出SIGKILL信号，容器内所有操作会全部丢失

docker container stop [containerId]  # 向容器内发出SIGTERM信号，容器会进行收尾工作
```

#### 删除容器

```shell
docker container rm [containerId]
```

#### DockerFile相关

```
FROM node:8.4
COPY . /app
WORKDIR /app
RUN npm install --registry=https://registry.npm.taobao.org
EXPOSE 3000
CMD node demos/01.js
```

上面代码一共五行，含义如下。

> - `FROM node:8.4`：该 image 文件继承官方的 node image，冒号表示标签，这里标签是`8.4`，即8.4版本的 node。
>
> - `COPY . /app`：将当前目录下的所有文件（除了`.dockerignore`排除的路径），都拷贝进入 image 文件的`/app`目录。
>
> - `WORKDIR /app`：指定接下来的工作路径为`/app`。
>
> - `RUN npm install`：在`/app`目录下，运行`npm install`命令安装依赖。注意，安装后所有的依赖，都将打包进入 image 文件。 
>
> - `EXPOSE 3000`：将容器 3000 端口暴露出来， 允许外部连接这个端口。
>
> - `CMD node demos/01.js`，它表示容器启动后自动执行`node demos/01.js`
>
>   *CMD和RUN的区别:`RUN`命令在 image 文件的构建阶段执行，执行结果都会打包进入 image 文件；`CMD`命令则是在容器启动后执行。*

