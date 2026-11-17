基于 [FJH3576/GarrisonFarm-Personal](https://github.com/FJH3576/GarrisonFarm-Personal) 个人优化版 v1.1 二次优化，OCR 推理从 CPU 切到 NVIDIA GPU（CUDA）

- 上游原始项目：[UnknownGlyph/GarrisonFarm](https://github.com/UnknownGlyph/GarrisonFarm)（介绍视频 [BV1zMWZ6xED1](https://www.bilibili.com/video/BV1zMWZ6xED1/)）
- 个人优化版：[FJH3576/GarrisonFarm-Personal](https://github.com/FJH3576/GarrisonFarm-Personal)，由 轻骑可历#9000 优化
- GPU 加速版：由 壱津玉#0990 二次优化

原作者与来源版权归各自所有者所有；三个项目均未附项目级 LICENSE，本版本仅作个人学习与二次分发。

### 硬件要求
- 必须有 NVIDIA 显卡（CUDA 12，驱动建议 550+）。无 N 卡请用原版 CPU 包。
- 显存约 1~3 GB；MuMu 模拟器 12 + 明日方舟 1920×1080 横屏 + MAA 可正常连接。

### 更新内容
- GPU 推理：RapidOCR 的 det/cls/rec 三个 session 重建为 CUDAExecutionProvider；把老版 rapidocr 硬编码的 cudnn_conv_algo_search=EXHAUSTIVE 改为 HEURISTIC，消除每遇新尺寸穷举卷积算法导致的秒级卡顿。
- 无需重打包 exe：onedir 散包直接替换 onnxruntime 二进制 + 补了 CUDA 运行库 DLL。
- 自包含 OCR 模型：det/rec/cls 随包提供，不依赖 MAA 目录里的模型。
- 帧缓存：无输入期间复用截图，去掉主循环里紧邻的重复截图。
- MuMu 路径与官服/B 服自动检测，mumu_touch.json 留空即可。

### 使用
下载完整 ZIP 解压 → 打开 MuMu/明日方舟（1920×1080，卫戍协议界面）→ 首次在 MAA 确认连接 → 运行「开始刷角标.bat」选模式。详情见包内 README.md 与 使用说明.txt。

### 已知限制
无 NVIDIA 显卡不可用
