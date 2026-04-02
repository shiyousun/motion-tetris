# 🎮 动感俄罗斯方块 | Motion Tetris

<p align="center">
  <img src="https://img.shields.io/badge/JavaScript-ES6+-yellow.svg" alt="JavaScript">
  <img src="https://img.shields.io/badge/MediaPipe-Hands%20%2B%20FaceMesh-blue.svg" alt="MediaPipe">
  <img src="https://img.shields.io/badge/Web%20Audio-API-purple.svg" alt="Web Audio">
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License">
</p>

<p align="center">
  <b>🎯 <a href="https://shiyousun.github.io/motion-tetris/">在线体验 Live Demo</a></b>
</p>

<p align="center"><b>📖 <a href="#中文">中文</a> | <a href="#english">English</a></b></p>

---

<a name="中文"></a>

## 🇨🇳 中文

> **用身体玩俄罗斯方块！** 张开双手控制方块移动，倾斜手掌旋转方块，双手下压快速降落。还可以用头部控制——摇头移动、仰头旋转、点头快降。让你在电脑前也能活动身体，保护颈椎和手臂健康。

### ✨ 核心功能

- 🖐 **手势控制**：MediaPipe Hands 实时追踪双手，张开手掌即可控制
- 🗣 **头部控制**：MediaPipe FaceMesh 追踪面部，摇头/仰头/点头操控方块
- 🎮 **三种模式**：手控 / 头控 / 双模（手优先，无手时自动切换头控）
- 🎵 **动感音效**：Web Audio API 合成引擎，移动/旋转/消行/硬降各有专属爆裂音效
- 📱 **全平台适配**：桌面浏览器 + 手机浏览器（触屏按钮兼容）
- 📷 **摄像头选择**：启动时可选择不同摄像头，也可纯键盘游玩
- 🔄 **手势重启**：OK 手势（👌）或张大嘴（😮）重新开始游戏

### 🕹️ 操控指南

#### 🖐 手控模式
| 动作 | 效果 |
|------|------|
| 双手/单手偏左 | 方块左移（区域制：偏离越大速度越快） |
| 双手/单手偏右 | 方块右移 |
| 双手高低差倾斜 | 旋转方块 |
| 单手扭转手腕 | 旋转方块 |
| **双手同时大幅下压** | 硬降（两手都要往下才触发） |
| 单手大幅下压 | 硬降 |
| 👌 OK 手势长按 | 重新开始 |

#### 🗣 头控模式
| 动作 | 效果 |
|------|------|
| 头向左/右偏 | 方块左/右移 |
| 大幅仰头 | 旋转方块 |
| 大幅点头 | 硬降 |
| 😮 张大嘴持续 0.8 秒 | 重新开始 |

#### ⌨️ 键盘控制
| 按键 | 效果 |
|------|------|
| ← → | 左右移动 |
| ↑ | 旋转 |
| 空格 | 硬降 |
| 1-5 | 调节速度 |
| P | 暂停 |
| M | 静音 |
| R | 重启 |

### 🧠 核心算法

#### 区域制移动（Zone-Based Movement）
手部水平位置被划分为 5 个区域：
- **中央死区（±14%）**：方块静止不动，避免抖动
- **慢速区（14%~28%）**：每 220ms 移动一格
- **快速区（>28%）**：每 80ms 移动一格

输入经过指数平滑（α=0.15）和滚动平均滤波，消除手部自然抖动。

#### 双手硬降检测
左右手各自维护独立的 Y 坐标历史队列（500ms 窗口），只有两只手 **各自** 下移超过 12% 才触发硬降，冷却 1.2 秒。避免单手移动造成误触。

#### 防卡死看门狗
MediaPipe `send()` 调用增加 3 秒超时保护（`Promise.race`），帧发送锁 4 秒自动重置，确保检测管线不会因模型挂起而永久阻塞。

### 🛠️ 技术栈

| 技术 | 用途 |
|------|------|
| MediaPipe Hands | 双手 21 关键点实时追踪 |
| MediaPipe FaceMesh | 面部 468 关键点追踪 |
| Canvas 2D API | 游戏渲染 + 摄像头叠加 |
| Web Audio API | 动态音效合成（振荡器+噪声+kick） |
| getUserMedia | 摄像头访问 |
| CSS @media | 响应式布局 |

### 📁 项目结构

```
motion-tetris/
└── index.html    # 完整的单文件应用（700+ 行，零依赖框架）
```

### 🚀 部署

```bash
# 本地运行
python3 -m http.server 8080
# 打开 http://localhost:8080

# 或直接访问在线版
# https://shiyousun.github.io/motion-tetris/
```

### 💡 创作初衷

长时间坐在电脑前工作，颈椎和手臂容易僵硬。这款游戏让你在工作间隙用身体控制方块，活动颈椎、肩膀和手臂，在娱乐中保持身体健康。

---

<a name="english"></a>

## 🇬🇧 English

> **Play Tetris with your body!** Open your palms to move pieces, tilt hands to rotate, push both hands down for hard drop. You can also use head movements — tilt head to move, look up to rotate, nod to drop. Stay active and protect your neck and shoulders while gaming at your desk.

### ✨ Key Features

- 🖐 **Hand Gesture Control**: Real-time dual-hand tracking via MediaPipe Hands, open palm to control
- 🗣 **Head Motion Control**: Face landmark tracking via MediaPipe FaceMesh, head tilt/nod to control
- 🎮 **Three Modes**: Hand / Head / Dual (hands take priority, auto-fallback to head when no hands detected)
- 🎵 **Dynamic Sound Effects**: Web Audio API synthesis engine with unique explosive sounds for move/rotate/clear/hard drop
- 📱 **Cross-Platform**: Desktop browsers + mobile browsers (touch buttons as fallback)
- 📷 **Camera Selection**: Choose camera device at startup, or play with keyboard only
- 🔄 **Gesture Restart**: OK gesture (👌) or wide open mouth (😮) to restart the game

### 🕹️ Control Guide

#### 🖐 Hand Control Mode
| Action | Effect |
|--------|--------|
| Hands shift left | Piece moves left (zone-based: further = faster) |
| Hands shift right | Piece moves right |
| Dual-hand height difference | Rotate piece |
| Single-hand wrist twist | Rotate piece |
| **Both hands push down simultaneously** | Hard drop (both hands must descend) |
| Single hand push down | Hard drop |
| 👌 OK gesture hold | Restart game |

#### 🗣 Head Control Mode
| Action | Effect |
|--------|--------|
| Tilt head left/right | Move piece left/right |
| Look up significantly | Rotate piece |
| Nod down significantly | Hard drop |
| 😮 Open mouth wide for 0.8s | Restart game |

#### ⌨️ Keyboard Controls
| Key | Effect |
|-----|--------|
| ← → | Move left/right |
| ↑ | Rotate |
| Space | Hard drop |
| 1-5 | Adjust speed |
| P | Pause |
| M | Mute |
| R | Restart |

### 🧠 Core Algorithms

#### Zone-Based Movement
Hand horizontal position is divided into 5 zones:
- **Central Dead Zone (±14%)**: Piece stays still, prevents jitter
- **Slow Zone (14%~28%)**: Moves one column every 220ms
- **Fast Zone (>28%)**: Moves one column every 80ms

Input passes through exponential smoothing (α=0.15) and rolling average filter to eliminate natural hand tremor.

#### Dual-Hand Hard Drop Detection
Left and right hands maintain independent Y-coordinate history queues (500ms window). Hard drop triggers **only when both hands individually** descend more than 12%, with a 1.2s cooldown. Prevents false triggers from single-hand movement.

#### Anti-Freeze Watchdog
MediaPipe `send()` calls are wrapped with 3-second timeout protection (`Promise.race`). The frame-sending lock auto-resets after 4 seconds, ensuring the detection pipeline never permanently blocks due to model hang.

### 🛠️ Tech Stack

| Technology | Purpose |
|-----------|---------|
| MediaPipe Hands | Dual-hand 21-keypoint real-time tracking |
| MediaPipe FaceMesh | Face 468-keypoint tracking |
| Canvas 2D API | Game rendering + camera overlay |
| Web Audio API | Dynamic sound synthesis (oscillator + noise + kick) |
| getUserMedia | Camera access |
| CSS @media | Responsive layout |

### 📁 Project Structure

```
motion-tetris/
└── index.html    # Complete single-file app (700+ lines, zero framework dependencies)
```

### 🚀 Deployment

```bash
# Local
python3 -m http.server 8080
# Open http://localhost:8080

# Or visit the live version
# https://shiyousun.github.io/motion-tetris/
```

### 💡 Motivation

Sitting at a computer for long hours leads to stiff necks and shoulders. This game lets you control Tetris pieces with your body during work breaks — exercising your neck, shoulders, and arms while having fun. Gaming meets fitness!

---

## 📄 License

MIT License - 自由使用 | Free to use

## 👨‍💻 Author / 作者

**友哥 (YooGe)** · 友哥 & AI 创造 | Created by YooGe & AI
