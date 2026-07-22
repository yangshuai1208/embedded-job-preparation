# 第五个月第1周总结：项目验收、README 完整化与简历 v2 初稿

## 一、本周目标

第五个月第1周的核心目标不是继续开发新功能，而是对已有项目进行统一验收和整理，使项目从“能够运行”升级为：

- 能在 GitHub 上展示
- 能写入秋招简历
- 能支撑面试讲解
- 能说明个人代码产出
- 能复盘调试问题和解决方案

本周主要完成项目 README 审计、三个主项目文档完善、系统级架构梳理以及简历 v2 初稿。

---

## 二、本周完成内容

### Day1：项目 README 审计

对以下项目进行了 README 检查：

1. env-monitor-v2
2. linux-iot-gateway
3. weather-dashboard
4. aiot-smart-glasses
5. embodied-robotic-hand
6. stm32_f407_hand_controller
7. aiot-embodied-control-system

重点检查：

- 项目介绍
- 技术栈
- 硬件组成
- 软件架构
- 通信流程
- 关键代码模块
- 调试问题
- 实验现象
- 编译运行方式
- 面试可讲点

建立了：

```text
project_readme_audit.md
notes/day01.md
```

明确后续每一天都需要同步更新 README、notes 和 GitHub commit。

---

### Day2：完善 STM32 + FreeRTOS 环境监测项目

将 `stm32-learning` 中的最终环境监测综合工程提取到独立仓库：

```text
env-monitor-v2
```

完成内容：

- 整理项目介绍和硬件组成
- 整理 7 个 FreeRTOS 任务
- 补充消息队列、互斥量和事件标志组
- 补充 Flash 参数掉电保存
- 补充任务心跳和 IWDG
- 补充调试问题和实验现象
- 补充项目难点和面试可讲点
- 添加 `.gitignore`
- 完成独立 GitHub 仓库提交

同时明确：

```text
env-monitor-v2
```

和：

```text
weather-dashboard
```

是两个不同项目，不能混写。

环境监测项目突出：

- FreeRTOS 多任务
- 队列
- 互斥量
- 事件标志组
- Flash
- IWDG
- 异常监控

天气仪表盘突出：

- EC11
- OLED 多页面
- W25Q64
- 历史曲线
- 桌面交互展示

---

### Day3：完善 Linux IoT Gateway

整理了 Linux IoT Gateway 当前真实功能：

```text
数据源抽象
→ 自定义协议解析
→ SensorData 结构体
→ JSON 构造
→ 本地日志
→ MQTT 发布
```

完成内容：

- 检查当前正式仓库功能边界
- 整理 Linux C 模块化结构
- 整理模拟数据源和串口扩展设计
- 整理协议解析流程
- 整理 libmosquitto MQTT 发布流程
- 整理业务日志和应用日志
- 修复 JSON 中湿度字段缺少冒号的问题
- 补充 Makefile 编译运行说明
- 整理调试问题和面试可讲点

当前已实现：

- 模拟数据输入
- 协议解析
- JSON 构造
- 本地日志
- MQTT 发布
- Makefile 编译

当前待继续整合：

- 完整 termios 串口收发
- pthread 多线程
- TCP Server
- 串口、TCP、MQTT 并行转发

---

### Day4：完善 AIoT 智能眼镜控制端

整理了智能眼镜真实控制主线：

```text
MPU6050 姿态采集
→ 阈值手势识别
→ NORMAL / CONTROL 模式判断
→ 手势到命令映射
→ OLED 状态显示
→ UART JSON 输出
→ MQTT 命令发布
```

完成内容：

- 精简原有冗余 README
- 将每日开发过程移动到独立文档
- 整理 MPU6050 I2C 采集流程
- 整理手势识别阈值
- 整理 OPEN、GRAB、RELEASE、STOP 映射
- 整理 OLED 和按键交互
- 整理 UART JSON 与 MQTT Payload
- 补充误识别优化思路
- 补充 OTA 规划
- 清理 WiFi SSID 和密码等敏感配置

当前算法边界：

- 使用原始加速度和角速度阈值
- 未实现复杂姿态融合
- 后续考虑校准、滤波、多帧确认、迟滞和状态机

---

### Day5：整理 STM32F407 灵动手执行端

建立并整理：

```text
stm32_f407_hand_controller
```

完成内容：

- 初始化独立 Git 仓库
- 绑定 GitHub 远程仓库
- 整理 STM32F407 执行端定位
- 整理 PCA9685 12 位 PWM 原理
- 整理 MG90S 多舵机通道
- 整理 HAND_OPEN、HAND_GRAB、HAND_RELEASE、HAND_STOP
- 整理舵机角度和 PWM 限幅
- 整理非法命令处理
- 整理舵机独立供电和共地要求
- 整理常见硬件调试问题

执行链路：

```text
UART 控制命令
→ STM32F407 协议解析
→ 动作映射
→ 舵机安全限幅
→ I2C 配置 PCA9685
→ 五路 PWM
→ 灵动手动作
```

---

### Day6：完善系统级旗舰项目

完善：

```text
aiot-embodied-control-system
```

统一整理三个端的系统闭环：

```text
ESP32-S3 智能眼镜
→ UART JSON
→ Linux Gateway
→ HAND_* 文本协议
→ STM32F407
→ PCA9685
→ MG90S 舵机
```

完成内容：

- 区分当前真实协议和后续 V2 协议
- 明确当前主要闭环为 UART JSON
- 明确 ESP32 MQTT 发布已实现
- 明确 Linux MQTT 订阅转发仍需继续整合
- 编写当前通信协议说明
- 编写系统演示步骤
- 修复 `GRAB` 被写成 `GARB` 的问题
- 修复 Linux 串口 `termios` 配置错误
- 整理异常处理和 STOP 安全机制

当前协议：

```text
ESP32 → Linux：单行 JSON + \n
Linux → STM32：HAND_* 文本命令 + \n
```

后续 V2 规划：

```text
AA 55 CMD LEN DATA CHECKSUM 0D 0A
```

V2 计划增加：

- 帧头和帧尾
- 长度字段
- 校验和
- ACK
- 心跳
- 错误码
- 动作参数

---

### Day7：简历 v2 初稿

新建：

```text
resume_v2.md
```

将以下三个项目作为秋招主项目：

1. AIoT 智能眼镜与具身智能灵动手控制系统
2. STM32 + FreeRTOS 环境监测与报警系统
3. Linux IoT Gateway

每个项目整理了：

- 项目技术栈
- 3 条以上技术亮点
- 个人完成的核心模块
- 项目难点与解决方案
- 对应 GitHub 仓库

同时完成简历真实性检查，删除或降低以下夸大表述：

- 精通 C/C++
- 复杂姿态融合算法
- 完整商业级 MQTT 系统
- OTA 已集成主项目
- ROS2 已接入灵动手
- 工业级高可靠系统

---

## 三、本周形成的主要成果

### 1. 项目文档成果

- 项目 README 审计记录
- env-monitor-v2 完整 README
- linux-iot-gateway 文档整理
- aiot-smart-glasses README 精简
- stm32_f407_hand_controller 项目整理
- aiot-embodied-control-system 系统级说明
- 当前通信协议文档
- 系统演示说明

### 2. GitHub 成果

本周完成多个仓库的代码或文档提交，确保项目具备持续可追踪的开发记录。

主要仓库：

```text
env-monitor-v2
linux-iot-gateway
aiot-smart-glasses
stm32_f407_hand_controller
aiot-embodied-control-system
embedded-job-preparation
```

### 3. 简历成果

完成简历 v2 初稿，初步形成：

```text
MCU + RTOS
Linux 网关
ESP32 感知端
STM32 执行端
系统级通信闭环
```

的技术主线。

---

## 四、本周核心知识点

### STM32 与 FreeRTOS

- FreeRTOS 任务划分
- 消息队列
- 互斥量
- 事件标志组
- 任务心跳
- IWDG
- Flash 掉电保存
- 传感器超时处理

### Linux IoT Gateway

- Linux 设备文件
- `open/read/write/close`
- `termios`
- 115200、8N1
- 数据源抽象
- 自定义协议解析
- JSON 构造
- MQTT 发布
- Makefile
- 日志和异常处理

### ESP32 智能眼镜

- ESP-IDF 组件化开发
- MPU6050 I2C 通信
- 原始数据阈值识别
- 手势到命令映射
- OLED 本地显示
- UART JSON
- WiFi 与 MQTT
- 敏感配置管理
- OTA 基础规划

### 灵动手执行端

- PCA9685
- 16 路 12 位 PWM
- PRESCALE
- 舵机角度到 PWM 转换
- 五路舵机动作库
- 角度限幅
- STOP 安全命令
- 独立供电和共地

### 系统设计

- 感知、网关和执行三端分层
- UART 和 MQTT 的职责区别
- 当前文本协议与后续二进制协议
- 已实现、部分实现和后续规划的边界
- README、GitHub、简历和面试内容一致性

---

## 五、本周遇到的问题和解决方案

### 1. 项目边界混淆

问题：

env-monitor-v2 和 weather-dashboard 的功能被混在一起。

解决：

重新区分两个项目的真实代码和技术重点，分别维护 README。

### 2. Git 仓库未初始化或未绑定远程

问题：

出现：

```text
fatal: not a git repository
No configured push destination
```

解决：

使用：

```bash
git init
git branch -M main
git remote add origin <仓库地址>
git push -u origin main
```

### 3. GitHub 网络连接被重置

问题：

```text
Recv failure: Connection was reset
```

解决：

切换 HTTP/1.1、检查代理和网络连接后重新推送。

### 4. WSL 和 VS Code Server 异常

问题：

```text
VS Code Server for WSL closed unexpectedly
Code.exe: Exec format error
```

解决：

使用：

```powershell
wsl --shutdown
wsl --update
```

并检查 WSL Interop 和 VS Code Server。

### 5. README 与代码不一致

问题：

文档中写入了尚未真正实现的 TCP、多线程、二进制协议、OTA 和 ROS2。

解决：

统一划分为：

```text
当前已实现
部分实现
后续规划
```

---

## 六、本周面试可讲点

1. 为什么使用 FreeRTOS，而不是全部写在 `while(1)` 中？
2. 队列、互斥量和事件标志组分别解决什么问题？
3. 如何使用任务心跳配合 IWDG？
4. Linux 串口如何配置 115200、8N1？
5. 为什么使用 Linux Gateway 作为中间层？
6. UART 和 MQTT 分别适合什么场景？
7. 为什么当前先使用 JSON 和文本协议？
8. 为什么未来需要升级为二进制协议？
9. MPU6050 阈值法为什么容易误识别？
10. 如何通过多帧确认、迟滞和状态机优化？
11. 为什么使用 PCA9685 控制多舵机？
12. 多舵机为什么需要独立供电并共地？
13. STOP 命令如何保证安全优先级？
14. 如何保证简历内容与项目代码一致？

---

## 七、本周不足

1. linux-iot-gateway 正式仓库的 TCP 和 pthread 模块仍需继续整合。
2. 智能眼镜手势识别仍为基础阈值算法。
3. Linux MQTT 订阅到 STM32 转发尚未完成正式闭环。
4. OTA 尚未合并到智能眼镜主工程。
5. ROS2 尚未建立最小通信闭环。
6. 项目还缺少统一的架构图片、实物照片和演示视频。
7. 简历 v2 当前仍是 Markdown 初稿，需要进一步压缩为一页 PDF。

---

## 八、下周计划

第2周重点进行 C++ 基础补强和 Linux 网关模块升级：

1. 学习类和对象
2. 编写 LogManager 类
3. 学习构造函数和析构函数
4. 学习引用和 `this` 指针
5. 学习 `string` 和 `vector`
6. 学习 `map`
7. 编写 gesture 到 command 映射
8. 编写 C++ 协议解析模块
9. 更新 Linux IoT Gateway README
10. 整理 C++ 面试题

---

## 九、本周总结

本周最大的成果不是新增了多少代码，而是将已有项目重新整理为可以用于秋招的技术证据。

目前已经初步形成：

```text
STM32 + FreeRTOS 环境监测系统
Linux IoT Gateway
AIoT 智能眼镜与灵动手控制系统
```

三条主要项目线。

下一阶段将继续补强 C++、ESP-IDF、OTA 和 ROS2，并逐步把简历、GitHub、项目讲解和岗位投递连接起来。