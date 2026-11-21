# 面试题

## 一、模拟电路

**1. 画一个共射放大电路，说明每个元件的作用。**
<details><summary>答案</summary>

VCC 供电；Rb 提供基极偏置电流、定 Q 点；Rc 把集电极电流变化转换成电压变化；C1/C2 隔直通交；三极管工作在放大区，iC = β·iB。

</details>

**2. 为什么共射输出与输入反相？**
<details><summary>答案</summary>

uCE = VCC − Rc·iC，交流分量 uce = −Rc·ic = −βRc·ib。负号来自 Rc：电流增大时集电极电压被拉低。

</details>

**3. 静态工作点怎么算？Q 点选在哪里最好？**
<details><summary>答案</summary>

IBQ=(VCC−UBEQ)/Rb，ICQ=β·IBQ，UCEQ=VCC−ICQ·Rc。Q 点取在交流负载线中点，可得到最大不失真输出。

</details>

**4. 输出波形顶部削平是什么失真？怎么调？**
<details><summary>答案</summary>

NPN 共射，顶部削平是截止失真，Q 点太低（IBQ 太小），应减小 Rb 抬高 Q 点。底部削平是饱和失真，方向相反。

</details>

**5. 共射、共集、共基有什么区别？**
<details><summary>答案</summary>

| | 共射 | 共集（射随） | 共基 |
|---|---|---|---|
| 电压增益 | 大，反相 | ≈1 | 大，同相 |
| 输入电阻 | 小 | 大 | 很小 |
| 输出电阻 | 大 | 小 | 大 |
| 用途 | 电压放大 | 缓冲/驱动 | 高频 |

</details>

**6. 运放的虚短、虚断是什么？成立条件？**
<details><summary>答案</summary>

虚短 u+ ≈ u−，虚断 i+ ≈ i− ≈ 0。条件是开环增益极大且处于负反馈闭环；没有负反馈就不能用虚短。

</details>

**7. MOS 管、三极管、二极管的特性区别？**
<details><summary>答案</summary>

二极管：单向导电，硅管正向 0.7 V。
三极管：电流控制电流源，iC=βiB，输入特性指数型。
MOS：电压控制电流源，栅极几乎不取电流，按 Vgs 分截止/线性/饱和区。

</details>

**8. 为什么固定偏置电路的 Q 点会漂移？**
<details><summary>答案</summary>

温度升高时 UBEQ 下降、β 上升、ICBO 增大，三者叠加使 ICQ 升高、Q 点上移，容易饱和。改进用分压式偏置 + Re 负反馈。

</details>

## 二、数字电路

**9. 组合逻辑和时序逻辑的区别？**
<details><summary>答案</summary>

组合逻辑输出只取决于当前输入，无记忆（加法器、译码器、MUX）；时序逻辑输出取决于当前输入和历史状态，含触发器/寄存器，受时钟控制。组合逻辑可用固定向量测，时序逻辑需要时钟序列。

</details>

**10. 给一个电路或真值表，算出输出波形。**
<details><summary>答案</summary>

逐级展开真值表：输入 → 中间节点 → 输出。有时钟的先画时钟沿，再按建立/保持时间确定采样值。毛刺只出现在组合逻辑的瞬态。

</details>

**11. 建立时间和保持时间？违反会怎样？**
<details><summary>答案</summary>

建立时间：时钟沿前数据必须稳定的最短时间；保持时间：时钟沿后必须保持的最短时间。违反导致亚稳态，在测试上表现为随机失效。

</details>

**12. D 触发器和锁存器的区别？**
<details><summary>答案</summary>

锁存器电平敏感（使能期间输出跟随输入），触发器边沿敏感（只在时钟沿采样）。Scan Chain 用边沿触发器。

</details>

## 三、测试

**13. DC 测试测什么？为什么先测？**
<details><summary>答案</summary>

测直流电平/电流/阻抗：输入阈值、输出高低电平、漏电流、电源电流、开短路。先测因为快且便宜，能挡掉开短路、漏电、ESD 坏片。

</details>

**14. CP、FT、SLT 的区别？**
<details><summary>答案</summary>

CP：晶圆级，封装前挑坏 die；FT：封装后保证出厂性能并分 bin；SLT：系统级，模拟真实应用抓漏掉的问题。成本依次递增。

</details>

**15. Scan Chain 是什么？为什么能测到内部逻辑？**
<details><summary>答案</summary>

把内部触发器串成移位寄存器，用 Scan-In 移入激励、Scan-Out 移出响应，把不可见的内部节点搬到可观察端口，从而检测固定型故障。

</details>

**16. BIST 和 Boundary Scan 各解决什么问题？**
<details><summary>答案</summary>

BIST 片内自测（LFSR + MISR），减少 ATE 资源占用，常用于存储器和逻辑；Boundary Scan（JTAG）在 IO 上串扫描链，用于板级互连测试和内部寄存器访问，不需要探针。

</details>

**17. Shmoo 图是什么？怎么看？**
<details><summary>答案</summary>

两个参数二维扫描得到的 Pass/Fail 图。边界随电压升高而外扩说明受速度限制；某区域成片失效说明功能、时序或电源问题。

</details>

**18. Cpk 是什么？Cpk = 1.0 意味着什么？**
<details><summary>答案</summary>

工序能力指数，衡量分布中心与规格限的关系。Cpk=1 表示 3σ 刚好落在规格内，约 0.27% 超规格风险，一般要求 ≥1.33。

</details>

## 四、编程与项目

**19. 用 Python 处理测试数据怎么做？**
<details><summary>答案</summary>

读入 → 清洗（单位、空值、重复）→ 统计（良率、分布、Cpk）→ 可视化（直方图、Shmoo 热力图）→ 出报告。强调可复现与自动化。

</details>

**20. 讲一个你做的项目，最大的问题是什么？**
<details><summary>答案</summary>

按背景 → 任务 → 行动 → 结果讲，准备一个“失败—定位—解决”的过程。

</details>
