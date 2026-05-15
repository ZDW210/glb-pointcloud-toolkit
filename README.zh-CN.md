# GLB 点云工具包

**语言：** [English](README.md) | 中文

这是一个 Windows 工具包，用于压缩 GLB 模型、将 GLB 文件转换为点云数据，并在浏览器中预览生成的点云。

## 文件

- `GLBPointCloudConverter.exe`：将 `.glb` 模型转换为点云文件。
- `GLB模型压缩工具.exe`：压缩和优化 `.glb` 模型文件。
- `pointcloud-test.html`：基于浏览器的点云预览页面。

## 运行环境

### 操作系统

- Windows 10 或 Windows 11
- 64 位系统
- 建议使用较新的 Windows 版本

这两个工具都是 Windows 桌面程序，不适用于 macOS、Linux、Android 或 iOS。

### 运行时要求

正常双击使用时，不需要额外安装 Python 或 Node.js。

这些工具已经打包为独立的 Windows 可执行文件：

- `GLBPointCloudConverter.exe` 内置 Python 运行环境。
- `GLB模型压缩工具.exe` 内置 Python 运行环境、Node.js 运行环境和 GLTF-Transform 相关依赖。

用户下载文件后，直接运行 `.exe` 即可。

### Windows 组件

工具界面依赖 Windows 标准桌面组件：

- Windows PowerShell
- Windows Forms / .NET 桌面组件
- Tkinter 运行文件，已随压缩工具一起打包

如果使用的是精简版 Windows，缺少某些桌面组件时可能会导致界面无法打开。

### 浏览器要求

`pointcloud-test.html` 需要支持 WebGL 的现代浏览器，例如：

- Microsoft Edge
- Google Chrome
- 其他 Chromium 内核浏览器

如果浏览器禁用了 WebGL，点云预览可能无法显示。

## 硬件建议

大型 GLB 文件和高密度点云会占用较多内存和显卡资源。

建议配置：

- 内存：至少 8 GB，较大模型建议 16 GB 或以上
- 显卡：支持 WebGL 的独立显卡或较新的集成显卡
- 磁盘空间：建议预留原始 GLB 文件数倍的空间

点数越高，生成的 `.points.bin` 文件越大，浏览器预览时也越容易卡顿。

## 工具说明

### GLBPointCloudConverter.exe

该工具可以：

- 读取 `.glb` 文件
- 从模型网格表面采样点
- 生成：
  - `.points.meta.json`
  - `.points.bin`

推荐点数：

- 移动端预览：`80000` 到 `160000`
- 桌面端预览：`200000` 到 `320000`

兼容性说明：

- 支持常见 GLB 2.0 模型。
- 如果模型使用特殊压缩扩展、accessor/bufferView 数据异常，或没有可采样网格，可能会转换失败。
- 如果转换失败，可以先使用 `GLB模型压缩工具.exe` 优化模型后再转换。

### GLB模型压缩工具.exe

该工具可以：

- 压缩 `.glb` 文件
- 优化网格和纹理数据
- 导出优化后的 `.glb` 文件

工具内已打包所需的 GLTF-Transform 相关依赖。

### pointcloud-test.html

该页面用于在浏览器中预览生成的点云数据。

需要加载同一次转换生成的两个文件：

- `.points.meta.json`
- `.points.bin`

## 使用方法

### 1. 可选：先压缩 GLB 模型

运行：

```text
GLB模型压缩工具.exe
```

选择源 `.glb` 文件，并按照界面提示创建优化后的模型。

### 2. 将 GLB 转换为点云

运行：

```text
GLBPointCloudConverter.exe
```

步骤：

1. 选择 `.glb` 文件。
2. 设置目标点数。
3. 选择输出目录。
4. 点击生成。
5. 等待 `.points.meta.json` 和 `.points.bin` 创建完成。

### 3. 预览点云

打开：

```text
pointcloud-test.html
```

然后选择：

- 生成的 `.points.meta.json`
- 生成的 `.points.bin`

## 常见问题

### 工具无法打开

可以尝试：

- 右键 `.exe`，选择“以管理员身份运行”。
- 将文件移动到较短路径，例如 `D:\tools\glb-pointcloud-toolkit`。
- 检查 Windows Defender 或杀毒软件是否拦截。
- 确认系统是 64 位 Windows。

### 转换很慢

常见原因：

- GLB 模型很大。
- 模型三角面很多。
- 选择的点数较高。

可以先优化模型，或降低点数后再试。

### 浏览器预览卡顿

可以尝试：

- 降低点数。
- 使用 Chrome 或 Edge。
- 关闭其他占用显卡或内存的软件。
- 使用显卡性能更好的设备。

### 浏览器或 Windows 提示安全风险

因为仓库包含 `.exe` 文件，浏览器或 Windows 安全工具可能会提示风险。请确认文件来源可信后再运行。

## GitHub 文件大小说明

GitHub 单个文件大小限制为 100 MB。本仓库中的两个可执行文件都低于该限制：

- `GLBPointCloudConverter.exe`：约 6.1 MB
- `GLB模型压缩工具.exe`：约 58.9 MB

