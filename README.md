## Hyperledger Fabric 国密补丁

用于Hyperledger Fabric项目支持国密算法，当前支持release1.3.x，暂不支持非release版本。

包含国密算法插件(bccsp插件)，包括支持国密证书和秘钥的cryptogen

### 准备条件
---
* 可以编译fabric的主机环境，如ubuntu或者osx

* 安装git环境

* 拉取并且切换到所需要的fabric版本

### 安装步骤
---

(**注意**，当前只支持release1.3.x版本，如果需要支持非release版本，需要自行解决冲突)

在fabric主目录下

* git clone https://github.com/flyinox/fabric-sm-patch.git

* git am ./fabric-sm-patch/fabric-sm-patch

* make [docker | native]

  使用make编译国密版native或者docker镜像

  推荐使用docker镜像方式，其中自带bccsp密码插件

  若使用native方式运行，请注意在peer或者orderer启动时，配置config文件中bccsp密码插件的位置（peer对应core.yaml, orderer对应orderer.yaml），更改方式参见下一章节


### cryptogen使用方式
------


​	使用方式为和普通cryptogen相似，增加--pluginPath选项，指定国密版bccsp插件位置，若不指定bccsp插件位置，则默认位置为/etc/hyperledger/fabric/smPlugin.so

cryptogen generate   --pluginPath [smPlugin.so]