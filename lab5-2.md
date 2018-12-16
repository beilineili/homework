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



流畅度max，体验极好

![bandicam 2018-12-16 17-31-02-522 (1).gif](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/bandicam%202018-12-16%2017-31-02-522%20(1).gif?raw=true)





## 四、编写贪吃蛇智能算法

我们希望能够造出一条只要不死就能自动走的蛇，它能够计算怎样走去吃食物距离最小。



##### 1.和之前一样，先写好伪代码：（决定蛇行走的方向的函数）

```
Hx,Hy: the position of the head
Fx,Fy: the position of the food

function Where_To_Go_Next(Hx,Hy,Fx,Fy) {

	move[4]={'a','s','d','w'} is the direction that the snake can go
	
	distance[4]={0,0,0,0} is the distance between the food and the snake

	calculate the distance from the head to the food separately
	
	IF Hx-1!=BLANK or Hy!=BLANK THEN
		distance=9999
	ELSE 
		distance=|Fx – (Hx-1)| + |Fy – Hy|

	return the index of the smallest number of distance
	
	return moveable[p]

}
```



##### 2.智能蛇的程序框架

```c
输出字符矩阵
	WHILE not 游戏结束 DO
        wait(time)
		ch＝whereGoNext(Hx,Hy,Fx,Fy)
		CASE ch DO
		‘A’:左前进一步，break 
		‘D’:右前进一步，break    
		‘W’:上前进一步，break    
		‘S’:下前进一步，break    
		END CASE
		输出字符矩阵
	END WHILE
	输出 Game Over!!! 
```



##### 3.c语言实现：

```c
char where_to_move(int Hx,int Hy,int Fx,int Fy) {
	char move[4]={'a','s','d','w'};
	int distance[4]={0,0,0,0};
	int index=0;
	
	if(zone[Hy][Hx-1]==SNAKE_AREA) {
		distance[0]=abs((Fx-(Hx-1)))+abs((Fy-Hy));
	}
	else {
		distance[0]=999;
	}
	
	if(zone[Hy+1][Hx]==SNAKE_AREA) {
		distance[1]=abs(Fx-Hx)+abs(Fy-(Hy+1));
	} 
	else {
		distance[1]=999;
	}
	if(zone[Hy][Hx+1]==SNAKE_AREA) {
		distance[2]=abs(Fx-(Hx+1))+abs(Fy-Hy);
	}
	else {
		distance[2]=999;
	}
	if(zone[Hy-1][Hx]==SNAKE_AREA) {
		distance[3]=abs(Fx-Hx)+abs(Fy-(Hy-1));
	}
	else {
		distance[3]=999;
	}

	
	index=min(distance);
	
	return move[index];
}

int min(const int*distance) {
	int i=0;
	int min=distance[0];
	int index=0;
	
	for(i=1;i<4;i++) {
		if(min>distance[i]&&distance[i]!=999) {
			min=distance[i];
			index=i;
		}
	}
	
	return index;
}
```

![智能蛇.png](https://github.com/beilineili/huangjzmhomework/blob/gh-pages/images/%E6%99%BA%E8%83%BD%E8%9B%87.png?raw=true)

好吧其实这条蛇一点都不智能甚至撞墙了。。



##### ​     在这次作业中我比较大的收获是用虚拟机在linux进行c语言编译和运行，学会了很多新姿势，有些函数在windows系统里是没有的。