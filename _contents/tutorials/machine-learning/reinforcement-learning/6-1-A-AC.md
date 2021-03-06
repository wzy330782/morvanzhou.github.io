---
youku_id: XMjY0NTA4NzE5Mg
youtube_id: HTONz4ZLGxw
title: 什么是 Actor Critic
description: "今天我们会来说说强化学习中的一种结合体 Actor Critic (演员评判家), 它合并了 以值为基础 (比如 Q learning) 和 以动作概率为基础 (比如 Policy Gradients) 两类强化学习算法.
我们有了像 Q-learning 这么伟大的算法, 为什么还要瞎折腾出一个 Actor-Critic? 原来 Actor-Critic 的 Actor 的前生是 Policy Gradients , 这能让它毫不费力地在连续动作中选取合适的动作, 而 Q-learning 做这件事会瘫痪. 那为什么不直接用 Policy Gradients 呢? 原来 Actor Critic 中的 Critic 的前生是 Q-learning 或者其他的 以值为基础的学习法 , 能进行单步更新, 而传统的 Policy Gradients 则是回合更新, 这降低了学习效率."
chapter: 6
thumbnail: /static/thumbnail/ML-intro/AC.png
post-headings:
  - 为什么要有 Actor 和 Critic
  - Actor 和 Critic
  - 增加单步更新属性
  - 改进版 Deep Deterministic Policy Gradient (DDPG)
---

学习资料:
  * [强化学习教程]({% link _contents/pages/table-contents/machine-learning/reinforcement-learning/reinforcement-learning.html %})
  * [强化学习模拟程序](https://www.youtube.com/watch?v=G5BDgzxfLvA&list=PLXO45tsB95cLYyEsEylpPvTY-8ErPt2O_)
  * [Actor Critic Python 教程]({% link _contents/tutorials/machine-learning/reinforcement-learning/6-1-actor-critic.md %})
  * 学习书籍 [Reinforcement learning: An introduction](http://ufal.mff.cuni.cz/~straka/courses/npfl114/2016/sutton-bookdraft2016sep.pdf)

今天我们会来说说强化学习中的一种结合体 Actor Critic (演员评判家), 它合并了 以值为基础 (比如 Q learning) 和 以动作概率为基础 (比如 Policy Gradients) 两类强化学习算法.

**注: 本文不会涉及数学推导. 大家可以在很多其他地方找到优秀的数学推导文章.**

<h4 class="tut-h4-pad" id="{{ page.post-headings[0] }}">{{ page.post-headings[0] }}</h4>

<img class="course-image" src="/static/results/ML_intro/AC1.png" alt="{{ page.title }}{% increment image-count %}">


我们有了像 Q-learning 这么伟大的算法, 为什么还要瞎折腾出一个 Actor-Critic? 原来 Actor-Critic 的 Actor 的前生是 Policy Gradients , 这能让它毫不费力地在连续动作中选取合适的动作, 而 Q-learning 做这件事会瘫痪. 那为什么不直接用 Policy Gradients 呢? 原来 Actor Critic 中的 Critic 的前生是 Q-learning 或者其他的 以值为基础的学习法 , 能进行单步更新, 而传统的 Policy Gradients 则是回合更新, 这降低了学习效率.


<h4 class="tut-h4-pad" id="{{ page.post-headings[1] }}">{{ page.post-headings[1] }}</h4>

<img class="course-image" src="/static/results/ML_intro/AC2.png" alt="{{ page.title }}{% increment image-count %}">

现在我们有两套不同的体系, Actor 和 Critic, 他们都能用不同的神经网络来代替 . 在 Policy Gradients 的影片中提到过,  现实中的奖惩会左右 Actor 的更新情况. Policy Gradients 也是靠着这个来获取适宜的更新. 那么何时会有奖惩这种信息能不能被学习呢? 这看起来不就是 以值为基础的强化学习方法做过的事吗. 那我们就拿一个 Critic  去学习这些奖惩机制, 学习完了以后. 由 Actor 来指手画脚, 由 Critic 来告诉 Actor 你的那些指手画脚哪些指得好, 哪些指得差, Critic 通过学习环境和奖励之间的关系, 能看到现在所处状态的潜在奖励, 所以用它来指点 Actor 便能使 Actor 每一步都在更新, 如果使用单纯的 Policy Gradients, Actor 只能等到回合结束才能开始更新.


<h4 class="tut-h4-pad" id="{{ page.post-headings[2] }}">{{ page.post-headings[2] }}</h4>

<img class="course-image" src="/static/results/ML_intro/AC3.png" alt="{{ page.title }}{% increment image-count %}">

但是事物终有它坏的一面, Actor-Critic 涉及到了两个神经网络, 而且每次都是在连续状态中更新参数,  每次参数更新前后都存在相关性, 导致神经网络只能片面的看待问题, 甚至导致神经网络学不到东西. Google DeepMind 为了解决这个问题, 修改了 Actor Critic 的算法,

{% include google-in-article-ads.html %}


<h4 class="tut-h4-pad" id="{{ page.post-headings[3] }}">{{ page.post-headings[3] }}</h4>

<img class="course-image" src="/static/results/ML_intro/AC4.png" alt="{{ page.title }}{% increment image-count %}">

将之前在电动游戏 Atari 上获得成功的 DQN 网络加入进 Actor Critic 系统中,  这种新算法叫做 Deep Deterministic Policy Gradient, 成功的解决的在连续动作预测上的学不到东西问题. 所以之后, 我们再来说说什么是这种高级版本的 Deep Deterministic Policy Gradient 吧.

