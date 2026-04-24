# PROJECT_BRIEF

## 项目概览

- 项目名称：Game Map Real-time Tracker
- 项目目标：基于屏幕小地图和完整大地图进行实时位置追踪，并通过悬浮窗展示玩家位置。
- 当前阶段：源码运行调试。
- 主要平台：Windows 桌面。

## 技术栈

- 语言：Python
- 框架：Tkinter、OpenCV、MSS、Pillow
- 构建工具：无固定构建工具
- 架构：脚本式桌面应用
- 数据层：本地 JSON 配置与地图图片资源
- 网络层：仅部分下载或 AI 模型相关脚本可能使用网络
- 依赖管理：requirements.txt

## 目录结构

- `main_sift.py`：SIFT 版本启动入口。
- `main_ai.py`：LoFTR AI 版本启动入口。
- `selector.py`：小地图区域选择器。
- `config.py`：配置加载与默认配置。
- `config.json`：运行配置。
- `tracker_engine.py`：AI 跟踪引擎相关逻辑。
- `route_manager.py`：路线数据管理相关逻辑。

## 关键模块

### 入口与启动

- 入口文件：`main_sift.py`、`main_ai.py`
- 启动流程：校准小地图区域，加载配置，加载地图资源，初始化跟踪器，启动 Tkinter 窗口。
- 初始化逻辑：`main_sift.py` 会强制运行 `run_selector_if_needed(force=True)`。

### 业务模块

- SIFT 跟踪：从屏幕小地图提取特征，与逻辑大地图匹配。
- AI 跟踪：使用 LoFTR 引擎进行密集匹配。
- 悬浮窗显示：裁剪显示地图并绘制当前位置。

### 数据与存储

- 本地配置：`config.json`
- 必需地图资源：`big_map.png`、`big_map-1.png`
- 路线与点位数据：`point.json`、`update.json`

### 系统能力

- 权限 / 配置：需要可截屏权限和正确的小地图区域配置。
- 后台任务：无独立后台服务。
- 外部集成：屏幕截图、Tkinter 桌面窗口。

## 构建与运行

- 本地运行命令：`python main_sift.py`
- 调试命令：按入口脚本直接运行。
- 构建命令：当前未确认。
- 发布命令：当前未确认。
- 关键环境变量：当前未确认。

## 当前任务状态

- 当前任务：优化 SIFT 跟踪稳定性，降低位置乱窜。
- 当前结论：已新增 SIFT 稳定性配置项，收紧匹配参数，并在 `main_sift.py` 接入内点质量校验、越界拒绝、跳变拒绝、平滑更新和传送后重定位确认逻辑。
- 已确认约束：优先修复 `main_sift.py`，不引入 AI 依赖。
- 影响范围：SIFT 匹配结果接受条件、位置更新策略、运行配置。

## 下一步

- 下一步 1：校验语法和配置读取。
- 下一步 2：重新启动 `main_sift.py`。
- 下一步 3：观察传送后是否能自动恢复定位。

## 已知风险

- Python 版本当前为 3.8.6，低于 README 推荐的 3.9+。
- 缺少地图资源时，启动会在地图加载阶段失败。
