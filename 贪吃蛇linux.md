```c
#include<stdio.h>
#include<stdlib.h>
#include <stdio.h>
#include <string.h>
#include <sys/time.h>
#include <sys/types.h>
#include <unistd.h>
#include <termios.h>
#include <unistd.h>


#define SNAKE_MAX_LENGTH 20//表示蛇的最大长度 
#define SNAKE_HEAD 'H'//表示蛇头部的符号 
#define SNAKE_BODY 'X'//表示蛇身的符号 
#define SNAKE_AREA ' '//蛇可以活动的区域 
#define WALL_AREA  '*'//表示墙的符号 
#define SNAKE_FOOD '$'//表示食物的符号 




void isgamebegin(); //判断游戏是否开始 

void Printzone(); //打印地图 

void snakemove(int x,int y);//控制蛇移动

void put_food(); //放置食物 
void extent();   //蛇吃食物后变长 

int iswin(int snakeLength); //判断是否胜利 
int isgameover();  //判断游戏是否结束 


     //画出游戏区域 
char zone[12][15]=
    {"*************",
     "*XXXXH      *",
     "*           *",
     "*           *",
     "*           *",
     "*           *",
     "*           *",
     "*           *",
     "*           *",
     "*           *",
     "*           *",
     "*************"
	  };
//蛇头部和身体的坐标 
int snakeX[SNAKE_MAX_LENGTH]={5,4,3,2,1};
int snakeY[SNAKE_MAX_LENGTH]={1,1,1,1,1}; 
int snakeLength=5;


static struct termios ori_attr, cur_attr;

static __inline 
int tty_reset(void)
{
        if (tcsetattr(STDIN_FILENO, TCSANOW, &ori_attr) != 0)
                return -1;

        return 0;
}


static __inline
int tty_set(void)
{
        
        if ( tcgetattr(STDIN_FILENO, &ori_attr) )
                return -1;
        
        memcpy(&cur_attr, &ori_attr, sizeof(cur_attr) );
        cur_attr.c_lflag &= ~ICANON;
//        cur_attr.c_lflag |= ECHO;
        cur_attr.c_lflag &= ~ECHO;
        cur_attr.c_cc[VMIN] = 1;
        cur_attr.c_cc[VTIME] = 0;

        if (tcsetattr(STDIN_FILENO, TCSANOW, &cur_attr) != 0)
                return -1;

        return 0;
}

static __inline
int kbhit(void) 
{
                   
        fd_set rfds;
        struct timeval tv;
        int retval;

        /* Watch stdin (fd 0) to see when it has input. */
        FD_ZERO(&rfds);
        FD_SET(0, &rfds);
        /* Wait up to five seconds. */
        tv.tv_sec  = 0;
        tv.tv_usec = 0;

        retval = select(1, &rfds, NULL, NULL, &tv);
        /* Don't rely on the value of tv now! */

        if (retval == -1) {
                perror("select()");
                return 0;
        } else if (retval)
                return 1;
        /* FD_ISSET(0, &rfds) will be true. */
        else
                return 0;
        return 0;
}

int main()
{
    //设置终端进入非缓冲状态
    int tty_set_flag;
    tty_set_flag = tty_set();
     isgamebegin(); //判断游戏是否开始 
     char ch='d';   //默认第一步的操作 
     put_food();
	 Printzone();
     
	 while(1){ 
     	scanf("%c",&ch);
     	switch(ch){  //通过输入wasd来控制蛇的移动 
     		case 'a':
     			snakemove(-1,0);
     			break;
     		case 's':
     			snakemove(0,1);
     			break;
     		case 'd':
     			snakemove(1,0);
     			break;
     		case 'w':
     			snakemove(0,-1);
     			break;
		 } 
      extent();
      if(iswin(snakeLength)==1){
      	printf("You win!");
      	break;
	  }

      if(isgameover()==0){
        printf("GAME OVER!\n");
        break;
	  } 
}
     printf("pressed `q` to quit!\n");
        while(1) {

                if( kbhit() ) {
                        const int key = getchar();
                        printf("%c pressed\n", key);
                        if(key == 'q')
                                break;
                } else {
                       ;// fprintf(stderr, "<no key detected>\n");
                }
        }

        //恢复终端设置
        if(tty_set_flag == 0) 
                tty_reset();
        return 0;
}
} 


void isgamebegin(){
	char c;
	printf("按回车键以开始贪吃蛇游戏\n");
	while(1)  //输入回车开始游戏 
	{
		if((c=getchar())=='\n')
		{
			break;
		}
	} 
}


void Printzone (){
    int i=0;
    for ( i=0; i<12; i++ ) {
        printf("%s\n", zone[i]);
    }
}


void snakemove(int x,int y){
	int i; 
	zone[snakeY[snakeLength-1]][snakeX[snakeLength-1]]=' '; //蛇原先所在的最后一个位置空出来 
	for(i=snakeLength-1;i>0;i--){   //蛇的所有位置取代它们前一截的身体 
		snakeX[i]=snakeX[i-1];    
		snakeY[i]=snakeY[i-1];
		zone[snakeY[i]][snakeX[i]]='X';
	} 
	snakeX[0]+=x;
	snakeY[0]+=y;
	zone[snakeY[0]][snakeX[0]]='H';  //移动蛇头 
	Printzone();  //重新设置地图 
}


int isgameover(){
	int i;
	for(i=1;i<snakeLength;i++){    //如果碰到自己就输 
	 	if(snakeX[0]==snakeX[i]&&snakeY[0]==snakeY[i])
	 	return 0;}
	if(snakeX[0]==0||snakeX[0]==12||snakeY[0]==0||snakeY[0]==12) {    //如果冲出地图范围也输 
	 return 0;}
	return 1;
}


void put_food(){
		//随机设置食物位置 
	int foodX = rand () % 9;
	int foodY = rand ()  % 9;
	//判断位置是否为空 
	if (zone[foodY][foodX] == ' ') {
		zone[foodY][foodX]='$';
	}
	else	//不为空重新选位置 
		put_food();		

}


void extent(){
	int i=0,j=0,flag=0; //判断还有没有食物 
	for(i;i<12;i++){
		for(j;j<15;j++){
			if(zone[i][j]=='$')
			flag=1;
		}
		j=0;
	}
	if(flag==0){
			put_food();//蛇吃到食物后重置食物位置

		snakeY[snakeLength] = snakeY[snakeLength-1];
		snakeX[snakeLength] = snakeX[snakeLength-1];
		snakeLength ++ ;
	}
}


int iswin(int snakeLength){
	if(snakeLength>=15){
		return 1;
	}
}
```

