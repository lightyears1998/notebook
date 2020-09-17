# PM2

Node进程管理器。

```sh
yarn global add pm2
pm2 startup # 生成启动脚本
# pm2 unstartup

pm2 list
pm2 monit
pm2 start
```

## PM2 Deploy

---

## 疑难杂症

PM2 Deploy 需要 git >= 1.9，否则无法从上游拉取后续的代码更新；而在 CentOS 7 上 git 的默认版本是 1.8。

由于 PM2 是通过 SSH 登录到远程主机的，因此一些在 SHELL 登录时运行的启动脚本如 `.zshrc` 或 `/etc/profile.d` 不会在此时加载。
因此，如果安装了多个版本的 git，那么调整 PATH 时不能在上面所述的启动脚本中调整。
