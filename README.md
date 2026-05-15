# GLB Point Cloud Toolkit

**Language:** English | [中文](README.zh-CN.md)

A Windows toolkit for compressing GLB models, converting GLB files into point cloud data, and previewing generated point clouds in the browser.

## Files

- `GLBPointCloudConverter.exe` - Converts `.glb` models into point cloud files.
- `GLB模型压缩工具.exe` - Compresses and optimizes `.glb` model files.
- `pointcloud-test.html` - Browser-based point cloud preview page.

## System Requirements

### Operating System

- Windows 10 or Windows 11
- 64-bit system
- A recent Windows version is recommended

These tools are Windows desktop applications. They are not intended for macOS, Linux, Android, or iOS.

### Runtime Requirements

For normal use, you do not need to install Python or Node.js separately.

The tools are packaged as standalone Windows executables:

- `GLBPointCloudConverter.exe` includes its Python runtime.
- `GLB模型压缩工具.exe` includes its Python runtime, Node.js runtime, and GLTF-Transform-related dependencies.

Users can download the files and run the `.exe` tools directly.

### Windows Components

The desktop interfaces rely on standard Windows components:

- Windows PowerShell
- Windows Forms / .NET desktop components
- Tkinter runtime files, bundled with the compressor tool

On heavily stripped-down Windows installations, missing desktop components may prevent the UI from opening.

### Browser Requirements

`pointcloud-test.html` requires a modern browser with WebGL support, such as:

- Microsoft Edge
- Google Chrome
- Other Chromium-based browsers

If WebGL is disabled, the point cloud preview may not render.

## Hardware Recommendations

Large GLB files and dense point clouds can use significant memory and GPU resources.

Recommended:

- RAM: 8 GB minimum, 16 GB or more for larger models
- GPU: WebGL-capable dedicated GPU or modern integrated GPU
- Disk space: several times the size of the source GLB file

Higher point counts create larger `.points.bin` files and may reduce browser preview performance.

## Tool Details

### GLBPointCloudConverter.exe

This tool:

- Reads `.glb` files
- Samples points from the model mesh surface
- Generates:
  - `.points.meta.json`
  - `.points.bin`

Suggested point counts:

- Mobile preview: `80000` to `160000`
- Desktop preview: `200000` to `320000`

Compatibility notes:

- Supports common GLB 2.0 models.
- Models using special compression extensions, invalid accessors/bufferViews, or no sampleable mesh may fail.
- If conversion fails, try optimizing the model first with `GLB模型压缩工具.exe`.

### GLB模型压缩工具.exe

This tool:

- Compresses `.glb` files
- Optimizes mesh and texture data
- Exports optimized `.glb` files

It bundles the required GLTF-Transform-related dependencies.

### pointcloud-test.html

This page previews generated point cloud data in the browser.

Load both files from the same conversion result:

- `.points.meta.json`
- `.points.bin`

## Usage

### 1. Optional: Compress the GLB model

Run:

```text
GLB模型压缩工具.exe
```

Select a source `.glb` file and follow the UI to create an optimized model.

### 2. Convert GLB to point cloud

Run:

```text
GLBPointCloudConverter.exe
```

Steps:

1. Select a `.glb` file.
2. Set the target point count.
3. Choose an output folder.
4. Click generate.
5. Wait for `.points.meta.json` and `.points.bin` to be created.

### 3. Preview the point cloud

Open:

```text
pointcloud-test.html
```

Then select:

- the generated `.points.meta.json`
- the generated `.points.bin`

## Troubleshooting

### The tool does not open

Try:

- Right-click the `.exe` and choose "Run as administrator".
- Move the files to a shorter path, such as `D:\tools\glb-pointcloud-toolkit`.
- Check whether Windows Defender or antivirus software blocked the file.
- Confirm that the system is 64-bit Windows.

### Conversion is slow

Common causes:

- The GLB model is large.
- The model has many triangles.
- The selected point count is high.

Try optimizing the model first or lowering the point count.

### Browser preview is slow

Try:

- Lowering the point count.
- Using Chrome or Edge.
- Closing other GPU- or memory-heavy applications.
- Running on a machine with a stronger GPU.

### Browser or Windows shows a security warning

Because this repository contains `.exe` files, browsers or Windows security tools may show warnings. Only run the files if you trust the source.

## GitHub File Size Notes

GitHub has a 100 MB limit for individual files. Both executables in this repository are below that limit:

- `GLBPointCloudConverter.exe`: about 6.1 MB
- `GLB模型压缩工具.exe`: about 58.9 MB

