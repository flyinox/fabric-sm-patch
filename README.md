## Hyperledger Fabric 国密补丁

#####开启动态链接版本

用于Hyperledger Fabric项目支持国密算法，支持V1.1.x以上版本

cryptogen工具配套支持

当前版本采用非插件方式

### 准备条件
---
* 可以编译fabric的主机环境，如ubuntu或者osx

* 安装git环境

* 拉取并且切换到所需要的fabric版本

### 安装步骤
---


在fabric主目录下

* git clone https://github.com/flyinox/fabric-sm-patch.git

* git am ./fabric-sm-patch/fabric-sm-patch

* make [docker | native]

  使用make编译国密版native或者docker镜像

  推荐使用docker镜像方式，其中自带bccsp密码插件

  若使用native方式运行，请注意在peer或者orderer启动时，配置config文件中bccsp密码插件的位置（peer对应core.yaml, orderer对应orderer.yaml），更改方式参见下一章节

  (**注意**，当前dep 和 test 跑不过，所以make docker的时候最后会报错，不影响使用)

  (**注意** 此版本开启了动态链接，并且补丁工程内部带有libltdl.so.7，如果需要动态链接方式加载so库，请在启动peer/orderer容器时，将此文件映射到peer/orderer容器的/usr/lib/x86_64-linux-gnu/libltdl.so.7上)

