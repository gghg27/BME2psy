# 03 心理学统计题库答案

> 先独立作答，再核对。方法名只是起点；得分点是变量类型、依赖结构、核心效应和假设。

## A. 方法选择

1. Welch independent t-test；DV 连续、两独立组。报均值差、CI、d。
2. Paired t-test；以个体内差值为分析对象。若多个时点/缺失则 LMM。
3. One-way ANOVA；三独立组。若方差不齐用 Welch ANOVA。
4. Repeated-measures ANOVA；四组内条件，检查球形性；有缺失或 trial 数据优先 LMM。
5. Mixed ANOVA/LMM；关键是 group×time。不能用“患者显著、对照不显著”替代交互。
6. Two-way ANOVA；检验性别、情绪及交互。性别是测量组别，因果措辞受限。
7. Mixed ANOVA/LMM；group 组间、load 组内，核心通常为 group×load。
8. Pearson correlation/linear regression；先查散点、线性与影响点，报告 r/CI。
9. Spearman；适合等级且关注单调关系。仍需查异常和关系形态。
10. Partial correlation 或回归；报告控制年龄后的条件关联，但不称消除全部混淆。
11. Multiple linear regression；预先定义变量、查共线与残差，以交叉验证评估预测。
12. Logistic regression；报 OR/CI、校准、辨别；事件数必须足够。
13. Trial-level LMM；trial 嵌套于被试，至少被试随机效应，按设计考虑随机斜率。
14. Crossed random-effects LMM；被试和图片均为随机因素，避免 stimulus-as-fixed-effect fallacy。
15. LMM；用所有可用时点并说明 missing-at-random 假设，敏感性分析缺失机制。
16. Mann-Whitney U 或有序 logistic；取决于问题是分布位置还是等级概率。
17. ICC；先决定 absolute agreement/consistency 和 single/average，再报告对应类型。
18. Alpha 可作起点，并查 omega、项目结构；不能据此断言单维或有效。
19. CFA；检验预设三因子结构，报告多个拟合指标并防止只靠 modification indices 追拟合。
20. 回归/ANOVA 中的 emotion×anxiety；连续焦虑保留连续，中心化便于解释但不改变交互检验。

## B. 结果解释

1. 中等标准化差异，CI 排除 0 且 p=.02；真实效应可能从很小到较大，需结合实际重要性。
2. 数据与零效应相容，也与中等正效应相容；证据不精确，不能说“无效”。
3. 一个因素的效应取决于另一个因素；查看计划简单效应。主效应平均后不显著不矛盾。
4. 平均而言因素有效，且没有足够证据说明其随另一因素变化；不是证明交互绝对为零。
5. 样本中中等正线性关联，约 16% 方差共享；不说明因果，需查 CI、离群和非线性。
6. odds 加倍，不是概率加倍；基线风险不同会产生不同绝对概率变化。
7. 在该发现集合及程序假设下控制 FDR，q=.04；仍需报告效应量与预设 family。
8. 内部一致性很高，可能也提示项目冗余；不证明单维、重测可靠或效度。
9. 可靠性水平需结合 ICC 类型、CI 与用途；群体研究尚可不等于个体决策足够。
10. 内部数据辨别好但外部明显下降，提示过拟合、分布偏移或泄漏；不能宣称可泛化。

## C. 错误诊断

1. 错在未直接检验交互；应比较两个效应之差及其 CI。
2. 伪重复；独立信息单位主要是被试，trial 用层级模型而非膨胀自由度。
3. 分析者自由度；应预定规则，并做含/不含影响点的敏感性分析。
4. 选择性报告与多重比较；定义 family、校正并公开全部结果。
5. 相关不排除反向因果和共同原因；需随机操纵、纵向/自然实验及更强假设。
6. alpha 只涉及一致性且依赖假设；应另证结构、收敛、区分和效标效度。
7. 处理后变量可能是中介或 collider；控制会改变目标效应并引入偏差。
8. 数据泄漏；预处理、特征选择和调参必须在训练折内，最终只评一次独立测试集。
9. 非显著不等价于相同；需等价检验/贝叶斯证据和预定最小重要差异。
10. I 类错误膨胀；使用 Greenhouse-Geisser/Huynh-Feldt 或 LMM，并报告校正自由度。
