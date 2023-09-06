# 更新 [Clash.Meta 内核](https://github.com/MetaCubeX/Clash.Meta)、Dashboard 面板和 [AdGuardHome](https://github.com/AdguardTeam/AdGuardHome)
# 一、 说明
每天早上 3 点（北京时间）自动构建生成：
1. Clash.Meta Alpha 版和 Release 版内核  
2. Dashboard 面板：[Clash 官方面板](https://github.com/Dreamacro/clash-dashboard)、[Razord-meta 面板](https://github.com/MetaCubeX/Razord-meta)、[yacd 面板](https://github.com/haishanh/yacd)、[Yacd-meta 面板](https://github.com/MetaCubeX/Yacd-meta)和 [metacubexd 面板](https://github.com/MetaCubeX/metacubexd)

|面板类型|在线地址|
|-----|-----|
|Clash 官方面板|http://clash.razord.top|
|Razord-meta 面板|http://clash.metacubex.one|
|yacd 面板|http://yacd.haishan.me|
|Yacd-meta 面板|http://yacd.metacubex.one|
|metacubexd 面板|http://d.metacubex.one|
3. AdGuardHome

注：
- 1. 本教程中的下载链接以 CPU 架构 ARMv8 为例，请注意修改链接后缀
- 2. 查看 CPU 架构可连接 SSH 后执行命令 `uname -ms`，若执行结果是“linux aarch64”，就是搭载的 ARMv8 架构

# 二、 使用方法
## 1. 导入 Clash.Meta 内核 Linux 版（以 [ShellClash](https://github.com/juewuy/ShellClash) 为例）
Clash.Meta 内核 CPU 架构和链接后缀对应关系如下：
|CPU 架构|AMD64|ARMv5|ARMv6|ARMv7|ARMv8|mips-softfloat|mipsle-hardfloat|mipsle-softfloat|
|-----|-----|-----|-----|-----|-----|-----|-----|-----|
|**链接后缀**|`amd64`|`armv5`|`armv6`|`armv7`|`armv8`|`mips-softfloat`|`mipsle-hardfloat`|`mipsle-softfloat`|

如 CPU 架构为 ARMv7，则下载链接须修改为：`https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/Clash.Meta-release/clash.meta-linux-armv7`
和 `https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@release/clash.meta-linux-armv7`  
① Release 版  
连接 SSH 后执行如下命令：
```
curl -o $clashdir/clash -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/Clash.Meta-release/clash.meta-linux-armv8
chmod +x $clashdir/clash && $clashdir/start.sh restart
```
② Alpha 版  
连接 SSH 后执行如下命令：
```
curl -o $clashdir/clash -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@release/clash.meta-linux-armv8
chmod +x $clashdir/clash && $clashdir/start.sh restart
```
## 2. 导入 Clash.Meta 内核 Windows 版（以 [Clash Verge](https://github.com/zzzgydi/clash-verge) 为例）
① Release 版  
编辑文本文档，粘贴如下内容：
```
taskkill /f /t /im "Clash Verge*"
taskkill /f /t /im clash-meta*
curl -o %PROGRAMFILES%\Clash Verge\clash-meta.exe -L https://ghproxy.com/https://raw.githubusercontent.com/DustinWin/clash-tools/main/Clash.Meta-release/clash.meta-windows-amd64.exe
```
另存为 .bat 文件，右击并选择以管理员身份运行  
② Alpha 版  
编辑文本文档，粘贴如下内容：
```
taskkill /f /t /im "Clash Verge*"
taskkill /f /t /im clash-meta*
curl -o %PROGRAMFILES%\Clash Verge\clash-meta.exe -L https://ghproxy.com/https://github.com/DustinWin/clash-tools/releases/download/latest/clash.meta-windows-amd64.exe
```
另存为 .bat 文件，右击并选择以管理员身份运行
## 3. 导入 Dashboard 面板（以 ShellClash 安装 Yacd-meta 面板为例）
Dashboard 面板类型和文件名对应关系如下：
|面板类型|Clash 官方面板|Razord-meta 面板|yacd 面板|Yacd-meta 面板|metacubexd 面板|
|-----|-----|-----|-----|-----|-----|
|**文件名**|`clash-dashboard.tar.gz`|`Razord-meta.tar.gz`|`yacd.tar.gz`|`Yacd-meta.tar.gz`|`metacubexd.tar.gz`|

如需要安装 Razord-meta 面板，则命令中的文件名须修改为 `Razord-meta.tar.gz` 且下载链接修改为 `https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/Dashboard/Razord-meta.tar.gz`  
连接 SSH 后执行如下命令：
```
curl -o /tmp/Yacd-meta.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/Dashboard/Yacd-meta.tar.gz
mkdir -p $clashdir/ui && tar -zxf /tmp/Yacd-meta.tar.gz -C $clashdir/ui && rm -f /tmp/Yacd-meta.tar.gz
$clashdir/start.sh restart
```
## 4. 安装 AdGuardHome
AdGuardHome CPU 架构和链接后缀对应关系如下：
|CPU 架构|AMD64|ARMv5|ARMv6|ARMv7|ARMv8|mips-softfloat|mipsle-softfloat|
|-----|-----|-----|-----|-----|-----|-----|-----|
|**链接后缀**|`amd64`|`armv5`|`armv6`|`armv7`|`armv8`|`mips-softfloat`|`mipsle-softfloat`|

如 CPU 架构为 ARMv7，则下载链接须修改为：  
`https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/AdGuardHome/AdGuardHome_linux_armv7` 和 `https://ghproxy.com/https://raw.githubusercontent.com/DustinWin/clash-tools/main/AdGuardHome/AdGuardHome_linux_armv7`  
① 安装 AdGuardHome  
连接 SSH 后执行如下命令：
```
mkdir -p /data/AdGuardHome
curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/AdGuardHome/AdGuardHome_linux_armv8
chmod +x /data/AdGuardHome/AdGuardHome
/data/AdGuardHome/AdGuardHome -s install
/data/AdGuardHome/AdGuardHome -s start
```
② 升级 AdGuardHome  
连接 SSH 后执行如下命令：
```
curl -o /data/AdGuardHome/AdGuardHome -L https://ghproxy.com/https://raw.githubusercontent.com/DustinWin/clash-tools/main/AdGuardHome/AdGuardHome_linux_armv8
chmod +x /data/AdGuardHome/AdGuardHome && reboot
```
# 三、 配置 ShellClash 定时任务
可以在 ShellClash 里添加定时更新 Clash.Meta 内核、Yacd-meta 面板和 AdGuardHome 的任务，连接 SSH 后运行 `crontab -e`，按一下 Ins 键（Insert 键），在最下方粘贴如下内容：
- 注：留意链接后缀是否与 CPU 架构匹配

```
30 3 * * * curl -o /data/clash/clash -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@release/clash.meta-linux-armv8 && chmod +x /data/clash/clash && /data/clash/start.sh restart >/dev/null 2>&1 #每天早上 3 点半更新 Clash.Meta 内核
0 4 * * 1,3,5 curl -o /tmp/Yacd-meta.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/Yacd-meta/Yacd-meta.tar.gz && rm -rf /data/clash/ui/* && tar -zxf /tmp/Yacd-meta.tar.gz -C /data/clash/ui && rm -f /tmp/Yacd-meta.tar.gz && /data/clash/start.sh restart >/dev/null 2>&1 #每周一、三、五早上 4 点更新 Yacd-meta 面板
30 4 * * 2,4,6 curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash-tools@main/AdGuardHome/AdGuardHome_linux_armv8 && chmod +x /data/AdGuardHome/AdGuardHome && reboot >/dev/null 2>&1 #每周二、四、六早上 4 点半更新 AdGuardHome 并重启路由器
```
按一下 Esc 键（退出键），输入英文冒号“:”，继续输入“wq”并回车，再运行 `/etc/init.d/cron restart`
