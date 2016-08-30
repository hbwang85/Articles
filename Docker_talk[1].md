# Docker talk[1]
##Status: WIP
##What is Docker
Docker的主要目标是“build, ship and run any app, anywhere", 即通过对应用组件的封装（Packaging），分发（Distribution)，部署（Deployment），运行（Runtime）等生命周期的管理，达到应用组件级别的”一次封装，到处运行“；  

* 基于Go语言实现，诞生于2013年初；
* Totally open-source，遵循Apache 2.0 protocol， 代码全部放在https://github.com/docker/docker
* Most of the popular Linux OS support it;

##Linux Containers
* Docker engine的基础是Linux Containers（LXC）。IBM developerWorks 关于LXC的description如下：  

>容器有效的将由单个操作系统管理的资源划分到独立的组中，以便更好的在独立的组之间平衡有冲突的资源使用需求。与虚拟化相比，这样既不需要指令级的模拟，也不需要即时编译。容器可以在核心CPU本地运行指令，而不需要任何专门的解释机制。此外也避免了准虚拟化（paravirtualization）和系统调用替换中的复杂性。      
>

* 可以将Docker容器理解为一种sandbox。每个容器内运行一个应用，不同的容器相互隔离，容器之间也可以建立通信机制。容器的创建和停止特别快速，容器自身对资源的需求也十分有限，远低于VM。

##Docker 在DevOps的优势
* Faster delivery and deployment: 开发人员可以使用image来快速构建一套标准的开发环境；开发完成之后，测试和运维人员可以直接使用相同的环境来部署代码。
* 更高效的资源利用： Docker容器的运行不需要而我的虚拟化管理程序（Virtual Machine Manager， VMM， 以及Hypervisor）支持，它是内核级的虚拟化，可以实现更高的性能，同时对资源的额外需求很低。
* 更轻松的迁移和扩展： Docker容器几乎可以在任何平台运行。
* 更简单的更新管理。使用Dockerfile 增量更新。

##Docker与VM的比较
特性 | Docker  | VM
----|----------|-------|
启动速度 | 秒级 | 分钟级|
硬盘使用 | MB | GB|
性能 | 接近原生 | 弱 |
系统支持量 | 单机支持上千个container | 几十个|
隔离行 | 安全隔离 | 完全隔离

## Docker和虚拟化
* 虚拟化（Virtualization）是一种资源管理，是将计算机的各种实体资源，如服务器，网路、内存及存储等，予以抽象，转换后呈现出来，打破实体结构件的不可分割的障碍，使用户可以用比原本的组态更好的方式来应用这些资源。
* Docker容器是在操作系统层面上实现虚拟化，直接复用本地主机的操作系统，因此更加轻量级。

##Core Concept
###Image
* Similar as VM Image.
* read-only.
* methods to create Image: 基于已有的Image的container， 基于本地模板（OpenVZ），基于Dockerfile
* Useful commands:

```
docker pull xxx
docker images
docker rmi xxx
```

###Container
* 类似于一个轻量级的sandbox。是从Image创建的instance。
* 可以把Container看做一个简易版的Linux系统环境；
* Useful commands:

```
docker run image == docker create + docker start
docker run -ti xxx /bin/bash
docker stop
docker kill
docker attach/ docker exec  进入container
docker exec -ti xxx /bin/bash
```

###Repository
目前，最大的是Docker hub， 国内公开的有 Docker pool







