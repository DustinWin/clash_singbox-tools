# 更新 [Clash Premium 内核](https://github.com/Dreamacro/clash/releases/tag/premium)、[mihomo 内核](https://github.com/MetaCubeX/mihomo)、[sing-box 内核](https://github.com/SagerNet/sing-box)、[sing-box PuerNya 版内核](https://github.com/PuerNya/sing-box)、[Clash](https://github.com/Dreamacro/clash) dashboard 面板和 [AdGuardHome](https://github.com/AdguardTeam/AdGuardHome)
# 一、 说明
每天凌晨（北京时间）自动构建生成：
1. Clash Premium Release 版和 Latest 版内核（已停更）
2. mihomo Release 版和 Alpha 版内核
3. sing-box Release 版和 Pre-release 版内核
4. sing-box PuerNya 版内核（支持 `outbound_providers` 代理集合）
5. Clash dashboard 面板：[Clash 官方面板](https://github.com/Dreamacro/clash-dashboard)、[Razord-meta 面板](https://github.com/MetaCubeX/Razord-meta)、[yacd 面板](https://github.com/haishanh/yacd)、[Yacd-meta 面板](https://github.com/MetaCubeX/Yacd-meta)和 [metacubexd 面板](https://github.com/MetaCubeX/metacubexd)
5. AdGuardHome Release 版和 Pre-release 版

**注：**
- 1. 本教程中的下载链接以 CPU 架构 ARMv8 为例，请注意修改链接后缀
- 2. 查看 CPU 架构可连接 SSH 后执行命令 `uname -ms`，若执行结果是“linux aarch64”，就是搭载的 ARMv8 架构

# 二、 使用方法
## 1. 导入内核到 Linux 端（以 [ShellCrash](https://github.com/juewuy/ShellCrash) 导入内核为例）
**mihomo 内核下载链接后缀和 CPU 架构对应关系如下表：**
|CPU 架构|AMD64|ARMv5|ARMv6|ARMv7|ARMv8&ARM64&AArch64|mips-softfloat|mipsle-hardfloat|mipsle-softfloat|
|-----|-----|-----|-----|-----|:---:|-----|-----|-----|
|**链接后缀**|`amd64`|`armv5`|`armv6`|`armv7`|`armv8`|`mips-softfloat`|`mipsle-hardfloat`|`mipsle-softfloat`|

**sing-box 内核下载链接后缀和 CPU 架构对应关系如下表：**
|CPU 架构|AMD64|AMD64v3|ARMv5|ARMv6|ARMv7|ARMv8&ARM64&AArch64|mips-softfloat|mipsle-hardfloat|mipsle-softfloat|
|-----|-----|-----|-----|-----|-----|:---:|-----|-----|-----|
|**链接后缀**|`amd64`|`amd64v3`|`armv5`|`armv6`|`armv7`|`armv8`|`mips-softfloat`|`mipsle-hardfloat`|`mipsle-softfloat`|

① 首次导入  
连接 SSH 后执行如下命令：
```
# mihomo 内核 Release 版
curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/mihomo-release/mihomo-linux-armv8.tar.gz | tar -zx -C /tmp/ && mv -f /tmp/CrashCore /tmp/mihomo-linux-armv8 && crash
# mihomo 内核 Alpha 版
curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/mihomo-alpha/mihomo-linux-armv8.tar.gz | tar -zx -C /tmp/ && mv -f /tmp/CrashCore /tmp/mihomo-linux-armv8 && crash
# sing-box 内核 Release 版
curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/sing-box-release/sing-box-linux-armv8.tar.gz | tar -zx -C /tmp/ && mv -f /tmp/CrashCore /tmp/sing-box-linux-armv8 && crash
# sing-box 内核 Pre-release 版
curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/sing-box-prerelease/sing-box-linux-armv8.tar.gz | tar -zx -C /tmp/ && mv -f /tmp/CrashCore /tmp/sing-box-linux-armv8 && crash
# sing-box 内核 PuerNya 版
curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/sing-box-puernya/sing-box-linux-armv8.tar.gz | tar -zx -C /tmp/ && mv -f /tmp/CrashCore /tmp/sing-box-linux-armv8 && crash
```
此时脚本会自动“发现可用的内核文件”，选择 1 加载，后选择对应的内核  
② 升级导入  
连接 SSH 后执行如下命令：
```
# mihomo 内核 Release 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/mihomo-release/mihomo-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
# mihomo 内核 Alpha 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/mihomo-alpha/mihomo-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
# sing-box 内核 Release 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/sing-box-release/sing-box-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
# sing-box 内核 Pre-release 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/sing-box-prerelease/sing-box-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
# sing-box 内核 PuerNya 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/sing-box-puernya/sing-box-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
```
## 2. 导入内核到 Windows 端（以 [Clash Verge](https://github.com/clash-verge-rev/clash-verge-rev) 导入 mihomo 内核为例，且 Clash Verge 为默认安装路径）
以管理员身份打开 CMD 命令提示符，执行如下命令：
```
taskkill /f /t /im "Clash Verge*"
taskkill /f /t /im Clash-Verge*
taskkill /f /t /im clash-meta*
# mihomo 内核 Release 版
curl -o "%LOCALAPPDATA%\Clash Verge\clash-meta.exe" -L https://mirror.ghproxy.com/https://raw.githubusercontent.com/DustinWin/clash_singbox-tools/main/mihomo-release/mihomo-windows-amd64-compatible.exe
curl -o "%LOCALAPPDATA%\Clash Verge\clash-meta.exe" -L https://mirror.ghproxy.com/https://raw.githubusercontent.com/DustinWin/clash_singbox-tools/main/mihomo-release/mihomo-windows-amd64.exe
# mihomo 内核 Alpha 版
curl -o "%LOCALAPPDATA%\Clash Verge\clash-meta-alpha.exe" -L https://mirror.ghproxy.com/https://raw.githubusercontent.com/DustinWin/clash_singbox-tools/main/mihomo-alpha/mihomo-windows-amd64-compatible.exe
curl -o "%LOCALAPPDATA%\Clash Verge\clash-meta-alpha.exe" -L https://mirror.ghproxy.com/https://raw.githubusercontent.com/DustinWin/clash_singbox-tools/main/mihomo-alpha/mihomo-windows-amd64.exe
```
## 3. 安装 Clash dashboard 面板（以 ShellCrash 安装 metacubexd 面板为例）
**Clash dashboard 面板对应文件名和在线地址关系如下表：**
|面板类型|文件名|在线地址|
|-----|-----|-----|
|Clash 官方面板|`clash-dashboard.tar.gz`|https://clash.razord.top|
|Razord-meta 面板|`Razord-meta.tar.gz`|https://clash.metacubex.one|
|yacd 面板|`yacd.tar.gz`|https://yacd.haishan.me|
|Yacd-meta 面板|`Yacd-meta.tar.gz`|https://yacd.metacubex.one|
|metacubexd 面板|`metacubexd.tar.gz`|https://metacubex.github.io/metacubexd|

连接 SSH 后执行如下命令：
```
curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/Clash-dashboard/metacubexd.tar.gz | tar -zx -C $CRASHDIR/ui/ && $CRASHDIR/start.sh restart
```
## 4. 安装 AdGuardHome
**AdGuardHome CPU 架构和链接后缀对应关系如下表：**
|CPU 架构|AMD64|ARMv5|ARMv6|ARMv7|ARMv8|mips-softfloat|mipsle-softfloat|
|-----|-----|-----|-----|-----|-----|-----|-----|
|**链接后缀**|`amd64`|`armv5`|`armv6`|`armv7`|`armv8`|`mips-softfloat`|`mipsle-softfloat`|

① 安装 AdGuardHome  
连接 SSH 后执行如下命令：
```
mkdir -p /data/AdGuardHome
# AdGuardHome Release 版
curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/AdGuardHome-release/AdGuardHome_linux_armv8
# AdGuardHome Pre-release 版
curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/AdGuardHome-prerelease/AdGuardHome_linux_armv8
chmod +x /data/AdGuardHome/AdGuardHome
/data/AdGuardHome/AdGuardHome -s install
/data/AdGuardHome/AdGuardHome -s start
```
② 升级 AdGuardHome  
连接 SSH 后执行如下命令：
```
# AdGuardHome Release 版
curl -o /data/AdGuardHome/AdGuardHome -L https://mirror.ghproxy.com/https://raw.githubusercontent.com/DustinWin/clash_singbox-tools/main/AdGuardHome-release/AdGuardHome_linux_armv8
# AdGuardHome Pre-release 版
curl -o /data/AdGuardHome/AdGuardHome -L https://mirror.ghproxy.com/https://raw.githubusercontent.com/DustinWin/clash_singbox-tools/main/AdGuardHome-prerelease/AdGuardHome_linux_armv8
chmod +x /data/AdGuardHome/AdGuardHome
/data/AdGuardHome/AdGuardHome -s restart
```
# 三、 配置 ShellCrash 定时任务
可以在 ShellCrash 里添加定时更新 mihomo 内核、sing-box 内核、metacubexd 面板和 AdGuardHome 的任务  
1. 连接 SSH 后执行 `vi $CRASHDIR/task/task.user`，按一下 Ins 键（Insert 键），粘贴如下内容：
注：
- 1. 留意链接后缀是否与 CPU 架构匹配
- 2. ShellCrash 安装路径为 */data/ShellCrash*

```
201#curl -o /data/ShellCrash/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/mihomo-release/mihomo-linux-armv8.tar.gz && /data/ShellCrash/start.sh restart >/dev/null 2>&1#更新mihomo内核
202#curl -o /data/ShellCrash/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/sing-box-release/sing-box-linux-armv8.tar.gz && /data/ShellCrash/start.sh restart >/dev/null 2>&1#更新sing-box内核
203#curl -o /data/ShellCrash/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/sing-box-puernya/sing-box-linux-armv8.tar.gz && /data/ShellCrash/start.sh restart >/dev/null 2>&1#更新sing-box-PuerNya内核
204#curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/Clash-dashboard/metacubexd.tar.gz | tar -zx -C $CRASHDIR/ui/ && /data/ShellCrash/start.sh restart >/dev/null 2>&1#更新metacubexd面板
205#curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@main/AdGuardHome-prerelease/AdGuardHome_linux_armv8 && /data/AdGuardHome/AdGuardHome -s restart >/dev/null 2>&1#更新AdGuardHome
```
2. 按一下 Esc 键（退出键），输入英文冒号 `:`，继续输入 `wq` 并回车
3. 执行 `crash`，进入 ShellCrash->5 配置自动任务->1 添加自动任务，可以看到末尾就有添加的定时任务，输入对应的数字并回车后可设置执行条件
