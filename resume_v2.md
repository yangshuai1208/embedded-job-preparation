# 杨帅｜嵌入式软件开发

## 个人信息

- 学校：兰州理工大学
- 专业：物联网工程 / 计算机相关专业
- 学历：本科，2027 届
- 电话：请填写
- 邮箱：请填写
- GitHub：yangshuai1208
- 求职方向：嵌入式软件开发、机器人嵌入式、IoT 设备开发、Linux C/C++、物联网网关

---·

## 教育经历

### 兰州理工大学｜物联网工程 / 计算机相关专业｜本科

- 在校时间：
- 主修课程：C 语言程序设计、数据结构、计算机网络、操作系统、单片机原理、嵌入式系统、物联网通信技术
- 武术校队成员，长期坚持健身和武术训练

---

## 专业技能

### 嵌入式开发

- 熟悉 C 语言，掌握指针、结构体、函数指针、内存管理、文件操作及常用数据结构。
- 熟悉 STM32 HAL 库、STM32CubeMX 和 Keil MDK，能够完成 GPIO、UART、I2C、SPI、定时器、ADC、外部中断等外设开发。
- 熟悉 FreeRTOS 任务管理、消息队列、互斥量、事件标志组、软件定时器及任务间通信。
- 熟悉 ESP32-S3 和 ESP-IDF，具备 I2C、UART、FreeRTOS、WiFi、MQTT 和组件化工程实践。
- 熟悉 DHT11、MPU6050、OLED、W25Q64、PCA9685 和舵机等常用模块。

### Linux 与通信

- 熟悉 Linux C 编程，掌握 `open/read/write/close`、`termios`、`pthread`、互斥锁、条件变量及 Socket 网络编程基础。
- 能够使用 Makefile、GDB、Git 和 GitHub 完成多文件编译、调试和版本管理。
- 了解 MQTT 发布订阅模型、自定义串口协议、JSON 数据格式及设备到网关的数据转发流程。
- 掌握 Qt5 / QWidget 基础，了解信号槽、TCP Socket 和串口上位机开发流程。

### 补强方向

- C++：掌握 C++17 嵌入式岗位常用基础，能够使用类与对象、引用、构造与析构、RAII，以及 string、vector、map 等常用标准库完成 Linux 应用模块开发。
- OTA：了解双分区、固件校验、启动确认和失败回滚原理。
- ROS2：了解 Node、Topic、Publisher、Subscriber 等基础概念。

---

## 项目经历

### AIoT 智能眼镜与具身智能灵动手控制系统

**技术栈：ESP32-S3、ESP-IDF、MPU6050、OLED、Linux C、UART、MQTT、STM32F407、PCA9685、MG90S**

- 基于 ESP32-S3 和 MPU6050 开发智能眼镜控制端，通过 I2C 读取加速度及角速度数据，使用阈值法识别 LEFT、RIGHT、NOD 等头部动作，并设计 NORMAL / CONTROL 模式和长按 STOP 安全控制。
- 将姿态结果映射为 OPEN、GRAB、RELEASE、STOP 等标准命令，通过 OLED 显示本地状态，并使用 UART 输出包含模式、手势、命令和状态的单行 JSON。
- 在 Linux 端使用 `termios` 配置 115200、8N1 双串口通信，解析 JSON 中的 `cmd` 字段，将命令转换为 `HAND_OPEN`、`HAND_GRAB`、`HAND_RELEASE`、`HAND_STOP` 并下发至 STM32F407。
- STM32F407 通过 I2C 配置 PCA9685，使用五路 PWM 控制 MG90S 舵机完成张开、抓取、释放和停止动作，并针对舵机角度越界、多舵机供电和非法命令设计安全保护。
- **难点与解决：**针对多端协议容易不一致的问题，将感知、命令和执行协议分层；当前使用 JSON 与文本命令快速完成 MVP，并将带帧头、长度和校验的二进制协议作为后续 V2，避免把设计功能写成已完成成果。

项目仓库：

- `aiot-smart-glasses`
- `aiot-embodied-control-system`
- `stm32_f407_hand_controller`

---

### STM32 + FreeRTOS 环境监测与报警系统

**技术栈：STM32F103C8T6、FreeRTOS、DHT11、OLED、UART、Flash、IWDG、ESP8266**

- 基于 STM32F103C8T6 和 FreeRTOS 实现温湿度采集、OLED 显示、报警阈值配置、串口日志和 Flash 配置掉电保存。
- 将系统划分为传感器、显示、串口、按键、任务监控、看门狗和 ESP8266 等 7 个任务，使用消息队列传递结构化传感器数据。
- 使用互斥量保护 UART、OLED 和配置资源，使用事件标志组记录任务运行、传感器、报警和 WiFi 状态。
- 设计任务心跳与 IWDG 联动机制，只有关键任务正常运行时才刷新看门狗，任务异常时停止喂狗并等待系统复位。
- **难点与解决：**针对 DHT11 读取超时和 `SYS TASK TIMEOUT`，增加通信超时退出、任务运行事件和监控时间窗口，避免外设或任务异常导致系统永久阻塞。

项目仓库：

- `env-monitor-v2`

---

### Linux IoT Gateway

**技术栈：Linux C、termios、MQTT、libmosquitto、JSON、自定义协议、Makefile、Git**

- 使用 Linux C 完成设备数据源抽象、自定义传感器协议解析、结构体数据转换和 JSON 构造，支持模拟数据脱离硬件测试。
- 使用 libmosquitto 连接 MQTT Broker，将有效传感器 JSON 发布到指定 Topic，并分别记录传感器业务日志和应用运行日志。
- 在系统联调工具中使用 `termios` 配置 115200、8N1 串口，逐字节接收 ESP32 JSON，按换行组帧并完成控制命令提取与 STM32 串口下发。
- 使用 Makefile 管理多模块编译与第三方库链接，对初始化、读取、协议解析、日志写入和 MQTT 发布进行返回值与异常处理。
- **难点与解决：**针对非法数据和协议格式错误，增加字段数量检查、接收缓冲区边界保护和异常数据丢弃，并修复 JSON 字段格式及串口位配置错误。

项目仓库：

- `linux-iot-gateway`
- `aiot-smart-glasses/tools/linux_uart_receiver`

---

## 其他项目

### STM32 桌面天气仪表盘

基于 STM32F103C8T6、DHT11、OLED、EC11 和 W25Q64，实现温湿度显示、旋钮页面切换、LED 舒适度提示及历史数据曲线展示。

项目仓库：

- `weather-dashboard`

---

## 个人优势

- 完成从 STM32、FreeRTOS、Linux 网关到 ESP32-S3 和机器人执行端的连续项目训练，能够独立进行模块开发、串口联调和问题排查。
- 具备较完整的项目文档习惯，持续维护中文 README、开发 notes、实验现象和 GitHub 提交记录。
- 武术校队成员，长期坚持健身和训练，具备较强执行力、抗压能力和团队意识。