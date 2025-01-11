# 更新 [mihomo 内核](https://github.com/MetaCubeX/mihomo)、[sing-box 内核](https://github.com/SagerNet/sing-box)、[sing-box PuerNya 版内核](https://github.com/PuerNya/sing-box/tree/building)、Dashboard 面板和 [AdGuard Home](https://github.com/AdguardTeam/AdGuardHome)
# 一、 说明
每天凌晨（北京时间 UTC+8）自动构建生成：
1. [Clash Premium Release 版和 Nightly 版内核](https://github.com/DustinWin/proxy-tools/releases/tag/Clash-Premium)（已停更）
2. mihomo [Meta 版](https://github.com/MetaCubeX/mihomo/tree/Meta)和 [Alpha 版](https://github.com/MetaCubeX/mihomo/tree/Alpha)内核
3. sing-box [Release 版](https://github.com/SagerNet/sing-box/tree/main)、[Dev 版](https://github.com/SagerNet/sing-box/tree/dev)和 [PuerNya 版](https://github.com/PuerNya/sing-box/tree/building)（支持[出站提供者](https://sing-boxp.dustinwin.top/zh/configuration/provider/) `outbound_providers`，类似于 mihomo 内核的[代理集合](https://wiki.metacubex.one/config/proxy-providers/) `proxy-providers`）内核
4. Dashboard 面板：[yacd 面板](https://github.com/haishanh/yacd)、[Yacd-meta 面板](https://github.com/MetaCubeX/Yacd-meta)、[metacubexd 面板](https://github.com/MetaCubeX/metacubexd)和 [zashboard 面板](https://github.com/Zephyruso/zashboard)
5. AdGuard Home [Release 版](https://github.com/AdguardTeam/AdGuardHome/tree/beta-v0.107)和 [Beta 版](https://github.com/AdguardTeam/AdGuardHome/tree/beta-v0.108)

**注：**
- 1. 本教程中的下载链接以 CPU 架构 ARMv8 为例，请注意修改链接后缀
- 2. 查看 CPU 架构可连接 SSH 后执行命令 `uname -ms`，若执行结果是“linux aarch64”，就是搭载的 ARMv8 架构
- 3. 对下载源的说明，可[点此](https://proxy-tutorials.dustinwin.top/about/#%E5%AF%B9%E4%B8%8B%E8%BD%BD%E6%BA%90%E7%9A%84%E8%AF%B4%E6%98%8E)了解

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
curl -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/mihomo/mihomo-meta-linux-armv8.tar.gz | tar -zx -C /tmp/ && crash
# mihomo 内核 Alpha 版
curl -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/mihomo/mihomo-alpha-linux-armv8.tar.gz | tar -zx -C /tmp/ && crash
# sing-box 内核 PuerNya 版
curl -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/sing-box/sing-box-puernya-linux-armv8.tar.gz | tar -zx -C /tmp/ && crash
# sing-box 内核 Release 版
curl -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/sing-box/sing-box-release-linux-armv8.tar.gz | tar -zx -C /tmp/ && crash
# sing-box 内核 Dev 版
curl -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/sing-box/sing-box-dev-linux-armv8.tar.gz | tar -zx -C /tmp/ && crash
```
此时脚本会自动“发现可用的内核文件”，选择 1 加载，后选择对应的内核  
</details>
<details>
<summary>② 升级导入（ShellCrash -> 9 更新/卸载 -> 2 切换内核文件，内核版本不会刷新）</summary>

连接 SSH 后执行如下命令：
```
# mihomo 内核 Meta 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/mihomo/mihomo-meta-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
# mihomo 内核 Alpha 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/mihomo/mihomo-alpha-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
# sing-box 内核 PuerNya 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/sing-box/sing-box-puernya-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
# sing-box 内核 Release 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://cdn.jsdelivr.net/gh/DustinWin/proxy-tools/@sing-box/sing-box-release-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
# sing-box 内核 Dev 版
curl -o $CRASHDIR/CrashCore.tar.gz -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/sing-box/sing-box-dev-linux-armv8.tar.gz && $CRASHDIR/start.sh restart
```
</details>

## 2. 安装 Dashboard 面板（以 ShellCrash 安装 metacubexd 面板为例）
**Dashboard 面板对应文件名和网址关系如下表：**
|面板名称|文件名|网址|
|-----|-----|-----|
|yacd 面板|`yacd.tar.gz`|<https://yacd.haishan.me>|
|Yacd-meta 面板|`Yacd-meta.tar.gz`|<https://yacd.metacubex.one>|
|metacubexd 面板|`metacubexd.tar.gz`|<https://metacubex.github.io/metacubexd/>|
|zashboard 面板|`zashboard.tar.gz`|<https://board.zash.run.place>|

连接 SSH 后执行如下命令：
```
curl -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/Dashboard/metacubexd.tar.gz | tar -zx -C $CRASHDIR/ui/ && $CRASHDIR/start.sh restart
```
- 注：若使用基于 [Chromium 项目](https://www.chromium.org/Home/)开发的浏览器打开网址去访问 Dashboard 面板时，以 [Chrome 浏览器](https://www.google.com/chrome/)为例，需要设置该网址域名“允许显示不安全内容”。方法如下：  
进入设置 -> 隐私和安全 -> 网站设置 -> 更多内容设置 -> 不安全内容（或者地址栏直接打开 chrome://settings/content/insecureContent 进行设置），在“允许显示不安全内容”内添加网址域名如：`metacubex.github.io`

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
curl -o /data/AdGuardHome/AdGuardHome -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/AdGuardHome/AdGuardHome_release_linux_armv8
# AdGuard Home Beta 版
curl -o /data/AdGuardHome/AdGuardHome -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/AdGuardHome/AdGuardHome_beta_linux_armv8
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
curl -o /data/AdGuardHome/AdGuardHome -L https://ghgo.xyz/https://github.com/DustinWin/proxy-tools/releases/download/AdGuardHome/AdGuardHome_release_linux_armv8
# AdGuard Home Beta 版
curl -o /data/AdGuardHome/AdGuardHome -L https://ghgo.xyz/https://github.com/DustinWin/proxy-tools/releases/download/AdGuardHome/AdGuardHome_beta_linux_armv8
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
201#curl -o /data/ShellCrash/CrashCore.tar.gz -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/mihomo/mihomo-meta-linux-armv8.tar.gz && /data/ShellCrash/start.sh restart >/dev/null 2>&1#更新mihomo内核
202#curl -o /data/ShellCrash/CrashCore.tar.gz -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/sing-box/sing-box-puernya-linux-armv8.tar.gz && /data/ShellCrash/start.sh restart >/dev/null 2>&1#更新sing-box_PuerNya版内核
203#curl -o /data/ShellCrash/CrashCore.tar.gz -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/sing-box/sing-box-release-linux-armv8.tar.gz && /data/ShellCrash/start.sh restart >/dev/null 2>&1#更新sing-box内核
204#curl -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/Dashboard/metacubexd.tar.gz | tar -zx -C $CRASHDIR/ui/ && /data/ShellCrash/start.sh restart >/dev/null 2>&1#更新metacubexd面板
205#curl -o /data/AdGuardHome/AdGuardHome -L https://ghfast.top/https://github.com/DustinWin/proxy-tools/releases/download/AdGuardHome/AdGuardHome_beta_linux_armv8 && /data/AdGuardHome/AdGuardHome -s restart >/dev/null 2>&1#更新AdGuardHome
```
2. 按一下 Esc 键（退出键），输入英文冒号 `:`，继续输入 `wq` 并回车
3. 执行 `crash`，进入 ShellCrash -> 5 配置自动任务 -> 1 添加自动任务，可以看到末尾就有添加的定时任务，输入对应的数字并回车后可设置执行条件