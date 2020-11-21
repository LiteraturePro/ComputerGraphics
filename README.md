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
void open() 
{ 
	setviewport(100,100,500,380,1); /* 设置图形窗口区域 */ 
	setcolor(RED); /* 设置作图色 */ 
	rectangle(0,0,399,279); /* 以矩形填充所设的图形窗口区域 */ 
	setfillstyle(SOLID_FILL,7); /* 设置填充方式 */ 
	floodfill(60,60,6); /* 设置填充范围 */ 
	setcolor(8); 
	settextstyle(0,0,1.5); /* 文本字体设置 */ 
	outtextxy(80,80,"Experiment 1 - Line Generation"); /* 输出文本内容 */ 
	settextstyle(0,0,2); 
	outtextxy(160,180,"NJUPT");
	settextstyle(0,0,1); 
	outtextxy(130,200,"by B18150118 YWX"); 
	settextstyle(0,0,1); 
	outtextxy(90,240,"Press any key to continue");  
} 
void main()
{
	int gd=DETECT,gm; /*图形屏幕初始化*/
	initgraph(&gd,&gm,"c:\\turboc3\\bgi");
	open();
	getch(); /* 暂停 */ 
	cleardevice(); /* 图形状态下清屏 */ 
	lineBres(0,0,500,300,YELLOW);
	lineBres(0,0,500,400,BLUE);
	lineBres(0,0,500,500,RED);
	lineBres(0,0,500,200,GREEN);
	lineBres(0,0,500,100,WHITE);
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
void open() 
{ 
	setviewport(100,100,500,380,1); /* 设置图形窗口区域 */ 
	setcolor(RED); /* 设置作图色 */ 
	rectangle(0,0,399,279); /* 以矩形填充所设的图形窗口区域 */ 
	setfillstyle(SOLID_FILL,7); /* 设置填充方式 */ 
	floodfill(60,60,6); /* 设置填充范围 */ 
	setcolor(8); 
	settextstyle(0,0,1); /* 文本字体设置 */ 
	outtextxy(40,80,"Experiment 2 - Generation of Free Curves"); /* 输出文本内容 */ 
	settextstyle(0,0,2); 
	outtextxy(160,180,"NJUPT");
	settextstyle(0,0,1); 
	outtextxy(130,200,"by B18150118 YWX"); 
	settextstyle(0,0,1); 
	outtextxy(90,240,"Press any key to continue"); 
}
void main()
{
	static double p[4][2]={25,200,70,10,200,20,317,210};
    const NO=3;
    int i;
	//初始化绘图
    int driver=DETECT,mode;
    initgraph(&driver,&mode,"c:\\TURBOC3\\BGI");
	//清屏
    cleardevice();
	open();
	getch(); /* 暂停 */ 
	cleardevice(); /* 图形状态下清屏 */
    setcolor(BLUE);
    moveto(p[0][0],p[0][1]);
    for (i=1;i<NO;i++)
		lineto(p[i][0],p[i][1]);
    bezier_3(p); //按ESC、Enter退出
    getch();  //关闭图形
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
void open() 
{ 
	setviewport(100,100,500,380,1); /* 设置图形窗口区域 */ 
	setcolor(RED); /* 设置作图色 */ 
	rectangle(0,0,399,279); /* 以矩形填充所设的图形窗口区域 */ 
	setfillstyle(SOLID_FILL,7); /* 设置填充方式 */ 
	floodfill(60,60,6); /* 设置填充范围 */ 
	setcolor(8); 
	settextstyle(0,0,1); /* 文本字体设置 */ 
	outtextxy(55,80,"Experiment 3 - Geometric Transformation"); /* 输出文本内容 */ 
	settextstyle(0,0,2); 
	outtextxy(160,180,"NJUPT");
	settextstyle(0,0,1); 
	outtextxy(130,200,"by B18150118 YWX"); 
	settextstyle(0,0,1); 
	outtextxy(90,240,"Press any key to continue"); 
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
  cleardevice(); /* 图形状态下清屏 */
  open();
  getch(); /* 暂停 */ 
  closegraph();
  return 0;
}
```

## Exp 4
小车
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
	outtextxy(290,40,"0"); 
	outtextxy(290,400,"6"); 
	outtextxy(108,220,"9"); 
	outtextxy(480,220,"3"); 
	outtextxy(255,180,"NJUPT");// 表盘上显示的字符 // 
	settextstyle(1,0,1);
	outtextxy(250,280,"B18150118");// 表盘上显示的字符 // 
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
void open() 
{ 
	//setviewport(100,100,500,380,1); /* 设置图形窗口区域 */ 
	setviewport(0,0,800,680,1); /* 设置图形窗口区域 */
	setcolor(RED); /* 设置作图色 */ 
	rectangle(0,0,399,279); /* 以矩形填充所设的图形窗口区域 */ 
	setfillstyle(SOLID_FILL,7); /* 设置填充方式 */ 
	floodfill(60,60,6); /* 设置填充范围 */ 
	setcolor(8); 
	settextstyle(0,0,2); /* 文本字体设置 */ 
	outtextxy(80,80,"Experiment 4 - Walking Clock"); /* 输出文本内容 */ 
	settextstyle(0,0,3); 
	outtextxy(260,180,"NJUPT");
	settextstyle(0,0,2); 
	outtextxy(200,260,"by B18150118 YWX"); 
	settextstyle(0,0,2); 
	outtextxy(120,350,"Press any key to continue"); 
} 
void main() 
{
	int x,y; 
	int gd=DETECT,gm; 
	unsigned char h,m,s; 
	struct time t[1]; 
	initgraph(&gd,&gm,"c:\\turboc3\\bgi"); 
	open();
    getch(); /* 暂停 */
	cleardevice(); /* 图形状态下清屏 */
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

游戏打砖
```C

```
卫星
```C

```
流星雨
```C

```
流星雨
```C

```
时钟
```C

```

