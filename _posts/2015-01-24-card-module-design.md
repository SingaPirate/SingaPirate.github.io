---
layout: post
title: 卡牌模块架构设计
description: "新架构卡牌模块架构设计提案"
tags: [架构设计]
author: 叮咚
---

一个控制用户使用卡牌操作规范的模块构想：

********************************************************************************************************
卡牌需要提供的参数：



写在每一个卡牌中：

{% highlight c++ %}
public:
int get额定使用次数() {return 额定使用次数;}
enum CountType get计数类型() {return 计数类型;}
int get距离限制() {return 距离限制;}
int get目标上限() {return 目标上限;}
bool 能重铸() {return 重铸许可;}
bool 能连横() {return 连横许可;}
bool get合法性(&玩家1, &玩家2) {...}    //函数体中写出判断的具体代码，如果玩家1对玩家2使用此牌合法（不考虑距离）则返回true

private:
int 额定使用次数;  //默认1000，相当于无限制
enum CountType 计数类型    //一定要初始化
int 距离限制; //默认1000，相当于无限制
bool 重铸许可; //默认false
bool 连横许可; //默认false
{% endhighlight %}


********************************************************************************************************
接下来是模块本体的实现过程：



先扫描所有牌检查可用性，每张卡牌对应执行下面函数，返回false则该卡牌低暗不可选，返回true高亮可选：
{% highlight c++ %}
bool cardUsable(&玩家, &此牌)
{
    int 额定次数 = 此牌->get额定次数() + 技能修正；
    int 额外次数 = 技能修正；
    if ( (玩家->has无次数限制效果(此牌) != true)
      && (玩家->get额定使用计数(此牌) >= 额定次数)           //计数模块需读取此牌的限制类型并按照计数类型条件计数。
      && (玩家->get额外使用计数(此牌) >= 额外次数) )
        return false;

    bool 存在目标 = false;
    int 距离限制 = 此牌->get距离限制() + 技能修正；
    for (auto &tmp玩家 : 所有玩家) {
        if ( 此牌->get额外距离以及合法性(tmp) == true ) {
            存在目标 = true
            break;
        }

        if ( (玩家->has无距离限制效果(此牌) == false)
          && (玩家:get距离(tmp玩家) >= 距离限制) )
            continue;

        if ( 此牌->get合法性(玩家,tmp玩家) == true ) {
            存在目标 = true;
            break;
        }
    }

    if (存在目标 == false)
        return false;


    if (玩家:被禁止使用(此牌) == true)
        return false;

    return true;
}
{% endhighlight %}


当玩家选中一张牌后，选择目标前：

扫描检查所有玩家作为目标的可选性，每个玩家对应执行下面函数，返回false则该玩家低暗不可选，返回true高亮可选：
{% highlight c++ %}
bood cardTargetChoosable(&玩家, &此牌, Qlist &已选目标, &待选目标)  //待选目标相当于filter里的to_select
{
    if ( 此牌->get额外距离以及合法性(tmp) == true )
        return true;


    int 已选额定目标数 = 0;
    for (auto &tmp目标 : 已选目标) {
        if (tmp目标->hasFlag("额定目标"))
            ++已选额定目标数;
    }
    额定目标 = 此牌->get目标上限 + 技能修正；
    if (已选额定目标数 >= 额定目标)
        return false;

    if ( (玩家->has无距离限制效果(此牌) == false)
      && (玩家:get距离(tmp玩家) >= 距离限制) )
        return false;

    if ( 此牌->get合法性(玩家,tmp玩家) == false ) {
        return false;
}
{% endhighlight %}


玩家选择目标的过程中还需要判断是否可以点击确定
{% highlight c++ %}
bool cardUseFeasible(&玩家, &此牌, Qlist &已选目标)
{
    if (此牌->能重铸() = true)
        return true;
    return (已选目标->empty() == false); //卡牌只要有已选目标就能用
}
{% endhighlight %}