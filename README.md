# ComputerGraphics codes


## Exp 1
```C
#include "graphics.h"
#include <conio.h>
#include <math.h>

void lineBres(int x0, int y0, int xEnd, int yEnd,int c)
{
    int dx = fabs (xEnd -x0), dy = fabs (yEnd-y0);
    int p =2* dy-dx;
    int twoDy = 2*dy, twoDyMinusDx = 2* (dy - dx);
    int x,y;
    if (x0>xEnd)
    {
        x=xEnd;
        y=yEnd;
        xEnd=x0;
    }
    else
	{
        x=x0;
        y=y0;
    }
    putpixel (x,y,c);
    while (x<xEnd)
    {
        x++;
        if(p<0)
            p+=twoDy;
        else
		{
            y++;
            p+=twoDyMinusDx;
        }
        putpixel (x,y,c);
    }
}

void main()
{
	int gd=DETECT,gm; /*图形屏幕初始化*/
	initgraph(&gd,&gm,"c:\\turboc3\\bgi");
	lineBres(0,0,500,300,YELLOW);
	lineBres(0,0,500,400,BLUE);
	lineBres(0,0,500,500,RED);
	getch();
 	closegraph();
}
```

## Exp 2
```C
//三次贝塞尔曲线
#include <graphics.h>

//三次贝塞尔曲线绘制函数
void bezier_3(double p[4][2])
{
    double t,t1,t2,xt,yt;
    int rate=200,x,y;
    setcolor(LIGHTRED);
    moveto(p[0][0],p[0][1]);
    for (t=0;t<=1;t+=1.0/rate)
    {
        yt=1-t;
		t1=yt*yt;
		t2=3*yt*t;
        xt=p[0][0]*t1*yt+p[1][0]*t2*yt+p[2][0]*t2*t+p[3][0]*t*t*t;
        yt=p[0][1]*yt*t1+p[1][1]*t2*yt+p[2][1]*t2*t+p[3][1]*t*t*t;
        x=(int)(xt);
        y=(int)(yt);
        lineto(x,y);
    }
}
void main()
{
    //static double p[4][2]={50,400,140,20,400,40,635,420};
	static double p[4][2]={25,200,70,10,200,20,317,210};
    const NO=3;
    int i;
	//初始化绘图
    int driver=DETECT,mode;
    initgraph(&driver,&mode,"c:\\TURBOC3\\BGI");
	//清屏
    cleardevice();
    setcolor(BLUE);
    moveto(p[0][0],p[0][1]);
    for (i=1;i<NO;i++)
		lineto(p[i][0],p[i][1]);
    bezier_3(p);
	//按ESC、Enter退出
    getch();
	//关闭图形
    closegraph();
} 
```

## Exp 3
```C
#include <stdio.h>
#include <graphics.h>
#include <math.h>
int p1_x=540,p1_y=240;
int p2_x=650,p2_y=150;
int p3_x=560,p3_y=120;
void xuanzhuan()
{
	int xz[3][3]={0,1,0,-1,0,0,0,0,1};
	int pos[3][3] ={0,0,1,110,-90,1,20,-120,1}; 
	int i,j,k,sum;
	int ans[3][3];
	for(i=0;i<=2;i++){
	  for(j=0;j<=2;j++){
	    sum = 0;
            for(k=0;k<=2;k++)
              sum = sum + pos[i][k]*xz[k][j];
             ans[i][j] = sum;
	  }
	}
        ans[0][0]+=540;ans[1][0]+=540;ans[2][0]+=540;
        ans[0][1]+=240;ans[1][1]+=240;ans[2][1]+=240;
	line(ans[0][0],ans[0][1],ans[1][0],ans[1][1]);
	line(ans[1][0],ans[1][1],ans[2][0],ans[2][1]);
	line(ans[0][0],ans[0][1],ans[2][0],ans[2][1]);
}
void pingyi()
{
	int pingyi[3][3]={1,0,0,0,1,0,-100,-100,1};
	int pos[3][3] ={540,240,1,650,150,1,560,120,1};
	int i,j,k,sum;
	int ans[3][3];
	for(i=0;i<=2;i++){
	  for(j=0;j<=2;j++){
	    sum = 0;
            for(k=0;k<=2;k++)
              sum = sum + pos[i][k]*pingyi[k][j];
             ans[i][j] = sum;
	  }
	}
	line(ans[0][0],ans[0][1],ans[1][0],ans[1][1]);
	line(ans[1][0],ans[1][1],ans[2][0],ans[2][1]);
	line(ans[0][0],ans[0][1],ans[2][0],ans[2][1]);
}
void draw()
{
	line(p1_x,p1_y,p2_x,p2_y);
	line(p2_x,p2_y,p3_x,p3_y);
	line(p1_x,p1_y,p3_x,p3_y);
}
int main()
{
  int gdriver=DETECT,gmode;
  initgraph(&gdriver,&gmode,"c:\\turboc3\\bgi");
  setcolor(4);
  setbkcolor(0);
  draw();
  xuanzhuan();
  pingyi();
  getch();
  closegraph();
  return 0;
}
```

## Exp 4
小车
```C
#include<stdio.h> 
#include<stdlib.h>
#include<graphics.h> 
void name() 
{ 
	char c1[ ][20]={"Yang WenXuan","B18150118"}; 
	setbkcolor(12); 
	setcolor(15); 
	settextstyle(3,0,4); 
	outtextxy(200,100,c1[0]); 
	outtextxy( 200,200,c1[1]); 
	outtextxy(200,300,"welcome"); 
	getch(); 
	cleardevice(); 
	settextstyle(1,0,10); 
	outtextxy(300,200,"3"); 
	sleep(1); 
	cleardevice(); 
	outtextxy(300,200,"2"); 
	sleep(1); 
	cleardevice(); 
	outtextxy(300,200,"1"); 
	sleep(1); 
} 
void lou1() 
{ 
	setcolor(4); 
	setfillstyle(1,14); 
	bar3d(320,30,410,190,20,1); 
	floodfill(415,150,4); 
	floodfill(400,28,4); 
	rectangle(335,40,350,60); 
	rectangle(335,90,350,110); 
	rectangle(335,140,350,160); 
	rectangle(380,40,395,60); 
	rectangle(380,90,395,110); 
	rectangle(380,140,395,160); 
} 
void lou2() 
{ 
	setfillstyle(1,2); 
	bar3d(120,30,210,190,20,1); 
	floodfill(215,150,4); 
	floodfill(200,28,4); 
	rectangle(135,40,150,60); 
	rectangle(135,90,150,110); 
	rectangle(135,140,150,160); 
	rectangle(180,40,195,60); 
	rectangle(180,90,195,110); 
	rectangle(180,140,195,160); 
} 
void shu() 
{ 
	setfillstyle(1,3); 
	ellipse(265,110,0,360,20,40); 
	floodfill(265,110,4); 
	rectangle(260,120,270,190); 
	floodfill(265,180,4); 
} 
void main() 
{ 
	int i,gdriver=DETECT,gmode,size; 
	int arw[18]={130,210,120,260,100,260,100,300,320,300,320,260,260,260,230,210,130,210}; 
	void *buf; 
	initgraph(&gdriver,&gmode,"c:\\turboc3\\bgi"); 
	name(); 
	setbkcolor(1); 
	cleardevice(); 
	setcolor(4); 
	setlinestyle(0,0,1); 
	setfillstyle(1,9); 
	drawpoly(9,arw); 
	floodfill(200,250,4); 
	rectangle(140,230,170,250); 
	rectangle(200,230,230,250); 
	arc(150,300,180,360,30); 
	floodfill(150,305,4); 
	arc(250,300,180,360,30); 
	floodfill(250,305,4); 
	lou1(); 
	lou2(); 
	shu(); 
	size=imagesize(99,199,321,331); 
	buf=malloc(size); 
	getimage(99,199,321,331,buf); 
	line(0,333,639,333); 
	for(i=0;i<430;i++) 
	{ 
		putimage(100+i,200,buf,COPY_PUT); 
		delay(3000); 
	} 
	cleardevice(); 
	arc(235,280,30,180,10); 
	arc(325,280,0,150,10); 
	arc(280,340,180,360,20); 
	setbkcolor(9); 
	setcolor(15); 
	settextstyle(3,0,5); 
	outtextxy(200,100,"the end"); 
	outtextxy(200,200,"bye-bye"); 
	delay(5000); 
	getch(); 
	closegraph(); 
}
```

游戏打砖
```C
#include "graphics.h" 
#include "stdio.h" 
#include "conio.h" /* 所需的头文件 */ 
int on; /* 声明具有开关作用的全局变量 */ 
static int score; /* 声明静态的记分器变量 */ 
/* 定义开始界面函数 */ 
void open() 
{ 
	setviewport(100,100,500,380,1); /* 设置图形窗口区域 */ 
	setcolor(RED); /* 设置作图色 */ 
	rectangle(0,0,399,279); /* 以矩形填充所设的图形窗口区域 */ 
	setfillstyle(SOLID_FILL,7); /* 设置填充方式 */ 
	floodfill(60,60,6); /* 设置填充范围 */ 
	setcolor(8); 
	settextstyle(0,0,3); /* 文本字体设置 */ 
	outtextxy(80,80,"COME ON BOY"); /* 输出文本内容 */ 
	settextstyle(0,0,1); 
	outtextxy(100,180,"by lcx"); 
	settextstyle(0,0,1); 
	outtextxy(120,240,"Press any key to continue......"); 
} 
/* 定义退出界面函数 */ 
void quitwindow() 
{ 
	char s[100]; /* 声明用于存放字符串的数组 */ 
	setviewport(100,150,540,420,1); 
	setcolor(YELLOW); 
	rectangle(0,0,439,279); 
	setfillstyle(SOLID_FILL,7); 
	floodfill(50,50,14); 
	setcolor(12); 
	settextstyle(0,0,8); 
	outtextxy(120,80,"End"); 
	settextstyle(0,0,2); 
	outtextxy(120,200,"quit? Y/N"); 
	sprintf(s,"Your score is:%d",score);/* 格式化输出记分器的值 */ 
	outtextxy(120,180,s); 
	on=1; /* 初始化开关变量 */ 
} 
/* 主函数 */ 
void main() 
{ 
	int gdriver,gmode; 
	gdriver=DETECT; /*设置图形适配器 */ 
	gmode=VGA; /* 设置图形模式 */ 
	//registerbgidriver(EGAVGA_driver); /* 建立独立图形运行程序 */ 
	initgraph(&gdriver,&gmode,"c:\\turboc3\\bgi"); /* 图形系统初试化 */ 
	setbkcolor(14); 
	open(); /* 调用开始界面函数 */ 
	getch(); /* 暂停 */ 
	while(1) /* 此大循环体控制游戏的反复重新进行 */ 
	{ 
		int driver,mode,l=320,t=400,r,a,b,dl=5,n,x=240,y=400,r1=10,dx=-2,dy=-2;/* 初始化小球相关
		参数 */ 
		int left[100],top[100],right[100],bottom[100],i,j,k,off=1,m,num[100][100];/* 方砖阵列相关参
		数*/ 
		static int pp; 
		static int phrase; /* 一系列起开关作用的变量 */ 
		int oop=1; 
		pp=1; 
		score=0; 
		driver=DETECT; 
		mode=VGA; 
		//registerbgidriver(EGA VGA_driver); 
		initgraph(&driver,&mode,"c:\\turboc3\\bgi"); 
		setbkcolor(10); 
		cleardevice(); /* 图形状态下清屏 */ 
		clearviewport(); /* 清除现行图形窗口内容 */ 
		b=t+6; 
		r=l+60; 
		setcolor(1); 
		rectangle(0,0,639,479); 
		setcolor(4); 
		rectangle(l,t,r,b); 
		setfillstyle(SOLID_FILL,1); 
		floodfill(l+2,t+2,4); 
		for(i=0,k=0;i<=6;i++) /* 此循环绘制方砖阵列 */ 
		{ 
			top[i]=k; 
			bottom[i]=top[i]+20; 
			k=k+21; 
			oop--; 
			for(j=0,m=0;j<=7;j++) 
			{ 
				left[j]=m; 
				right[j]=left[j]+80; 
				m=m+81; 
				setcolor(4); 
				rectangle(left[j],top[i],right[j],bottom[i]); 
				setfillstyle(SOLID_FILL,j+oop); 
				floodfill(left[j]+1,top[i]+1,4); 
				num[i][j]=pp++; 
			} 
		} 
		while(1) /* 此循环控制整个动画 */ 
		{ 
			while(!kbhit()) 
			{ 
				x=x+dx; /* 小球运动的圆心变量控制 */ 
				y=y+dy; 
				if(x+r1>r||x+r1<r) 
				{ 
					phrase=0;
				} 
				if((x-r1<=r||x+r1<=r)&&x+r1>=l) 
				{ 
					if(y<t) 
					phrase=1; 
					if(y+r1>=t&&phrase==1) 
					{
						dy=-dy;y=t-1-r1;
					} 
				} 
				if(off==0) 
					continue; 
				for(i=0;i<=6;i++) /* 此循环用于判断、控制方砖阵列的撞击、擦除 */ 
					for(j=0;j<=7;j++) 
					{ 
						if((x+r1<=right[j]&&x+r1>=left[j])||(x-r1<=right[j]&&x-r1>=left[j])) 
						{ 
							if(( y-r1>top[i]&&y-r1<=bottom[i])||(y+r1>=top[i]&&y+r1<=bottom[i] )) 
							{ 
								if(num[i][j]==0) 
								{
									continue; 
								} 
								setcolor(10); 
								rectangle(left[j],top[i],right[j],bottom[i]); 
								setfillstyle(SOLID_FILL,10); 
								floodfill(left[j]+1,top[i]+1,10); 
								dy=-dy; 
								num[i][j]=0; 
								score=score+10; 
								printf("%d\b\b\b",score); 
							} 
						} 
						if((y+r1>=top[i]&&y+r1<=bottom[i])||(y-r1>=top[i]&&y-r1<=bottom[i])) 
						{ 
							if((x+r1>=left[j]&&x+r1<right[j])||(x-r1<=right[j]&&x-r1>left[j])) 
							{ 
								if(num[i][j]==0) 
								{ 
									continue;
								} 
								setcolor(10); 
								rectangle(left[j],top[i],right[j],bottom[i]); 
								setfillstyle(SOLID_FILL,10); 
								floodfill(left[j]+1,top[i]+1,10); 
								dx=-dx; 
								num[i][j]=0; 
								score=score+10; 
								printf("%d\b\b\b",score); 
							} 
						}
					} 
					if(x+r1>639) /* 控制小球的弹射范围 */ 
					{dx=-dx;x=638-r1;} 
					if(x<=r1) 
					{dx=-dx;x=r1+1;} 
					if(y+r1>=479) 
					{off=0;quitwindow();break;} 
					if(y<=r1) 
					{dy=-dy;y=r1+1;} 
					if(score==560) 
					{off=0;quitwindow();break;} 
					setcolor(6); 
					circle(x,y,r1); 
					setfillstyle(SOLID_FILL,14); 
					floodfill(x,y,6); 
					delay(6000); 
					setcolor(10); 
					circle(x,y,r1); 
					setfillstyle(SOLID_FILL,10); 
					floodfill(x,y,10); 
			} 
			a=getch(); 
			setcolor(10); 
			rectangle(l,t,r,b); 
			setfillstyle(SOLID_FILL,10); 
			floodfill(l+5,t+5,10); 
			if(a==77&&l<=565) /* 键盘控制设定 */ 
			{dl=20;l=l+dl;} 
			if(a==75&&l>=15) 
			{dl=-20;l=l+dl;} 
			if(a=='y'&&on==1) 
			break; 
			if(a=='n'&&on==1) 
			break; 
			if(a==27) 
			{quitwindow();off=0;} 
			r=l+60; 
			setcolor(4); 
			rectangle(l,t,r,b); 
			setfillstyle(SOLID_FILL,1); 
			floodfill(l+5,t+5,4); 
			delay(100); 
		} 
		if(a=='y'&&on==1) /* 是否退出游戏 */ 
		{break;} 
		if(a=='n'&&on==1) 
		{ continue;} 
	}
	closegraph(); 
	getch(); 
}
```
卫星
```C
#include < graphics.h >
#include < stdlib.h >
#include < stdio.h >
#include < conio.h >
#define  IMAGE_SIZE 10 /* 宏定义*/
void  draw_image( int  x,  int  y);  /**/ /* 画飞船函数的说明语句*/
void  Putstar( void );  /**/ /* 画星星函数的说明语句*/
main ()
  {
    int graphdriver=DETECT; /**//* 检测适配器*/
    int graphmode, color; /**//* 最高分辨率的值和色彩的值*/
    void * pt_addr; /**//* 全局变量, 用于存储图像, 定义缓冲区空间*/
    int x,y,maxx,maxy,midy,midx,i; /**//* 定义各变量数据类型*/
    unsigned int size;
	
    initgraph(&graphdriver, &graphmode, "c:\\turboc3\\bgi");
    maxx=getmaxx(); /**//* 取得当前图形方式下允许的x 最大值*/
    maxy=getmaxy(); /**//* 取得当前图形方式下允许的y 最大值*/
    midx=maxx/2;
    x=0; /**//* 定义x 的初始量为0*/
    midy=y=maxy/2;
    setcolor(YELLOW); /**//* 前景颜色设置为黄色*/
    settextstyle(TRIPLEX_FONT, HORIZ_DIR, 4);
    settextjustify(CENTER_TEXT, CENTER_TEXT);
    outtextxy(midx, 400, "WELCOME ON TO NJUPT");
    setbkcolor(BLACK); /**//* 背景颜色设置函数, 用法和setcolor相同*/
    setcolor(RED);
    setlinestyle(SOLID_LINE, 0, THICK_WIDTH);
    ellipse(midx, midy, 130, 50, 160, 30);
    setlinestyle(SOLID_LINE, 0, NORM_WIDTH);
    draw_image(x, y); /**//* 画飞船*/
    size=imagesize (x, y- IMAGE_SIZE, x+(4*IMAGE_SIZE), y+
        IMAGE_SIZE);
    pt_addr=malloc(size);
    getimage (x, y - IMAGE_SIZE, x +(4*IMAGE_SIZE), y +IMAGE_SIZE, pt_addr);
    Putstar(); /**//* 画星*/
    setcolor(WHITE); /**//* 前景颜色为白色*/
    setlinestyle(SOLID_LINE, 0, NORM_WIDTH);
    rectangle(0, 0, maxx, maxy); /**//* 画矩形框*/
    while(! kbhit())
    {
        Putstar();
        setcolor(RED);
        setlinestyle(SOLID_LINE, 0, THICK_WIDTH);
        ellipse(midx, midy, 130, 50, 160, 30); /**//* 画一个围绕地球的
                                               光环*/
        setcolor(BLACK);
        ellipse(midx, midy, 130, 50, 160, 30);
        for(i=0; i<=13; i++)
        {
            setcolor(i%2==0?LIGHTBLUE:BLACK); /**//*I 的值不同时选
                                              择的颜色也不同*/
            ellipse(midx, midy, 0, 360, 100, 100- 8*i); /**//* 画地球*/
            setcolor(LIGHTBLUE);
            ellipse(midx, midy, 0, 360, 100- 8*i, 100);
        }
        putimage (x, y- IMAGE_SIZE, pt_addr, XOR_PUT); /**//* 恢复
                                                       原先的画面*/
        x=x>=maxx?0:x+6;
        putimage(x, y- IMAGE_SIZE, pt_addr, XOR_PUT); /**//* 在另
                                                      一位置显示飞船*/
    }
    free(pt_addr); /**//* 释放缓冲区空间*/
    closegraph();
    return;
}
 void  draw_image( int  x,  int  y)
  {
    int arw[11];
    arw[0]=x+10; arw[1]=y- 10; arw[2]=x+34; arw[3]=y- 6;
    arw[4]=x+34; arw[5]=y+6; arw[6]=x+10; arw[7]=y+10;
    arw[9]=x+10; arw[10]=y- 10;
    moveto(x+10, y- 4);
    setcolor(14);
    setfillstyle(1, 4);
    linerel(- 3*10, - 2*8);
    moveto(x+10, y+4);
    linerel(- 3*10, +2*8);
    moveto(x+10, y);
    linerel(- 3*10, 0);
    setcolor(3);
    setfillstyle(1, LIGHTBLUE);
    fillpoly(4, arw);
}
 void  Putstar( void )
  {
    int seed=1858;
    int i, dotx, doty, h, w, color, maxcolor;
    maxcolor=getmaxcolor();
    w=getmaxx();
    h=getmaxy();
    srand(seed);
    for(i=0; i<250; ++i)
    {dotx=i+random(w- 1);
    doty=i+random(h- 1);
    color=random(maxcolor);
    setcolor(color);
    putpixel(dotx, doty, color);
    circle(dotx+1, doty+1, 1); }
    srand(seed);
}
```
流星雨
```C
/* Note:Y our choice is C IDE */ 
#include "stdio.h"
#include "stdlib.h"  
#include "graphics.h" 
void main() 
{ 
	int size,size2,i,size3,size4; 
	void *buffer,*buffer2,*buffer3,*buffer4; 
	int driver=DETECT,mode; 
	initgraph(&driver,&mode,"c:\\turboc3\\bgi"); 
	setcolor(15); 
	rectangle(0,280,639,479); 
	setfillstyle(0,1); 
	floodfill(1,290,15); 
	setcolor(15); 
	arc(10,0,270,360,10); 
	arc(30,0,180,270,10); 
	arc(10,20,0,90,10); 
	arc(30,20,90,180,10); 
	setfillstyle(1,14); 
	floodfill(20,10,15);/*xingxing*/ 
	setcolor(12); 
	circle(30,400,15); 
	line(30,415,10,435); 
	line(30,415,50,435); 
	line(20,425,20,460); 
	line(40,425,40,465);/*ren*/ 
	circle(70,400,15); 
	line(70,415,50,435); 
	line(70,415,100,435); 
	line(60,425,60,460); 
	line(80,425,80,465); 
	setcolor(15); 
	arc(10,70,270,360,10); 
	arc(30,70,180,270,10); 
	arc(10,90,0,90,10); 
	arc(30,90,90,180,10); 
	setfillstyle(1,14); 
	floodfill(20,80,15); 
	setcolor(15); 
	arc(110,0,270,360,10); 
	arc(130,0,180,270,10); 
	arc(110,20,0,90,10); 
	arc(130,20,90,180,10); 
	setfillstyle(1,0); 
	floodfill(120,110,15); 
	size=imagesize(9,0,31,21); 
	buffer=malloc(size); 
	getimage(9,0,31,21,buffer); 
	size2=imagesize(109,0,131,21); 
	buffer2=malloc(size2); 
	getimage(109,0,131,21,buffer2); 
	size3=imagesize(1,383,101,475); 
	buffer3=malloc(size3); 
	getimage(1,383,101,475,buffer3); 
	size4=imagesize(4,69,31,91); 
	buffer4=malloc(size4); 
	getimage(4,69,31,91,buffer4); 
	do 
	{ 
		putimage(20,30,buffer2,0); 
		delay(10000); 
		putimage(20,30,buffer,0); 
		delay(100000000); 
		putimage(20,30,buffer2,0); 
		delay(10000); 
		putimage(20,30,buffer,0); 
		delay(10000000); 
		putimage(220,130,buffer2,0); 
		delay(10000); 
		putimage(220,130,buffer,0); 
		delay(10000000); 
		putimage(210,100,buffer2,0); 
		delay(10000); 
		putimage(210,100,buffer,0); 
		delay(100000000); 
		putimage(150,90,buffer2,0); 
		delay(10000); 
		putimage(150,90,buffer,0); 
		delay(10000000 ); 
		putimage(350,70,buffer2,0); 
		delay(10000); 
		putimage(350,70,buffer,0); 
		delay(100000000); 
		putimage(300,100,buffer2,0); 
		delay(10000); 
		putimage(300,100,buffer,0); 
		delay(100000000); 
		putimage(500,40,buffer2,0); 
		delay(10000); 
		putimage(500,40,buffer,0); 
		delay(10000000); 
		putimage(600,20,buffer2,0); 
		delay(10000); 
		putimage(600,20,buffer,0); 
		delay(100000000); 
	}while(!kbhit()); 
	for(i=0;i<100 ;i+=10) 
	{ 
		putimage(9+i,384-i,buffer3,0); 
		delay(10000); 
	} 
	getch(); 
	getch(); 
	do 
	{ 
		for(i=0;i<100;i++) 
		{ 
			putimage(10+i+i+i+i+i+i,30+i,buffer4,0); 
			delay(100); 
			putimage(30+i+i ,70+i,buffer4,0); 
			delay(10000); 
		} 
	} while(!kbhit()); 
	cleardevice(); 
	for(i=0;i<680;i++) 
	{ 
		setfillstyle(1,12); 
		floodfill(1,1,15); 
		rectangle(0,0,3+i,479+i); 
		delay(1000); 
		setfillstyle(1,12); 
		floodfill(638,1,15); 
		rectangle(637-i,0,639,479); 
		delay(1000); 
	} 
	setcolor(4); 
	settextstyle(1,0,14); 
	outtextxy(100,100,"WE WILL BE TOGETHER FOR EVER!!!!!!!!"); 
	getch(); 
	getch(); 
	getch(); 
	setcolor(9); 
	cleardevice(); 
	for(i=0;i<400;i++) 
	{ 
		circle(320,240,i++); 
		delay(1000); 
	} 
	getch(); 
	cleardevice(); 
	setbkcolor(15); 
	setcolor(4); 
	for(i=0;i<400;i++) 
	{ 
		arc(0,0,270,360,i); 
		arc(0,480,0,90,i); 
		arc(640,480,90,180,i); 
		arc(639,0,180,270,i); 
		delay(1000); 
	} 
	getch(); 
	cleardevice(); 
	setcolor(4); 
	setbkcolor(12); 
	outtextxy(100,100,"Zhu Zhang Lao Shi : Wan Shi ru yi"); 
	getch(); 
	outtextxy(100,150," Xin Xiang Shi Cheng "); 
	getch(); 
	outtextxy(100,200," Xiao Kou Chang Kai ");
	getch(); 
	outtextxy(100,250," yi sheng ping an "); 
	getch(); 
	outtextxy(100,300,"zui hou dui ni de jiao dao "); 
	getch(); 
	outtextxy(100,350," biao shi zheng xin de xie yi "); 
	getch(); 
	closegraph(); 
}
```
流星雨
```C
#include<graphics.h>
#include<stdio.h>
#include<conio.h>
#include<math.h>
#include<stdlib.h>
void beijing1();
void beijing2();
void main()
{
	
	int gdriver=DETECT,gmode;
	int x1=100,y1=110,x2=10,y2=15,x3=20,y3=50,x4=70,y4=40,size,*buf;
    initgraph(&gdriver,&gmode,"c:\\turboc3\\bgi");
	cleardevice();
	setbkcolor(BLACK);
    beijing1();
    
	while(!(kbhit()))
	{
	    beijing2();
		delay(1000);
		setcolor(15);
		circle(x1,y1,2);
		setfillstyle(1,15);
		floodfill(x1,y1,15);
		
		setcolor(15);
		circle(x2,y2,2);
		setfillstyle(1,15);
		floodfill(x2,y2,15);
		
		setcolor(15);
		circle(x3,y3,2);
		setfillstyle(1,15);
		floodfill(x3,y3,15);
		
		setcolor(15);
		circle(x4,y4,2);
		setfillstyle(1,15);
		floodfill(x4,y4,15);

		size=imagesize(x1-2,y1-2,x1+2,y1+2);
		size=imagesize(x2-2,y2-2,x2+2,y2+2);
		size=imagesize(x3-2,y3-2,x3+2,y3+2);
		size=imagesize(x4-2,y4-2,x4+2,y4+2);

		buf=(int *)malloc(size);
		getimage(x1-2,y1-2,x1+2,y1+2,buf);
		putimage(x1-2,y1-2,buf,1);
		getimage(x2-2,y2-2,x2+2,y2+2,buf);
		putimage(x2-2,y2-2,buf,1);
		getimage(x3-2,y3-2,x3+2,y3+2,buf);
		putimage(x3-2,y3-2,buf,1);
		getimage(x4-2,y4-2,x4+2,y4+2,buf);
		putimage(x4-2,y4-2,buf,1);

		x1=x1+6;
		y1=y1+2;
		x2=x2+6;
		y2=y2+2;
		x3=x3+6;
		y3=y3+2;
		x4=x4+6;
		y4=y4+2;
		putimage(x1-2,y1-2,buf,1);
		putimage(x2-2,y2-2,buf,1);
		putimage(x3-2,y3-2,buf,1);
		putimage(x4-2,y4-2,buf,1);
		free(buf);
    
		while(y1!=480)
		{
			delay(7500);
			getimage(x1-2,y1-2,x1+2,y1+2,buf);
			putimage(x1-2,y1-2,buf,1);
			getimage(x2-2,y2-2,x2+2,y2+2,buf);
			putimage(x2-2,y2-2,buf,1);
			getimage(x3-2,y3-2,x3+2,y3+2,buf);
			putimage(x3-2,y3-2,buf,1);
			getimage(x4-2,y4-2,x4+2,y4+2,buf);
			putimage(x4-2,y4-2,buf,1);
			x1=x1+6;
			y1=y1+2;
			x2=x2+6;
			y2=y2+2;
			x3=x3+6;
			y3=y3+2;
			x4=x4+6;
			y4=y4+2;
			putimage(x1-2,y1-2,buf,1);
			putimage(x2-2,y2-2,buf,1);
			putimage(x3-2,y3-2,buf,1);
			putimage(x4-2,y4-2,buf,1);
			free(buf);
		}
		getch();
		break;
	}	
}
void beijing1()
{
    setbkcolor(0);
    cleardevice();
    setcolor(2);
    line(110,270,140,310);
    line(110,270,80,310);
	line(80,310,140,310);

    line(110,310,170,360);
    line(110,310,50,360);
    line(50,360,170,360);

    line(110,360,210,400);
    line(110,360,10,400);
    line(10,400,210,400);
    rectangle(100,400,130,440);
    setfillstyle(1,2);
    floodfill(110,280,2);
    floodfill(110,320,2);
    floodfill(110,380,2);
    floodfill(110,420,2);

    setcolor(15);
    circle(250,320,20);
    line(250,340,250,400);
    line(210,380,250,360);
    line(290,380,250,360);
    line(250,400,200,440);
    line(250,400,300,440);
    setfillstyle(1,15);
    floodfill(250,320,15);

    setcolor(0);
    circle(260,310,2);
    circle(262,332,3);

    setcolor(15);
    circle(320,320,20);
    line(320,340,320,400);
    line(280,380,320,360);
    line(360,380,320,360);
    line(320,400,270,440);
    line(320,400,370,440);
    setfillstyle(1,15);
    floodfill(320,320,15);

    setcolor(0);
    circle(330,310,2);
    circle(332,332,3);

    setcolor(14);
    arc(580,60,60,300,20);
    arc(600,60,120,240,20);
    setfillstyle(1,14);
    floodfill(570,60,14);

}
void beijing2()
{
	int i,j;
    int x[200],y[200];
    int flag;
    
	for(i=1;i<=200;i++)
	{
		x[i]=(int)(random(640));
		y[i]=(int)(random(150));
		putpixel(x[i],y[i],3);
	}
	for(j=1;!kbhit();j++)
	{
		for(i=1;i<200;i+=2)
		{
			setcolor(3);
			fillellipse(x[i]+1,y[i],i%2,i%2);
		}

		for(i=1;i<=200;i+=2)
		{
			flag=random(100)%2;
			if(flag)
			{
				setcolor(15);
				fillellipse(x[i]+1,y[i],i%1+1,i%1+1);
			}
			else
			{
				setcolor(3);
				fillellipse(x[i]+1,y[i],i%1,i%1);
			}  
		}
	}
}
```
时钟
```C
#include<graphics.h>
#include<math.h> 
#include<dos.h> // 包含了三个头文件 graphics.h ，math.h，dos.h 
#define pi 3.1415926 // 定义参数 pi 用 3.1415926 表示
#define X(a,b,c) x=a*cos((b*c)*pi/180-pi/2)+300; // 定义 X(a,b,c) 
#define Y(a,b,c) y=a*sin((b*c)*pi/180-pi/2)+240; // 定义 Y(a,b,c) 
#define d(a,b,c) X(a,b,c);Y(a,b,c);line(300,240,x,y) // 定义 d(a,b,c) 
void init() 
{	int i,l,x1,x2,y1,y2; // 定义参数 i,l,x1,x2,y1,y2 
	setbkcolor(0); // 调用 setbkcolor 函数 ，用指定的颜色值来设置当前的背景色
	setcolor(1); 
	circle(300,240,205); 
	setcolor(5); 
	circle(300,240,208);// 表盘内外圈圆颜色及大小 // 
	setcolor(8); 
	circle(300,240,5); 
	setcolor(7); 
	circle(300,240,3);// 表心两圆圈颜色及大小 // 
	setcolor(250);// 表盘上字符的颜色 // 
	settextstyle(1,0,4); 
	outtextxy(290,40,"A"); 
	outtextxy(290,400,"6"); 
	outtextxy(108,220,"9"); 
	outtextxy(480,220,"3"); 
	outtextxy(260,180,"apple");// 表盘上显示的字符 // 
	setcolor(250); 
	for(i=0;i<60;i++) 
	{
		if(i%5==0)
		{
			setcolor(44);
			setlinestyle(0,0,3); 
			l=6;
		}// 整点分隔符颜色
		else 
		{
			setcolor(25);
			setlinestyle(0,0,1);
			l=6;
		}// 分钟分隔符 25// 
		x1=200*cos(i*6*pi/180)+300; 
		y1=200*sin(i*6*pi/180)+240; 
		x2=(200-l)*cos(i*6*pi/180)+300; 
		y2=(200-l)*sin(i*6*pi/180)+240; 
		line(x1,y1,x2,y2); 
	} 
} 
void main() 
{
	int x,y; 
	int gd=DETECT,gm; 
	unsigned char h,m,s; 
	struct time t[1]; 
	initgraph(&gd,&gm,"c:\\turboc3\\bgi"); 
	init(); 
	setwritemode(1); 
	gettime(t); 
	h=t[0].ti_hour; 
	m=t[0].ti_min; 
	s=t[0].ti_sec; 
	setcolor(55);// 时针颜色 // 
	d(140,(h*30+m*0.5),1);// 时针长度 // 
	setcolor(44);// 分针颜色 // 
	d(170,m,6);// 分针长度 // 
	setcolor(33);// 秒针颜色 // 
	d(190,s,6);// 秒针长度 // 
	while(!kbhit()) 
	{
		while(t[0].ti_sec==s) 
		gettime(t); 
		sound(400); 
		delay(70); 
		sound(200); 
		delay(30); 
		nosound(); 
		setcolor(33);// 秒针覆盖色 // 
		d(190,s,6); 
		s=t[0].ti_sec; 
		d(190,s,6); 
		if (t[0].ti_min!=m) 
		{ 
			setcolor(44);// 分针的覆盖色 // 
			d(170,m,6); 
			m=t[0].ti_min; 
			d(170,m,6); 
		} 
		if (t[0].ti_hour!=h) 
		{ 
			setcolor(55);// 时针覆盖色 // 
			if(m!=60)
				d(150,(h*30+m*0.5),1); 
			d(150,(h*30),1); 
			h=t[0].ti_hour; 
			if(m!=60) 
				d(150,(h*30+m*0.5),1); 
			d(150,(h*30),1); 
			sound(1000); 
			delay(240); 
			nosound(); 
			delay(140); 
			sound(2000); 
			delay(240); 
			nosound(); 
		} 
	} 
	getch(); 
	closegraph(); 
}
```
