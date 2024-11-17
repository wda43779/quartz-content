# 主要流程
- 买域名
- 买VPS
- 把域名指向VPS的IP
- 安装NGINX并配置
- 申请HTTPS证书
- 留一个上传脚本

# NGINX的文件权限
对于静态网站，在文件夹上至少要rx权限，文件上要有r权限。搞了半天中越调整了一个能用的rsync命令。

找问题的时候还以为是[[Quartz]]的示例写错了，结果是`/var/www/html` 的权限搞不明白。

没搜到Windows版本的rsync，还得从WSL里面借。

```powershell
npx quartz build
wsl rsync -avz --delete --chown=www-data:www-data --chmod=D755,F644 public/* root@38.55.194.90:/var/www/html
```