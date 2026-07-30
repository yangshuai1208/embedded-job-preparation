# 第五个月第二周总结

## 一、本周目标

补强嵌入式 Linux 岗位需要的 C++ 基础，并将所学内容用于 Linux IoT Gateway。

## 二、本周完成内容

### 1. LogManager

完成：

- 类与对象
- public 和 private
- 构造函数和析构函数
- RAII 文件资源管理
- 终端与文件双通道日志
- 链式配置接口
- 最近日志缓存
- 日志等级统计

### 2. ProtocolParser

完成：

- 文本协议输入清洗
- 大小写统一
- Command 枚举
- std::map 命令查找
- HAND_* 执行命令映射
- Unknown 安全默认状态
- 正常与异常输入测试

### 3. 模块集成

完成：

```text
字符串输入
→ ProtocolParser
→ Command
→ HAND_*
→ LogManager
```

## 三、本周掌握的 C++ 技术

- class 与对象
- public / private
- 构造函数与析构函数
- 成员初始化列表
- RAII
- explicit
- 引用与 const 引用
- this 与 *this
- 链式调用
- const 成员函数
- std::string
- std::vector
- std::map
- std::ofstream
- std::transform
- Lambda
- 范围 for
- Makefile 多文件编译

## 四、形成的技术证据

- cpp_modules/log_manager
- cpp_modules/protocol_parser
- cpp_modules/integration_demo
- Day8～Day14 notes
- Linux IoT Gateway README
- 编译运行结果
- 日志文件
- GitHub commit

## 五、本周遇到的问题

- C++ 标识符大小写错误
- 函数声明与定义不一致
- 分号遗漏
- std::cout 拼写错误
- 范围 for 冒号写错
- getFilePath 拼写错误
- 查询和修改接口职责混淆
- GitHub TLS 网络连接失败

## 六、解决方法

- 统一类名和函数名
- 声明与定义逐项核对
- 使用 -Wall -Wextra -Werror
- 使用独立 Demo 验证模块
- 使用 const 区分查询接口
- 非法协议统一返回 Unknown
- GitHub 网络恢复后只重新执行 git push

## 七、当前不足

- C++ 使用仍处于基础阶段
- 尚未系统学习拷贝控制与移动语义
- 尚未学习智能指针
- 尚未学习 std::thread 和 std::mutex
- C++ 模块尚未正式替换 C 主流程
- 协议模块尚未接入真实数据源

## 八、下周计划

1. 学习 C++ 多线程基础
2. 学习 std::thread
3. 学习 std::mutex
4. 学习 std::lock_guard
5. 实现线程安全日志
6. 将协议解析器接入网关输入
7. 增加集成测试
8. 继续简历投递和面试训练

## 九、本周总结

本周最大的成果不是学习了多少语法，而是将 C++ 基础用于 Linux IoT Gateway 的日志和协议解析模块，并形成了代码、文档、测试、README 和 GitHub 提交组成的求职证据。