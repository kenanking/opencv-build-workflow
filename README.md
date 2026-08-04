# OpenCV 4.5.5 静态库构建（VS2019/v142 工具集）

## 目标
为「只有 VS2019 的设备」编译 OpenCV 4.5.5 **静态库**（现有 ThirdParty 里的库是 VS2022/v143 编的，
VS2019 设备无法链接）。产物将整理到 `C:\IcraftMdz\ThirdParty_v0.2\opencv2_vs2019`，
与现有 `opencv2` 目录格式一致（include + lib，全部静态）。

## 使用方法

1. 在 GitHub 新建一个**私有空仓库**（如 `opencv-build`）
2. 把本目录推上去（只需 `.github` 目录内容）：

```bash
cd C:\IcraftMdz\ThirdParty_v0.2\opencv-build-workflow
git init
git add .
git commit -m "build opencv 4.5.5 static (v142)"
git branch -M main
git remote add origin https://github.com/<用户名>/<仓库名>.git
git push -u origin main
```

3. 打开仓库 Actions 页面 → 左侧 `build-opencv455-static-vs2019` → **Run workflow**
4. 等待约 40~70 分钟（v142 工具集安装 3~5 分钟 + 全模块静态编译）
5. 完成后回到该次运行页面，下载 artifact **`opencv455-static-vs2019`**
   （zip 内含 `include/` 与 `lib/`）
6. 解压后告知路径，由 Claude 整理到 `opencv2_vs2019` 并逐项校验：
   - 编译器必须是 cl 19.29（v142）—— vs2019 设备可直接链接
   - 静态库（无 DLL 依赖）、x64、Release、/MD
   - 模块清单与现有构建一致（40 个 contrib 模块 + NONFREE + IPP）
