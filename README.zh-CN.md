# Rockbase — 比特币独矿一体机

**[ 中文 ]** · [ English ](README.md)

---

### 这是什么？

Rockbase 是一台**开箱即用的比特币节点 + 独矿（Solo Mining）一体机**。

插上电源、连上网络，它就开始做两件事：

1. **运行一个比特币验证节点** —— 自己下载、验证区块链上的每一个区块，不依赖任何第三方数据（采用裁剪模式，只保留最近的区块数据以节省空间）；
2. **提供本地 Stratum 矿池接口** —— 把你的矿机接进来，直接挖比特币主网，挖到的区块奖励 100% 归你。

不需要装系统、不需要配软件、不需要懂命令行。设备自带一块彩色触摸屏和一套网页控制台，所有状态一目了然。

### 硬件规格

| 项目 | 参数 |
|------|------|
| 处理器 | Canaan K230（RISC-V 架构） |
| 内存 | 1 GB |
| 屏幕 | 彩色触摸屏（480×800 物理分辨率） |
| 网络 | 板载 WiFi + USB 转有线网卡（自动获取 IP） |
| 存储 | SD 卡（存放区块链数据） |
| 供电 | DC 电源 |

### 触摸屏界面

屏幕上有 4 个页面，**左右滑动即可切换**：

**① Bitcoind 页** —— 节点状态总览：当前区块高度、同步进度、连接的对等节点数、挖矿难度、UTXO 集大小。

![LCD Bitcoind 页](docs/img/lcd-bitcoind.png)

**② Stratum 页** —— 挖矿状态：矿池算力曲线、在线矿工数、最佳份额。

![LCD Stratum 页](docs/img/lcd-stratum.png)

**③ System 页** —— 设备健康：CPU 占用、温度、内存、区块链数据占用。

![LCD System 页](docs/img/lcd-system.png)

**④ Network 页** —— 网络信息：IP 地址、MAC 地址、WiFi 信号强度。

![LCD Network 页](docs/img/lcd-network.png)

**Peer Map（对等节点地图）** —— 在 Bitcoind 页点击节点数，可以看到一张世界地图，实时显示你的节点正在和全球哪些节点通信，连线动画表示数据流动方向。

![Peer Map](docs/img/lcd-peer-map.png)

### 网页控制台

用电脑或手机浏览器访问 `http://<设备IP>`（IP 可在 Network 页或路由器里查到），即可打开网页控制台。支持 10 种语言（英文、中文、西班牙语、法语、德语、葡萄牙语、俄语、日语、韩语、阿拉伯语），在页面右上角切换。

**Dashboard（仪表盘）** —— 一屏看全：节点同步状态、Stratum 端点与算力、CPU / 内存 / 温度 / 网络等系统指标。

![Web Dashboard](docs/img/web-dashboard.png)

**Miners（矿工）** —— 每台矿机的算力历史曲线、贡献份额，方便确认矿机是否正常工作。

![Web Miners](docs/img/web-miners.png)

**About（关于 / 固件更新）** —— 查看版本信息，并在这里进行固件升级（见下文）。

![Web About](docs/img/web-about.png)

### 网络连接

Rockbase 支持两种联网方式，开机时自动识别：

- **板载 WiFi** —— 连接家里的无线网即可；
- **USB 转有线网卡** —— 插一根 USB 网卡走有线网络，更稳定。兼容常见芯片的 USB 网卡（Realtek RTL8152/RTL8153、ASIX AX88179 千兆、AX88772 百兆等），即插即用，无需安装驱动。

两种方式都自动获取 IP（DHCP）。如果同时接了 USB 网卡和 WiFi，优先使用 USB 有线网络。

### 接入矿机

1. 确认矿机与 Rockbase 在**同一局域网**内；
2. 在矿机里填写矿池地址：

   ```
   stratum+tcp://<Rockbase的IP>:3333
   ```

   （IP 可在 LCD 的 Network 页或网页控制台看到；用户名/密码随意填写，例如 `worker1` / `x`）
3. 保存后，矿机开始向 Rockbase 提交工作量。在 LCD 的 Stratum 页或网页 Miners 页能看到算力曲线出现，即接入成功。

> 提示：建议给 Rockbase 在路由器里绑定固定 IP，避免重启后 IP 变化导致矿机断连。

### 固件升级

Rockbase 内置 **A/B 双分区 OTA 升级**，升级过程断电也不会变砖：

1. 打开网页控制台的 **About** 页；
2. 点击 **Check for Updates** 检查是否有新版本；
3. 有新版时点击 **Update Now**，设备会自动下载、校验签名、写入备用分区并重启；
4. 如果新固件启动异常，设备会**自动回滚**到旧版本。

所有固件包都发布在本仓库的 [Releases](https://github.com/NMminer1024/btc-solo-node-release/releases) 页面，设备检查更新时会自动从那里获取。

### 版本与发布说明

- 版本号格式：`vX.Y.ZZ`（如 `v0.4.00`），完整固件包名形如
  `v0.4.00-rockbase-k230-20260922-da181f46-ota`
  （版本号 - 平台 - 构建日期 - 代码指纹 - ota）；
- 所有固件包都经过**签名**，设备升级时会验证签名，确保固件来源可信；
- 历史版本可在 [Releases](https://github.com/NMminer1024/btc-solo-node-release/releases) 页面下载。

### 常见问题

**Q：刚开机要等多久才能用？**
A：首次启动需要下载并验证整个区块链（下载量约 15 GB），时间取决于网速，通常需要几个小时到一天。设备采用裁剪模式，验证完成后只保留最近约 4 GB 的区块数据。同步期间矿机可以正常接入，但出块概率极低；同步完成后即可正常挖矿。

**Q：矿机连不上怎么办？**
A：先确认两者在同一局域网；再确认矿机填的地址是 `stratum+tcp://IP:3333`（注意是 3333 端口）；最后看 LCD 的 Stratum 页是否显示 Running。

**Q：设备会发烫吗？**
A：正常工作温度约 55–65°C，System 页可实时查看。请保持设备周围通风良好。

**Q：如何重置设备？**
A：断电重新上电即可恢复。区块链数据保存在 SD 卡中，不会因重启丢失。

### 支持

- 固件下载与版本说明：[Releases](https://github.com/NMminer1024/btc-solo-node-release/releases)
- 问题反馈：请通过 GitHub Issues 提交，附上 LCD 截图或网页控制台截图会很有帮助。
