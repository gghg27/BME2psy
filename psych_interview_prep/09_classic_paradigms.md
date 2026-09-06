# 09 经典实验范式速查

> 本文件是范式的唯一主卡片。具体研究先选心理过程，再选范式；不要从“我会 n-back/EEG”倒推研究问题。

| 范式 | 研究什么/怎么做 | IV | DV/行为指标 | EEG 可看 | fMRI 可看 | 常见局限 |
|---|---|---|---|---|---|---|
| Stroop | 词义与字体颜色冲突，按颜色反应；冲突控制 | congruency | RT、正确率、冲突效应 | N2、P3、theta；需避免成分反推 | ACC/PFC 相关活动与网络 | 冲突效应混合阅读熟练度、速度-准确权衡 |
| Flanker | 中央靶被一致/冲突侧翼包围 | congruency、间距 | RT、错误率 | N2、ERN、theta | 冲突监测与控制网络 | 视觉拥挤与反应冲突难完全分离 |
| Posner cueing | 线索提示位置，靶出现在有效/无效位置 | cue validity、SOA | cueing cost/benefit | P1/N1、偏侧化 alpha | dorsal/ventral attention network | 外源/内源注意依赖 SOA；眼动混淆 |
| visual search | 从干扰物中寻找靶 | set size、特征/结合搜索 | 搜索斜率、RT、正确率 | N2pc、alpha | 视觉与顶叶注意区域 | 难度、眼动、目标显著性共变 |
| attentional blink | RSVP 中识别 T1/T2，短间隔 T2 受损 | lag、T1正确性 | T2|T1 正确率 | P3 与时间注意 | 前顶叶控制 | 工作记忆、掩蔽和报告要求共同影响 |
| Oddball | 频繁标准刺激中偶发靶/新异刺激 | 概率、任务相关性 | 命中率、RT | MMN、P3a/P3b | salience/attention systems | 稀有性、新异性、任务相关性难分离 |
| Go/No-Go | 多数 Go 反应，少数 No-Go 抑制 | trial type、比例 | commission error、RT | N2、P3、ERN | 右额下回/前额控制网络 | No-Go 稀有性和注意捕获混入抑制 |
| Stop-signal | Go 后偶发停止信号，动态调整 SSD | stop/go、SSD | SSRT、Go RT | stop-N2/P3、beta | 抑制网络 | 独立赛马假设；策略性变慢 |
| Task switching | 交替规则执行同一刺激 | switch/repeat、准备间隔 | switch cost | cue-P3、CNV、theta | frontoparietal control | 任务难度、线索变化和规则切换混合 |
| n-back | 判断当前刺激是否匹配 n 项前 | load、match | d'、RT、正确率 | theta/alpha、P3 | frontoparietal network | 同时涉及更新、保持、匹配；不是纯容量 |
| Sternberg | 记忆集合后判断探测项是否在集合 | set size、probe type | RT 斜率、正确率 | delay activity、P3 | 工作记忆网络 | 线性斜率不自动证明串行搜索 |
| delayed match-to-sample | 编码—延迟—匹配判断 | delay、load、match | 正确率、RT | 延迟期活动 | PFC/hippocampal systems | 编码、保持、提取阶段需分开建模 |
| dot probe | 情绪/中性刺激后探针替代其一 | congruency、情绪类型 | bias score、RT | 早期 ERP、LPP | amygdala-attention coupling | 差值信度低；单次 RT 噪声大 |
| emotion picture/video | 呈现标准化或自然情绪材料 | valence、arousal、调节策略 | valence/arousal 评分、生理反应 | LPP、alpha | amygdala/PFC/insula | 效价与唤醒共变；文化差异、需求特征 |
| fear conditioning | CS+ 与厌恶 US 配对，CS- 不配对 | CS type、阶段 | SCR、期待评分、恐惧评分 | ERP/振荡 | amygdala/insula/vmPFC | awareness、泛化和安全学习混杂；伦理限制 |
| reward task/MID | 线索提示潜在收益/损失，再快速反应 | valence、magnitude、outcome | RT、命中、愉悦评分 | reward positivity、P3 | striatum/vmPFC | 期待、动作准备与结果评价需分离 |
| resting state | 无明确任务，记录自发信号 | 组别/状态、扫描条件 | 连接、ALFF、网络指标 | 频谱/连接/微状态 | FC、network topology | 头动、警觉、全局信号；连接不是因果 |
| thermal pain | 控温刺激诱发可重复痛感 | temperature、expectancy、attention | 强度/不愉快评分、阈限 | 接触热 ERP 较慢 | pain-related distributed patterns | 强度与显著性共变；适应/敏化 |
| laser pain | 激光选择性激活伤害感受通路 | energy、attention、expectancy | 评分、反应时 | N1、N2-P2、gamma | thalamocortical/pain-related patterns | 皮肤安全、习惯化；LEP 非疼痛专属 |
| placebo/nocebo | 通过指令/条件化改变治疗期待 | expectation、treatment | 疼痛评分、期待、差值 | LEP、alpha/gamma | PFC-PAG 等调节相关系统 | 需求特征、回归均值、盲法失败 |

## 如何把范式写进研究设计

不要写：“采用 n-back 并采 EEG。”应写：“用 n-back 操纵工作记忆更新负荷（1/2/3-back），主终点为 d'，同时检验额中 theta 是否随负荷呈剂量关系；由于 n-back 还包含匹配和反应选择，结论限定为任务负荷相关控制过程。”

## 范式选择五问

1. 目标构念能否由该范式特异地改变？
2. 操纵还同步改变了难度、唤醒、稀有性或运动反应吗？
3. 主 DV 是准确率、RT、d'、评分，还是模型参数？
4. 是否需要 trial-level 模型、反平衡和操纵检验？
5. 神经指标提供的是时间、位置、表征还是预测证据？

## 面试高频问题

- Go/No-Go 和 Stop-signal 对“抑制”的操作化有何不同？
- 为什么 n-back 不能被直接称为工作记忆容量测验？
- dot-probe 的 bias score 为什么常不可靠？
- 静息态功能连接升高能说明信息传递增强吗？
- placebo 设计如何区分期待效应与报告偏差？
