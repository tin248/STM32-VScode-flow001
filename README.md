# VScode开发STM32基本流程

  本文参考了*Majerle*的[stm32-cube-cmake-vscode](https://github.com/MaJerle/stm32-cube-cmake-vscode.git)例程
  
  该仓库主要用于个人学习
  
# 第一步-工具安装

**1.[Visual Studio Code](https://code.visualstudio.com)**

 本地安装路径 `D:\software\VScode` 
 
  **相关插件**
  
  - `ms-vscode.cpptools`      :语法高亮以及C/C++开发的其他核心功能
  - `ms-vscode.cmake-tools`   :CMake核心工具，构建系统生成工具
  - `twxs.cmake`              :CMake语法高亮工具
  - `marus25.cortex-debug`    :Cortex-M调试扩展，是从 VSCode 调试 STM32 的必备工具
  - `dan-c-underwood.arm`     :ARM 汇编语法高亮工具
  - `zixuanwang.linkerscript` :GCC 链接脚本语法高亮工具

**2.[STM32CubeCLT](https://www.st.com/en/development-tools/stm32cubeclt.html)**

  本地安装路径 `D:\software\STM32CubeCLT_1.21.0` 
 
 - 命令行工具，涵盖 Ninja 构建系统与 CMake 构建生成器
 - 配合Vscode的开发，自动配置你的构建环境变量(windows,mac,linux)

**3.[STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)**

本地安装路径 `D:\software\STM32CubeIDE_2.1.1\STM32CubeIDE` 

-  `ARM none eabi GCC compiler ` :编译器
-  `ST-LINK GDBServer for debugging` :调试器
-  `STM32CubeProgrammer tool for code downloading and respective ST-Link drivers` :代码下载工具和驱动程序
-  `Folder with STM32 SVD files` :包含 STM32 SVD 文件的文件夹
-  `Drivers for ST-Link` :驱动程序

**配置环境变量**

配置名为`Path`的系统变量，具体配置如下：

- gcc编译器 `D:\software\STM32CubeIDE_2.1.1\STM32CubeIDE\plugins\com.st.stm32cube.ide.mcu.externaltools.gnu-tools-for-stm32.14.3.rel1.win32_1.0.100.202602081740\tools\bin\`
- ST-Link调试器 `D:\software\STM32CubeIDE_2.1.1\STM32CubeIDE\plugins\com.st.stm32cube.ide.mcu.externaltools.stlink-gdb-server.win32_2.2.400.202601091506\tools\bin\`
- 程序烧写工具 `D:\software\STM32CubeIDE_2.1.1\STM32CubeIDE\plugins\com.st.stm32cube.ide.mcu.externaltools.cubeprogrammer.win32_2.2.400.202601091506\tools\bin\`

在cmd中输入以下命令验证安装路径:
```
arm-none-eabi-gcc --version
STM32_Programmer_CLI --version
ST-LINK_gdbserver --version
```
<img width="730" height="512" alt="image" src="https://github.com/user-attachments/assets/f1059d06-3f7c-4169-8b30-2da6bebb51a5" />

---
**4.[STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html)**

本地安装路径 `D:\software\STM32CubeMX-6.17.0` 

- 图形界面配置工具，生成底层硬件配置文件.ioc,配合STM32CubeIDE使用

**5.[CMake](https://cmake.org/)**

> CMake = 自动生成 “编译脚本” 的工具

- **CMake是设计师**
- 写一个 CMakeLists.txt
- CMake 生成 Ninja 编译脚本
- 生成编译规则

**6.[Ninja](https://github.com/ninja-build/ninja/releases)**

> Ninja = 超快的小型编译工具

- **Ninja是施工队**
- 编译程序
- 执行编译，速度快

在cmd中输入以下命令验证安装路径:

```
cmake --version
ninja --version
```
<img width="637" height="144" alt="image" src="https://github.com/user-attachments/assets/55da8d33-acb4-4fc9-9563-f08490b041f1" />

---
# 第二步-使用STM32CubeMX生成IDE工程文件

**step1:新建工程**

<img width="1200" height="600" alt="屏幕截图 2026-04-15 174911" src="https://github.com/user-attachments/assets/92064d90-e89b-4d35-ad1c-dd2851231aca" />

**step2:芯片选型**

<img width="1200" height="600" alt="屏幕截图 2026-04-15 175345" src="https://github.com/user-attachments/assets/2d58f12b-f053-4039-b048-326c47feed55" />

**step3:引脚配置**

本文分别配置了GPIO引脚PB5和PE5，对应底板的2个LED灯，具体情况根据底板原理图判断
<img width="1200" height="600" alt="屏幕截图 2026-04-15 180934" src="https://github.com/user-attachments/assets/0162ebb2-0661-4068-8e49-fda64efb4526" />

**step4:工程管理**

需要将工具链改为STM32CubeIDE
<img width="1200" height="600" alt="屏幕截图 2026-04-15 181321" src="https://github.com/user-attachments/assets/0e22d281-1eb4-4885-8d67-3ceccce8abdc" />

这里使用的HAL库进行开发，然后点击generate code生成项目工程
<img width="1200" height="600" alt="屏幕截图 2026-04-15 181609" src="https://github.com/user-attachments/assets/43b2a3fc-22a7-4ccf-9ad8-6e86eb7de2d4" />

点击打开项目工程
<img width="1200" height="600" alt="屏幕截图 2026-04-15 181909" src="https://github.com/user-attachments/assets/91af3a16-2c91-4ef9-88e0-0088a8cf9569" />

选择一个工作空间，然后launch
<img width="797" height="367" alt="屏幕截图 2026-04-15 182003" src="https://github.com/user-attachments/assets/77e0340a-e466-48f7-89b1-e71f21bba4cc" />

# 第三步-使用IDE进行调试









