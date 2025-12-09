# ArenaMatrix

## 📖 简介 (Introduction)

**ArenaMatrix (AM)** 是一款专为 **房间式多人在线游戏和实时互动应用** 设计的开源商业级全栈引擎。

别称：`AM 引擎`、`Arena引擎`、`阿瑞娜引擎`、`阿瑞娜矩阵`、`竞技矩阵`。

通过 AM，开发者可以轻松开发出如 MOBA、IO、FPS、RTS、在线抢答、单词PK 等在线游戏和应用。

在当前的多人在线游戏和实时互动应用开发中，跨端同步依然是巨大的技术门槛。开发者们深受网络抖动、状态不一致和物理不同步的折磨。

**ArenaMatrix 旨在解决这些痛点，让研发团队可以快速开发出多端同步的游戏和应用。**

ArenaMatrix 包含了：
- **服务端核心：** 基于 Actor 模型的服务端框架，支持状态同步、帧同步、集群部署。
- **全平台客户端**：支持 Unity、Cocos、HarmonyOS 等客户端，可快速集成。
- **示例、教程与文档**：丰富的示例、教程与文档，方便开发者快速入门
- **CLI&MTools**：命令行工具与相关工具
- **MCP**：MCP 服务，可方便对接各类编程智能体。

> **我们的愿景：** 将游戏同步技术基础设施化、AI 化，让开发即时竞技游戏和多人互动应用像开发单机一样简单。

## 🌟 核心特性 (Features)

- **⚡ 高性能 Actor 模型:** 服务端基于极度优化的 Actor 并发模型构建，房间逻辑无需互斥锁，单节点轻松支撑万级并发。
- **⚡ 低内存开销:** 采用并发优势最强的 Golang 语言开发，将内存开销降到极致。
- **🧠 确定性核心 (Deterministic Core):** 保证核心战斗逻辑在 Go (服务端)、C# (Unity)、TypeScript (Cocos) 和 ArkTS (鸿蒙) 上运行结果完全一致（浮点数对齐）。

- **🚀 工业级竞技网络:** 内置 KCP (可靠 UDP) 协议，专为弱网环境下的竞技游戏优化，拒绝卡顿与拉扯。
- **⏪ 预测与回滚:** 开箱即用的状态快照与回滚逻辑。玩家操作零延迟响应，系统自动处理网络和解。
- **🤖 AI-Ready:** 原生支持服务端 AI Agent 接入，轻松实现 AI-Driven 内容。
- **📦 数据驱动 ECS:** 专为海量实体（单房间 10,000+ 单位）优化的内存布局，性能极致。

## 🏗️ 仓库结构 (Structure)

本项目采用单体仓库 (Monorepo) 管理，确保服务端与各端 SDK 版本完美对齐。

```text
ArenaMatrix/
├── ArenaServer/       # (Golang)核心服务端
├── ArenaUnity/        # (C#)Unity 客户端 SDK与相关示例
├── ArenaCocos/        # (TypeScript)Cocos Creator 客户端 SDK 与相关示例
├── ArenaHarmony/      # (ArkTS)鸿蒙 Next 原生 SDK 与相关示例
├── ArenaProtocols/    # (Protobuf) 前后端共享协议定义
└── Tools/             # 相关工具
```

## ⚡ 快速开始 (Quick Start)

### 1. 服务端 (Go)

只需几行代码，启动一个可扩展的竞技节点。

```go
package main

import (
    "github.com/ArenaMatrix/ArenaMatrix/ArenaServer"
    // 引入 KCP 网关支持
    _ "github.com/ArenaMatrix/ArenaMatrix/ArenaServer/gate/kcp"
)

func main() {
    // 1. 创建节点
    node := arenaserver.NewNode()
    
    // 2. 注册您的战斗逻辑 (ECS System)
    node.RegisterSystem(MyBattleSystem{})

    // 3. 启动引擎
    node.Run(":8888")
}
```

### 2. 客户端 (Unity / C#)

连接并驱动仿真逻辑。

```csharp
using ArenaMatrix.Unity;

void Start() {
    // 1. 连接服务器
    AM.Connect("127.0.0.1", 8888);
    
    // 2. 监听帧同步 (自动预测)
    AM.OnFrame += (frame) => {
        // 您只需编写推进逻辑，ArenaMatrix 会自动处理回滚与和解
        MyBattleSystem.Tick(frame);
    };
}
```

## 👨‍💻 开源项目组
>麒麟子@ArenaMatrix 架构师 & 主理人
- **团队位置：** 负责 ArenaMatrix 架构设计与方案落地。
- **相关经验:** 主导和参与了5款游戏引擎制作，曾任全球 Top 3 开源游戏引擎负责人；除引擎开发外，职业生涯中也主导并参与了多款 RTS、MOBA、MMO、FPS、休闲竞技类游戏项目的引擎、客户端、服务端开发。
- **商业验证:** 开源房间式游戏框架作者，累计 500+ 付费客户，开源项目被数千家研发团队使用，ArenaMatrix 为这一系列经验的延续。
- **主要目标**：让 ArenaMatrix 成为 AI 时代最好用的多人在线与实时互动应用开发引擎。
- **自媒体号**：麒麟子MrKylin 全网垂类粉丝 15W+。

>晓衡@ArenaMatrix 资源中心运营负责人
- **团队位置**：负责 ArenaMatrix 资源中心的传播推广与运营，帮助开发者进行变现。
- **相关经验**：拥有近10年资源商店运营经验，累计销售额数千万。
- **主要目标**：帮助 1000 名开发者年入10万+。
- **自媒体号**：晓衡的游戏开发圈  全网垂类粉丝 7W+。

>玉兔@ArenaMatrix 媒体负责人
- **团队位置：** 负责 ArenaMatrix 的推广与传播。
- **相关经验：** 5年+ 游戏引擎技术传播和自媒体经验，擅长产出高质量、深入浅出的教学视频，多条视频播放量 10w+。
- **主要目标：** 让更多人使用 ArenaMatrix。
- **自媒体号：** -不捣药的玉兔- 全网垂类粉丝 10W+。

## 📦 行业解决方案 (Solutions)
此开源项目不设计任何限制，任何房间类项目均可基于此开源项目进行开发。
对于一些想要快速获得特定类型的项目模板，快速掌握核心用法的朋友，可参考以下信息：
1. 提供经过商业验证的 MVP 模板，助您快速立项（构建中...）
2. 提供高品质的课程、培训以及学习社群，帮助您快速使用 ArenaMatrix 构建多人在线游戏和互动应用。（构建中...）

## 🤝 支持我们 (Support)

AM 引擎的发展离不开大家的支持。
方便的话，请点击右上角的 ⭐ **Star**，这不仅是对我们的鼓励，也能让更多开发者看到这个项目！