---
layout: post
---

## How to Think Like Git

2018年9月底开始准备《玩转Git、Github和GitLab》的视频课程，并非在非常宽裕的时间中进行：白天有工作，下班了得先辅导好孩子的功课（小升初关键的时期）。
再加上课程涉及的Git、GitHub和GitLab，涉及代码管理、项目协作和持续交付相关的众多话题，内容多且涉猎广。 

这些个因素，导致课程虽然录制完了，但还是感觉少了些什么，就 “Think Like Git” 相关的内容，课程准备过程中也是在“讲，还是不讲”左右徘徊中。
个人还是认为很有必要和大家聊一聊“做哪些努力，我才能如 Git 一样思考”诸如此类的话题的。借直播的机会，我们不妨说一说这些个事情。

Google上有类似的文章，我认为《Demystifying Git: 3 Concepts to Do Everything with Git》 写得非常好，我们不妨跟着它的步伐，挑一些关键的内容，
一起来揭秘 Git 。

### 三个必要的概念

在构筑 Git model 时，我们先理解 snapshots、graph 和 changesets 三个概念。

#### snapshots（commit）

Git仓库的快照，也就是 commit 。反过来来说，commit 就是 快照。

一个 commit 就对应了 “在这个 commit 被创建的时间点上，从项目根目录开始的所有文件的一个copy” 。

取出一个 commit ，我们就能得到：我们曾经存放的项目某个时间点的状态。比如很容易地通过 commit 取到某个发布版本，某个需要修复的版本，
或者需要继续开发的版本。

#### graph

多个commit之间不是独立存在的，而是通过父-子关系联系在一起的。它代表了一个 commit 是从哪儿来的。

由于 Git 中父的 commit 不知道它的孩子，而子的 commit 是知道它的父亲的，因此，父-子之间连接线的箭头，我们都是从子指向父。

当两个 commit 共享一个父 commit 的时候，就产生了分叉开的分支，不同的分支以并行的方式继续发展。
而两个分支 merge 在一起的时候，会产生一个 commit，这个 commit 有两个父亲。
如此一来，Git演变的历史其实就是一副 commit 的有向图。

很重要的是，这副历史图可以让我们很方便地计算出两个不同状态的差异。自然而然地引出下面这个 “changeset” 的概念。

#### changeset

当我们从 commit A 创建出 commit B，我们又创建了一个快照。不过，我们也可以把这个过程看作是基于前一个 commit 的增量的变化。
由 commit 带来的贡献：产生了一组不可分割的变更，我们也称为 changeset／变更集。
changeset记录了哪些文件发生了什么样的变更（不含没变更的文件）。Git中的 patch 就是变更集的

Git以文本文件行的级别来看待变更（行与行比较差异）。
Git能够计算任意两个 commit 之间的 changeset ，并且可以把这个 changeset 应用到任何 commit 上面。

