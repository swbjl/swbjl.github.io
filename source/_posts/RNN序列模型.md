---
title: RNN序列模型
date: 2026-11-1 18:00:00
tags:
  - 博客
  - 随笔
categories: it学习
aliases:
  - 终于完成了第一篇文章
---

## 目的

学习一个句子，不仅要学习其中词语的含义，还要学习词语的顺序信息

生成下一token时，结合当前词和前面的上下文信息



## 实现原理分析

以x1-x4为例，
![隐藏状态公式](/img/RNN/隐藏状态公式.jpg)
h1,由x1，三维转向四维得到,Xout1由h1得到
h2,由x2+h1，七维转向四维得到,Xout2由h2得到

之后同理
### RNN的最小单元基本原理
<video width="80%" controls autoplay loop muted>
  <source src="/video/RNN/RNN最小单元基本原理.mp4" type="video/mp4">
</video>

这样我们就到了

### RNN单层表现
接下来看一下他在一层里面的表现
<video width="80%" controls autoplay loop muted>
  <source src="/video/RNN/单层实现.mp4" type="video/mp4">
</video>


ok 我们目前得到了一层的RNN是如何实现的

### RNN多层实现
现在接受一个新的假设：
低层网络更容易捕捉局部模式（如词组、短语），
而高层网络则能学习更抽象的语义信息（如句子主题或语境）。
如此，我们可以实现一个多层的RNN

<video width="80%" controls autoplay loop muted>
  <source src="/video/RNN/多层实现.mp4" type="video/mp4">
</video>

在最后 我们得到了学习到 低层和高层  所有信息的隐藏信息，之后只要再经历一层linear层  那么就可以得到输出
就像这样：
![从隐藏状态到最终输出](/img/RNN/从隐藏状态到最终输出.png)

## 简单总结
ok，是不是觉得学完了，算...是吧

基础的，学完了，那我们稍微总结下，什么效果吧，
我们现在可以读一个句子，按顺序读，然后得到他的信息，再输出一层我们想要的信息

可是，我们是按从左到右的顺序来的，对吧，反过来，是不是也可能存在可以学习的信息，不是给人学的，是给机器学习，你这家伙，别局限在人类视角啊

so，双向来喽
## 双向
### 单层双向

<video width="80%" controls autoplay loop muted>
  <source src="/video/RNN/单层双向.mp4" type="video/mp4">
</video>

由此，就可以，得到正向和反向的所有信息

### 多层双向

ok，那么如同搭积木一般，之前我们实现了多层的单向，从而获取低层和高层的信息，
现在我们就可以实现多层的双向了--》从而得到 （低层+高层；前向+后向 ） 的所有信息
下面是我手写的示例，当时懵逼了一下，见谅见谅

<video width="80%" controls autoplay loop muted>
  <source src="/video/RNN/多层双向.mp4" type="video/mp4">
</video>

如此我们就实现了多层双向的RNN

如此，RNN可以说所有内容我们都学完了，站在前人的肩膀上前进就是舒服