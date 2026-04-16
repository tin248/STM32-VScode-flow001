# VScode开发STM32基本流程

  本文参考了*Majerle*的[stm32-cube-cmake-vscode](https://github.com/MaJerle/stm32-cube-cmake-vscode.git)例程
  
  该仓库主要用于个人学习
  
# 第一章-工具安装

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

window系统下，在win+R打开的窗口中输入cmd进入命令行，然后输入以下命令验证安装版本信息:
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

验证安装版本信息:

```
cmake --version
ninja --version
```
**请注意:CMake的最低版本限制为3.25.1**

<img width="637" height="144" alt="image" src="https://github.com/user-attachments/assets/55da8d33-acb4-4fc9-9563-f08490b041f1" />

---
# 第二章-使用STM32CubeMX生成IDE工程文件

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

然后点击打开所在文件夹即可

本地路径为：`E:\VScode\STM32CubeIDE\ding26_4_15`

<img width="700" height="300" alt="image" src="https://github.com/user-attachments/assets/a7ab08ba-e4cd-4b99-aa1b-3c5ae3a0e4ad" />


# 第三章-使用Visual Studio Code进行调试

VScode开发，实际只需要这几个文件，其他不必要的可以进行裁剪
<img width="700" height="300" alt="image" src="https://github.com/user-attachments/assets/211173bc-bcb0-4f14-8a3b-a2aa78c12121" />

使用VScode打开路径`E:\VScode\STM32CubeIDE\ding26_4_15`下的项目工程
<img width="1911" height="1028" alt="image" src="https://github.com/user-attachments/assets/ea351632-6004-4bd6-aefa-18b36082779f" />

**step1:编写gcc-arm-none-eabi.cmake**

文件路径:`ding26_4_15/cmake/gcc-arm-none-eabi.cmake`
```
# =============================================================================
# CMake工具链配置文件 
# =============================================================================


# 步骤1: 定义工具链路径(根据STM32CubeIDE的安装路径进行修改)
# 设置GCC ARM工具链的bin目录路径
set(CMAKE_TOOLCHAIN_PATH "D:/software/STM32CubeIDE_2.1.1/STM32CubeIDE_2.1.1/plugins/com.st.stm32cube.ide.mcu.externaltools.make.stm32cubef1_2.1.1.202405161235/tools/bin")
#工具链的父目录，用于查找库文件，此处父路径就是 ../ding26_4_15
set(CMAKE_FIND_ROOT_PATH "${CMAKE_TOOLCHAIN_PATH}/../")


# 步骤2: 指定交叉编译工具链各组件的完整路径(所有ARM芯片共用同一套工具链，无需修改)
#   CMake需要知道用什么编译器来编译C/C++/汇编代码
set(CMAKE_C_COMPILER   "${CMAKE_TOOLCHAIN_PATH}/arm-none-eabi-gcc")      # C编译器
set(CMAKE_CXX_COMPILER "${CMAKE_TOOLCHAIN_PATH}/arm-none-eabi-g++")      # C++编译器
set(CMAKE_ASM_COMPILER "${CMAKE_TOOLCHAIN_PATH}/arm-none-eabi-gcc")      # 汇编编译器
set(CMAKE_OBJCOPY      "${CMAKE_TOOLCHAIN_PATH}/arm-none-eabi-objcopy")  # 生成bin/hex文件
set(CMAKE_OBJDUMP      "${CMAKE_TOOLCHAIN_PATH}/arm-none-eabi-objdump")  # 反汇编工具
set(CMAKE_SIZE         "${CMAKE_TOOLCHAIN_PATH}/arm-none-eabi-size")     # 查看程序大小


# 步骤3: 设置CMake目标系统信息(无需修改)
#   告诉CMake这是交叉编译环境，目标系统是Generic(通用)，处理器是ARM
set(CMAKE_SYSTEM_NAME Generic)       # 目标系统名称
set(CMAKE_SYSTEM_PROCESSOR arm)      # 目标处理器架构


# 步骤4: 配置库文件搜索模式(无需修改)
set(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)   # 可执行文件搜索策略
set(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)    # 库文件搜索策略
set(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)    # 头文件搜索策略


# 步骤5: 设置编译选项（最重要！必须与芯片匹配）
#   -mthumb       : 使用Thumb指令集（ARM Cortex-M必须）
#   -mcpu=cortex-m3 : 指定CPU内核类型
#   -mfloat-abi=soft: 软件浮点运算（F1系列无FPU）
#
#   【更换芯片时】: 必须根据芯片内核修改以下内容:
#     - cortex-m0/m0+: 使用 -mcpu=cortex-m0 或 cortex-m0plus
#     - cortex-m3    : 使用 -mcpu=cortex-m3
#     - cortex-m4    : 使用 -mcpu=cortex-m4
#     - cortex-m7    : 使用 -mcpu=cortex-m7
#
#   【关于-mfloat-abi参数】:
#     - soft  : 纯软件浮点运算（适用于无FPU的芯片，如F1/F0系列）
#     - softfp: 硬件FPU但用软件传参（兼容性）
#     - hard  : 硬件FPU用硬件传参（F4/F7/H7等有FPU的芯片）
#   【关于-mfpu-config】(仅m4/m7等有FPU的芯片需添加):
#     - -mfpu=fpv4-sp-d16 (F4系列)
#     - -mfpu=fpv5-d16    (F7/H7系列)
# -----------------------------------------------------------------------------
set(CMAKE_C_FLAGS_INIT   "-mthumb -mcpu=cortex-m3 -mfloat-abi=soft")
set(CMAKE_CXX_FLAGS_INIT "-mthumb -mcpu=cortex-m3 -mfloat-abi=soft")
set(CMAKE_ASM_FLAGS_INIT "-mthumb -mcpu=cortex-m3 -mfloat-abi=soft")


# 步骤6: 设置链接器脚本(CubeMX会自动生成这个文件，到时候ctlr+C就行了)
set(CMAKE_EXE_LINKER_FLAGS_INIT "-T${CMAKE_SOURCE_DIR}/STM32F103ZETX_FLASH.ld")

```
**step2:编写CMakeLists.txt**

文件路径:`ding26_4_15/CMakeLists.txt`

```
# =============================================================================
# STM32项目构建配置文件
# =============================================================================


# 步骤1: CMake版本要求(无需修改)
cmake_minimum_required(VERSION 3.25)


# 步骤2: 定义项目名称和编程语言(无需修改)
project(ding26_4_15 C ASM)


# 步骤3: 设置编译输出目录(无需修改)
#   CMAKE_RUNTIME_OUTPUT_DIRECTORY: 可执行文件输出路径
#   ${CMAKE_SOURCE_DIR}: 项目根目录
#   ${CMAKE_BUILD_TYPE}: Debug/Release/RelWithDebInfo/MinSizeRel
#   【说明】编译产物会输出到 build/Debug/ 目录下
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/build/${CMAKE_BUILD_TYPE})


# 步骤4: 收集所有源文件路径(需要修改，很麻烦，后面记得搞个自动化脚本，自动读取IDE的配置文件，然后自己写CMakeLists.txt)
set(SOURCES
    # --- 应用程序代码 (Core层) ---
    Core/Src/main.c                 # 主程序入口
    Core/Src/stm32f1xx_hal_msp.c    # HAL外设底层初始化
    Core/Src/stm32f1xx_it.c         # 中断服务程序
    Core/Src/syscalls.c             # 系统调用实现
    Core/Src/sysmem.c               # 内存操作函数
    Core/Src/system_stm32f1xx.c     # 系统初始化

    # --- 启动文件 (汇编) ---
    Core/Startup/startup_stm32f103zetx.s

    # --- HAL驱动库 ---
    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal.c         # HAL核心
    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_cortex.c  # Cortex内核
    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_gpio.c    # GPIO
    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_rcc.c      # 时钟配置
    Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_hal_rcc_ex.c  # 扩展时钟

    # --- CMSIS设备层 ---
    Drivers/CMSIS/Device/ST/STM32F1xx/Source/system_stm32f1xx.c
)


# 步骤5: 定义头文件搜索目录(需要修改)
set(INCLUDES
    Core/Inc                                     # 应用程序头文件
    Drivers/STM32F1xx_HAL_Driver/Inc           # HAL驱动头文件
    Drivers/CMSIS/Device/ST/STM32F1xx/Include  # 芯片寄存器定义
    Drivers/CMSIS/Include                       # ARM Cortex-M内核头文件
)


# 步骤6: 定义编译预处理宏(需要修改)
set(DEFINES
    STM32F103xE      # 芯片型号定义 (告诉HAL使用的是哪款芯片)
    USE_HAL_DRIVER   # 使用HAL驱动 (启用STM32 HAL库)
)


# 步骤7: 创建可执行文件目标
#   add_executable(目标名 源文件列表)
#   【说明】生成最终的可执行文件 ding26_4_15.elf
add_executable(${PROJECT_NAME}.elf ${SOURCES})

# -----------------------------------------------------------------------------
# 步骤8: 配置目标属性
#   target_include_directories: 添加头文件搜索路径
#   target_compile_definitions: 添加编译预处理宏
#   PRIVATE: 作用域为当前目标，不影响依赖项目
# -----------------------------------------------------------------------------
target_include_directories(${PROJECT_NAME}.elf PRIVATE ${INCLUDES})
target_compile_definitions(${PROJECT_NAME}.elf PRIVATE ${DEFINES})

# -----------------------------------------------------------------------------
# 步骤9: 添加编译后处理命令
#   POST_BUILD: 在编译完成后自动执行的命令
#   【功能】
#     1. 生成.bin二进制文件 (用于直接烧录)
#     2. 生成.hex格式文件 (用于串口/USB烧录)
#     3. 显示程序大小统计
# -----------------------------------------------------------------------------
add_custom_command(TARGET ${PROJECT_NAME}.elf POST_BUILD
    # 将elf转换为bin格式
    COMMAND ${CMAKE_OBJCOPY} -O binary ${PROJECT_NAME}.elf ${PROJECT_NAME}.bin
    # 将elf转换为hex格式
    COMMAND ${CMAKE_OBJCOPY} -O ihex ${PROJECT_NAME}.elf ${PROJECT_NAME}.hex
    # 显示程序大小信息
    COMMAND ${CMAKE_SIZE} ${PROJECT_NAME}.elf
    COMMENT "Building binary and hex files..."
)

# =============================================================================
# 【补充说明】
# =============================================================================
# 1. 如何添加新的源文件？
#    在SOURCES列表中添加即可，如: Core/Src/my_driver.c
#
# 2. 如何添加新的HAL驱动？
#    在Drivers/STM32F1xx_HAL_Driver/Src/目录下找到对应的.c文件并添加
#    常用驱动: stm32f1xx_hal_tim.c, stm32f1xx_hal_uart.c, stm32f1xx_hal_spi.c 等
#
# 3. 如何更换芯片型号？
#    需要修改以下内容:
#      - gcc-arm-none-eabi.cmake: CPU内核、链接脚本
#      - CMakeLists.txt: DEFINES中的芯片型号定义
#      - 启动文件: startup_stm32f103zetx.s
# =============================================================================
```

**step3:编写CMakePresets.json**

