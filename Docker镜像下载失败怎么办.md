# 方法0：上网

# 方法1：`docker save` & `docker load`

部署的服务不想装上网软件。
可以在本地开发机上保存下载好或者build好的镜像，传到服务器，使用`docker load`。

# 方法2：内网起一个Docker Registry设置成Pull through cache