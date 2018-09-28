# Bresenham_Line
//C code for Computer Graphics to draw a Bresenham Line
#include<GL/glut.h>
#include<stdio.h>

int xa=0;
int ya=0;
int xb=0;
int yb=0;
void SetPixel(int x, int y);
void bresenham(int xa, int xb, int ya, int yb);

void draw()
{
    glBegin(GL_LINES);
    glColor4f(1.0f,0.0f,0.0f,1.0f);
    glVertex3f(-1000.0f,0.0f,0.0f);
    glVertex3f(1000.0f,0.0f,0.0f);
    glVertex3f(0.0f,1000.0f,0.0f);
    glVertex3f(0.0f,-1000.0f,0.0f);
    glEnd();
    bresenham(xa,xb,ya,yb);
}


void sceneRander()
{
    glClear(GL_COLOR_BUFFER_BIT);
    draw();
    glFlush();
}


void InitGL()
{
    glClearColor(0.0f,0.0f,0.0f,1.0f);
    glOrtho(-100.0f,100.0f,-100.0f,100.0f,-1.0f,1.0f);

}


int main(int a,char **v)
{
    printf("Enter Starting point X1 Y1");
    scanf("%d%d",&xa , &ya);
    printf("Enter Starting point X2 Y2");
    scanf("%d%d",&xb ,&yb);
    glutInit(&a,v);
    glutInitDisplayMode(GLUT_SINGLE|GLUT_RGBA);
    glutCreateWindow("SUBRATA");
    glutInitWindowPosition(100,100);
    glutInitWindowSize(500,350);
    InitGL();
    glutDisplayFunc(sceneRander);
    glutMainLoop();
    return 0;
}

void SetPixel(int x, int y)
{
    glBegin(GL_POINTS);
    glColor4f(0.0f,1.0f,0.0f,1.0f);
    glVertex3i(x,y,0);
    glEnd();
}

void bresenham(int xa,int xb,int ya,int yb)
{
int   m_new = 2 * (yb - ya);
int   slope_error_new = 0;
int x, y;
   for (x = xa, y = ya; x <= xb; x++)
   {
      SetPixel(x,y);

      slope_error_new += m_new;


      if (slope_error_new >= 0)
      {
         y++;
         slope_error_new  -= 2 * (xb - xa);
      }
   }
}

