# 字符游戏-智能蛇

## 一、实验目的

1. 了解 算法 与 “智能” 的关系
2. 通过算法赋予蛇智能
3. 了解 Linux IO 设计的控制



## 二、实验环境

1.我使用了windows10专业版自带的虚拟机Hyper-v（里面自带ubuntu最新版的下载）

2.编译环境我尝试了用vim和codeblocks



## 三、控制输入/输出设备

#### 1.VT 100终端标准



在codeblocks中编译运行的结果，打印出了在坐标系中正弦的动态图像

![Snipaste_2018-12-16_15-49-10.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/Snipaste_2018-12-16_15-49-10.png?raw=true)



#### 2、实现 kbhit()

codeblocks中编译运行结果，可以实时记录键盘输入了什么，解决了原函数中按一次键盘就要按一次回车才能进行下一步的尴尬操作。

![Snipaste_2018-12-16_15-54-28.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/Snipaste_2018-12-16_15-54-28.png?raw=true)



利用vim编辑后在终端中编译运行

![Snipaste_2018-12-16_16-19-22.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/Snipaste_2018-12-16_16-19-22.png?raw=true)



## 四、编写贪吃蛇智能算法

