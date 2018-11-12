## Hyperledger Fabric 国密补丁

用于Hyperledger Fabric项目支持国密算法，当前支持release 1.1.x, release1.2.x,release1.3.x，暂不支持非release版本。

包含国密算法插件(bccsp插件)，msp生成工具cryptogensm

### 准备条件
---
* 可以编译fabric的主机环境，如ubuntu或者osx

* 安装git环境

* 拉取并且切换到所需要的fabric版本

### 安装步骤
---

(**注意**，当前只支持release版本，如果需要支持非release版本，需要自行解决冲突)

在fabric主目录下

* git clone https://github.com/flyinox/fabric-sm-patch.git

* git am ./fabric-sm-patch/fabric-sm-patch

* make [docker | native]

  使用make编译国密版native或者docker镜像

* cd ./examples/plugins/smPlugin; go build --buildmode=plugin

   编译国密bccsp插件,文件位置在 ./examples/plugins/smPlugin/smPlugin.so

* make cryptogensm

   如需使用国密版本msp生成工具，请运行此命令,生成的工具在./build/bin/cryptogensm


### 使用步骤
---

1. peer端配置bccsp插件

   更改core.yaml文件, 将BCCSP改为
`````yaml
   Default: PLUGIN
         Plugin:
           Library: [fabric路径]/examples/plugins/smPlugin/smPlugin.so
`````
2. orderer端配置bccsp插件

   更改orderer.yaml文件, 将BCCSP改为
`````yaml
   Default: PLUGIN
         Plugin:
           Library: [fabric路径]/examples/plugins/smPlugin/smPlugin.so
`````
3. cryptogensm使用方式

通过make cryptogensm编译后，可以通过cryptogensm生成国密版crypto-config，
使用方式为和普通cryptogen相似，增加--pluginPath选项，指定国密版bccsp插件位置

* cryptogensm generate   --pluginPath [smPlugin.so]
