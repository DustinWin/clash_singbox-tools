**注意：本项目生成文件所在的分支已全部删除（包括文件历史记录），所有文件将不再发布到分支中，仅分发到 [Releases](https://github.com/DustinWin/clash_singbox-tools/releases) 中，以节省占用空间（文件历史记录过大），详细请看《[关于 GitHub 上的大文件](https://docs.github.com/zh/repositories/working-with-files/managing-large-files/about-large-files-on-github)》**

# 更新 [mihomo 内核](https://github.com/MetaCubeX/mihomo)、[sing-box 内核](https://github.com/SagerNet/sing-box)、[sing-box PuerNya 版内核](https://github.com/PuerNya/sing-box/tree/building)、Clash dashboard 面板和 [AdGuard Home](https://github.com/AdguardTeam/AdGuardHome)
# 一、 说明
每天凌晨（北京时间 UTC+8）自动构建生成：
1. Clash Premium Release 版和 Nightly 版[内核](https://github.com/DustinWin/clash_singbox-tools/releases/tag/Clash-Premium)（已停更）
2. mihomo Meta 版和 Alpha 版内核
3. sing-box Release 版和 Dev 版内核
4. sing-box PuerNya 版内核（支持 `outbound_providers` 代理集合）
5. Clash dashboard 面板：[Razord-meta 面板](https://github.com/MetaCubeX/Razord-meta)、[yacd 面板](https://github.com/haishanh/yacd)、[Yacd-meta 面板](https://github.com/MetaCubeX/Yacd-meta)、[metacubexd 面板](https://github.com/MetaCubeX/metacubexd)和 [zashboard 面板](https://github.com/Zephyruso/zashboard)
6. AdGuard Home Release 版和 Beta 版

**注：**
- 1. 本教程中的下载链接以 CPU 架构 ARMv8 为例，请注意修改链接后缀
- 2. 查看 CPU 架构可连接 SSH 后执行命令 `uname -ms`，若执行结果是“linux aarch64”，就是搭载的 ARMv8 架构

# 二、 使用方法
## 1. 导入内核（以 [ShellCrash](https://github.com/juewuy/ShellCrash) 导入内核为例）
**mihomo 内核和 sing-box 内核 Linux 版下载链接后缀和 CPU 架构对应关系如下表：**
|CPU 架构|AMD64|AMD64v3|ARMv5|ARMv6|ARMv7|ARMv8&ARM64&AArch64|mips-softfloat|mipsle-hardfloat|mipsle-softfloat|
|-----|-----|-----|-----|-----|-----|:---:|-----|-----|-----|
|**链接后缀**|`amd64`|`amd64v3`|`armv5`|`armv6`|`armv7`|`armv8`|`mips-softfloat`|`mipsle-hardfloat`|`mipsle-softfloat`|

<details>
<summary>① 首次导入</summary>

连接 SSH 后执行如下命令：
```
# mihomo 内核 Meta 版
curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@mihomo/mihomo-meta-linux-armv8.tar.gz | tar -zx -C /tmp/ && crash
# mihomo 内核 Alpha 版
curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@mihomo/mihomo-alpha-linux-armv8.tar.gz | tar -zx -C /tmp/ && crash
# sing-box 内核 PuerNya 版
curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@sing-box/sing-box-puernya-linux-armv8.tar.gz | tar -zx -C /tmp/ && crash
# sing-box 内核 Release 版
curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@sing-box/sing-box-release-linux-armv8.tar.gz | tar -zx -C /tmp/ && crash
# sing-box 内核 Dev 版
curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@sing-box/sing-box-dev-linux-armv8.tar.gz | tar -zx -C /tmp/ && crash
```
此时脚本会自动“发现可用的内核文件”，选择 1 加载，后选择对应的内核  
</details>
<details>
<summary>② 升级导入（ShellCrash -> 9 更新/卸载 -> 2 切换内核文件，内核版本不会刷新）</summary>

连接 SSH 后执行如下命令：
```
# mihomo 内核 Meta 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@mihomo/mihomo-meta-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
# mihomo 内核 Alpha 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@mihomo/mihomo-alpha-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
# sing-box 内核 PuerNya 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@sing-box/sing-box-puernya-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
# sing-box 内核 Release 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools/@sing-box/sing-box-release-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
# sing-box 内核 Dev 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@sing-box/sing-box-dev-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
```
</details>

## 2. 安装 Clash Dashboard 面板（以 ShellCrash 安装 metacubexd 面板为例）
**Clash Dashboard 面板对应文件名和在线地址关系如下表：**
|面板类型|文件名|在线地址|
|-----|-----|-----|
|Razord-meta 面板|`Razord-meta.tar.gz`|<https://clash.metacubex.one>|
|yacd 面板|`yacd.tar.gz`|<https://yacd.haishan.me>|
|Yacd-meta 面板|`Yacd-meta.tar.gz`|<https://yacd.metacubex.one>|
|metacubexd 面板|`metacubexd.tar.gz`|<https://metacubex.github.io/metacubexd/>|
|zashboard 面板|`zashboard.tar.gz`|<https://board.zash.run.place>|

连接 SSH 后执行如下命令：
```
curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@Dashboard/metacubexd.tar.gz | tar -zx -C $CRASHDIR/ui/ && $CRASHDIR/start.sh restart
```
## 3. 安装 AdGuard Home
**AdGuard Home Linux 版 CPU 架构和链接后缀对应关系如下表：**
|CPU 架构|AMD64|ARMv5|ARMv6|ARMv7|ARMv8|mips-softfloat|mipsle-softfloat|
|-----|-----|-----|-----|-----|-----|-----|-----|
|**链接后缀**|`amd64`|`armv5`|`armv6`|`armv7`|`armv8`|`mips-softfloat`|`mipsle-softfloat`|

<details>
<summary>① 安装 AdGuard Home</summary>

连接 SSH 后执行如下命令：
```
mkdir -p /data/AdGuardHome
# AdGuard Home Release 版
curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@AdGuardHome/AdGuardHome_release_linux_armv8
# AdGuard Home Beta 版
curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@AdGuardHome/AdGuardHome_beta_linux_armv8
chmod +x /data/AdGuardHome/AdGuardHome
/data/AdGuardHome/AdGuardHome -s install
/data/AdGuardHome/AdGuardHome -s start
```
</details>
<details>
<summary>② 升级 AdGuard Home</summary>

连接 SSH 后执行如下命令：
```
# AdGuard Home Release 版
curl -o /data/AdGuardHome/AdGuardHome -L https://ghgo.xyz/https://github.com/DustinWin/clash_singbox-tools/releases/download/AdGuardHome/AdGuardHome_release_linux_armv8
# AdGuard Home Beta 版
curl -o /data/AdGuardHome/AdGuardHome -L https://ghgo.xyz/https://github.com/DustinWin/clash_singbox-tools/releases/download/AdGuardHome/AdGuardHome_beta_linux_armv8
/data/AdGuardHome/AdGuardHome -s restart
```
</details>

# 三、 扩展（以 ShellCrash 配置定时任务为例）
可在 ShellCrash 里添加定时更新 mihomo 内核、sing-box 内核、metacubexd 面板和 AdGuard Home 的任务
1. 连接 SSH 后执行 `vi $CRASHDIR/task/task.user`，按一下 Ins 键（Insert 键），粘贴如下内容：
注：
- 1. 留意链接后缀是否与 CPU 架构匹配
- 2. ShellCrash 安装路径为 */data/ShellCrash*

```
201#curl -o /data/ShellCrash/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@mihomo/mihomo-meta-linux-armv8.tar.gz && /data/ShellCrash/start.sh restart >/dev/null 2>&1#更新mihomo内核
202#curl -o /data/ShellCrash/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@sing-box/sing-box-puernya-linux-armv8.tar.gz && /data/ShellCrash/start.sh restart >/dev/null 2>&1#更新sing-box_PuerNya版内核
203#curl -o /data/ShellCrash/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@sing-box/sing-box-release-linux-armv8.tar.gz && /data/ShellCrash/start.sh restart >/dev/null 2>&1#更新sing-box内核
204#curl -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@Dashboard/metacubexd.tar.gz | tar -zx -C $CRASHDIR/ui/ && /data/ShellCrash/start.sh restart >/dev/null 2>&1#更新metacubexd面板
205#curl -o /data/AdGuardHome/AdGuardHome -L https://cdn.jsdelivr.net/gh/DustinWin/clash_singbox-tools@AdGuardHome/AdGuardHome_beta_linux_armv8 && /data/AdGuardHome/AdGuardHome -s restart >/dev/null 2>&1#更新AdGuardHome
```
2. 按一下 Esc 键（退出键），输入英文冒号 `:`，继续输入 `wq` 并回车
3. 执行 `crash`，进入 ShellCrash -> 5 配置自动任务 -> 1 添加自动任务，可以看到末尾就有添加的定时任务，输入对应的数字并回车后可设置执行条件
