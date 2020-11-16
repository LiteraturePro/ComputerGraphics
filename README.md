# ComputerGraphics codes


## Exp 1


## Exp 2


## Exp 3


## Exp 4


# JAVA
```Java
import java.awt.*;
import java.applet.*;
public class HelloApplet extends Applet 
{
    public void paint(Graphics g )
    {
        g.drawString("Hello!",10,10);
        g.drawString("Welcome to Applet Programming!",30,30);
     }
}

```
```Html
<!doctype html> 
<html> 
<title>Hello Applet</title>
<Applet code="HelloApplet.class" width=300 height=300 >
</Applet>
</html>


```
```Java
import java.awt.*;
import java.awt.event.*;
import java.applet.Applet;
public class Ex4_1 extends Applet implements ActionListener {
	Label label1 = new Label("+");
	Label label2 = new Label("=");
	TextField field1 = new TextField(6);
	TextField field2 = new TextField(6);
	TextField field3 = new TextField(6);
	Button button1 = new Button("相加");
	public void init() {	//初始化
	add(field1);
	add(label1);
	add(field2);
	add(label2);
	add(field3);
	add(button1);
	button1.addActionListener(this);
	}
	
	public void actionPerformed(ActionEvent e) {
		int x = Integer.parseInt(field1.getText()) + Integer.parseInt(field2.getText());
		field3.setText(Integer.toString(x));
	}
}

```
```Html
<!doctype html> 
<html> 
<title>Hello Applet</title>
<applet codebase="." code="Ex4_1.class" width=360 height=120></applet>
</html>


```
```Java
import java.applet.*;
 import java.awt.*;
 public class LifeCycle extends Applet{
        private int InitCnt;
        private int StartCnt;
        private int StopCnt;
        private int DestroyCnt;
        private int PaintCnt;
        public LifeCycle(){//在init()执行前执行构造函数
               InitCnt = 0;
               StartCnt = 0;
               StopCnt = 0;
               DestroyCnt = 0;
               PaintCnt = 0;
        }
        public void init(){
               resize(320, 240);
               InitCnt++;
        }
        public void destroy(){
               DestroyCnt++;
        }
        public void start(){
               StartCnt++;
        }
        public void stop(){
               StopCnt++;
        }
        public void paint(Graphics g){
               PaintCnt++;
               g.drawLine(20,200,300,200);  //画出坐标轴和标尺
               g.drawLine(20,200,20,20);
               g.drawLine(20,170,15,170);
               g.drawLine(20,140,15,140);
               g.drawLine(20,110,15,110);
               g.drawLine(20,80,15,80);
               g.drawLine(20,50,15,50);
               g.drawString("Init()",25,213);
               g.drawString("Start()",75,213);
               g.drawString("Stop()",125,213);
               g.drawString("Destroy()",175,213);
               g.drawString("paint()",235,213);
               g.fillRect(25,200-InitCnt*30,40,InitCnt*30); //显示各种方法被调用的次数
               g.fillRect(75,200-StartCnt*30,40,StartCnt*30);
               g.fillRect(125,200-StopCnt*30,40,StopCnt*30);
               g.fillRect(175,200-DestroyCnt*30,40,DestroyCnt*30);
               g.fillRect(235,200-PaintCnt*30,40,PaintCnt*30);
        }
 }

```
```Java
import java.awt.; 
import java.applet.; 
public class PicApplet extends Applet 
{ 
       Image pic;
       public void init( )
       { 
           pic=getImage(getCodeBase(),fish.jpg); 
       } 
      public void paint(Graphics g) 
      { 
           g.drawImage(pic,30,30,this);  
      } 
}

```
```Java
import java.awt.*; 
import java.applet.*; 
public class AudioApplet extends Applet 
{ 
       AudioClip audio; //声音对象 
       public void init( )
       { 
           audio=getAudioClip(getCodeBase(),"fire.au"); //获得声音 
       } 
      public void paint(Graphics g) 
      { 
           g.drawString("循环播放声音的Applet小程序",30,30);  
      } 
      public void start( ) 
      {   audio.loop( ); //循环播放声音 
      } 
     public void stop( ) 
     {    audio.stop( ); //停止播放
     } 
}

```
