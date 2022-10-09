## 模型评估与选择

### 模型评估方法

书后习题

<img src="/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220930231043281.png" alt="image-20220930231043281" style="zoom:50%;" />

### 经验误差和泛化误差

#### 定义

![image-20220930140833923](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220930140833923.png)

![image-20220930141041690](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220930141041690.png)

#### 解决过拟合现象：正则化

![image-20220930141142762](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220930141142762.png)

### 性能度量

#### 基本概念

![image-20220930163038120](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220930163038120.png)

#### P-R曲线和ROC曲线

<p align="center"><img alt="image-20220927211547461" height=""src="https://raw.githubusercontent.com/Lunaticsky-tql/my_picbed/main/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0-%E6%A8%A1%E5%9E%8B%E8%AF%84%E4%BC%B0%E4%B8%8E%E9%80%89%E6%8B%A9/20220930234211807031_249_norm.gif" width=""/></p>


$$
E(f ; D)=\operatorname{bias}^2(\boldsymbol{x})+\operatorname{var}(\boldsymbol{x})+\varepsilon^2,
$$
也就是说, 泛化误差可分解为偏差、方差与噪声之和。

这个式子中的$\boldsymbol{x}$其实并不与”特定的“测试样本相关联。

注意这个式子的推导，详见南瓜书。

- **「偏差」**度量了学习算法的期望预测与真实结果的偏离程度，即**「刻画了学习算法本身的拟合能力」**；
- **「方差」**度量了同样大小的训练集的变动所导致的学习性能的变化，即**「刻画了数据扰动所造成的影响」**;
- **「噪声」**则表达了在当前任务上任何学习算法所能达到的期望泛化误差的下界，即**「刻画了学习问题本身的难度」**.

偏差一方差分解说明，泛化性能是由**「学习算法的能力」**、**「数据的充分性」**以及**「学习任务本身的难度所共同决定」**的。

<img src="/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220930230353084.png" alt="image-20220930230353084" style="zoom:50%;" />

随训练强度，偏差减小，方差增大，即学习的越充分，但受数据影响越大，可能出现过拟合现象。
