# 服务管理

### 服务管理工具

- `service`
  - `/etc/init.d/network`
- `systemctl`
  - `/usr/lib/systemd/system/`

##### 系统启动的级别

```bash
chkconfig --list
#  0：关机无法被kill -9  init 0
#  6：重启 1：单用户 2:无网络的多用户 3：字符模式 5：图形化
```

