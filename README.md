# Xiaomi MiMo Intel 本地测试版 Edit by ChatGPT

基于原安装包 26.1010.101546 重新打包，适用于 Intel Mac。本机验证环境为 macOS 13.7.8。

## 使用

双击 Xiaomi MiMo Intel.app 即可启动，也可把它放到 Applications 文件夹。保留原来的 ARM App 便于对照。需要自行登录小米账号。

这是本地 ad-hoc 签名的非官方兼容版，没有小米的 Developer ID 签名或 Apple 公证。若 macOS 拦截打开，可在 Finder 中右键 App 选择“打开”，或按系统提示在隐私与安全性中允许打开。

应用使用独立的数据目录 ~/Library/Application Support/Xiaomi MiMo Intel，自动更新已关闭。不要用官方 ARM 更新包覆盖此版本。

## 已验证

- Electron 41.7.2 x64，运行时压缩包通过官方 SHA256 校验。
- 本机实际启动，React 主页面与内嵌小米账号登录页成功加载。
- 终端进程执行与输出、Canvas 绘图、FSEvents 文件监听。
- ONNX CPU 模型的实际推理（小型 Identity 测试模型）。
- 内置 Node.js 24.15.0、Python 3.12.13、ripgrep 14.1.1。
- Python pydantic/jiter/wcwidth/httpx 导入与基础调用。
- sharp 实际生成 PNG，GitHub MCP 1.7.0 命令启动。
- 41 个 Mach-O 文件均支持 x86_64，应用通过 codesign 深度验证。

## 变化与限制

- 已替换 Electron、终端、Canvas、文件监听、ONNX、Node、Python、ripgrep、sharp、libvips 和 GitHub MCP 的 ARM 二进制。
- 复用原安装包中的业务 JavaScript 及架构无关的工具依赖。这是重新打包的兼容版，不是从完整源码重建的官方版本。
- ONNX Runtime 从 1.27.0 调整为 1.22.0，配套 onnxruntime-common 同步调整。真实业务模型仍需验证；测试配置中查询分类模型尚未下载，启动日志显示 resource-missing。
- 原业务代码明确把电脑操作/录制回放/浏览器自动操作插件限制为 darwin-arm64。此版本未强行启用这些原生自动操作插件。
- 未登录任何个人账号，所以登录后的模型对话、编程任务、语音和账户功能未完成端到端验证。
- Python 换成 x64 3.12.13，保留原 python-evolve-site 的纯 Python 内容，并替换 pydantic-core 2.50.0、jiter 0.17.0、wcwidth 0.9.2 的原生扩展。
- 应用版本号保持与原包相同；显示名称和 bundle ID 增加 Intel 本地版本标识。

## 运行时来源

Electron 与 Node.js 使用官方版本并校验官方 SHA256；原生 Node 模块取自对应版本的 npm 包；Python 通过 uv 获取 python-build-standalone 的 x86_64 版本；ripgrep 和 GitHub MCP 来自其官方 GitHub Releases。
