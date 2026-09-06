<div align="center">
  <img src="frontend/echo_logo.svg" alt="EchoSmith Logo" width="200"/>

  # 闻见 · EchoSmith

  **高性能本地语音转录桌面应用，基于 SenseVoice + sherpa-onnx**

  **本仓库为 Windows 版分支：只发布 Windows 安装包，仅在 Windows 10/11 x64 上测试。**

  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
  [![Platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011%20x64-blue)](https://github.com/Barnabas-creator/EchoSmith/releases)
  [![Version](https://img.shields.io/badge/version-1.4.5-green)](https://github.com/Barnabas-creator/EchoSmith/releases)

</div>

## 特性

- **完全离线** — 本地运行，无需联网，数据不出本机
- **极速转录** — RTF ~0.042，1 小时音频约 2.5 分钟完成
- **智能分句** — Silero VAD 语音活动检测，按语音停顿自动断句
- **批量处理** — 多文件批量转写，自动导出到源文件目录
- **URL 下载** — 粘贴链接直接下载并转写（基于 yt-dlp）
- **实时进度** — WebSocket 推送转录进度和中间结果
- **多格式导出** — TXT、SRT 字幕、JSON 三种格式
- **面向 Windows** — 本分支提供 Windows 10 / 11 x64 安装包（NSIS / MSI）
- **现代界面** — 毛玻璃质感 UI，支持浅色 / 深色模式

## 性能

| 指标 | 数值 |
|------|------|
| RTF（实时率） | ~0.042 |
| 1 小时音频转写 | ~2.5 分钟 |
| 模型大小 | 228 MB（INT8 量化） |
| 安装包大小 | ~290 MB |
| 内存占用 | ~500 MB |

> 测试环境：Apple M1 Max，8 性能核心。应用会自动检测 CPU 核心数以获得最佳性能。

## 安装

### 下载预编译版本（Windows）

前往 [Releases](https://github.com/Barnabas-creator/EchoSmith/releases) 页面下载：

| 文件 | 说明 |
|------|------|
| `EchoSmith_x.x.x_x64-setup.exe` | NSIS 安装包，推荐 |
| `EchoSmith_x.x.x_x64_en-US.msi` | MSI 安装包 |

系统要求：Windows 10 / 11 64 位。首次启动 SmartScreen 可能提示未知发行者，点击「更多信息」→「仍要运行」即可。

macOS 用户请使用上游仓库 [JingZhaoQi/EchoSmith](https://github.com/JingZhaoQi/EchoSmith/releases) 的 DMG。

### 从源码构建

#### 前置要求

- Node.js 20+、pnpm
- Python 3.12+
- Rust（最新稳定版）
- FFmpeg

#### 快速开始

```bash
# 克隆仓库
git clone https://github.com/Barnabas-creator/EchoSmith.git
cd EchoSmith

# 创建虚拟环境
python3 -m venv .venv
source .venv/bin/activate

# 安装依赖
pip install -r backend/requirements.txt
cd frontend && pnpm install && cd ..
cd tauri && pnpm install && cd ..

# 下载模型（首次运行，约 230MB）
python scripts/download_models.py

# 启动开发模式
cd tauri && pnpm tauri dev
```

#### 构建安装包

```powershell
# Windows（在 Windows 上运行）
powershell scripts/build_backend.ps1
cd tauri; npm run build
```

打 `v*` 标签推送后，GitHub Actions 会自动构建 Windows 安装包并发布到 Releases。

## 使用说明

### 单文件转写
1. 点击上传区域或拖拽音视频文件
2. 等待转写完成
3. 导出为 TXT / SRT / JSON

### 批量转写
1. 切换到「批量转写」标签
2. 选择导出格式
3. 添加多个文件
4. 点击「开始转写」，结果自动保存到源文件目录

### URL 转写
1. 切换到「URL 转写」标签
2. 粘贴音视频链接
3. 自动下载并转写

### 支持的格式

音频：MP3、WAV、M4A、FLAC、OGG、AAC、WMA、AIFF、CAF
视频：MP4、MOV、AVI、MKV、WEBM、M4V

## 技术栈

| 层级 | 技术 |
|------|------|
| 桌面框架 | Tauri 2.x + Rust |
| 前端 | React 18 + TypeScript + TailwindCSS + Vite |
| 状态管理 | Zustand |
| 后端 | FastAPI + uvicorn |
| ASR 引擎 | sherpa-onnx + SenseVoice INT8 |
| 语音分段 | Silero VAD |
| 音视频处理 | FFmpeg（内置） |
| URL 下载 | yt-dlp |

## 许可证

MIT License — 详见 [LICENSE](LICENSE)

## 致谢

- [SenseVoice](https://github.com/FunAudioLLM/SenseVoice) — 阿里 FunAudioLLM 语音识别模型
- [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx) — 高性能 ONNX 推理引擎
- [Silero VAD](https://github.com/snakers4/silero-vad) — 语音活动检测模型
- [Tauri](https://tauri.app/) — 现代桌面应用框架
- [FastAPI](https://fastapi.tiangolo.com/) — 高性能 Web 框架
- [yt-dlp](https://github.com/yt-dlp/yt-dlp) — 视频下载工具

---

<div align="center">
  Made with ❤️ by JingZhaoQi
</div>
