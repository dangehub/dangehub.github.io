---
{"dg-publish":true,"permalink":"/101 日记/利用 Digital Garden 插件将我的 ob 笔记发布成博客/","dgPassFrontmatter":true,"noteIcon":""}
---


# 汇总信息
1. 我的 github 库 [dangehub/qlog (github.com)](https://github.com/dangehub/qlog)
2. 我的  [vervel 网址](https://qlog-one.vercel.app/)
3. 我的自定义域名：https://qlog.9udange.top/


# 部署记录 

## 如何删除已经构建的笔记？

发现一个问题，我已经在github删除了一篇笔记，但是构建好的静态页面里，对应笔记依然存在

## 安装插件 

## 申请 token

## ob 内发布流程

# 优劣分析


## 本地部署的方法
参考[本地部署 ·奥利斯基尔德/黑曜石数字花园 ·讨论 #160 (github.com)](https://github.com/oleeskild/obsidian-digital-garden/discussions/160)

值得一提的是，这个本地部署的功能并不完善。

我尝试构建一个镜像来使用 docker 完成部署 

参考了如下资料：
	[Node.js (nodejs.org)](https://nodejs.org/en/docs/guides/nodejs-docker-webapp/)
	

首先根据教程把原 git 仓库 clone 到自己的账号下，再把自己的仓库 clone 到本地 

```docker
# FROM 表示设置要制作的镜像基于哪个镜像，FROM指令必须是整个Dockerfile的第一个指令，如果指定的镜像不存在默认会自动从Docker Hub上下载。
# 指定我们的基础镜像是node，latest表示版本是最新
FROM node:latest

# 执行命令，创建文件夹
RUN mkdir -p /home/nodeNestjs

# 将根目录下的文件都copy到container（运行此镜像的容器）文件系统的文件夹下
COPY . /home/nodeNestjs

# WORKDIR指令用于设置Dockerfile中的RUN、CMD和ENTRYPOINT指令执行命令的工作目录(默认为/目录)，该指令在Dockerfile文件中可以出现多次，如果使用相对路径则为相对于WORKDIR上一次的值，
# 例如WORKDIR /data，WORKDIR logs，RUN pwd最终输出的当前目录是/data/logs。
# cd到 /home/nodeNestjs
WORKDIR /home/nodeNestjs

# 安装项目依赖包
RUN npm install express --save && npm install && npm run build

# 配置环境变量
#ENV HOST 0.0.0.0
#ENV PORT 8080

# 容器对外暴露的端口号(笔者的nestjs运行的端口号是3000)
EXPOSE 8080

# 容器启动时执行的命令，类似npm run start
CMD ["node", "app.js"]
```

进行镜像 build 的过程中，很有可能出现网络问题，多尝试几次

```
#这个可以
FROM node:latest
RUN mkdir -p /digital_garden
COPY . /digital_garden
WORKDIR /digital_garden
RUN npm install express --save && npm install && npm run build
EXPOSE 8080
CMD ["node", "app.js"]

#这个不行，为什么？
FROM node:latest
RUN mkdir -p /digital_garden
COPY . /digital_garden
WORKDIR /digital_garden
RUN npm install express --save && npm install -g pm2 && npm install && npm run build
EXPOSE 8080
CMD ["pm2","start","app.js"]
```
