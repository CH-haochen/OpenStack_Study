# 一 云计算与OpenStack

## 1 OpenStack核心项目

**Compute Service ("Nova")：**计算资源生命周期管理组件

**NetWork Service ("Neutron")：**提供云计算环境下的虚拟网络功能

**Block Storage Service ("Cinder")：**管理计算实例所使用的块级存储

**Object Storage Service ("Swift")：**对象存储，用于永久类型的静态数据的长期存储

**Image Service ("Glance")：**提供虚拟机镜像的发现，注册，获取服务

**Identity Service("Keystone")：**提供了用户信息管理，为其他组件提供认证服务

**Dashboard ("Horizon")：**用以管理、控制OpenStack服务的Web控制面板

### 1.1  核心项目如何关联

**例：创建一个虚拟机**

首先需要一个web界面（Horizon），那么在使用web界面的话，需要做一个身份认证，就是由Keystone来做。

在经过Keystone认证后，就可以进入Horizon的web界面了。

进入web界面后，可以通过像Nova发出指令，创建虚拟机VMs。

创建虚拟机后，需要给虚拟机安装操作系统，那么用到的就是镜像文件，使用的是Glance

Glance收到获取镜像的请求后，那么镜像是存储在哪里呢？就是Swift中。

所以，在给虚拟机使用镜像装操作系统，首先Glance要从Swift中取到镜像文件，然后提供到Nova，用于创建虚拟机。

虚拟机创建后，会将创建好的虚拟机加入到已存在的计算集群中，那么这就设计到了分配网络地址，搭建网络，就是Neutron。

在创建好虚拟机后，如果发现硬盘存储不够，那么可以使用Cinder，为虚拟机挂载硬盘，来管理硬盘的生命周期。