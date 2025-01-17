# API 使用说明

> API (Application Programming Interface), 也称为应用程序编程接口函数，是预定义的函数。使用以下函数接口时，请在开始时输入以下代码导入我们的 API 库，否则将无法成功运行

```python
from pymycobot import MyArmM

# 示例
myarmm = MyArmM('/dev/ttyAMA1')

# 获取所有关节的当前角度
angles = myarmm.get_joints_angle()
print(angles)

# 设置关节1移动到40, 速度为20
myarmm.set_joint_angle(1, 40, 20)
```

# 1. 机器人状态查询

**1.1** `get_robot_modified_version()`

- **功能:** 获取机器人更正版本号
- **参数:** 无
- **返回:** 无

**1.2** `get_robot_firmware_version()`

- **功能:** 获取机器人固件版本（主次版本）
- **参数:** 无
- **返回:** 无

**1.3** `get_robot_tool_modified_version()`

- **功能:** 获取机器人工具修正版本
- **参数:** 无
- **返回:** 无

**1.4** `get_robot_tool_firmware_version()`

- **功能:** 获取机器人工具固件版本(末端Atom)
- **参数:** 无
- **返回:** 无

**1.5** `set_robot_err_check_state(status)`

- **功能:** 设置错误检测状态 您可以关闭错误检测，但除非必要，否则不要将其关闭
- **参数:**
  - **status** - int
    - 1 - 打开错误检测
    - 0 - 关闭错误检测
- **返回:** 无

**1.6** `get_robot_err_check_state()`

- **功能:** 读取错误检测状态
- **参数:** 无
- **返回:**
  - 1 - 错误检测打开
  - 0 - 错误检测关闭

**1.7** `get_robot_error_status()`

- **功能:** 获取机器人错误状态, 此接口返回在15s内
- **参数:** 无
- **返回:** 没有错误返回: [0,0,0,0,0,0,0,0],假设在第 1 节中报告了错误 1 和 3，它应该返回：[[1,3]，0,0,0,0,0,0,0,0]

**1.8** `get_robot_power_status()`

- **功能:** 获取机器人电源状态
- **参数:** 无
- **返回:**
  - 1 - 开机状态
  - 0 - 关机状态

**1.9** `set_robot_power_on()`

- **功能:** 将机器人设置为开机状态
- **参数:** 无
- **返回:** 无

**1.10** `set_robot_power_off()`

- **功能:** 将机器人设置为关机状态
- **参数:** 无
- **返回:** 无

**1.11** `clear_robot_err()`

- **功能:** 清除机器人异常，忽略报错关节，继续运动
- **参数:** 无
- **返回:** 无

**1.12** `get_recv_queue_max_len()`

- **功能:** 读取接收指令队列总长度
- **参数:** 无
- **返回:** 
  - `max_len`: `(int)` 指令队列总长度，默认值`100`

**1.13** `set_recv_queue_max_len(max_len)`

- **功能:** 设置接收指令队列总长度
- **参数:** 
  - `max_len`: `(int)` 队列长度
- **返回:**  无

**1.14** `clear_recv_queue()`

- **功能:** 清除接收指令队列
- **参数:** 无
- **返回:** 无

**1.15** `get_recv_queue_len()`

- **功能:** 读取接收指令队列当前长度
- **参数:** 无
- **返回:** 
  - `queue_len`: `(int)` 当前指令队列长度

# 2. 关节伺服控制

**2.1** `set_joint_angle(joint_id, angle, speed)`

- **功能:** 将各个关节设置为移动到目标角度

- **参数:**
  - `joint_id`: `(int)` 关节编号
  - `angle`: `(int)` 目标角度
  - `speed`: `(int)` 移动速度，取值范围 `1 - 100`

- **返回** 无

**2.2** `get_joint_angle(joint_id)`

- **功能:** 获取指定关节的当前角度
- **参数:**
  - `joint_id`: 机械臂的指定关节,范围为 1~6
- **返回:** 
  - `angle` 表示当前关节的角度

**2.3** `set_joints_angle(angles, speed)`

- **功能:** 将所有关节设置为移动到目标角度
- **参数:**
  - `angles`: `(list[int])` 目标角度
  - `speed`: `(int)` 移动速度，取值范围 `1 - 100`
- **返回** 无

**2.4** `get_joints_angle()`

- **功能:** 获取所有关节的当前角度
- **参数:** 无
- **返回:** 
  - `angles` 返回一个浮点型的列表，表示所有关节的当前角度

**2.5** `get_joints_max()`

- **功能:** 读取所有关节的最大角度
- **参数:** 无
- **返回:** 
  - `angles` 返回一个浮点型的列表，表示所有关节的最大角度

**2.6** `get_joints_min()`

- **功能:** 读取所有关节的最小角度
- **参数:** 无
- **返回:** 
  - `angles` 返回一个浮点型的列表，表示所有关节的最小角度


**2.7** `is_robot_moving()`

- **功能:** 查看机器人是否在移动
- **参数:** 无
- **返回**
    - 1 - 正在移动
    - 0 - 静止

**2.8** `stop_robot()`

- **功能:** 机器人停止移动
- **参数:** 无
- **返回** 无


# 3. 伺服电机控制

**3.1** `set_servo_calibrate(servo_id)`

- **功能:** 设置指定伺服电机的零位
- **参数:** 
  - `servo_id` 表示伺服电机索引位，取值范围 `1 - 6`
- **返回:** 无

**3.2** `set_servos_encoder_drag(encoders, speeds)`

- **功能:** 将多个具有指定速度的伺服电机设置为目标编码器电位值
- **参数:**
  - `encoders`: `(list[int])` 电位值
  - `speeds`: `(list[int])` 速度
- **返回:** 无

**3.3** `get_servos_encoder_drag()`

- **功能:** 读取所有伺服电机当前编码器值和运行速度
- **参数:** 无
- **返回:** 
  - `encoders`: `(list[int])` 电位值
  - `speeds`: `(list[int])` 速度

**3.4** `set_servo_encoder(servo_id, encoder, speed)`

- **功能:** 将单个电机运动设置为目标编码器电位值
- **参数:**
  - `servo_id`: `(int)` 表示伺服电机索引位，取值返回 `1 - 6`
  - `encoder`: `(int)` 电机电位值， 取值返回 `0 - 4095`
  - `speed`: `(int)` 电机移动速度，取值范围 `1 - 100`
- **返回** 无

**3.5** `get_servo_encoder(servo_id)`

- **功能:** 获取指定伺服电机的当前编码器电位值
- **参数:** 
  - `servo_id`: `(int)` 表示伺服电机索引位，取值返回 `1 - 6`
- **返回:** 
  - `encoder`:`(int)` 表示机械臂的电位值，取值范围是 0 ~ 4096

**3.6** `set_servos_encoder(positions, speed)`

- **功能:** 设置移动到目标的多个电机的编码器电位值
- **参数:**
  - `positions`: `(list[int])` 多个电机的目标电位值 `0 - 4095`
  - `speed`: `(int)` 电机移动速度，取值范围 `1 - 100`
- **返回** 无

**3.7** `get_servos_encoder()`

- **功能:** 获取多个伺服电机的当前编码器电位值
- **参数:** 无
- **返回:** 
  - `encoders`: `(list[int])` 表示机械臂的电位值，取值范围是 0 ~ 4096，六轴长度为 6，四轴长度为 4，表示方法为：[2048,2048,2048,2048,2048,2048] 

**3.8** `get_servos_speed()`

- **功能:** 获取多个伺服电机的当前运动速度
- **参数:** 无
- **返回:** 
  - `speeds`: `(list[int])` 伺服电机运动速度 

**3.9** `is_all_servos_enabled()`

- **功能:** 获取多个伺服电机的连接状态
- **参数:** 无
- **返回:** 
  - `status`: `(list[int])`
    - 1 : 连接成功
    - 0 : 连接失败

**3.10** `get_servos_temp()`

- **功能:** 获取多个伺服电机的温度
- **参数:** 无 
- **返回:** `list(float)` 每个伺服电机的温度

**3.11** `get_servos_voltage()`

- **功能:** 获取多个伺服电机的电压
- **参数:** 无 
- **返回:** `list(float)` 每个伺服电机的电压

**3.12** `get_servos_current()`

- **功能:** 获取多个伺服电机的电流
- **参数:** 无 
- **返回:** `list(float)` 每个伺服电机的电流

**3.13** `get_servos_status()`

- **功能:** 获取多个伺服电机的所有状态
- **参数:** 无 
- **返回:** `list(int)` 每个伺服电机的状态

**3.14** `get_servos_protect_current()`

- **功能:** 获得多个伺服电机保护电流
- **参数:** 无 
- **返回:** `list(int)` 每个伺服电机的保护电流

**3.15** `set_servo_enabled(joint_id, state)`

- **功能:** 设置伺服电机转矩开关
- **参数:**
  - `joint_id`: `(int)`电机索引位
  - `state`: `(int)`
    - 1 - 上电
    - 0 - 释放
- **返回:** 无

# 4. 伺服电机系统参数修改

**4.1** `set_servo_p(servo_id, data)`

- **功能:** 设置指定伺服电机的位置环P比例系数
- **参数:**
  - `servo_id`: `(int)` 电机索引位
  - `data`: `(int)` 环P比例系数
- **返回:** 无

**4.2** `get_servo_p(servo_id)`

- **功能:** 读取指定伺服电机的位置环P比例系数
- **参数:**
  - `servo_id`: `(int)` 电机索引位
- **返回:** 环P比例系数

**4.3** `set_servo_i(servo_id, data)`

- **功能:** 设置指定伺服电机的位置环I比例系数

- **参数:**
  - `servo_id`: `(int)` 电机索引位，取值范围 `0 -254`
  - `data`: `(int)` 环I比例系数，取值范围 `0 -254`
- **返回:** 无

**4.4** `get_servo_i(servo_id)`

- **功能:** 读取指定伺服电机的位置环I比例系数
- **参数:** 
  - `servo_id`: `(int)` 电机索引位，取值范围 `0 -254`
- **返回:** 
  - `data`: `(int)` 环I比例系数，范围 `0 -254`

**4.5** `set_servo_d(servo_id, data)`

- **功能:** 设置指定伺服电机的位置环D比例系数

- **参数:**
  - `servo_id`: `(int) ` 伺服电机的索引号，按照关节id给入`1 - 6`
  - `data`: `(int)` `0 - 254`

- **返回:** 无

**4.6** `get_servo_d(servo_id)`

- **功能:** 读取指定伺服电机的位置环D比例系数
- **参数:**
  - `servo_id`: `(int) ` 伺服电机的索引号，按照关节id给入`1 - 6`
- **返回:** 
    - `data`: `(int)` `0 - 254`

**4.7** `set_servo_cw(servo_id, data)`

- **功能:** 设置指定伺服电机的编码器顺时针不灵敏区
- **参数:**
  - `servo_id`: `(int) ` 伺服电机的索引号，按照关节id给入`1 - 6`
  - `data`: `(int)` `0 - 32`
- **返回:** 无

**4.8** `get_servo_cw(servo_id)`

- **功能:** 读取指定伺服电机的编码器顺时针不灵敏区

- **参数:**
  - `servo_id`: `(int) ` 伺服电机的索引号，按照关节id给入`1 - 6`
- **返回:** 
  - `data`: `(int)` `0 - 32`

**4.9** `set_servo_cww(servo_id, data)`

- **功能:** 设置指定伺服电机的编码器逆时针不灵敏区
- **参数:**
  - `servo_id`: `(int) ` 伺服电机的索引号，按照关节id给入`1 - 6`
  - `data`: `(int)` `0 - 32`
- **返回:** 无

**4.10** `get_servo_cww(servo_id)`

- **功能:** 读取指定伺服电机的编码器逆时针不灵敏区
- **参数:**
  - `servo_id`: `(int) ` 伺服电机的索引号，按照关节id给入`1 - 6`
- **返回:** 无

**4.11** `set_servo_system_data(servo_id, addr, data, mode)`

- **功能:** 设置指定伺服电机的系统参数

- **参数:**
  - `servo_id`: `(int) ` 伺服电机的索引号，按照关节id给入`1 - 6`
  - `addr`: `(int)` 数据地址
  - `data`: `(int)` `0-4096` 数据
  - `mode`: `(int)` `1/2`
- **返回:** 无

**4.12** `get_servo_system_data(servo_id, addr, mode)`

- **功能:** 读取指定伺服电机的系统参数

- **参数:**
  - `servo_id`: `(int)` 伺服电机的索引号，按照关节id给入`1 - 6`
  - `addr`: `(int)` 数据地址
  - `mode`: `(int)` `1/2`

- **返回:** 数据

# 5. IO 控制

**5.1** `set_master_out_io_state(io_number, status)`

- **功能:** 设置主控引脚状态
- **参数:**
  - `io_number`: `(int)` 引脚位置，取值范围 `1-2`
  - `status`: `(int)`
    - 1 - 高电平
    - 0 - 低电平
- **返回:** 无

**5.2** `get_master_in_io_state(io_number)`

- **功能:** 读取主控引脚状态
- **参数:**
  - `io_number`: `(int)` 引脚位置，取值范围 `1-2`
- **返回:**
  - 1 - 高电平
  - 0 - 低电平

**5.3** `set_tool_out_io_state(io_number, status)`
- **功能:** 设置末端引脚状态
- **参数:**
  - `io_number`: `(int)` 引脚位置，取值范围 `1-2`
  - `status`: `(int)`
    - 1 - 高电平
    - 0 - 低电平
- **返回:** 无

**5.4** `get_tool_in_io_state(io_number)`

- **功能:** 读取末端引脚状态
- **参数:**
  - `io_number`: `(int)` 引脚位置，取值范围 `1-2`
- **返回:**
  - 1 - 高电平
  - 0 - 低电平

# 6. Atom 控制

**6.1** `set_tool_led_color(r, g, b)`

- **功能:** 设置 Atom LED 颜色
- **参数:**
  - `R`: `(int)` `0 - 255`
  - `G`: `(int)` `0 - 255`
  - `B`: `(int)` `0 - 255`
- **返回:** 无

**6.2** `is_tool_btn_clicked()`

- **功能:** 读取 Atom 按下状态
- **参数:** 无
- **返回:**
   - 1 - 按下
   - 0 - 未按下

---

[← 上一页](1_download.md) | [下一页 →](6_example.md)