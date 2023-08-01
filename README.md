# 更新 [Clash.Meta 内核](https://github.com/MetaCubeX/Clash.Meta)、[Yacd-meta 面板](https://github.com/MetaCubeX/Yacd-meta)和 [AdGuardHome](https://github.com/AdguardTeam/AdGuardHome)
# 一、 说明
每天早上 3 点（北京时间）自动构建生成：
## 1. Clash.Meta Alpha 版和 Release 版内核  
包含架构：amd64、armv5、armv6、armv7、armv8、mips-softfloat、mipsle-hardfloat、mipsle-softfloat 和 windows-amd64
## 2. Yacd-meta 面板  
## 3. AdGuardHome  
包含架构：amd64、armv5、armv6、armv7、armv8、mips_softfloat、mipsle_softfloat 和 windows_amd64
# 二、 使用方法
## 1. 导入 Clash.Meta 内核（以 [ShellClash](https://github.com/juewuy/ShellClash)  为例）
① Release 版  
连接 SSH 后执行如下命令：
```
curl -o $clashdir/clash -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/Clash.Meta-release/clash.meta-linux-armv8
chmod +x $clashdir/clash && $clashdir/start.sh restart
```
- 注：若是其它架构，可将命令中的 `armv8` 修改为上述“说明”中对应的架构名称

② Alpha 版  
连接 SSH 后执行如下命令：
```
curl -o $clashdir/clash -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@release/clash.meta-linux-armv8
chmod +x $clashdir/clash && $clashdir/start.sh restart
```
- 注：若是其它架构，可将命令中的 `armv8` 修改为上述“说明”中对应的架构名称

## 2. 导入 Clash.Meta 内核（以 [Clash Verge](https://github.com/zzzgydi/clash-verge) Windows 版为例）
① Release 版  
连接 SSH 后执行如下命令：
```
taskkill /f /t /im "Clash Verge*"
taskkill /f /t /im clash-meta*
curl -o %PROGRAMFILES%\Clash Verge\clash-meta.exe -L https://ghproxy.com/https://github.com/DustinWin/clash-tools/raw/main/Clash.Meta-release/clash.meta-windows-amd64.exe
```
② Alpha 版  
连接 SSH 后执行如下命令：
```
taskkill /f /t /im "Clash Verge*"
taskkill /f /t /im clash-meta*
curl -o %PROGRAMFILES%\Clash Verge\clash-meta.exe -L https://ghproxy.com/https://github.com/DustinWin/clash-tools/releases/download/latest/clash.meta-windows-amd64.exe
```
## 3. 导入 Yacd-meta 面板（以 ShellClash 为例）
连接 SSH 后执行如下命令：
```
curl -o /tmp/Yacd-meta.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/Yacd-meta/Yacd-meta.tar.gz
mkdir -p $clashdir/ui && tar -zxf /tmp/Yacd-meta.tar.gz -C $clashdir/ui && rm -f /tmp/Yacd-meta.tar.gz
$clashdir/start.sh restart
```
## 4. 安装或升级 AdGuardHome
连接 SSH 后执行如下命令：
```
curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/AdGuardHome/AdGuardHome_linux_armv8
chmod +x /data/AdGuardHome/AdGuardHome && reboot
```
- 注：若是其它架构，可将命令中的 `armv8` 修改为上述“说明”中对应的架构名称

# 三、 配置 ShellClash 定时任务
可以在 ShellClash 里添加定时更新 Clash.Meta 内核、Yacd-meta 面板和 AdGuardHome 的任务，连接 SSH 后运行 `crontab -e`，按一下 Ins 键（Insert 键），在最下方粘贴如下内容：
```
30 3 * * * curl -o /data/clash/clash -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@release/clash.meta-linux-armv8 && chmod +x /data/clash/clash && /data/clash/start.sh restart >/dev/null 2>&1 #每天早上 3 点半更新 Clash.Meta 内核
0 4 * * 1,3,5 curl -o /tmp/Yacd-meta.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/Yacd-meta/Yacd-meta.tar.gz && rm -rf /data/clash/ui/* && tar -zxf /tmp/Yacd-meta.tar.gz -C /data/clash/ui && rm -f /tmp/Yacd-meta.tar.gz && /data/clash/start.sh restart >/dev/null 2>&1 #每周一、三、五早上 4 点更新 Yacd-meta 面板
0 4 * * 2,4,6 curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/AdGuardHome/AdGuardHome_linux_armv8 && chmod +x /data/AdGuardHome/AdGuardHome && reboot >/dev/null 2>&1 #每周二、四、六早上 4 点更新 AdGuardHome 并重启路由器
```
按一下 Esc 键（退出键），输入英文冒号“:”，继续输入“wq”并回车，再运行 `/etc/init.d/cron restart`
