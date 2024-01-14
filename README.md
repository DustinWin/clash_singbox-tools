# 更新 [Clash Premium 内核](https://github.com/Dreamacro/clash/releases/tag/premium)、[Clash.Meta 内核](https://github.com/MetaCubeX/mihomo)、[sing-box 内核](https://github.com/SagerNet/sing-box)、[Clash](https://github.com/Dreamacro/clash) dashboard 面板和 [AdGuardHome](https://github.com/AdguardTeam/AdGuardHome)
# 一、 说明
每天凌晨（北京时间）自动构建生成：
1. Clash Premium Latest 版和 Release 版内核
2. Clash.Meta Alpha 版和 Release 版内核
3. sing-box Pre-release 版和 Release 版内核
4. Clash dashboard 面板：[Clash 官方面板](https://github.com/Dreamacro/clash-dashboard)、[Razord-meta 面板](https://github.com/MetaCubeX/Razord-meta)、[yacd 面板](https://github.com/haishanh/yacd)、[Yacd-meta 面板](https://github.com/MetaCubeX/Yacd-meta)和 [metacubexd 面板](https://github.com/MetaCubeX/metacubexd)

|面板类型|在线地址|
|-----|-----|
|Clash 官方面板|http://clash.razord.top|
|Razord-meta 面板|http://clash.metacubex.one|
|yacd 面板|http://yacd.haishan.me|
|Yacd-meta 面板|http://yacd.metacubex.one|
|metacubexd 面板|http://d.metacubex.one|
4. AdGuardHome Pre-release 版和 Release 版

注：
- 1. 本教程中的下载链接以 CPU 架构 ARMv8 为例，请注意修改链接后缀
- 2. 查看 CPU 架构可连接 SSH 后执行命令 `uname -ms`，若执行结果是“linux aarch64”，就是搭载的 ARMv8 架构

# 二、 使用方法
## 1. 导入内核 Linux 版（以 [ShellClash](https://github.com/juewuy/ShellCrash) 导入 Clash.Meta 内核为例）
CPU 架构和内核下载链接后缀对应关系如下：
|CPU 架构|AMD64|ARMv5|ARMv6|ARMv7|ARMv8|mips-softfloat|mipsle-hardfloat|mipsle-softfloat|
|-----|-----|-----|-----|-----|-----|-----|-----|-----|
|**链接后缀**|`amd64`|`armv5`|`armv6`|`armv7`|`armv8`|`mips-softfloat`|`mipsle-hardfloat`|`mipsle-softfloat`|

如 CPU 架构为 ARMv7，则下载链接须修改为：`https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/Clash.Meta-release/clash.meta-linux-armv7`
和 `https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/Clash.Meta-alpha/clash.meta-linux-armv7`  
连接 SSH 后执行如下命令：
```
# Release 版
curl -o $CRASHDIR/clash -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/Clash.Meta-release/clash.meta-linux-armv8
# Alpha 版
curl -o $CRASHDIR/clash -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/Clash.Meta-alpha/clash.meta-linux-armv8
chmod +x $CRASHDIR/clash && $CRASHDIR/start.sh restart
```
## 2. 导入内核 Windows 版（以 [Clash Verge](https://github.com/MetaCubeX/clash-verge) 导入 Clash.Meta 内核为例）
编辑文本文档，粘贴如下内容：
```
taskkill /f /t /im "Clash Verge*"
taskkill /f /t /im Clash-Verge*
taskkill /f /t /im mihomo*
# Release 版
curl -o %PROGRAMFILES%\Clash Verge\mihomo.exe -L https://mirror.ghproxy.com/https://raw.githubusercontent.com/DustinWin/clash_singbox-tools/main/Clash.Meta-release/clash.meta-windows-amd64.exe
# Pre-release 版
curl -o %PROGRAMFILES%\Clash Verge\mihomo.exe -L https://mirror.ghproxy.com/https://raw.githubusercontent.com/DustinWin/clash_singbox-tools/main/Clash.Meta-alpha/clash.meta-windows-amd64.exe
```
另存为 .bat 文件，右击并选择以管理员身份运行
## 3. 安装 Clash dashboard 面板（以 ShellClash 安装 metacubexd 面板为例）
Clash dashboard 面板类型和文件名对应关系如下：
|面板类型|文件名|
|-----|-----|
|Clash 官方面板|`clash-dashboard.tar.gz`|
|Razord-meta 面板|`Razord-meta.tar.gz`|
|yacd 面板|`yacd.tar.gz`|
|Yacd-meta 面板|`Yacd-meta.tar.gz`|
|metacubexd 面板|`metacubexd.tar.gz`|

如需要安装 Yacd-meta 面板，则命令中的文件名须修改为 `Yacd-meta.tar.gz` 且下载链接修改为 `https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/Clash-dashboard/Yacd-meta.tar.gz`  
连接 SSH 后执行如下命令：
```
curl -o /tmp/metacubexd.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/Clash-dashboard/metacubexd.tar.gz
mkdir -p $CRASHDIR/ui && tar -zxf /tmp/metacubexd.tar.gz -C $CRASHDIR/ui && rm -f /tmp/metacubexd.tar.gz
$CRASHDIR/start.sh restart
```
## 4. 安装 AdGuardHome
AdGuardHome CPU 架构和链接后缀对应关系如下：
|CPU 架构|AMD64|ARMv5|ARMv6|ARMv7|ARMv8|mips-softfloat|mipsle-softfloat|
|-----|-----|-----|-----|-----|-----|-----|-----|
|**链接后缀**|`amd64`|`armv5`|`armv6`|`armv7`|`armv8`|`mips-softfloat`|`mipsle-softfloat`|

如 CPU 架构为 ARMv7，则下载链接须修改为：  
`https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/AdGuardHome-release/AdGuardHome_linux_armv7` 和 `https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/AdGuardHome-prerelease/AdGuardHome_linux_armv7`  
① 安装 AdGuardHome  
连接 SSH 后执行如下命令：
```
mkdir -p /data/AdGuardHome
# Release 版
curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/AdGuardHome-release/AdGuardHome_linux_armv8
# Pre-release 版
curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/AdGuardHome-prerelease/AdGuardHome_linux_armv8
chmod +x /data/AdGuardHome/AdGuardHome
/data/AdGuardHome/AdGuardHome -s install
/data/AdGuardHome/AdGuardHome -s start
```
② 升级 AdGuardHome  
连接 SSH 后执行如下命令：
```
# Release 版
curl -o /data/AdGuardHome/AdGuardHome -L https://mirror.ghproxy.com/https://raw.githubusercontent.com/DustinWin/clash_singbox-tools/main/AdGuardHome-release/AdGuardHome_linux_armv8
# Pre-release 版
curl -o /data/AdGuardHome/AdGuardHome -L https://mirror.ghproxy.com/https://raw.githubusercontent.com/DustinWin/clash_singbox-tools/main/AdGuardHome-prerelease/AdGuardHome_linux_armv8
chmod +x /data/AdGuardHome/AdGuardHome
/data/AdGuardHome/AdGuardHome -s restart
```
# 三、 配置 ShellClash 定时任务
可以在 ShellClash 里添加定时更新 Clash.Meta 内核、metacubexd 面板和 AdGuardHome 的任务  
1. 连接 SSH 后执行 `vi $CRASHDIR/task/task.user`，按一下 Ins 键（Insert 键），粘贴如下内容：
- 注：留意链接后缀是否与 CPU 架构匹配

```
201#curl -o /data/clash/clash -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/Clash.Meta-release/clash.meta-linux-armv8 && chmod +x /data/clash/clash && /data/clash/start.sh restart >/dev/null 2>&1#更新Clash.Meta内核
202#curl -o /tmp/metacubexd.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/Clash-dashboard/metacubexd.tar.gz && rm -rf /data/clash/ui/* && tar -zxf /tmp/metacubexd.tar.gz -C /data/clash/ui && rm -f /tmp/metacubexd.tar.gz && /data/clash/start.sh restart >/dev/null 2>&1#更新metacubexd面板
203#curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/AdGuardHome-prerelease/AdGuardHome_linux_armv8 && chmod +x /data/AdGuardHome/AdGuardHome && /data/AdGuardHome/AdGuardHome -s restart >/dev/null 2>&1#更新AdGuardHome
```
2. 按一下 Esc 键（退出键），输入英文冒号`:`，继续输入 `wq` 并回车
3. 执行 `crash`，进入 ShellClash->5 配置自动任务->1 添加自动任务，可以看到末尾就有添加的定时任务，输入对应的数字并回车后可设置执行条件
