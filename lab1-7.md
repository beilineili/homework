
# Construct 2 游戏制作（进阶篇）



#### <a href="#实验/学习工具">实验/学习工具</a>

#### <a href="#游戏背景">游戏背景</a>

#### <a href="#游戏玩法">游戏玩法</a>

#### <a href="#制作顺序">制作顺序</a>

#### <a href="#游戏设计">游戏设计</a>

#### <a href="#制作步骤">制作步骤</a>

#### <a href="#最终效果">最终效果</a>



### 实验/学习工具

Construct 2：https://www.scirra.com/construct2



### 游戏背景：

当代大学生在学习的压迫下鸭梨山大，他们需要在高数、程序设计、软件工程导论等学科的魔爪中逃出生天，杀出一天血路争取到高绩点。

### 游戏玩法：

在游戏中，玩家不仅需要方向键移动、鼠标转身，躲避高等数学、c语言的追杀，用手中武器击杀他们，还要担心脚下是否有不能被杀死的软件工程导论，否则将体验一波踩雷的感觉。杀死足够数量的怪物即可得到高绩点，成为大佬。（这是不可能的）

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
| ![bullet.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/bullet.png?raw=true)（放在背景外的位置）![Snipaste_2018-10-13_18-16-13.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/Snipaste_2018-10-13_18-16-13.png?raw=true) |
|                    player,monster,explode                    |
| 1.会移动 2.从大学生的枪中发出 3.碰到高数，c语言后消失，产生爆炸效果 |



|                           monster                            |
| :----------------------------------------------------------: |
| ![Snipaste_2018-10-10_21-21-52.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/Snipaste_2018-10-10_21-21-52.png?raw=true) |
|                        bullet，player                        |
| 1.会移动，撞到背景边界后会朝大学生方向来 2.被bullet击中5次后消失 |



|            monster2             |
| :-----------------------------: |
|                                 |
|         bullet，player          |
| 1.不会移动 2.被bullet击中后消失 |



|                           monster3                           |
| :----------------------------------------------------------: |
|                                                              |
|                            player                            |
| 1.不会移动 2.不会被bullet击中消失 3.大学生撞到他之后会当场去世 |



|                            player                            |
| :----------------------------------------------------------: |
|                                                              |
|                       bullet，monster                        |
| 1.能由方向键和鼠标控制移动和转向 2.碰到monster会消失，游戏结束 |

|                explode                |
| :-----------------------------------: |
|                                       |
|            bullet，monster            |
| bullet和monster相撞后出现，并渐变消失 |



#### 最终效果：

![23-10-49-10-13-6325.gif](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/23-10-49-10-13-6325.gif?raw=true)



![23-11-31-10-13-6462.gif](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/23-11-31-10-13-6462.gif?raw=true)

快去制作你自己的游戏试试看吧。