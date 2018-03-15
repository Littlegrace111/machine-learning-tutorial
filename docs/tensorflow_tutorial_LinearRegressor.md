TensorFlow新司机开车指南一: 基于单特征的线性回归模型预测
===

前言
---
机器学习很热门，我很好奇到底怎么玩。
研究生时期，学过python语言，入门tensorflow无缝对接。

TensorFlow安装与环境配置
---
tensorflow google官方网站上已经详细介绍了各种平台的安装流程，不赘述。

我的需求：
使用IPython notebook和JuPyter做所见即所得的数据分析，可以看到直观的dataFrame和直方图，散点图等；
同时，需要在IPython中import tensorflow模块。

所以我的安装步骤比较复杂：macOS自带python2.7.x版本，要管理多版本的python，最好安装pyenv；

1. 安装pyenv,管理多个版本的python，安装anaconda；
2. 安装tensorflow,根据官网的步骤，选择Installing tensorflow with anaconda;
3. activate tensorflow;
4. 在tensorflow环境下，安装IPython和jupyter；
5. 打开Jupyter，测试`import tensorflow as tf`，没有报错，就说明tensorflow成功引入；

以上繁琐的安装步骤前后的各种坑搞了我整整两个晚上，加之pandas，sciki-learn, matplotlib这些统计和图形必备的库也需要安装，导致一写代码就发现各种库 `can't not find in module`，大大打击了我的学习热情。

之后，在一起偶然的google中，发现了docker这种技术，可以理解成轻量级虚拟机VM这种东西，可以使得工程人员解脱出繁琐地安装各种库的痛苦中，通过打包image，把所需要的环境一并打包。

目前我需要的就是敏捷，迅速地学习tensorflow的各种api功能和训练模型，至于怎么部署tensorflow环境，不是我目前的重点。docker很好地解决了环境部署的各种复杂问题。

通过docker安装google cloud data学习环境：
---
```
docker run -it -p "127.0.0.1:8081:8080" -v "${HOME}:/content" \
    gcr.io/cloud-datalab/datalab:local-20170224
```
通过以上命令就可以打包安装tensorflow学习环境所需的各种库，包括pandas，scikit-learn, matplotlib等用来画散点图的库；
 
理解线性回归模型所需要的部分数学知识：
---
本人在开始学习tensorflow之前，曾经痛苦地看了几个晚上，《深度学习》前三章的数学基础知识，由MIT的Ian Goodfellow撰写的那本。当然，基本没怎么看懂，大学四年学的高等数学和线性代数，统计学在拿到毕业证那一刻全部还给老师了。

了解线性回归模型，首先需要回顾几个词：
1. 标签 label，可以理解成预测目的和预测结果，predict函数的中，y轴的数据；
2. 特征 feature，预测模型中的输入变量，即x变量；
