---
layout: post
title: "对于游戏设计的思考"
author: "Kong Weihang"
categories: talk
tags: [develop,game,design]
image: the-think-of-game-design.jpg
---

# KGN Talk

[toc]

## 前言

今天在聊天的时候谈到了设计流程上的区别，我觉得区别还是挺大的，特别是盈利方式，导致开发流程上的不同．

## 不同的游戏设计方法

### 设计思路

国内倾向于找到一个简单, 轻度, 充分利用碎片时间, 不断重复的循环, 然后在上面添加细节, 微创新之类的, 套上美少女, 世界毁灭的世界观, 来个时间穿越的剧情. 当然这是我对国内手游的理解, 我没有完整呆过国内的项目, 就我自己玩到的来说, 设计上比较保守, 通常针对碎片化来设计．

### 碎片化时间

关于碎片化时间，我觉得有待商榷，究竟手游的设计是不是围绕着碎片化时间来开展．早期的水果忍者，我觉得是，现在的战双帕米什，不是．特别是很多的手游对于日常的清理会定到半个小时，网易可能会比较狠设计到一个小时，那么两个月就是３０个小时游戏时间，是一款３A的通关时间，而且你还不一定会通关．而且要坚持每天抽半个小时打游戏，毕竟有的时候加班或者出去玩，忘记清理日常很正常，连着几天忘记可能就不想玩了．所以我觉得对于这些玩家来说挺不容易的，从时间上来看和主机游戏没有区别，甚至主机游戏更碎片一些，因为你可以想玩就玩，想走就走，一周之后还没忘记剧情回来继续玩都是ｏｋ的，反而更轻松一些．所以对于碎片化时间，我对于现在重度的手游称之为碎片化时间随便刷刷表示怀疑，我认为现在这已经是个伪命题了．在如何抢占用户时间这点上，手游没有让步的迹象．

### 设计流程

设计的流程也不一样, 我接触的设计文档, 一开始都会讲述一个故事, 那是他们希望玩家在游戏中体验到的流程, 这个希望带给玩家的体验是整个设计的核心, 会有一个小故事, 来描述玩家所体验到玩法, 比如说: 

> 杰西卡在石窟中穿行, 巨大的穹顶之下是一片野生的蕨类丛林, 她被肆意生长的藤曼缠绕着, 远处传来滴答的流水声, 地面很滑, 当她尝试蹑手蹑脚的从中钻出中, 一不小心她滑入一个水坑之中, 巨大的声响惊醒了在附近休息的恐龙群, 敏捷的迅猛龙从四处跳出, 疯狂地朝向音源跑来, 面对着嘶吼的龙群, 杰西卡掏出自己27mm口径霰弹枪: "丹尼! 它们发现我了! 你们从另一测离开, 我来杀出一条血路! ". 

在有了一个对整体的印象后, 他们提炼出关键词, 例如: 
- 侏罗纪时代 
- 狂野感
- 血腥的战斗
- 潜行
- 植物丛生

用来总结对于游戏的整体观感, 之后围绕这些关键要素, 打造
- 3C
- 叙事
- 环境,　野生动物
- 角色, NPC, companion 
- 战斗 
- 潜入
- 技术，例如AI，无缝加载
- 任务分支

等步骤, 把大块提炼成文档, 开始设计prototype, 一开始只有很少的人参加, 一旦通过了总部的审查, 那么就作为正式游戏开始开发．

其中第一部的讲个故事特别特别重要, 故事没决定他们干脆就不做的, 就一直在纠结这个叙事, 直到定下来, 定下来就不会大改了．这个故事就是手游里的loop, loop定下来可以加细节, 但是不能大改, 是"核心玩法", 这个所谓的"核心故事"的重要性可以理解成手游的"核心玩法"．

问题是很多元素, 比如说GD希望玩家能够自由探索世界, 按照自己的方式来体验剧情, 给玩家带来独一无二的体验(相信我, 每次他们都这么说) 然后他们就会加入open world, 然后不可避免的复用了之前的设计, 毕竟都是同一批人在开发, 没理由不搞成一样的. 然后就可以坐等玩家说罐头开放世界了. 

其次就是对于叙事上也不同, 我不能在手机上看长篇小说, 毕竟屏幕就那么小, 一般也懒得做剧情演出, 但是演出其实是主机游戏的设计中特别重要的一环, 给玩家带来沉浸感, 结合叙事, 游戏要说是的浪漫故事, 还是悲剧色彩的故事; 结合表演, 是否做动画, 是否加入队友的语音; 结合环境, LA要设计对应风格的level; 结合音乐音效等一堆乱七八糟的东西．

### 运营

国内手游全是长线运营的游戏，这点非常不一样，毕竟主机上的游戏一旦发售了就是结束开发了，原本的开发团队在发售的时候基本就散掉大多数的人，这些成员会被安排到其他需要人手的项目中．至于说DLC, 通常是是发售前一(几)年就定好的. 本质上没有发售后内容

像是剧情, 新玩法, 主机游戏没有, 就那么多了, 发售怎样就怎样, 如果你觉得某个设计不合理, 那也只能忍着, 大概率不会改, 因为原本的团队都没了, 早就release到其他项目了．