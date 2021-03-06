---
youku_id: XMjUyMzI1NzgwMA
youtube_id: b7PO_xfEMwE
title: 什么是 DQN
description: "今天我们会来说说强化学习中的一种强大武器, Deep Q Network 简称为 DQN. Google Deep mind 团队就是靠着这 DQN 使计算机玩电动玩得比我们还厉害.
之前我们所谈论到的强化学习方法都是比较传统的方式,
而如今, 随着机器学习在日常生活中的各种应用, 各种机器学习方法也在融汇,
合并, 升级. 而我们今天所要探讨的强化学习则是这么一种融合了神经网络和
Q learning 的方法, 名字叫做 Deep Q Network."
chapter: 4
thumbnail: /static/thumbnail/ML-intro/DQN_thumbnail.png
post-headings:
  - 强化学习与神经网络
  - 神经网络的作用
  - 更新神经网络
  - DQN 两大利器
---

学习资料:
  * [强化学习教程]({% link _contents/pages/table-contents/machine-learning/reinforcement-learning/reinforcement-learning.html %})
  * [强化学习模拟程序](https://www.youtube.com/watch?v=G5BDgzxfLvA&list=PLXO45tsB95cLYyEsEylpPvTY-8ErPt2O_)
  * [DQN Tensorflow Python 教程]({% link _contents/tutorials/machine-learning/reinforcement-learning/4-1-DQN1.md %})
  * [DQN PyTorch Python 教程]({% link _contents/tutorials/machine-learning/torch/4-05-DQN.md %})
  * 论文 [Playing Atari with Deep Reinforcement Learning](https://arxiv.org/abs/1312.5602)

今天我们会来说说强化学习中的一种强大武器, Deep Q Network 简称为 DQN. Google Deep mind 团队就是靠着这 DQN 使计算机玩电动玩得比我们还厉害.

**注: 本文不会涉及数学推导. 大家可以在很多其他地方找到优秀的数学推导文章.**

<h4 class="tut-h4-pad" id="{{ page.post-headings[0] }}">{{ page.post-headings[0] }}</h4>


<img class="course-image" src="/static/results/ML_intro/DQN1.png" alt="{{ page.title }}{% increment image-count %}">


之前我们所谈论到的强化学习方法都是比较传统的方式,
而如今, 随着机器学习在日常生活中的各种应用, 各种机器学习方法也在融汇,
合并, 升级. 而我们今天所要探讨的强化学习则是这么一种融合了神经网络和
Q learning 的方法, 名字叫做 Deep Q Network.
这种新型结构是为什么被提出来呢? 原来, 传统的表格形式的强化学习有这样一个瓶颈.

<h4 class="tut-h4-pad" id="{{ page.post-headings[1] }}">{{ page.post-headings[1] }}</h4>

<img class="course-image" src="/static/results/ML_intro/DQN2.png" alt="{{ page.title }}{% increment image-count %}">

我们使用表格来存储每一个状态 state, 和在这个 state 每个行为 action 所拥有的 Q 值. 而当今问题是在太复杂, 状态可以多到比天上的星星还多(比如下围棋). 如果全用表格来存储它们, 恐怕我们的计算机有再大的内存都不够, 而且每次在这么大的表格中搜索对应的状态也是一件很耗时的事. 不过, 在机器学习中, 有一种方法对这种事情很在行, 那就是神经网络. 我们可以将状态和动作当成神经网络的输入, 然后经过神经网络分析后得到动作的 Q 值, 这样我们就没必要在表格中记录 Q 值, 而是直接使用神经网络生成 Q 值. 还有一种形式的是这样, 我们也能只输入状态值, 输出所有的动作值, 然后按照 Q learning 的原则, 直接选择拥有最大值的动作当做下一步要做的动作. 我们可以想象, 神经网络接受外部的信息, 相当于眼睛鼻子耳朵收集信息, 然后通过大脑加工输出每种动作的值, 最后通过强化学习的方式选择动作.


<h4 class="tut-h4-pad" id="{{ page.post-headings[2] }}">{{ page.post-headings[2] }}</h4>

<img class="course-image" src="/static/results/ML_intro/DQN3.png" alt="{{ page.title }}{% increment image-count %}">

接下来我们基于第二种神经网络来分析, 我们知道, 神经网络是要被训练才能预测出准确的值. 那在强化学习中, 神经网络是如何被训练的呢? 首先, 我们需要 a1, a2 正确的Q值, 这个 Q 值我们就用之前在 Q learning 中的 Q 现实来代替. 同样我们还需要一个 Q 估计 来实现神经网络的更新. 所以神经网络的的参数就是老的 NN 参数 加学习率 alpha 乘以 Q 现实 和 Q 估计 的差距. 我们整理一下.

<img class="course-image" src="/static/results/ML_intro/DQN4.png" alt="{{ page.title }}{% increment image-count %}">

我们通过 NN 预测出Q(s2, a1) 和 Q(s2,a2) 的值, 这就是 Q 估计. 然后我们选取 Q 估计中最大值的动作来换取环境中的奖励 reward. 而 Q 现实中也包含从神经网络分析出来的两个 Q 估计值, 不过这个 Q 估计是针对于下一步在 s' 的估计. 最后再通过刚刚所说的算法更新神经网络中的参数. 但是这并不是 DQN 会玩电动的根本原因. 还有两大因素支撑着 DQN 使得它变得无比强大. 这两大因素就是 Experience replay 和 Fixed Q-targets.


{% include google-in-article-ads.html %}

<h4 class="tut-h4-pad" id="{{ page.post-headings[3] }}">{{ page.post-headings[3] }}</h4>

<img class="course-image" src="/static/results/ML_intro/DQN5.png" alt="{{ page.title }}{% increment image-count %}">

简单来说, DQN 有一个记忆库用于学习之前的经历. 在之前的简介影片中提到过, Q learning 是一种 off-policy 离线学习法, 它能学习当前经历着的, 也能学习过去经历过的, 甚至是学习别人的经历. 所以每次 DQN 更新的时候, 我们都可以随机抽取一些之前的经历进行学习. 随机抽取这种做法打乱了经历之间的相关性, 也使得神经网络更新更有效率. Fixed Q-targets 也是一种打乱相关性的机理, 如果使用 fixed Q-targets, 我们就会在 DQN 中使用到两个结构相同但参数不同的神经网络, 预测 Q 估计 的神经网络具备最新的参数, 而预测 Q 现实 的神经网络使用的参数则是很久以前的. 有了这两种提升手段, DQN 才能在一些游戏中超越人类.

