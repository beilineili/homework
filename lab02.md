
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
| ![bullet.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/bullet.png?raw=true)（放在背景外的位置）![Snipaste_2018-10-13_18-16-13.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/Snipaste_2018-10-13_18-16-13.png?raw=true) |
|                    player,monster,explode                    |
| 1.会移动 2.从player的枪中发出 3.碰到monster后消失，产生explode效果 |



|                           monster                            |
| :----------------------------------------------------------: |
| ![Snipaste_2018-10-10_21-21-52.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/Snipaste_2018-10-10_21-21-52.png?raw=true) |
|                        bullet，player                        |
| 1.会移动，撞到背景边界后会朝player方向来 2.被bullet击中5次后消失 |



|                            player                            |
| :----------------------------------------------------------: |
| ![player.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/player.png?raw=true) |
|                       bullet，monster                        |
| 1.能由方向键和鼠标控制移动和转向 2.碰到monster会消失，游戏结束 |

|                           explode                            |
| :----------------------------------------------------------: |
| ![explode.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/explode.png?raw=true) |
|                       bullet，monster                        |
|            bullet和monster相撞后出现，并渐变消失             |

### 制作步骤：

#### 1.创建新的布局及背景

在软件左上角的file中点击New从而新建一个布局

![Snipaste_2018-10-13_21-14-37.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/Snipaste_2018-10-13_21-14-37.png?raw=true)

在布局的空白处双击鼠标左键，点击tile background，插入背景图片并调整大小至与布局相同且适合





![Snipaste_2018-10-13_21-32-31.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/Snipaste_2018-10-13_21-32-31.png?raw=true)

![bg.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/bg.png?raw=true)

#### 2.添加图层

在画面右上方从project切换到layers，修改图层名并锁定，新建一个图层



![687474703a2f2f7778312e73696e61696d672e636e2f6c617267652f3030376d4236616c6c793166767963686870373567673330633230626c6163672e676966.gif](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/687474703a2f2f7778312e73696e61696d672e636e2f6c617267652f3030376d4236616c6c793166767963686870373567673330633230626c6163672e676966.gif?raw=true)

*当属性栏，状态栏不见了的时候点击左上角VIEW，把能勾的选项都勾了

![Snipaste_2018-10-13_21-14-09.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/Snipaste_2018-10-13_21-14-09.png?raw=true)

#### 3.添加游戏对象

（1）鼠标左键双击背景选择插入Sprite，添加我们所需的游戏对象，重命名。

（2）选中游戏对象，在左侧属性栏点击Behaviors，添加我们想要的行为，如：

-  **8 Direction movement**.这使您可以使用箭头键移动对象。它会很好地适应玩家的运动。
-  **Bullet movement**. 这只是以当前角度向前移动一个物体。它对玩家的子弹很有用。尽管有这个名字，它也可以很好地移动怪物 - 因为所有的移动都是以某种速度向前移动物体。
-  **Scroll to**.这使得屏幕在移动时跟随对象（也称为滚动）。这对玩家有用。
-  **Bound to layout**. 这将停止一个物体离开布局区域。这对玩家也很有用，所以他们不能在游戏区域外游荡！
-  **Destroy outside layout**.而不是停止离开布局区域的对象，如果它停止，则会破坏它。它对我们的子弹很有用。没有它，子弹将永远飞离屏幕，总是占用一点内存和处理能力。相反，我们应该在他们离开布局后销毁子弹。
-  **Fade**.这逐渐使物体淡出，我们将用于爆炸。
-  ![Snipaste_2018-10-13_21-54-10.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/Snipaste_2018-10-13_21-54-10.png?raw=true)

（3）改变游戏对象的一些属性从而增加或降低游戏难度，如monster的数量（可通过选中monster后按ctrl+鼠标左键进行复制黏贴）和移动速度

#### 4.添加游戏事件

在Event sheet 1中，我们能添加很多事件和动作。![eventsheettab.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/eventsheettab.png?raw=true)

比如设置monster的生命值，消灭一只monster之后的分数显示，播放音乐等。







这里回答一个常见的问题，

​       如果你运行游戏，你会注意到子弹从玩家中间射击，而不是从枪尾射出。让我们通过在枪的末端放置一个图像点来解决这个问题。（图像点只是图像上可以从中生成对象的位置。）右键单击项目或对象栏中的播放器，然后选择“编辑动画”。播放器的图像编辑器重新出现。单击原点和图像点工具：并打开图像点对话框，对象原点显示为红点。这是对象的“热点”或“枢轴点”。如果旋转对象，它会围绕原点旋转。我们想要添加另一个图像点来表示枪，所以单击绿色*添加*按钮。出现蓝点 - 这是我们的新图像点。在玩家枪的末端单击鼠标左键，将图像点放在那里。

#### 最终效果：

![23-10-49-10-13-6325.gif](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/23-10-49-10-13-6325.gif?raw=true)



![23-11-31-10-13-6462.gif](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/23-11-31-10-13-6462.gif?raw=true)

快去制作你自己的游戏试试看吧。