# 测试专业知识

## 一、测试分类

| 类别 | 测什么 | 典型测试项 | 资源 |
|---|---|---|---|
| DC 参数 | 直流电平、电流、阻抗 | 阈值 VIL/VIH/VT、输出 VOH/VOL、输入漏电 IIL/IIH、电源电流 IDD/ICC、IDDQ、开路短路 | PMU / DC unit / DPS |
| AC 参数 | 时间与频率 | 上升/下降时间、传播延迟 tPD、建立/保持、最大频率、增益、带宽、相位裕度 | 高速 digital pin + 比较器 |
| 功能 | 逻辑是否正确 | Pattern 比对、真值表、状态机序列、通信协议 | Pattern memory + 驱动器 |
| 混合信号 | ADC/DAC 指标 | INL、DNL、SNR、THD、ENOB | AWG + 数字化仪 |

**DC 测试放在最前面**：快、便宜，能挡掉开路、短路、漏电、ESD 损伤，避免后面浪费测试时间。

**AC 测试常用手段**：

- **Shmoo**：两个变量（常见 VCC × 周期/频率）扫描，画出 Pass/Fail 边界。
- **Pin Margin**：把每个 pin 的时序/电平往边界推，量剩余余量。
- **Guard band**：测试限值留的保护带，防止量测误差误杀好品。

## 二、DFT

| 技术 | 原理 | 用途 |
|---|---|---|
| Scan Chain | 内部触发器串成移位寄存器，Pattern 移入激励、移出响应 | 检测内部逻辑固定型故障（stuck-at） |
| BIST | 片内自测：LFSR 产生激励，MISR 压缩响应 | 存储器与逻辑自测，减少 ATE 资源占用 |
| Boundary Scan（JTAG） | IO 上加边界扫描单元串成链（IEEE 1149.1） | 板级互连测试、无需探针访问内部 |

## 三、CP / FT / SLT

| 阶段 | 时机 | 对象 | 设备 | 目的 |
|---|---|---|---|---|
| CP（Chip Probing） | 封装前 | 晶圆上的裸 die | 探针台 + ATE | 挑出坏 die，避免封装浪费 |
| FT（Final Test） | 封装后 | 成品芯片 | ATE + Handler | 保证出厂性能、分 bin |
| SLT（System Level Test） | FT 之后 | 成品 | 板级/系统级测试台 | 模拟真实应用，抓 FT 漏掉的系统级问题 |

成本：CP < FT < SLT，所以能往前挡的尽量往前挡。

## 四、数据分析

| 指标 | 含义 | 用途 |
|---|---|---|
| 良率 Yield | 通过数 / 总数 | 日常监控、批次对比 |
| Bin | 失效分类（bin 1 = pass） | 定位主要失效模式 |
| Cpk | 工序能力指数 | 判断限值是否合理、工艺是否稳定（一般要求 ≥ 1.33） |
| SPC | 统计过程控制 | 控制图监控漂移，异常预警 |
| Shmoo | 二维 Pass/Fail 扫描 | 找失效边界与余量 |
| Wafer Map | 晶圆上每颗 die 的结果 | 判断失效是否与位置相关 |

## 五、术语

| 术语 | 含义 |
|---|---|
| DUT | 被测器件 |
| DIB / Load Board | 测试接口板 |
| Probe Card / Socket | 探针卡（CP）/ 测试座（FT） |
| Test Program / Test Plan | 测试程序 / 测试计划 |
| Pattern / Vector | 测试向量 |
| Timing Set | 时序配置（驱动沿、采样沿） |
| Levels | 电平配置（VIL/VIH/VOL/VOH、比较阈值） |
| PMU | 参数测量单元 |
| Guard band | 保护带 |
| OQC / IQC | 出货 / 来料检验 |
