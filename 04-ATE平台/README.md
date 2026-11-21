# ATE 平台

## 一、主流平台

| 平台 | 厂商 | 特点 |
|---|---|---|
| J750 | Teradyne | 结构清晰、资料多，逻辑/混合信号，入门资料最全 |
| V93000 | Advantest | 模块化、高速数字与 SoC 强，装机量大 |
| ETS-800 | Eagle | 模拟/混合信号、电源类 |
| Chroma 3650 | Chroma | 电源管理 IC |

选定一个学透，不要两个都学一半。

## 二、一台 ATE 的组成

```
测试程序 → 时序(Timing) → Pin Electronics → DUT
              │                 │
           电平(Levels)      比较器(Compare)
                                │
                           结果(Pass/Fail) → 数据记录
```

| 概念 | 含义 |
|---|---|
| Test Program | 测试流程与所有测试项 |
| Test Method | 单个测试项的实现 |
| Pattern | 输入 / 期望输出的向量序列 |
| Timing Set | 每个 pin 的驱动沿、采样沿 |
| Levels | VIL/VIH/VOL/VOH、比较阈值 |
| PMU / DC unit | 强制电压电流并测量 |

## 三、上手顺序

1. 读一支官方 demo program，逐行标出每个测试项在做什么。
2. 改：改限值、改时序、加一个 DC 测试项，跑通。
3. 写：从零写一支 `connect → DC 测试 → 功能 Pattern → disconnect` 的程序。
4. 调：人为制造失效（改限值、接错 pin），用 Shmoo 和 Pin Margin 找出来。

## 四、要练到的操作

- 建工程、配引脚映射
- 配 Levels 与 Timing
- 加载并运行 Pattern
- 用 PMU 做一次 IV 扫描（开短路测试）
- 跑一次 Shmoo（VCC × 频率）
- 读结果文件，定位失败 pin 与失败周期
