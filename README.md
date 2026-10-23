# 黑粉助手

**手机连接电脑上的 AI。** 电脑运行 DeepSeek Harness 原任务，手机浏览器进入同一工作区，查看会话并继续发送要求。

黑粉科技制作的独立辅助工具，当前为 **0.1.2 预览版**。官方 Harness 是被连接的目标软件，需要先在电脑上安装、配置好模型并能正常使用。黑粉助手内置自己的运行依赖，无需另外安装 Node.js、通道程序或二维码组件。

## 近期新增与改进

- 精简连接界面：接入会话、启动连接、手机扫码，状态清楚。
- 修复断开确认：取消、确认与退出键可用，更新弹窗文案独立。
- 保留入口设置：重新打开页面可看到已保存的地址，证书可继续沿用。
- 匿名使用统计：按日去重，支持在检查页关闭，不采集会话和配对资料。
- 官网与赞助入口：侧栏查看更多自制软件，自愿扫码支持开发。

## 下载与安装

通过[发行页](https://github.com/HackerChi-Hub/hyphen-assistant-releases/releases)选择对应系统的安装包，并核对同名 `.sha256` 文件。没有附件的平台暂不提供下载，不使用源码压缩包代替安装包。

| 系统 | 安装方式 | 下载 |
|---|---|---|
| macOS Apple Silicon，13及以上 | 下载DMG，把黑粉助手拖入应用程序 | [Mac安装包](https://github.com/HackerChi-Hub/hyphen-assistant-releases/releases/latest/download/HyphenAssistant-0.1.2-macos-arm64.dmg) |
| Windows x64 | 下载EXE安装程序，按向导安装；包含离线WebView2安装器 | [Windows安装程序](https://github.com/HackerChi-Hub/hyphen-assistant-releases/releases/latest/download/HyphenAssistant-0.1.2-windows-x64-setup.exe) |
| Linux x64 | 使用AppImage或适合发行版的deb/rpm包，仍需兼容的桌面系统；AppImage首次需在文件属性中允许作为程序执行 | [AppImage](https://github.com/HackerChi-Hub/hyphen-assistant-releases/releases/latest/download/HyphenAssistant-0.1.2-linux-x64.AppImage) · [deb](https://github.com/HackerChi-Hub/hyphen-assistant-releases/releases/latest/download/HyphenAssistant-0.1.2-linux-x64.deb) · [rpm](https://github.com/HackerChi-Hub/hyphen-assistant-releases/releases/latest/download/HyphenAssistant-0.1.2-linux-x64.rpm) |

安装件尚未完成 Apple 公证或 Windows 商业代码签名。Mac首次打开受阻时，在系统设置的“隐私与安全性”中核实来源后选择仍要打开；Windows出现SmartScreen提示时核实发行来源，再按“更多信息”继续。更新包的数字签名用于校验更新完整性，不等同于操作系统发行证书。

## 实际界面

以下为0.1.2预览版Mac实际安装界面，未展示私人配对码。

![黑粉助手连接中心](screenshots/connection.png)

![端口映射设置示例，示例地址未保存](screenshots/network.png)

![匿名统计设置](screenshots/privacy.png)

## 两种连接方式

| 方式 | 使用方法 | 用户需要准备 |
|---|---|---|
| 临时链接 | 启动后自动生成地址，再扫码配对 | 网络能访问内置通道服务 |
| 端口映射 | 将公网TCP端口映射到应用显示的本机地址及端口 | 公网可达条件、路由器映射、访问域名及HTTPS证书 |

端口映射方式通过受配对保护的HTTPS入口访问dsh；模型接口密钥仍由原Harness管理。域名可使用现有动态解析服务维护，树莓派是可选的部署设备。公网端口与本机端口可以不同，界面会显示映射关系。

## 第一次使用

1. 先打开官方 DeepSeek Harness，确认电脑能正常收到模型回复。
2. 打开黑粉助手。已有手机连接器时选择“接入已有 Harness”；新用户选择当前 Harness 配置，点击挂载连接器。
3. 等待 Harness 加载连接器。若未自动加载，等原任务空闲后重新打开 Harness，不中断正在进行的任务。
4. 点击启动远程连接，等待入口就绪。
5. 生成二维码，用本人手机系统浏览器扫码并确认配对。
6. 进入一个不重要的会话，发送“只回复：手机连接正常，不调用工具”，核实实际回复。

## 网络与费用边界

内置临时通道由 Cloudflare 转发，网页内容经过该服务，需要网络可达，没有持续可用保证，重新创建后地址变化。第三方通道不支持的传输方式可能影响特定功能，真实消息和长任务恢复须实际核实。端口映射方式需要用户准备访问地址和HTTPS证书，并让路由器将公网TCP端口映射到本机指定地址及端口。域名解析、动态域名维护、端口映射和证书续期由用户管理，应用不会自动配置树莓派、路由器或防火墙。导入的证书保存为应用私有副本，不自动继承旧服务的续期链路。

工具不包含模型权重、供应商额度、域名或第三方付费服务。模型请求的费用与数据流向继续由原 Harness 配置决定。电脑、Harness、所用模型服务及网络须保持在线。

## 隐私与管理

二维码、链接和配对资料仅交给本人设备。配对后可操作原会话，手机浏览器应妥善保管。关闭窗口收起到菜单栏或托盘，退出界面保留后台；停止本应用连接不停止原任务。撤销登录会要求手机重新配对。

匿名统计仅包含不可逆设备哈希、应用版本、系统和架构，用于统计活跃设备与版本分布；默认开启，可在“检查与帮助”关闭。不采集会话、指令、文件、密钥、配对资料或用户名，统计数据库不保存 IP。设备哈希在本机按产品隔离后生成。同一设备同一 UTC 日去重，升级当天可更新版本。

源码仓库私有；本仓库发布使用说明、真实截图、安装件与更新元数据。安装件不包含开发者证书私钥、原会话、模型密钥或私人部署配置。

## 常见问题

**打开了但没有原会话？** 检查原 Harness 是否在线、配置是否选对、连接器是否加载，进入检查页查看原会话认证。

**临时连接失败？** 检查网络可达性，稍后重试或改用端口映射。不要关闭来源校验、证书校验或配对保护。

**配对失效？** 使用最新生成的完整链接，在十分钟内兑换；每个浏览器分别配对。网关重启后需要重新配对。

**手机切网和长任务是否都可靠？** 以当前发行说明列出的实际验收为准，一次页面打开不代表所有场景均已通过。

## 已核实的验收范围

- Mac：从DMG安装，原生界面、内置后端、真实Harness认证、临时通道HTTPS配对、原网页、原会话目录和实时握手通过。
- Windows：原生27项检查、中文EXE安装、安装后内置后端及应用启动检查通过。
- Linux：原生27项检查、AppImage解包后的内置后端及虚拟桌面启动检查通过；同时提供deb和rpm。
- 三个平台的安装件都有SHA-256；更新包另有独立数字签名。Mac和Linux AppImage支持对应的签名更新包，deb/rpm使用新版安装包更新。
- 真实手机切网、真实任务工具批准和长任务恢复仍待专项验收；隔离启动检查不等同于真机持续使用。

## 相关资源

- [官方 DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness)
- [Cloudflare 临时通道说明](https://developers.cloudflare.com/tunnel/get-started/quick-tunnels/)
- [黑粉科技](https://hyphentech.top)
