# bank-Predict
<!-- 对数据集进行初步分析、可视化和特征选择 -->

导入必要的包，并读取数据
这一步需要注意的是缺失值在这个数据集中被标注为['?']，且第一行非表头

统计并处理缺失值
由于缺失值占比不高，故直接删去

可视化目标变量（A16）的分布情况
可以看出样本分布较为平均，为后面选用目标特征refit作为参考。

将离散特征转换为数值表示，方便机器学习算法处理

对数据集中的连续特征进行归一化处理
这里使用的是最小-最大归一化方法，将连续特征的值线性映射到[0, 1]的范围内。

使用方差阈值进行特征选择

对筛选后的特征进行可视化，以便更好地理解每个特征的分布情况
其中可以看出大部分二值离散特征和连续特征分布都较为均衡，而三值特征则存在某一取值数量明显少于其余二者。

探索筛选后的特征之间的相关性，绘制热力图
从中可以看出A4,A5之间存在明显强相关，A9,A16之间存在明显负相关，但因为数据已被脱敏，无法做出更深层次分析。

<!-- 选取合适的机器学习方法完成预测任务 -->

提取特征列；拆分数据集并保存

对不同的分类模型进行训练和测试
d.使用五种分类模型：决策树（DecisionTree），K近邻（KNN），随机森林（RandomForest），逻辑回归（LogisticRegression）和支持向量机（SVM）对数据集进行训练；
e.评价指标包括准确率（accuracy）、精确率（precision）、召回率（recll）和F1-score；
f.使用交叉验证的方法进行评估。具体来说，使用K-fold交叉验证方法，将数据集分成5份，每次使用其中4份作为训练集，1份作为测试集，并将这个过程重复5次，最终得到每个模型在不同评价指标上的平均得分；

<!-- 对实验结果进行比较评估
对结果进行评估
优化实验结果 -->

对各项指标进行可视化处理，这里用的是 Pyecharts 库来绘制雷达图
从中可以看出，
e.逻辑回归模型和KNN在所有评估指标中表现不佳，其F1分数、精确度和召回率都相对较低，训练也非常慢；
f.随机森林模型在所有指标中表现最好。它的F1分数、正确度和召回率都很高，精确度分数也很高。随机森林模型通常表现出色，因为它可以处理复杂的数据集，并且能够捕捉非线性关系。
g.SVM模型的训练和测试速度都非常快，在正确率表现上略逊于随机森林模型，它的精确度都相对较高，但召回率F1分数过低，；
h.决策树模型的表现不如随机森林模型和SVM模型，但它的正确度和召回率都比逻辑回归模型要好；

综上，对于该数据集发挥较好的模型确定为随机森林模型和SVM模型，下面对这两个模型做出进一步优化。

对随机森林模型进行调参优化；参数的范围分别是n_estimators（决策树的数量）、max_depth（决策树的最大深度）、min_samples_split（内部节点再划分所需最小样本数）、min_samples_leaf（叶子节点最少样本数）

对支持向量机模型进行调参优化；参数的范围分别是

可以看出与上面相比在accuracy指标上二者都有略微提升，但不是很明显。
