---
title: csgo rws是什么？
date: 2020-04-21 19:33:01
tags:
- csgo
- esea
- steam
- rws
- csgodata
- csgo rws是什么
categories:
- 闲言碎语
---

<img src="https://tva1.sinaimg.cn/large/007S8ZIlly1ge1nlvs6bfj310s0rw45o.jpg" style="zoom:33%;" />

<img src="https://tva1.sinaimg.cn/large/007S8ZIlly1ge1nqmyakxj30yn0ovn1f.jpg" style="zoom:33%;" />

5e对战平台和esea都采用了`RWS`值来统计选手的能力，那`RWS`到底是什么呢？`RWS`多少才是正常的？为什么我rating很高，`RWS`却是全队平均水平呢？🤔️

<!--more-->

### 定义

​		`RWS`统计数据是**R**ound **W**in **S**hares的缩写，用于表示玩家对团队整体成功的贡献。

### 我怎么加RWS?

- `RWS`值的范围从`0`到`100`，数值高的选手表示更厉害，平均`RWS`是10。
- 每回合只有胜利方获得100`RWS`或者说100胜利贡献。
- 输掉回合的队伍没有`RWS`增加。
- 掉线的人每回合都是0`RWS`

在纯靠击杀完成的回合，100点`RWS`根据每个人造成的伤害平均分配

+ 栗子#1：你造成了140伤害，你队伍其余的人总共造成了360伤害，你将得到28.00`RWS`（140 / 500 * 100)

在雷包爆炸或者被拆除的回合，完成拆包或者下包的选手将会得到30`RWS`，剩下的70`RWS`将根据你们造成的伤害平均分配。

+ 栗子#2：你下包，包炸了，并且你当前回合造成的伤害是0，你的队友每人造成50伤害，那么你当前回合将得到30`RWS`，你的队友每人得到17.50`RWS`（(100-30)/4)
+ 栗子#3：你拆了雷包，并且造成了100伤害，你的队友每人造成了50点伤害，那么你会得到53.33`RWS`（其中30是拆包，其余的23.33是根据伤害分配的）

[esea原文链接](https://support.esea.net/hc/en-us/articles/360008740634-What-is-RWS-)

