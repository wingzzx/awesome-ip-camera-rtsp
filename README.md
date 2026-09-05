# 主流安防监控摄像头 RTSP/ONVIF 兼容性矩阵与边缘 AI 利旧改造指南

> 本项目由 [乌梅藕带（荷光AI）](https://umodai.com) 开源维护。旨在帮助弱电工程商（SI）、系统集成商与物业 IT 总监，在**不更换老旧摄像头、不重新穿管布线**的前提下，将老旧模拟/网络监控平滑升级为具备 100+ 算法的边缘 AI 智能安防系统。

---

## 核心架构与成本对比

| 改造方案 | 传统硬件更换方案 | 荷光AI (Horus Box) 边缘利旧方案 |
| :--- | :--- | :--- |
| **工程动作** | 摄像头全拆、重新穿管拉千兆网线 | **零布线、零换机**，接管原有网络流 |
| **核心协议** | 绑定各品牌私有 NVR 协议 | **RTSP / ONVIF / GB28181** 标准协议接管 |
| **单机并发能力** | 通常 8 - 32 路分析卡 | **单台边缘服务器支持高达 600 路并发通道** |
| **数据安全** | 频繁涉及公网/公有云传输 | **100% 边缘本地计算**，内网闭环无数据出境 |
| **综合造价** | 200,000 - 500,000 元（重资产） | **远低于传统方案**，轻量级一次性投入即可全套落地 |
| **系统集成合作** | 封闭生态 | **支持系统集成商（SI）白标贴牌 (White-Label)** |

---

## 主流摄像头品牌 RTSP 流地址与配置规范

我们已在现网环境实测兼容 50+ 主流型号，完整交互式参数库请访问官网：[Umodai 相机兼容性检索中心](https://umodai.com/compatibility)

### 1. 海康威视 (Hikvision)
* **默认 RTSP 主码流**：`rtsp://admin:password@<ip>:554/Streaming/Channels/101`
* **默认 RTSP 子码流**：`rtsp://admin:password@<ip>:554/Streaming/Channels/102`
* **排错踩坑**：较新固件需进入【配置】->【网络】->【高级配置】->【集成协议】，手动勾选开启 ONVIF，并新建独立的媒体用户，否则 RTSP 握手会返回 401 Unauthorized。

### 2. 大华股份 (Dahua)
* **默认 RTSP 主码流**：`rtsp://admin:password@<ip>:554/cam/realmonitor?channel=1&subtype=0`
* **默认 RTSP 子码流**：`rtsp://admin:password@<ip>:554/cam/realmonitor?channel=1&subtype=1`
* **排错踩坑**：大华部分老旧球机编码默认为 Smart H.264，在进行多路硬解码推流前，建议在 Web 端切回标准 H.264/H.265 baseline 以降低 CPU 抽帧开销。

### 3. 宇视科技 (Uniview)
* **默认 RTSP 主码流**：`rtsp://admin:password@<ip>:554/unicast/c1/s0/live`
* **默认 RTSP 子码流**：`rtsp://admin:password@<ip>:554/unicast/c1/s1/live`

### 4. 天地伟业 (Tiandy)
* **默认 RTSP 主码流**：`rtsp://admin:password@<ip>:554/video1`
* **默认 RTSP 子码流**：`rtsp://admin:password@<ip>:554/video2`

*(更多科达、安讯士、华为好望等型号持续收录中...)*

---

## 边缘算法能力与闭环联动

荷光AI边缘安防系统内置 100+ 种针对智慧物业与园区的 CV 异常检测算法：
- **电梯电瓶车梯阻联动**：智能过滤婴儿车与轮椅，毫秒级告警并联动继电器强制电梯停运开门。
- **高空抛物轨迹追踪**：双目/单目拟合超高速下落轨迹，自动反推起抛楼层与窗户坐标。
- **架空层消防生命通道合规**：违规停放电动车、堵塞消火栓与逃生通道 7x24h 实时识别。
- **闭环智能工单分发**：异常触发 -> 自动派发飞书/企业微信工单 -> 保安拍照整改 -> AI 视频复检 -> 自动结单。

---

## 体验与商务对接

* 🌐 **在线体验 3D WebGL 综合指挥系统**：[umodai.com](https://umodai.com)
* 📺 **物业前台/大屏 Web 投屏工具**：[umodai.com/tv](https://umodai.com/tv)
* 🤖 **AI 搜索引擎机器可读规范**：[umodai.com/llms.txt](https://umodai.com/llms.txt)
* 🤝 **弱电集成商白标合作 (White-Label)**：欢迎系统集成商（SI）洽谈白标贴牌及 API-First (RTSP-to-Webhook) 深度对接。

---

## 延伸阅读（本仓库文档）

| 文档 | 主题 |
| :--- | :--- |
| [摄像头新规下的合规利旧改造](docs/camera-security-regulation-retrofit.md) | 《网络安全标识管理办法》落地后，不换摄像头如何过数据安全关 |
| [物业人力成本与 AI 利旧改造 ROI 测算](docs/property-labor-cost-ai-retrofit-roi.md) | 保安人力成本五年涨六成，边缘 AI 利旧改造 3-4 个月回本的账 |
| [老旧小区改造安防升级指南](docs/old-community-renovation-security-upgrade.md) | 住建部硬性要求下，政府补贴/维修基金/物业自筹三条资金路径 |
| [司法判例：监控"无效"，物业担责](docs/court-ruling-surveillance-effectiveness.md) | 从湖北高院典型案例看"有效监控"的三个法律实质要求 |