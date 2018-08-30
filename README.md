# prong/subversion-edge

这是 Collabnet Subversion Edge 服务器的 docker 镜像，镜像来自 [mamohr/subversion-edge](mamohr/subversion-edge)。

在官方的基础上做了如下变更：

- 将5.2.0升级到5.2.2。
- 将时区从UTC改为中国上海。

## 使用说明

这个镜像将csvn的数据目录暴露为卷`/opt/csvn/data`，如果将其映射为宿主机的一个空文件夹，则初始化脚本将负责将基本配置复制到这个卷。

这个容器的公开端口有：

 * 3343 - HTTP CSVN 管理界面
 * 4434 - HTTPS CSVN 管理界面 (如果启用了SSL)
 * 18080 - Apache Http SVN

运行容器：
```shell
$ docker run -d -p 3343:3343 -p 4434:4434 -p 18080:18080 \
    --name svn-server prong/subversion-edge
```

管理界面为 [http://docker-host:3343/csvn](http://docker-host:3343/csvn)。

如果你希望映射宿主机的数据目录：

```shell
$ docker run -d -p 3343:3343 -p 4434:4434 -p 18080:18080 \
    -v /srv/svn-data:/opt/csvn/data --name svn-server prong/subversion-edge
```

更多信息请参考 [CollabNet](http://collab.net/products/subversion)。

