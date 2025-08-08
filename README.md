# STM32 CMake 工程模板

本工程是一个基于 CMake 的 STM32 工程模板，适用于 STM32F4 系列，使用 ARM GCC 工具链进行编译，OpenOCD 进行固件下载和调试。

可以debug实时更新变量值

## 主要特性
- 支持 STM32F4 系列芯片
- 使用 CMake 进行跨平台构建
- 兼容 ARM GCC (arm-none-eabi-gcc) 工具链
- 支持 OpenOCD 下载与调试
- 结构清晰，便于移植和扩展

## 目录结构
```
├── Core/           # 用户代码（头文件和源文件）
├── Drivers/        # STM32 HAL/CMSIS 驱动
├── cmake/          # CMake 工具链和相关脚本
├── build/          # 构建输出目录
├── CMakeLists.txt  # 主 CMake 构建脚本
├── STM32F407XX_FLASH.ld # 链接脚本
└── ...
```

## 环境准备
1. 安装 [ARM GCC 工具链](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads)
2. 安装 [MinGW](https://github.com/skeeto/w64devkit/releases)
3. 安装 [ninja](https://link.zhihu.com/?target=https%3A//github.com/ninja-build/ninja/releases)
4. 安装 [OpenOCD](http://openocd.org/)
5. 安装 [CMake](https://cmake.org/download/)

6. 推荐使用 VS Code + CMake Tools 插件进行开发

## 编译方法
```sh
# 1. 配置工程（Debug 模式）
cmake --preset=Debug
# 2. 编译生成固件
cmake --build build/Debug --target all
点击 ui按钮：🛠️ build
```

## 下载固件
连接好调试器（如 ST-Link、CMSIS-DAP、J-Link），使用如下命令下载：

```sh
# 以 ST-Link 为例
openocd -f interface/stlink.cfg -f target/stm32f4x.cfg -c "program build/Debug/<工程名>.elf verify reset" -c "reset run" -c exit

或者点击ui按钮 ⚡ Download
```

## 其他说明
- 工程名和 .elf 文件名需保持一致，无需在.json中更改。
- 无需替换编译链路径，自动寻找
- 可通过修改 CMakeLists.txt 和 toolchain 文件适配不同芯片和工具链。

---

如有问题欢迎提 issue 或 PR。
