# 2022graphics
```c
#include <GL/glut.h>
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT );

    glColor3f(1,1,0);
    glBegin(GL_TRIANGLES);
                glColor3f(1.0f, 0.0f, 0.0f);   glVertex2f(0.0f,   1.0f);
                glColor3f(0.0f, 1.0f, 0.0f);   glVertex2f(0.87f,  -0.5f);
                glColor3f(0.0f, 0.0f, 1.0f);   glVertex2f(-0.87f, -0.5f);

            glEnd();
   // glutSolidTeapot(0.3);///
    glutSwapBuffers();
}
int main(int argc,char**argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("week03");

    glutDisplayFunc( display );

    glutMainLoop();
    return 0;
}
```

```c
#include <GL/glut.h>
void display()
{
    glClear ( GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT );

    glColor3f(1,1,0);
    glutSolidTeapot(0.3);

    glutSwapBuffers();
}
int main(int argc,char**argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("week03的視窗");

    glutDisplayFunc( display );

    glutMainLoop();
    return 0;
}
```
這個是4個紅色茶壺
```c
void myTeapot(float x,float y)
{


    glPushMatrix();
        glTranslatef(x,y,0);
        glutSolidTeapot(0.3);
    glPopMatrix();

}
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glColor3f(1,0,0);
    myTeapot(+0.5, +0.5);
    myTeapot(+0.5, -0.5);
    myTeapot(-0.5, -0.5);
    myTeapot(-0.5, +0.5);

    glutSwapBuffers();
}
int main(int argc,char**argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("HW2 bonus");

    glutDisplayFunc( display );

    glutMainLoop();
    return 0;
}
```
這個是用滑鼠畫圖
```C
#include <GL/glut.h>
#include <stdio.h>
int mouseX=0,mouseY=0,N=0;
int mx[100],my[100];
void display()
{
        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
        glColor3f(1,0,0);
        glBegin(GL_LINE_LOOP);
        for(int i=0;i<N;i++){

            glVertex2f((mx[i]-150)/150.0 ,-(my[i]-150)/150.0);
}
        glEnd();
        glutSwapBuffers();

}
void mouse(int button, int state, int x,int y)
{
    //printf("%d %d %d %d\n", button , state , x , y);
    mouseX=x;mouseY=y;
    if(state==GLUT_DOWN){
        printf("     glVertex2f( (%d-150/150.0, -(%d-150)/150.0);\n", x,y);
        N++;
        mx[N-1]=x; my[N-1]=y;
    }
}
int main(int argc,char**argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("week04 mouse");

    glutDisplayFunc( display );
    glutMouseFunc(mouse);
    glutMainLoop();
}
```
下面這個是用滑鼠畫圖(新的)
```c
#include <GL/glut.h>
float angle=0, oldX=0;
void display()
{
    glClear( GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT );
    glPushMatrix();
    glRotatef(angle,0,0,1);
    glColor3f(1,1,0);
    glutSolidTeapot(0.3);
    glPopMatrix();
    glutSwapBuffers();
}
void mouse(int button,int state,int x,int y)
{
    oldX=x;
}
void motion(int x,int y)
{
    angle+=(x-oldX);
    oldX=x;
    display();
}
int main(int argc,char**argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("week05 Rotate");
    glutDisplayFunc(display);
    glutMouseFunc(mouse);
    glutMotionFunc(motion);
    glutMainLoop();
    return 0;
}
```
這是可以用滑鼠順順的畫圖
```c
#include <GL/glut.h>
#include <stdio.h>
int N=0;
int x[1000],y[1000];
void display()
{
        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
        glBegin(GL_LINE_LOOP);
        for(int i=0;i<N;i++){

            glVertex2f((x[i]-150)/150.0 ,-(y[i]-150)/150.0);
}
        glEnd();
        glutSwapBuffers();

}
void motion(int mouseX,int mouseY)
{
  // if(state==GLUT_DOWN){
        N++;
        x[N-1]=mouseX;
        y[N-1]=mouseY;
        printf("現在按下滑鼠,得到一個新的坐標 %d %d\n", x[N-1],y[N-1]);
 //   }
    display();
}
int main(int argc,char**argv)
{
    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("week04 mouse");

    glutDisplayFunc( display );
    glutMotionFunc(motion);
    glutMainLoop();
}
```
這是一個可以用把滑鼠放在圖中 然後用鍵盤按出座標的城市碼
```c
#include <GL/glut.h>
#include <stdio.h>
float x=0, y=0,z=0,oldX,oldY;
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT );
    glPushMatrix();
        glTranslatef( (x-150)/150.0 , -(y-150)/150.0, z);

        glColor3f(1,1,0);
        glutSolidTeapot(0.3);
    glPopMatrix();
    glutSwapBuffers();
}
void keyboard (unsigned char key, int x, int y)
{
        printf("現在按下:%c 座標在: %x %x\n" ,key,x,y);
}
void mouse(int button, int state,int mouseX,int mouseY)
{
    oldX = mouseX; oldY = mouseY;
}
void motion (int mouseX,int mouseY)
{
    x += (mouseX-oldX);
    y += (mouseY-oldY);
    oldX = mouseX; oldY=mouseY;
    display();
}
int main(int argc , char**argv)
{

    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutCreateWindow("week06 keyboard");

    glutDisplayFunc( display );
    glutKeyboardFunc(keyboard);
    glutMouseFunc(mouse);
    glutMotionFunc(motion);
    glutMainLoop();
    return 0;
}

```
下面這個是可以旋轉移動縮放跟用鍵盤按座標的茶壺的程式碼
```c
#include <GL/glut.h>
#include <stdio.h>
float x=250, y=250,z=0,scale=1.0,angle=0.0,oldX,oldY;
int now=1;
void display()
{
    glClearColor(0.5,0.5,0.5,1);
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT );
    glPushMatrix();
        glTranslatef( (x-250)/250.0 , -(y-250)/250.0, z);
        glRotatef(angle, 0,0,1);
        glScalef(scale,scale,scale);
        glColor3f(1,1,0);
        glutSolidTeapot(0.3);
    glPopMatrix();
    glutSwapBuffers();
}
void keyboard (unsigned char key, int mouseX, int mouseY)
{
        printf("現在按下:%c 座標在: %x %x\n" ,key,mouseX,mouseY);
        if(key=='w' || key =='W') now=1;
        if(key=='e' || key =='E') now=2;
        if(key=='r' || key =='R') now=3;
}
void mouse(int button, int state,int mouseX,int mouseY)
{
    oldX = mouseX; oldY = mouseY;
}
void motion (int mouseX,int mouseY)
{
    if(now==1){
        x += (mouseX-oldX);
        y += (mouseY-oldY);
    }else if(now==2){
        angle += (mouseX-oldX);
    }else if(now==3){
        if( mouseX>oldX ) scale = scale *1.01;
        if( mouseX<oldX ) scale = scale *0.99;
    }
    oldX = mouseX; oldY=mouseY;
    display();
}
int main(int argc , char**argv)
{

    glutInit(&argc,argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_DEPTH);
    glutInitWindowSize(500,500);
    glutCreateWindow("week06 keyboard mouse motion");

    glutDisplayFunc( display );
    glutKeyboardFunc(keyboard);
    glutMouseFunc(mouse);
    glutMotionFunc(motion);
    glutMainLoop();
    return 0;
}

```
