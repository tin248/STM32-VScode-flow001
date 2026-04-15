# VScode开发STM32基本流程

  本文主要参考了*Majerle*的[stm32-cube-cmake-vscode](https://github.com/MaJerle/stm32-cube-cmake-vscode.git)例程
  
  该仓库主要用于个人学习
  
# 工具安装

1.[Visual Studio Code](https://code.visualstudio.com) 

 本地安装路径 `D:\software\VScode` 
 
  **相关插件**
  
  - `ms-vscode.cpptools`      :语法高亮以及C/C++开发的其他核心功能
  - `ms-vscode.cmake-tools`   :CMake核心工具，构建系统生成工具
  - `twxs.cmake`              :CMake语法高亮工具
  - `marus25.cortex-debug`    :Cortex-M调试扩展，是从 VSCode 调试 STM32 的必备工具
  - `dan-c-underwood.arm`     :ARM 汇编语法高亮工具
  - `zixuanwang.linkerscript` :GCC 链接脚本语法高亮工具

2.[STM32CubeCLT](https://www.st.com/en/development-tools/stm32cubeclt.html)

  本地安装路径 `D:\software\STM32CubeCLT_1.21.0` 
 
 - 命令行工具，涵盖 Ninja 构建系统与 CMake 构建生成器
 - 配合Vscode的开发，自动配置你的构建环境变量(windows,mac,linux)

3.[STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html)

本地安装路径 `D:\software\STM32CubeIDE_2.1.1\STM32CubeIDE` 

-  `ARM none eabi GCC compiler ` :编译器
-  `ST-LINK GDBServer for debugging` :调试器
-  `STM32CubeProgrammer tool for code downloading and respective ST-Link drivers` :代码下载工具和驱动程序
-  `Folder with STM32 SVD files` :包含 STM32 SVD 文件的文件夹
-  `Drivers for ST-Link` :驱动程序

配置环境变量

配置名为`Path`的系统变量，具体配置如下：

- gcc编译器 `D:\software\STM32CubeIDE_2.1.1\STM32CubeIDE\plugins\com.st.stm32cube.ide.mcu.externaltools.gnu-tools-for-stm32.14.3.rel1.win32_1.0.100.202602081740\tools\bin\`
- ST-Link调试器 `D:\software\STM32CubeIDE_2.1.1\STM32CubeIDE\plugins\com.st.stm32cube.ide.mcu.externaltools.stlink-gdb-server.win32_2.2.400.202601091506\tools\bin\`
- 程序烧写工具 `D:\software\STM32CubeIDE_2.1.1\STM32CubeIDE\plugins\com.st.stm32cube.ide.mcu.externaltools.cubeprogrammer.win32_2.2.400.202601091506\tools\bin\`

在cmd中输入以下命令验证路径:
```
arm-none-eabi-gcc --version
STM32_Programmer_CLI --version
ST-LINK_gdbserver --version
```


4.[STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html)

- 图形界面配置工具，生成底层硬件配置文件.ioc,配合STM32CubeIDE使用




