# 搭建精美H5AI文件服务器

> 很多人会遇到这样一个问题.有时候想方便快捷的下载或者分享VPS上面的一些文件.但是又不熟悉命令而且也不方便.这时候文件服务器就派上用场了.


## 更新记录

- 2017.11.19:再次更新镜像.本次更新极大的压缩了镜像的体积.请记得pull image.
- 2017.11.19:两个分支的镜像都更新了.修复BUG和增强性能.请记得pull image.
- 2017.11.14:增加了密码保护部分，并且更新了原来的镜像.请原来的用户也pull一下image.
- 2017.10.02:增加了联合Cloud-Torrent的部分
- 2017.09.02:重要更新!请所有看过这篇文章的朋友注意.镜像已经再次更新.体积缩小到110MB.同时功能更为丰富.另外挂载目录已修改以避免一些问题.请仔细查看文章图片.
- 2017.08.27:重要更新!把原来的docker换成我自己的镜像.做了大量的更新.

## 准备

* **Hyperapp**
* **一个已经解析正确的域名（ping验证）**
* **耐心.仔细.认真**


## 服务端部署

##### 首先我们先进入VPS的SSH窗口执行命令


```
sudo su
mkdir /share && chmod 777 /share
ln -s /share .
```
* 这时候/share就是共享目录并且已经软连接到/root目录下面.可以在root目录下面快速访问.也可以通过`cd /share`来访问
* 如果你想自定义目录也可以.替换/share即可.但是要注意权限设置


#### 其次转到Hyperapp进行设置

1. **转到商店页面.找到Docker Image然后选择服务器并且保存进入配置界面**
2. **请完全按照下图配置进行填写！**

|    应用设置名称     |          内容          |
| :-----------: | :------------------: |
|     Image     | fanvinga/docker-h5ai |
|    Options    |   -v /share:/share   |
|    Command    |                      |
|     Args      |                      |
| **Nginx设置名称** |        **内容**        |
|      域名       |      你要给h5ai的域名      |
|     应用端口      |                      |
|     Https     |    将http重定向到https    |
|      域名       |   你要给h5ai的域名（自动填写）   |
|      邮箱       |       域名所对应的邮箱       |


3. **保存并且进行安装.请确保这时候Nginx Proxy以及Nginx SSL Support正常默认安装并且启动了**

## 添加密码保护

> 不少朋友反应.h5ai默认访问不需要密码会不会很不安全？放点文件都被人看光了.那就寻思着增加个密码保护功能呗.一研究.h5ai本身的只能保护info界面.在php增加一来麻烦二来性能估计一般.想起来自己做docker的时候为了方便用nginx把这些都罩起来了.索性就用nginx来操作.朋友们按照下列步骤来操作即可.


1. **把上面`image`这个空替换为`fanvinga/docker-h5ai:auth`**
2. **把`options`的内容更改为`-v /share:/share -e USER=你要的用户名 -e PASSWD=你要的密码`**
3. **更新配置即可，要是第二步没有用-e指定用户名&密码的话，默认用户名&密码是两个`vinga`**

## 联合Cloud-Torrent

* **如果想做到利用Cloud-Torrent下载完BT之后直接可以在H5AI里面找到的话.只需要在上面的options里面加入`-v /srv/docker/Cloud-Torrent:/share/download`.然后更新配置.这样在h5ai目录下会出现download文件夹.里面就有CT下载完成的文件啦**

## 大功告成

* **这时候去访问你的域名吧٩(˃̶͈̀௰˂̶͈́)و**

## 写在最后

* 写了这么久.如果能有所收获那就是我最大的荣幸了:)
* 如果可以的话.可以关注一下 https://vinga.tech 这是我的私人博客地址:)
* 如有问题可发邮件至我邮箱fanalcest@gmail.com联系或telegram@fanvinga

<a href="https://vinga.tech"><img src="https://d.unlimit.fun/design/banner.png" alt="banner" target="_blank"></a>
