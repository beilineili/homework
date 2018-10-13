

# Construct 2 游戏制作

[TOC]



### 实验/学习工具

Construct 2：https://www.scirra.com/construct2



### 制作目的：

让玩家能控制一个人物，通过躲避和设计技巧杀死尽可能多的怪物来获得快感。（为使玩家更加快乐，游戏中的怪物设计得比较特别）

### 制作顺序：

（1）处理外部事件（process external events）
外部事件包含交互设备和游戏系统提供的事件（对象、条件、动作序列）。
交互设备事件：**（用键盘，鼠标来控制游戏对象的操作）**

> ```
> mouse | on left button clicked | actions
> ```

游戏系统事件：**（显示得分，播放音乐等事件）**

> ```
> system | on every tick |actions
> ```

（2）处理内部事件：**（游戏对象间的作用事件）**

> | game object | event | actions |
> | ----------- | ----- | ------- |
> |             |       |         |

### 游戏设计：CRC卡

|                            bullet                            |
| :----------------------------------------------------------: |
| ![](C:\Users\江泽进\Desktop\新建文件夹\bullet.png)（放在背景外的位置）![](C:\Users\江泽进\Desktop\新建文件夹\Snipaste_2018-10-13_18-16-13.png) |
|                    player,monster,explode                    |
| 1.会移动 2.从player的枪中发出 3.碰到monster后消失，产生explode效果 |



|                           monster                            |
| :----------------------------------------------------------: |
| ![](C:\Users\江泽进\Desktop\新建文件夹\Snipaste_2018-10-10_21-21-52.png) |
|                        bullet，player                        |
| 1.会移动，撞到背景边界后会朝player方向来 2.被bullet击中5次后消失 |



|                            player                            |
| :----------------------------------------------------------: |
|      ![](C:\Users\江泽进\Desktop\新建文件夹\player.png)      |
|                       bullet，monster                        |
| 1.能由方向键和鼠标控制移动和转向 2.碰到monster会消失，游戏结束 |

|                       explode                       |
| :-------------------------------------------------: |
| ![](C:\Users\江泽进\Desktop\新建文件夹\explode.png) |
|                   bullet，monster                   |
|        bullet和monster相撞后出现，并渐变消失        |

### 制作步骤：

#### 1.创建新的布局及背景

在软件左上角的file中点击New从而新建一个布局

![](C:\Users\江泽进\Desktop\新建文件夹\Snipaste_2018-10-13_21-14-37.png)