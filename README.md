# 自动更新配置文件、Clash.Meta 内核和 AdGuardHome
# 一、 说明
一直钟爱 Clash 的 fake-ip 模式，但一直有个头疼的问题：使用 [BT 下载](https://github.com/c0re100/qBittorrent-Enhanced-Edition)添加 [TrackersList](https://trackerslist.com) 后 UDP 协议无法连接。不管是以前使用的 [Clash for Windows](https://github.com/Fndroid/clash_for_windows_pkg)，还是现在使用的 [ShellClash](https://github.com/juewuy/ShellClash) 和 [Clash Verge](https://github.com/zzzgydi/clash-verge)。后来终于发现只要**将 TrackersList 列表内的域名添加到 fake-ip-filter 内，UDP 协议就可以连接了**。于是萌生出通过自动化脚本添加 TrackersList 列表域名到 fake-ip-filter 的想法，然后在本地客户端替换配置文件就可以了。
- 注：
- 1. 每天早上 3 点（北京时间）自动构建生成 user.yaml 和 Clash.Meta Alpha 版内核（arm64 和 amd64）
- 2. 若想自己生成配置文件 user.yaml，请 [Fork 本项目](https://github.com/DustinWin/Clash-Files)后编辑 MyConfig/front-user.yaml 文件，将 listen 参数的端口改为默认的 1053
- 3. 编辑 MyConfig/later-user.yaml 文件，将 nameserver 中的`🪜 国外域名`改成可以访问外网的代理组名，或者直接将 `'https://dns.google/dns-query#🪜 国外域名'`修改为 `tls://dns.google`

# 二、 使用方法
## 1. 配置文件 user.yaml
① ShellClash  
连接 SSH 后执行如下命令：
- 注：将 user.yaml 文件直链修改成自己的链接

```
curl -o $clashdir/user.yaml -L https://cdn.jsdelivr.net/gh/DustinWin/Clash-Files@release/user.yaml
$clashdir/start.sh start
```
② Clash Verge（Windows）  
首次使用可进入“配置”，新建”Merge“类型的配置，保存后进入文件夹 `%USERPROFILE%\.config\clash-verge\profiles`，可以看到这里新增了一个.yaml 文件，复制其文件名并替换下面命令中的{文件名}：
- 注：将 user.yaml 文件直链修改成自己的链接

```
curl -o %USERPROFILE%\.config\clash-verge\profiles\{文件名}.yaml -L https://cdn.jsdelivr.net/gh/DustinWin/Clash-Files@release/user.yaml
```
最好重启一下 Clash Verge 客户端
## 2. Clash.Meta 内核
① Release 版  
连接 SSH 后执行如下命令：
```
curl -o $clashdir/clash -L https://cdn.jsdelivr.net/gh/DustinWin/Clash-Files@main/Clash.Meta-Release/clash.meta-linux-arm64
chmod +x $clashdir/clash && $clashdir/start.sh restart
```
② Alpha 版  
连接 SSH 后执行如下命令：
```
curl -o $clashdir/clash -L https://cdn.jsdelivr.net/gh/DustinWin/Clash-Files@release/clash.meta-linux-arm64
chmod +x $clashdir/clash && $clashdir/start.sh restart
```
连接 SSH 后执行如下命令：
## 3. AdGuardHome
```
curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/Clash-Files@main/AdGuardHome/AdGuardHome
chmod +x /data/AdGuardHome/AdGuardHome && reboot
```
# 三、 配置 ShellClash 定时任务
可以在 ShellClash 里添加定时更新配置文件 user.yaml、Clash.Meta 内核、路由规则文件和 AdGuardHome 的任务，连接 SSH 后运行 `crontab -e`，按一下 Ins 键（Insert 键），在最下方粘贴如下内容：
```
0 3 * * 1,3,5 curl -o /data/clash/clash -L https://cdn.jsdelivr.net/gh/DustinWin/Clash-Files@release/clash.meta-linux-arm64 && chmod +x /data/clash/clash && /data/clash/start.sh restart >/dev/null 2>&1 #每周一、三、五早上 3 点更新 Clash.Meta 内核
30 3 * * 1,3,5 curl -o /data/clash/GeoSite.dat -L https://cdn.jsdelivr.net/gh/DustinWin/clash-geosite@release/geosite.dat && curl -o /data/clash/GeoIP.dat -L https://cdn.jsdelivr.net/gh/DustinWin/clash-geoip@release/geoip.dat && curl -o /data/clash/Country.mmdb -L https://cdn.jsdelivr.net/gh/DustinWin/clash-geoip@release/Country.mmdb && /data/clash/start.sh restart >/dev/null 2>&1 #每周一、三、五早上 3点半更新路由规则文件
30 4 * * 1,3,5 curl -o /data/clash/user.yaml -L https://cdn.jsdelivr.net/gh/DustinWin/Clash-Files@release/user.yaml && /data/clash/start.sh restart >/dev/null 2>&1 #每周一、三、五早上 4 点半更新 user.yaml
0 5 * * 1,3,5 /data/clash/start.sh updateyaml && /data/clash/start.sh restart >/dev/null 2>&1 #每周一、三、五早上 5 点更新订阅并重启 Clash 服务
0 6 * * 1,3,5 curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/Clash-Files@main/AdGuardHome/AdGuardHome && chmod +x /data/AdGuardHome/AdGuardHome && reboot >/dev/null 2>&1 #每周一、三、五早上 6 点更新 AdGuardHome 并重启路由器
```
按一下 Esc 键（退出键），输入英文冒号“:”，继续输入“wq”并回车，再运行 `/etc/init.d/cron restart`
