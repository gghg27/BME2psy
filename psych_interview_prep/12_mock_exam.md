# 12 综合模拟笔试（5 套，仅题目）

> 每套 150 分钟、100 分。材料均为基于常见研究结构重新编写的训练文本，不是论文原文，也不应当作真实研究引用。答案见独立文件 [12_mock_exam_answers.md](12_mock_exam_answers.md)。建议完整闭卷作答，不边做边查。

## 模拟卷一：注意、疼痛与因果边界

### Part 1 中文文献评述（30 分钟，20 分）

【材料】某研究招募 24 名大学生。被试先完成负性图片观看，再接受热刺激；另一批 24 名大学生先看中性图片，再接受热刺激。负性组平均疼痛评分更高（p=.04）。研究者又在 64 个脑区逐一计算负性情绪评分与 BOLD 的相关，发现 3 个脑区未经校正 p<.05，于是结论称“负性情绪通过岛叶激活导致疼痛敏感，且该脑区是客观疼痛生物标志物”。两组测试分别在上午和晚上完成，刺激温度由实验者“根据被试表现灵活调整”。

【问题】从研究问题、分组、操纵、测量、混淆、统计、结论和复现角度评述；给出最关键的三项改进。（20 分）

### Part 2 研究设计（35 分钟，25 分）

设计一个实验，检验工作记忆负荷是否调节疼痛强度辨别。必须区分 sensitivity 与 response bias，包含行为主终点，并说明是否加入 EEG 以及它能多回答什么。（25 分）

### Part 3 心理统计（25 分钟，20 分）

1. 40 名被试均完成低/高负荷×低/高疼痛强度。主终点为 trial-level 二分类“高强度”判断。选模型并写核心检验。（8 分）
2. 论文写道：“低焦虑组 p=.01，高焦虑组 p=.20，因此负荷效应只存在于低焦虑组。”指出错误并给正确检验。（6 分）
3. 解释 `interaction OR=0.72, 95% CI [0.55,0.94], p=.016`，并说明 OR 不能怎样解读。（6 分）

### Part 4 英文分析与翻译（35 分钟，20 分）

【Synthetic abstract】*Pain reports reflect both sensory evidence and decision criteria. We manipulated working-memory load while participants discriminated two individually calibrated heat intensities. High load reduced discrimination accuracy but did not shift the response criterion. Trial-level neural variability predicted between-person differences in sensitivity beyond mean evoked amplitude. Because the study used a single laboratory task and no external sample, the neural result should be considered preliminary.*

1. 将全文译为中文。（8 分）
2. 用一句英文概括 research question。（3 分）
3. 写出 IV、主要 DV 和一项可能的统计模型。（4 分）
4. 为什么最后一句重要？给一个 follow-up。（5 分）

### Part 5 综合科研能力（25 分钟，15 分）

有人说：“EEG 能直接测到疼痛，所以以后可以代替主观评分。”请用不超过 300 字回应，并提出验证“替代终点”的证据链。（15 分）

## 模拟卷二：工作记忆、儿童 ERP 与测量效度

### Part 1 中文文献评述（30 分钟，20 分）

【材料】研究者比较 18 名 8 岁儿童和 22 名 12 岁儿童的 2-back ERP。年幼组正确 trial 更少，因此研究者保留其全部 trial，却从年长组随机删除一半 trial。结果显示年幼组 P3 振幅较小，且正确率较低。研究据此认为“P3 是工作记忆容量的直接指标，儿童随年龄增长必然因 P3 增大而能力提高”。两组使用不同显示器，未记录头动和睡眠，也未报告效应量。

【问题】识别至少八个问题；重点讨论 ERP 可比性、发展推断、构念效度和可接受的结论。（20 分）

### Part 2 研究设计（35 分钟，25 分）

设计一项研究，检验一晚睡眠限制是否影响儿童/青少年的工作记忆更新。说明为什么直接让未成年人严重缺觉可能不合适，并给出更可行的伦理方案。（25 分）

### Part 3 心理统计（25 分钟，20 分）

1. 两个年龄组均完成 0/1/2-back，每个刺激项目在多人中重复。选择模型并说明随机效应。（8 分）
2. 解释 `age group × load: F(2,72)=5.40, Greenhouse-Geisser corrected p=.009, partial η²=.13`。（6 分）
3. P3 与正确率 r=.35，但控制年龄后 partial r=.08。可以得出什么？（6 分）

### Part 4 英文分析与翻译（35 分钟，20 分）

【Synthetic abstract】*Developmental differences in event-related potentials can arise from changes in cognition, anatomy, data quality, or task strategy. We therefore matched younger and older participants on performance using an adaptive n-back task and estimated component reliability across trials. The age difference in P3 amplitude became smaller after accounting for reliability, whereas latency differences remained. These findings constrain, but do not uniquely identify, developmental mechanisms.*

1. 翻译全文。（8 分）
2. 为什么要 adaptive matching 与 reliability estimation？（4 分）
3. 结果是否证明年龄导致 P3 潜伏期变化？（4 分）
4. 设计一个纵向 follow-up。（4 分）

### Part 5 综合科研能力（25 分钟，15 分）

请解释：“任务表现相同”为什么既可能帮助控制混淆，也可能引入选择/解释问题。结合儿童 n-back 作答。（15 分）

## 模拟卷三：焦虑、动态网络与预测

### Part 1 中文文献评述（30 分钟，20 分）

【材料】研究从一个数据集中提取 5,000 个动态连接特征。研究者先用全部 120 人筛选与焦虑显著相关的 200 个特征，再随机做五折交叉验证，得到 r=.62。样本包含两个站点，站点 A 多为高焦虑、站点 B 多为低焦虑，但拆分时未按站点分层。研究者将相关网络命名为“焦虑状态网络”，并称模型可用于临床筛查；未报告校准、外部样本或与年龄/站点基线模型的比较。

【问题】评述数据泄漏、站点混淆、状态命名、验证与临床结论，并重构一条可信的分析流程。（20 分）

### Part 2 研究设计（35 分钟，25 分）

设计一项 EEG-HMM 研究，检验负性干扰条件是否改变焦虑相关的动态脑状态。要求使用连续焦虑指标、外部行为锚点和状态稳定性检验。（25 分）

### Part 3 心理统计（25 分钟，20 分）

1. 每名被试有多个状态驻留时间，且部分状态未出现。你会怎样定义主终点和模型？（7 分）
2. 内部 CV r=.55，独立站点 r=.12、CI 跨 0。如何解释？（7 分）
3. 做 5,000 个检验后有 180 个 p<.05，但 FDR 后 0 个显著。能否报告“发现 180 个候选连接”？为什么？（6 分）

### Part 4 英文分析与翻译（35 分钟，20 分）

【Synthetic abstract】*Dynamic states are statistical summaries of recurring signal patterns rather than direct observations of mental states. In a discovery sample, we identified four reproducible EEG states and preregistered tests of their occupancy during emotional distraction. Only one state showed the predicted condition-by-anxiety interaction in an independent sample. The effect was robust to ocular artifacts but not to alternative reference schemes, limiting its interpretation.*

1. 翻译全文。（8 分）
2. 哪些做法降低了事后解释风险？（4 分）
3. “robust to A but not B”应如何解读？（4 分）
4. 给出下一步最关键分析。（4 分）

### Part 5 综合科研能力（25 分钟，15 分）

用“可靠性—心理锚定—排除伪迹—泛化”四层说明 HMM 状态如何获得有限的心理学意义。（15 分）

## 模拟卷四：多模态、精神疾病与跨尺度推断

### Part 1 中文文献评述（30 分钟，20 分）

【材料】某研究将 60 名抑郁患者和 60 名对照的结构 MRI、静息 fMRI、EEG 与公开成人脑转录组直接拼接，训练深度网络后在同一数据的随机十折中达到 94% 准确率。患者全部来自医院，对照来自大学；患者平均大 12 岁且头动更高。作者未与单模态或人口学模型比较，称“发现了由某基因导致的抑郁神经环路”。公开转录组来自另一批少数供体。

【问题】从抽样、混淆、融合、验证、空间统计和因果层级评述，并提出最小可行的重做方案。（20 分）

### Part 2 研究设计（35 分钟，25 分）

设计一个 MRI+EEG 研究，检验工作记忆负荷相关脑活动能否解释抑郁症状维度。说明同步/非同步采集的取舍、融合层级和单模态基线。（25 分）

### Part 3 心理统计（25 分钟，20 分）

1. 何时用 early、intermediate、late fusion？分别给一项风险。（8 分）
2. 影像脑图与基因表达脑图相关 r=.42、普通 permutation p<.001；还缺什么关键检验？（6 分）
3. AUC=.90 但校准斜率=.45，意味着什么？（6 分）

### Part 4 英文分析与翻译（35 分钟，20 分）

【Synthetic abstract】*Multimodal models are useful only when modalities provide complementary and generalizable information. We compared structural MRI, functional MRI, electrophysiology, and their late-fusion ensemble using leave-site-out validation. Fusion improved discrimination but not calibration, and its advantage disappeared when age and motion were carefully matched. Spatial correspondence with a normative transcriptomic atlas generated a molecular hypothesis; it did not establish a molecular cause.*

1. 翻译全文。（8 分）
2. 结果最可能提示原增量来自什么？（4 分）
3. 为什么 leave-site-out 比随机折更有信息？（4 分）
4. 最后一句体现何种推断边界？（4 分）

### Part 5 综合科研能力（25 分钟，15 分）

请用一个简洁流程回答“为什么做多模态、怎样证明值得做、怎样避免把跨尺度相关写成机制”。（15 分）

## 模拟卷五：开放科学、复现与导师综合方向

### Part 1 中文文献评述（30 分钟，20 分）

【材料】实验室预注册“负性情绪提高疼痛评分”，但主检验 p=.11。研究者随后尝试三种剔除标准、四个时间窗、五个 EEG 频段和两种参考，发现其中一种组合的 gamma 功率 p=.03，于是只报告该组合，并在摘要写“预注册研究证明 gamma 是疼痛的特异机制”。数据和代码以“隐私”为由不提供，且未说明停止收样规则。

【问题】评述其预注册执行、研究者自由度、多重比较、选择性报告、特异性和开放科学；写出透明报告这项研究的方式。（20 分）

### Part 2 研究设计（35 分钟，25 分）

从以下二选一作答：A. 设计一项跨刺激、跨中心验证疼痛 neural variability 指标的研究；B. 设计一项纵向多模态研究，检验青少年脑发育偏离是否预测焦虑/抑郁症状变化。明确 confirmatory 与 exploratory 部分。（25 分）

### Part 3 心理统计（25 分钟，20 分）

1. `d=.18, 95% CI [.04,.32], p=.012` 是否有实际意义？还需什么信息？（6 分）
2. 为什么 observed power 不宜用来“证明”本研究功效足够？（5 分）
3. 何时选 Bonferroni，何时选 FDR？先定义什么？（5 分）
4. alpha=.94 能否证明量表单维且有效？（4 分）

### Part 4 英文分析与翻译（35 分钟，20 分）

【Synthetic abstract】*The confirmatory analysis did not provide clear evidence for the preregistered effect. Exploratory analyses suggested that neural variability might relate to pain discrimination under one stimulation protocol, but the estimate was imprecise and did not replicate at a second site. Transparent separation of confirmatory and exploratory results prevents a promising hypothesis from being mistaken for an established finding.*

1. 翻译全文。（8 分）
2. `did not provide clear evidence` 为什么比 `proved no effect` 准确？（4 分）
3. 这项结果下一步最合理做什么？（4 分）
4. 用英文写一句不过度的结论。（4 分）

### Part 5 综合科研能力（25 分钟，15 分）

你有工程与 EEG/动态网络背景。请写一段不超过 400 字的研究计划口头提纲，说明如何在胡理疼痛方向或刘冰多模态方向提出一个可证伪、可验证、不过度依赖复杂算法的问题。（15 分）
