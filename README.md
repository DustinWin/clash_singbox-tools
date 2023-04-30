# 更新 [Clash.Meta 内核](https://github.com/MetaCubeX/Clash.Meta)、[Yacd-meta 面板](https://github.com/MetaCubeX/Yacd-meta)和 [AdGuardHome](https://github.com/AdguardTeam/AdGuardHome)
# 一、 说明
每天早上 3 点（北京时间）自动构建生成 Clash.Meta Alpha 版内核（arm64 和 amd64）、Clash.Meta Release 版内核（arm64 和 amd64）、Yacd-meta 面板和 AdGuardHome（arm64）
# 二、 使用方法
## 1. [ShellClash](https://github.com/juewuy/ShellClash) 导入 Clash.Meta 内核
① Release 版  
连接 SSH 后执行如下命令：
```
curl -o $clashdir/clash -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/Clash.Meta-release/clash.meta-linux-arm64
chmod +x $clashdir/clash && $clashdir/start.sh restart
```
② Alpha 版  
连接 SSH 后执行如下命令：
```
curl -o $clashdir/clash -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@release/clash.meta-linux-arm64
chmod +x $clashdir/clash && $clashdir/start.sh restart
```
## 2. [Clash Verge](https://github.com/zzzgydi/clash-verge)（Windows 版）导入 Clash.Meta 内核
① Release 版  
连接 SSH 后执行如下命令：
```
taskkill /f /t /im "Clash Verge*"
taskkill /f /t /im clash-meta*
curl -o %PROGRAMFILES%\Clash Verge\clash-meta.exe -L https://github.com/DustinWin/clash-tools/raw/main/Clash.Meta-release/clash-meta.exe
```
② Alpha 版  
连接 SSH 后执行如下命令：
```
taskkill /f /t /im "Clash Verge*"
taskkill /f /t /im clash-meta*
curl -o %PROGRAMFILES%\Clash Verge\clash-meta.exe -L https://github.com/DustinWin/clash-tools/releases/download/latest/clash-meta.exe
```
## 2. Yacd-meta
连接 SSH 后执行如下命令：
```
curl -o /tmp/Yacd-meta.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/Yacd-meta/Yacd-meta.tar.gz
mkdir -p $clashdir/ui && chmod +x $clashdir/ui && tar -zxf /tmp/Yacd-meta.tar.gz -C $clashdir/ui
rm -f /tmp/Yacd-meta.tar.gz && $clashdir/start.sh restart
```
## 3. AdGuardHome
连接 SSH 后执行如下命令：
```
curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/AdGuardHome/AdGuardHome
chmod +x /data/AdGuardHome/AdGuardHome && reboot
```
# 三、 配置 ShellClash 定时任务
可以在 ShellClash 里添加定时更新 Clash.Meta 内核和 AdGuardHome 的任务，连接 SSH 后运行 `crontab -e`，按一下 Ins 键（Insert 键），在最下方粘贴如下内容：
```
30 3 * * * curl -o /data/clash/clash -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@release/clash.meta-linux-arm64 && chmod +x /data/clash/clash && /data/clash/start.sh restart >/dev/null 2>&1 #每天早上 3 点半更新 Clash.Meta 内核
0 4 * * 1,3,5 curl -o /tmp/Yacd-meta.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/Yacd-meta/Yacd-meta.tar.gz && tar -zxf /tmp/Yacd-meta.tar.gz -C $clashdir/ui --overwrite && rm -f /tmp/Yacd-meta.tar.gz && /data/clash/start.sh restart >/dev/null 2>&1 #每周一、三、五早上 4 点更新 Yacd-meta 面板
0 4 * * 2,4,6 curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/AdGuardHome/AdGuardHome && chmod +x /data/AdGuardHome/AdGuardHome && reboot >/dev/null 2>&1 #每周二、四、六早上 4 点更新 AdGuardHome 并重启路由器
```
按一下 Esc 键（退出键），输入英文冒号“:”，继续输入“wq”并回车，再运行 `/etc/init.d/cron restart`
