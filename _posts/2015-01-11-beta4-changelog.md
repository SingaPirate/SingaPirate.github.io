---
layout: post
title: 国战beta4更新内容（持续更新）
description: "beta4的发布临近，看看有什么变动吧！"
tags: [动向]
image:
  feature: abstract-1.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
---

#Bugs Fixed:

* [AI贾诩对自己使用黑色【挟天子以令诸侯】](http://tieba.baidu.com/p/3439569041)

* AI有时会对自己使用得【无懈可击】使用【无懈可击】
  
* AI魏延暗置时不会发动【狂骨】

* [AI暗将贾诩1体力时不亮将以避免成为黑色【南蛮入侵】的目标](http://tieba.baidu.com/p/3439569041)
  
* [AI对同一角色连续使用多次【知己知彼】观看手牌效果](http://tieba.baidu.com/p/3439569041)
  
* [AI蒋钦没有手牌也能发动【尚义】](http://tieba.baidu.com/p/3439569041)
  
* AI被【挑衅】或【借刀杀人】时，不会发动【方天画戟】效果
  
* [AI黄盖即使弃牌阶段弃掉【桃】也不发动【苦肉】](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/258)
  
* [敌对张角在场时，AI在不恰当的时机发动【八卦阵】进行判定](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/258)
  
* [AI不会使用【木牛流马】里的牌](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/258)
  
* [AI华佗用装有很多红牌的【木牛流马】发动【急救】](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/258)
  
* [AI有时不会发动【挑衅】](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/258)
  
* [AI反复对装备【八卦阵】的甄姬/郭嘉使用【杀】](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/258)
  
* [AI对被【调虎离山】移出游戏的角色使用【远交近攻】](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/258)
  
* [同一角色被【断肠】两次时，第一次失去的技能会恢复](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/279)
  
* [对双暗的角色使用【断肠】，无论选什么，只能失去主将技能](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/270)
  
* [【戮力同心】的目标错误](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/274)
  
* [【方天画戟】不能指定野心家为目标](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/275)
  
* [录像回放中技能预亮后潜伏不消失](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/272)
  
* [只有第一个换皮肤的武将的相应皮肤有效](http://tieba.baidu.com/p/3439569041)
  
* 发动【八阵】不播放技能配音
  
* Linux版的窗口不正常
  
* Linux版中部分字体无法显示
  
* "不播放技能音效"选项影响背景音乐的播放
  
* [最小化托盘只能使用一次](http://tieba.baidu.com/p/2357497936)
  
* 禁止IP对话框中，部分玩家断开连接后，仍显示连接
  
* [孟获明置在场时，不为【南蛮入侵】的伤害来源](http://tieba.baidu.com/p/3439569041)
  
#API Changes：

* 增加Lua函数table:toSet(),返回无重复元素的table对象
  
* 以"&"开头的私有牌堆可以在检测时像【木牛流马】牌堆一样视为手牌
  
* 修复"使用TargetModSkill增加【顺手牵羊】的额外目标有时不亮将"的bug
  
* 修复"锁定视为锦囊时checkTargetModSkillShow返回0"的bug
  
* 新增对同一个角色点击多次的卡牌Lua接口
  
* 开放Lua读取ServerInfo的接口
  
* [升级Qt库支持至最新](5.4.0)
  
* [更新freetype至2.5.4，增加debug版库](OSX及Linux使用静态库)
  
* 更新fmodex至4.4.49
  
#New Features/Enhancements:

* AI使用装备牌时优先装备【玉玺】
  
* 优化【联军盛宴】相关的【无懈可击】AI使用策略
  
* [AI身份比较明显时，被【敕令】询问时不再弃置装备牌](http://tieba.baidu.com/p/3439569041)
  
* [优化AI身份判断](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/258)
  
* [优化【联军盛宴】的AI使用策略](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/258)
  
* [优化【水淹七军】的AI使用策略](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/258)
  
* [优化针对【流离】的【杀】的AI使用策略](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/258)
  
* [优化【神速】的AI使用策略](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/258)
  
* [支持在游戏中调整背景音乐音量，所有选项在点击“取消”后自动复原](https://github.com/Mogara/QSanguosha-For-Hegemony/issues/278)
  
* [重写往期的更新内容](http://tieba.baidu.com/p/3450767214)
  
* 更新“关于我们”
  
* 缩短询问技能发动顺序中技能按钮的长度
  
* [优化花色选择对话框](http://tieba.baidu.com/p/3399890782?pn=4)
  
* [手牌过多分两行显示时，上移倒计时条，防止被挡住](http://tieba.baidu.com/p/3439569041?pn=2)
  
* 优化【帷幕】关于【敕令】的亮将AI策略
  
* [优化【狂骨】AI策略](http://tieba.baidu.com/p/3439569041)
  
* 优化平局对话框的样式
  
* [调整“不询问无懈可击”按钮使用方式](http://tieba.baidu.com/p/3399890782?pid=60513158733#60513158733)