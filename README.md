# ability_user
# 开发者价值评估模型

## 一、问题描述

GitHub是一个面向开源及私有软件项目的托管平台，作为开源代码库，GitHub拥有超过900万开发者用户，随着越来越多的应用程序转移到了云上，GitHub已经成为了管理软件开发以及发现已有代码的首选方式。

开发者价值评估模型是一个十分有意义的指标，它能够直观地表现一个开发者的能力水平，并从多个维度来对开发者的价值进行分析与描述，从而能够更为全面的去表现开发者的价值。猎头也能通过对开发者的价值评估进而选择他们需要的开发者。

在一个开源社区中有众多的开发者，如何才能对一个开发者的价值进行评估？有哪些影响因素能够反映出开发者的项目管理能力？

## 二、设计目标

在GitHub中对一个开发者进行价值评估，不仅能展现自身的整体价值还能让他从多个维度了解自己的能力，能够让他有针对的去提升自己的能力，也能在招聘时让招聘公司更直观了解一个人的价值。

## 三、设计思路

开发者价值评估模型由五个小的指标组成，包括项目管理能力、编程能力、学习能力、团队协作能力、敬业度。

第一，项目管理能力能够展现出开发者对自己项目的管理能力和维护能力。GitHub中的开发者是巨多的，而其中的项目也是居多的，其中就有众多开发者来对这些项目进行维护，并且也有很多开发者创建了项目或者是参与了其他项目，做出了贡献。项目管理能力就能够体现出开发者对项目和团队的管理能力，还有和团队中成员的交流能力，也能体现所管理项目的一个活跃度。

第二，编程能力是刻画一个开发者价值必不可少的一部分。开发者在GitHub中自身会创建项目，也会参与到其他的项目中，自身也会有很多的follower。自身创建项目的数量，以及参与其他项目提交的pr数量以及被合并的pr的数量，这些都能去刻画编程能力，从而也能去表现开发者的价值。

第三，学习能力能够表现一个开发者是否能够主动去学习和掌握更多的知识。学习能力主要是由开发者掌握的编程语言数量来进行评估，开发者掌握的编程语言的数量越多，那么开发者的学习能力也就越强。

第四，团队协作能力能够反映出开发者和其他开发者协作完成任务的能力，通过有过协作的开发者的数量和其他开发者合作的紧密程度的均值能偶来刻画开发者的团队协作能力。

第五，敬业度能够反映开发者在GitHub中的一个活跃情况。如果一个开发者经常在GitHub中创建项目，发表issue或者是做出了其他的一些贡献，那么他在GitHub这个平台中肯定是比较敬业的，所以从活跃的天数和做出的工作量能够反映一名开发者的敬业度。

通过这五个影响因素进行分析，每个影响因素都能得到一个分数，每个影响因素的分数就刻画了开发者在该影响因素的能力高低。最后对这五个因素进行加权求和得到总分，即为开发者的价值评估的分数。分数越高，开发者的价值就越高。

## 四、评估指标模型

### 1、指标计算模型的设计

开发者价值评估模型由五个部分组成：项目管理能力、编程能力、学习能力、团队协作能力、敬业度。从这五个维度来整体刻画开发者价值评估模型。

![image-20230505155620028](https://github.com/1161295395/opengame/raw/img/image-20230505155620028.png?raw=true)

开发者价值评估模型的公式是一个分数计算，用一个具体的分数来刻画开发者的价值。开发者价值评估的总分数是由五个指标分数加权求和构成。
$$
S=X1×S_{编程能力} + X2×S_{项目管理能力}+X3×S_{项目管理能力}+X4×S_{团队协作能力}+X5×S_{敬业度}
$$
其中X1表示该影响因素的权重因子，S~编程能力~表示该影响因素的得分，例如某个开发者在编程能力这项指标的得分是多少。五个指标的得分能刻画开发者在五个维度上的能力，最后综合加权求和得到开发者总的得分，来对开发者价值进行评估。

S表示的就是开发者价值评估的总得分，由五个指标的加权求和得到。每个一级指标的满分是100分，通过加权求和之后就能得到总分S，这样得到的总分S的满分也是100分。

### 2、影响因素权重的设计

CRITIC权重法是一种客观赋权法。其思想在于用两项指标，分别是对比强度和冲突性指标。对比强度使用标准差进行表示，如果数据标准差越大说明波动越大，权重会越高；冲突性使用相关系数进行表示，如果指标之间的相关系数值越大，说明冲突性越小，那么其权重也就越低。对于多指标多对象的综合评价问题，CRITIC 法去消除一些相关性较强的指标的影响，减少指标之间信息上的重叠，更有利于得到可信的评价结果。

开发者价值评估模型中，有五个影响因素，我们取了三十万开发者的数据进行分析，用CRITIC权重法进行分析，得出各个影响因素的权重，进而完善开发者价值模型的评估公式。其中部分数据如下图所示：

![指标分数](https://github.com/1161295395/opengame/raw/img/%E6%8C%87%E6%A0%87%E5%88%86%E6%95%B0.png?raw=true)

利用SPSS软件平台来进行分析。我们随机选择三十万开发者中的五万个开发者来进行分析，以保证分析的合理性。进行数据分析后输出了一个表格，其中包括指标变异性，指标冲突性，信息量以及最后得到的权重，如下图所示：

![冲突性](https://github.com/1161295395/opengame/raw/img/%E5%86%B2%E7%AA%81%E6%80%A7.png?raw=true)



从上表可知，在指标变异性上，团队协作能力的指标变异性的值会小一些，意味着波动比较小，因此对应权重值也会小一些。指标冲突性来看，这五个因素没有明显区别，对权重影响不大。

因此得到权重如下图所示：

![CRITIC权重](https://github.com/1161295395/opengame/raw/img/CRITIC%E6%9D%83%E9%87%8D.png?raw=true)

## 五、数据来源及处理

从GitHub API中得到2020年全年的开发者的全域活动数据，并储存到clickhouse进行处理和筛选。根据五个影响因素我们选择需要的字段来进行计算。

例如项目管理能力中，其影响因素还有开发者管理项目的数量、更新项目版本的数量、合并项目里pull requests的数量和管理项目中亲自回复issue的数量。例如合并项目里pull requests的数量，我们就通过pull_merged_by_login这个字段，加上对应的id，分组进行求和即可。每一个二级因素都会进行分段打分，最后也会加权求和得到一个总分。这里的满分都是100分。

对于这些二级指标的分数，我们会通过spss工具进行分析和统计，最后确定指标的计算方式。

##  六、开发者价值评估得分与合理性分析

通过评估指标模型的计算公式，我们得到了每个开发者的价值评估得分。下图为部分开发者的价值评估得分：

![最终得分](https://github.com/1161295395/opengame/raw/img/%E6%9C%80%E7%BB%88%E5%BE%97%E5%88%86.png?raw=true)



上表中，第一列为开发者的用户名，第二到第六列依次是开发者五个能力的得分，最后一列是开发者的总分。排名第一的开发者，他的项目管理能力和敬业度都是满分，这能代表他是很活跃的。他的学习能力和编程能力也是90分以上，只是团队协作能力的分数会低一些，通过观察也能发现，总分排名靠前的开发者的团队协作能力都不是很高，而团队协作能力的影响因素是：与开发者有过协作的开发者的数量和与协作者之间紧密程度的平均值。我们去查看了排名第一的开发者的GitHub主页，发现确实是这样，掌握的编程语言的数量有十项，且几乎每天都是活跃的，但是通过查看开发者协作网络图，发现他协作的开发者只有三个，这也解释了为什么团队协作能力的分值不是很高的原因。

分数在70以上的开发者接近1000个，而分数在40到70之间的开发者有3万个，更多的开发者是40分以下，这也很合理，因为各个方面都优秀的开发者确实是很少的，更多的开发者是集中在一个中间的水平。

## 七、可视化



用雷达图来展示开发者在五个方面的能力

![雷达图](https://github.com/1161295395/opengame/raw/img/%E9%9B%B7%E8%BE%BE%E5%9B%BE.png?raw=true)



## 合作者

田明炎

周志峰








