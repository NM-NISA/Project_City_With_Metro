#include <iostream>
#include<windows.h>
#include<stdio.h>
#include<GL/glut.h>
#include<math.h>
#define pi 3.142857
#include<iostream>
using namespace std;

void circle(GLfloat rx,GLfloat ry,GLfloat cx,GLfloat cy)///radius_x,radius_y,centre_position_x,centre_position_y///
{
    glBegin(GL_TRIANGLE_FAN);
    glVertex2f(cx,cy);
    for(int i=0; i<=360; i++)
    {
        float angle = 3.1416f * i/180;
        float x = rx * cosf(angle);
        float y = ry * sinf(angle);
        glVertex2f((x+cx),(y+cy));
    }
    glEnd();
}

float metroSpeed = 0.9f;

bool isDay = true;
bool metroStop = false;
char scenario = '0'; // Current scenario: '0' for cover, '1', '2', '3' for scenarios
float h= -250;
float v= -100;
float p = -10;
int i= -700;
float j= -250;
float k= -100;
float a= -100;
float b= -100;
float c= 800;
float d= 850;

void renderBitmapString(float x, float y, float z, void *font, char *string)
{
    char *c;
    glRasterPos3f(x, y, z);
    for (c=string; *c != '\0'; c++)
    {
        glutBitmapCharacter(font, *c);
    }
}

void display() {
    glClear(GL_COLOR_BUFFER_BIT);

    if (scenario == '0') {

    /// Cover
    glBegin(GL_QUADS);
    glColor3f(0.18f, 0.46f, 0.96f);
    glVertex2f(0, 0);
    glVertex2f(800, 0);
    glColor3f(0.18f, 0.26f, 0.36f);
    glVertex2f(800, 800);
    glVertex2f(0, 800);
    glEnd();

    // Set text color to white
    glColor3f(1.0f, 1.0f, 1.0f);

    renderBitmapString(250, 670, 0, GLUT_BITMAP_HELVETICA_18, " 02389 - COMPUTER GRAPHICS [M]");

    glPushMatrix();
    renderBitmapString(270, 640, 0, GLUT_BITMAP_HELVETICA_18, "CITY WITH METRO TRAIN");
    glLoadIdentity();
    glPopMatrix();

    renderBitmapString(250, 490, 0, GLUT_BITMAP_HELVETICA_18, "Submitted by - ");
    renderBitmapString(250, 460, 0, GLUT_BITMAP_HELVETICA_18, "ID                                 Name");
    renderBitmapString(250, 430, 0, GLUT_BITMAP_HELVETICA_18, "23-51392-1                Nusrat Mazumder Nisa");
    renderBitmapString(250, 400, 0, GLUT_BITMAP_HELVETICA_18, "23-51375-1                Dilruba Akter Reshmi");
    renderBitmapString(250, 370, 0, GLUT_BITMAP_HELVETICA_18, "22-47752-2                Shehab Shahariar Asif");
    renderBitmapString(250, 340, 0, GLUT_BITMAP_HELVETICA_18, "22-47344-2                Md. Raihan Karim");

    renderBitmapString(305, 220, 0, GLUT_BITMAP_HELVETICA_18, "Submitted to");
    renderBitmapString(290, 190, 0, GLUT_BITMAP_HELVETICA_18, "NOBORANJAN DEY");
    renderBitmapString(273, 160, 0, GLUT_BITMAP_HELVETICA_12, "FACULTY OF SCIENCE & TECHNOLOGY");
    renderBitmapString(279, 130, 0, GLUT_BITMAP_HELVETICA_10, "American International University-Bangladesh");

    }
     else if (scenario == '1') {
        // Scenario 1
    glBegin(GL_QUADS);    // Upper Part
    glColor3ub(150, 150, 255);
    glVertex2f(800,800);
    glVertex2f(0,800);
    glVertex2f(0,450);
    glVertex2f(800,450);
    glEnd();
    glBegin(GL_QUADS);     // Lower part
    glColor3ub(165, 165, 255);
    glVertex2f(0,0);
    glVertex2f(800,0);
    glVertex2f(800,450);
    glVertex2f(0,450);
    glEnd();

    /// Rail Track
    glBegin(GL_QUADS);   //
    glColor3ub(80, 80, 80);
    glVertex2f(580,0);
    glVertex2f(708,0);
    glVertex2f(303,450);
    glVertex2f(255,450);
    glEnd();
    glBegin(GL_QUADS);   // light gray
    glColor3ub(150, 150, 150);
    glVertex2f(585,0);
    glVertex2f(715,0);
    glVertex2f(308,450);
    glVertex2f(257,450);
    glEnd();
    glBegin(GL_QUADS);    // black
    glColor3ub(0, 0, 0);
    glVertex2f(595,0);
    glVertex2f(705,0);
    glVertex2f(303,450);
    glVertex2f(262,450);
    glEnd();
    glBegin(GL_QUADS);     // dark gray
    glColor3ub(50, 50, 50);
    glVertex2f(600,0);
    glVertex2f(700,0);
    glVertex2f(300,450);
    glVertex2f(265,450);
    glEnd();
    glBegin(GL_QUADS);    // gray
    glColor3ub(80, 80, 80);
    glVertex2f(660,0);
    glVertex2f(670,0);
    glVertex2f(285,450);
    glVertex2f(280,450);
    glEnd();
    glBegin(GL_QUADS);   //
    glColor3ub(40, 40, 40);
    glVertex2f(655,0);
    glVertex2f(660,0);
    glVertex2f(280,450);
    glVertex2f(277,450);
    glEnd();

    /// Back side wall
    glBegin(GL_QUADS);   // light blue
    glColor3ub(195, 195, 255);
    glVertex2f(255,500);
    glVertex2f(0,500);
    glVertex2f(0,450);
    glVertex2f(255,450);
    glEnd();

    /// Right side wall
    glBegin(GL_QUADS);   // bluish gray
    glColor3ub(100, 100, 150);
    glVertex2f(247,500);
    glVertex2f(255,500);
    glVertex2f(800,910);
    glVertex2f(800,930);
    glEnd();
    glBegin(GL_QUADS);   // Light bluish gray
    glColor3ub(200, 200, 220);
    glVertex2f(255,490);
    glVertex2f(255,500);
    glVertex2f(800,910);
    glVertex2f(800,880);
    glEnd();
    glBegin(GL_QUADS);   //
    glColor3ub(100, 100, 225);
    glVertex2f(308,450);
    glVertex2f(308,527);
    glVertex2f(750,845);
    glVertex2f(715,0);
    glEnd();
    glBegin(GL_QUADS);   // Light bluish gray
    glColor3ub(200, 200, 220);
    glVertex2f(308,522);
    glVertex2f(308,455);
    glVertex2f(750,10);
    glVertex2f(750,790);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);   //
    glColor3ub(100, 100, 225);
    glVertex2f(680,50);
    glVertex2f(680,750);
    glVertex2f(630,110);
    glVertex2f(630,730);
    glVertex2f(580,160);
    glVertex2f(580,700);
    glVertex2f(530,210);
    glVertex2f(530,670);
    glVertex2f(480,260);
    glVertex2f(480,640);
    glVertex2f(430,320);
    glVertex2f(430,610);
    glVertex2f(380,370);
    glVertex2f(380,570);
    glVertex2f(340,420);
    glVertex2f(340,545);
    glEnd();
    glBegin(GL_QUADS);   // Light 1
    glColor3ub(255, 255, 150);
    glVertex2f(685,762);
    glVertex2f(682,782);
    glVertex2f(665,772);
    glVertex2f(668,752);
    glEnd();
    glLineWidth(3);
    glBegin(GL_LINES);
    glColor3ub(115, 115, 115);
    glVertex2f(685,762);
    glVertex2f(682,782);
    glEnd();
    glBegin(GL_QUADS);   // Light 2
    glColor3ub(255, 255, 150);
    glVertex2f(655,742);
    glVertex2f(652,762);
    glVertex2f(635,752);
    glVertex2f(638,732);
    glEnd();
    glLineWidth(3);
    glBegin(GL_LINES);
    glColor3ub(115, 115, 115);
    glVertex2f(655,742);
    glVertex2f(652,762);
    glEnd();
    glBegin(GL_QUADS);   // Light 3
    glColor3ub(255, 255, 150);
    glVertex2f(625,722);
    glVertex2f(622,742);
    glVertex2f(605,732);
    glVertex2f(608,712);
    glEnd();
    glLineWidth(3);
    glBegin(GL_LINES);
    glColor3ub(115, 115, 115);
    glVertex2f(625,722);
    glVertex2f(622,742);
    glEnd();
    glBegin(GL_QUADS);   // Light 4
    glColor3ub(255, 255, 150);
    glVertex2f(595,702);
    glVertex2f(592,722);
    glVertex2f(575,712);
    glVertex2f(578,692);
    glEnd();
    glLineWidth(3);
    glBegin(GL_LINES);
    glColor3ub(115, 115, 115);
    glVertex2f(595,702);
    glVertex2f(592,722);
    glEnd();

    /// Ceiling
    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 225);
    glVertex2f(227,500);
    glVertex2f(740,940);
    glVertex2f(200,500);
    glVertex2f(680,940);
    glVertex2f(170,500);
    glVertex2f(620,940);
    glVertex2f(140,500);
    glVertex2f(560,940);
    glVertex2f(110,500);
    glVertex2f(500,940);
    glVertex2f(80,500);
    glVertex2f(440,940);
    glVertex2f(50,500);
    glVertex2f(380,940);
    glVertex2f(20,500);
    glVertex2f(320,940);
    glVertex2f(-10,500);
    glVertex2f(260,940);
    glVertex2f(-40,500);
    glVertex2f(200,940);
    glVertex2f(-70,500);
    glVertex2f(140,940);
    glVertex2f(-100,500);
    glVertex2f(80,940);
    glVertex2f(-130,500);
    glVertex2f(20,940);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 225);
    glVertex2f(0,515);
    glVertex2f(267,515);
    glVertex2f(0,535);
    glVertex2f(292,535);
    glVertex2f(0,555);
    glVertex2f(319,555);
    glVertex2f(0,575);
    glVertex2f(344,575);
    glVertex2f(0,605);
    glVertex2f(383,605);
    glVertex2f(0,635);
    glVertex2f(422,635);
    glVertex2f(0,675);
    glVertex2f(472,675);
    glVertex2f(0,715);
    glVertex2f(524,715);
    glVertex2f(0,755);
    glVertex2f(575,755);
    glEnd();

    /// Floor
    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 225);
    glVertex2f(227,450);
    glVertex2f(540,0);
    glVertex2f(200,450);
    glVertex2f(490,0);
    glVertex2f(170,450);
    glVertex2f(420,0);
    glVertex2f(140,450);
    glVertex2f(360,0);
    glVertex2f(110,450);
    glVertex2f(300,0);
    glVertex2f(80,450);
    glVertex2f(240,0);
    glVertex2f(50,450);
    glVertex2f(180,0);
    glVertex2f(20,450);
    glVertex2f(120,0);
    glVertex2f(-10,450);
    glVertex2f(60,0);
    glVertex2f(-40,450);
    glVertex2f(0,0);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 225);
    glVertex2f(0,435);
    glVertex2f(267,435);
    glVertex2f(0,415);
    glVertex2f(282,415);
    glVertex2f(0,395);
    glVertex2f(295,395);
    glVertex2f(0,375);
    glVertex2f(308,375);
    glVertex2f(0,345);
    glVertex2f(331,345);
    glVertex2f(0,315);
    glVertex2f(353,315);
    glVertex2f(0,275);
    glVertex2f(382,275);
    glVertex2f(0,235);
    glVertex2f(411,235);
    glVertex2f(0,195);
    glVertex2f(440,195);
    glVertex2f(0,155);
    glVertex2f(469,155);
    glVertex2f(0,115);
    glVertex2f(497,115);
    glVertex2f(0,75);
    glVertex2f(526,75);
    glVertex2f(0,35);
    glVertex2f(556,35);
    glEnd();

    // Left side pillar 1......Back
    glBegin(GL_QUADS);
    glColor3ub(145, 145, 245);
    glVertex2f(0,375);
    glVertex2f(0,555);
    glVertex2f(125,555);
    glVertex2f(125,375);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(100, 100, 235);
    glVertex2f(135,395);
    glVertex2f(135,535);
    glVertex2f(125,555);
    glVertex2f(125,375);
    glEnd();
    glLineWidth(3);   //
    glBegin(GL_LINES);
    glColor3ub(105, 105, 155);
    glVertex2f(0,375);
    glVertex2f(125,375);
    glEnd();
    glLineWidth(3);   //
    glBegin(GL_LINES);
    glColor3ub(105, 105, 155);
    glVertex2f(125,375);
    glVertex2f(135,395);
    glEnd();
    // Map
    glBegin(GL_QUADS);    // Off-white
    glColor3ub(242, 242, 242);
    glVertex2f(75,420);
    glVertex2f(75,520);
    glVertex2f(115,520);
    glVertex2f(115,420);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);   // Border
    glColor3ub(202, 140, 0);
    glVertex2f(75,420);
    glVertex2f(115,420);
    glVertex2f(75,520);
    glVertex2f(115,520);
    glVertex2f(115,420);
    glVertex2f(115,520);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);   // Red
    glColor3ub(212, 0, 0);
    glVertex2f(105,510);
    glVertex2f(105,495);
    glVertex2f(98,495);
    glVertex2f(105,495);
    glEnd();
    glPointSize(3);
    glBegin(GL_POINTS);
    glColor3ub(212, 0, 0);
    glVertex2f(105,510);
    glVertex2f(105,495);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);   // Blue
    glColor3ub(0, 0, 155);
    glVertex2f(98,495);
    glVertex2f(91,495);
    glVertex2f(98,495);
    glVertex2f(98,470);
    glVertex2f(91,470);
    glVertex2f(98,470);
    glVertex2f(91,470);
    glVertex2f(91,450);
    glVertex2f(96,440);
    glVertex2f(91,450);
    glVertex2f(96,430);
    glVertex2f(96,440);
    glEnd();
    glPointSize(3);
    glBegin(GL_POINTS);
    glColor3ub(0, 0, 155);
    glVertex2f(98,495);
    glVertex2f(98,483);
    glVertex2f(98,470);
    glVertex2f(91,470);
    glVertex2f(91,460);
    glVertex2f(96,440);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);   // Green
    glColor3ub(0, 155, 0);
    glVertex2f(91,450);
    glVertex2f(86,440);
    glVertex2f(86,430);
    glVertex2f(86,440);
    glVertex2f(91,495);
    glVertex2f(86,505);
    glEnd();
    glPointSize(3);
    glBegin(GL_POINTS);
    glColor3ub(0, 155, 0);
    glVertex2f(91,450);
    glVertex2f(86,440);
    glVertex2f(91,495);
    glVertex2f(86,505);
    glEnd();
    // Left side pillar 2......Front
    glBegin(GL_QUADS);
    glColor3ub(185, 185, 245);
    glVertex2f(0,275);
    glVertex2f(0,605);
    glVertex2f(75,605);
    glVertex2f(75,275);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(100, 100, 235);
    glVertex2f(85,295);
    glVertex2f(85,585);
    glVertex2f(75,605);
    glVertex2f(75,275);
    glEnd();
    glLineWidth(4);   //
    glBegin(GL_LINES);
    glColor3ub(105, 105, 155);
    glVertex2f(0,275);
    glVertex2f(75,275);
    glEnd();
    glLineWidth(4);   //
    glBegin(GL_LINES);
    glColor3ub(105, 105, 155);
    glVertex2f(85,295);
    glVertex2f(75,275);
    glEnd();

    glLineWidth(1);   // Banner 1
    glBegin(GL_LINES);
    glColor3ub(0, 105, 0);
    glVertex2f(95,610);
    glVertex2f(95,640);
    glVertex2f(155,610);
    glVertex2f(155,640);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 105, 0); ///
    glVertex2f(95,610);
    glVertex2f(95,570);
    glVertex2f(156,570);
    glVertex2f(156,610);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(225, 225, 225);
    glVertex2f(95,610);
    glVertex2f(95,570);
    glVertex2f(115,570);
    glVertex2f(115,610);
    glEnd();
    glPointSize(20);   ///
    glBegin(GL_POINTS);
    glColor3ub(0, 165, 0);
    glVertex2f(105,590);
    glEnd();
    glColor3ub(225, 0, 0);
    circle(2.5,5,105,590);

    glColor3ub(255, 255, 255);
    glRasterPos2i(120,590);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'M');
    glColor3ub(255, 255, 255);
    glRasterPos2i(126,590);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'i');
    glColor3ub(255, 255, 255);
    glRasterPos2i(128,590);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'r');
    glColor3ub(255, 255, 255);
    glRasterPos2i(131,590);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'p');
    glColor3ub(255, 255, 255);
    glRasterPos2i(134,590);
     glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'u');
    glColor3ub(255, 255, 255);
    glRasterPos2i(138,590);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'r');
    glColor3ub(255, 255, 255);
    glRasterPos2i(142,590);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,' ');
     glColor3ub(255, 255, 255);
    glRasterPos2i(145,590);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'1');
    glColor3ub(255, 255, 255);
    glRasterPos2i(149,590);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'0');
    // End

    glLineWidth(1);   // Banner 2
    glBegin(GL_LINES);
    glColor3ub(0, 105, 0);
    glVertex2f(150,560);
    glVertex2f(150,540);
    glVertex2f(190,560);
    glVertex2f(190,540);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(225, 225, 225); ///
    glVertex2f(150,515);
    glVertex2f(150,540);
    glVertex2f(190,540);
    glVertex2f(190,515);
    glEnd();
    glLineWidth(1);   // Black line
    glBegin(GL_LINES);
    glColor3ub(0, 0, 0);
    glVertex2f(150,515);
    glVertex2f(190,515);
    glEnd();

    glColor3ub(0, 0, 0);
    glRasterPos2i(156,525);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'<');
    glColor3ub(0, 0, 0);
    glRasterPos2i(156,525);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'-');
    glColor3ub(0, 0, 0);
    glRasterPos2i(158,525);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'-');
    glColor3ub(0, 0, 0);
    glRasterPos2i(160,525);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'-');
    glColor3ub(0, 0, 0);
    glRasterPos2i(167,525);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,' ');
    glColor3ub(0, 0, 0);
    glRasterPos2i(169,525);
     glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'E');
    glColor3ub(0, 0, 0);
    glRasterPos2i(174,525);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'x');
    glColor3ub(0, 0, 0);
    glRasterPos2i(178,525);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'i');
    glColor3ub(0, 0, 0);
    glRasterPos2i(182,525);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'t');


    // Metro Train
    glBegin(GL_QUADS);    // Body
    glColor3ub(255, 255, 255);
    glVertex2f(255,450);
    glVertex2f(255,500);
    glVertex2f(520,600);
    glVertex2f(520,100);
    glEnd();
    // Front Part
    glBegin(GL_QUADS);
    glColor3ub(255, 255, 255);
    glVertex2f(520,150);
    glVertex2f(520,600);
    glVertex2f(630,600);
    glVertex2f(630,150);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 87);  // Sea Green
    glVertex2f(255,495);
    glVertex2f(255,500);
    glVertex2f(520,600);
    glVertex2f(520,555);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 87);  // Sea Green
    glVertex2f(630,350);
    glVertex2f(630,600);
    glVertex2f(520,600);
    glVertex2f(520,350);
    glEnd();
    glBegin(GL_POLYGON);
    glColor3ub(155, 0, 0);  // Red
    glVertex2f(520,100);
    glVertex2f(510,150);
    glVertex2f(510,180);
    glVertex2f(630,180);
    glVertex2f(630,150);
    glVertex2f(620,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(155, 0, 0);  // Red
    glVertex2f(560,180);
    glVertex2f(560,195);
    glVertex2f(590,195);
    glVertex2f(590,180);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(125, 125, 125);  // Light gray
    glVertex2f(550,175);
    glVertex2f(550,160);
    glVertex2f(600,160);
    glVertex2f(600,175);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(65, 65, 65);  // Gray.... lines
    glVertex2f(550,171);
    glVertex2f(600,171);
    glVertex2f(550,167);
    glVertex2f(600,167);
    glVertex2f(550,163);
    glVertex2f(600,163);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0,0,0);     // Black..... Light
    glVertex2f(560,100);
    glVertex2f(560,130);
    glVertex2f(590,130);
    glVertex2f(590,100);
    glEnd();
    glColor3ub(145,145,145);
    circle(5,10,570,110);
    glColor3ub(145,145,145);
    circle(5,10,582,110);
    glLineWidth(6);
    glBegin(GL_LINES);
    glColor3ub(35, 35, 35);  // Gray
    glVertex2f(560,127);
    glVertex2f(590,127);
    glVertex2f(560,100);
    glVertex2f(560,130);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(65,65,65);    // Window
    glVertex2f(530,400);
    glVertex2f(530,550);
    glVertex2f(620,550);
    glVertex2f(620,400);
    glEnd();
    glLineWidth(3);
    glBegin(GL_LINES);   // Border
    glColor3ub(0, 0, 0);
    glVertex2f(530,400);
    glVertex2f(620,400);
    glVertex2f(530,550);
    glVertex2f(620,550);
    glVertex2f(530,400);
    glVertex2f(530,550);
    glVertex2f(620,400);
    glVertex2f(620,550);
    glVertex2f(560,400);
    glVertex2f(560,550);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0,0,0);    // Heading
    glVertex2f(530,560);
    glVertex2f(530,580);
    glVertex2f(620,580);
    glVertex2f(620,560);
    glEnd();
    glColor3ub(255, 255, 0);
    glRasterPos2i(541,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'U');
    glColor3ub(255, 255, 0);
    glRasterPos2i(546,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'T');
    glColor3ub(255, 255, 0);
    glRasterPos2i(550,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'T');
    glColor3ub(255, 255, 0);
    glRasterPos2i(554,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'A');
    glColor3ub(255, 255, 0);
    glRasterPos2i(558,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'R');
    glColor3ub(255, 255, 0);
    glRasterPos2i(563,570);
     glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'A');
    glColor3ub(255, 255, 0);
    glRasterPos2i(569,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'-');
    glColor3ub(255, 255, 0);
    glRasterPos2i(575,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'M');
    glColor3ub(255, 255, 0);
    glRasterPos2i(581,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'O');
    glColor3ub(255, 255, 0);
    glRasterPos2i(585,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'T');
    glColor3ub(255, 255, 0);
    glRasterPos2i(589,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'I');
    glColor3ub(255, 255, 0);
    glRasterPos2i(592,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'J');
    glColor3ub(255, 255, 0);
    glRasterPos2i(595,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'H');
    glColor3ub(255, 255, 0);
    glRasterPos2i(600,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'E');
    glColor3ub(255, 255, 0);
    glRasterPos2i(604,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'E');
    glColor3ub(255, 255, 0);
    glRasterPos2i(609,570);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'L');
    glBegin(GL_POLYGON);  //
    glColor3ub(0,125,0);
    glVertex2f(565,215);
    glVertex2f(565,245);
    glVertex2f(585,245);
    glVertex2f(585,215);
    glEnd();
    glColor3ub(225, 0, 0);
    circle(5,10,575,230);
    // Lights
    glColor3ub(195, 195, 195);  // ......1...
    circle(5,10,535,230);
    glColor3ub(245, 245, 245);
    circle(4,8,535,230);
    glColor3ub(105, 105, 105);
    circle(3,6,535,230);
    glColor3ub(245, 245, 245);
    circle(2,4,535,230);
    glColor3ub(195, 195, 195);  // ......2...
    circle(5,10,615,230);
    glColor3ub(245, 245, 245);
    circle(4,8,615,230);
    glColor3ub(105, 105, 105);
    circle(3,6,615,230);
    glColor3ub(245, 245, 245);
    circle(2,4,615,230);
    glColor3ub(195, 195, 195);  // ......3...
    circle(5,10,550,215);
    glColor3ub(245, 245, 245);
    circle(4,8,550,215);
    glColor3ub(105, 105, 105);
    circle(3,6,550,215);
    glColor3ub(245, 245, 245);
    circle(2,4,550,215);
    glColor3ub(195, 195, 195);  // ......4...
    circle(5,10,600,215);
    glColor3ub(245, 245, 245);
    circle(4,8,600,215);
    glColor3ub(105, 105, 105);
    circle(3,6,600,215);
    glColor3ub(245, 245, 245);
    circle(2,4,600,215);
    glLineWidth(2);
    glBegin(GL_LINES);
    glColor3ub(105, 105, 105);
    glVertex2f(555,200);
    glVertex2f(555,350);
    glVertex2f(530,350);
    glVertex2f(530,200);
    glVertex2f(555,200);
    glVertex2f(530,200);
    glEnd();
    // .... End ....
    // Doors ..............1...
    glBegin(GL_QUADS);
    glColor3ub(105,105,105);
    glVertex2f(460,210);
    glVertex2f(460,515);
    glVertex2f(440,514);
    glVertex2f(440,230);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0,0,0);  // Window
    glVertex2f(457,390);
    glVertex2f(457,485);
    glVertex2f(443,485);
    glVertex2f(443,395);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);   // Border
    glColor3ub(0, 0, 0);
    glVertex2f(460,210);
    glVertex2f(460,515);
    glVertex2f(440,514);
    glVertex2f(440,230);
    glVertex2f(460,210);
    glVertex2f(440,230);
    glVertex2f(460,515);
    glVertex2f(440,514);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);   // Partition
    glColor3ub(195, 0, 0);
    glVertex2f(450,220);
    glVertex2f(450,513);
    glEnd();
    // Doors ..............2...
    glBegin(GL_QUADS);
    glColor3ub(105,105,105);
    glVertex2f(395,285);
    glVertex2f(395,505);
    glVertex2f(380,504);
    glVertex2f(380,305);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0,0,0);  // Window
    glVertex2f(392,415);
    glVertex2f(392,480);
    glVertex2f(383,480);
    glVertex2f(383,420);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);   // Border
    glColor3ub(0, 0, 0);
    glVertex2f(395,285);
    glVertex2f(395,505);
    glVertex2f(380,504);
    glVertex2f(380,305);
    glVertex2f(395,285);
    glVertex2f(380,305);
    glVertex2f(395,505);
    glVertex2f(380,504);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);   // Partition
    glColor3ub(195, 0, 0);
    glVertex2f(387.5,295);
    glVertex2f(387.5,503);
    glEnd();
    // Doors ..............3...
    glBegin(GL_QUADS);
    glColor3ub(105,105,105);
    glVertex2f(345,345);
    glVertex2f(345,495);
    glVertex2f(335,494);
    glVertex2f(335,360);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0,0,0);  // Window
    glVertex2f(343,435);
    glVertex2f(343,480);
    glVertex2f(337,480);
    glVertex2f(337,440);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);   // Border
    glColor3ub(0, 0, 0);
    glVertex2f(345,345);
    glVertex2f(345,495);
    glVertex2f(335,494);
    glVertex2f(335,360);
    glVertex2f(345,345);
    glVertex2f(335,360);
    glVertex2f(345,495);
    glVertex2f(335,494);
    glEnd();
    glLineWidth(1.5);
    glBegin(GL_LINES);   // Partition
    glColor3ub(195, 0, 0);
    glVertex2f(340,355);
    glVertex2f(340,493);
    glEnd();
    // Doors ..............4...
    glBegin(GL_QUADS);
    glColor3ub(105,105,105);
    glVertex2f(315,385);
    glVertex2f(315,490);
    glVertex2f(308,489);
    glVertex2f(308,395);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0,0,0);  // Window
    glVertex2f(313,440);
    glVertex2f(313,475);
    glVertex2f(309,475);
    glVertex2f(309,445);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);   // Border
    glColor3ub(0, 0, 0);
    glVertex2f(315,385);
    glVertex2f(315,490);
    glVertex2f(308,489);
    glVertex2f(308,395);
    glVertex2f(315,385);
    glVertex2f(308,395);
    glVertex2f(315,490);
    glVertex2f(308,489);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);   // Partition
    glColor3ub(195, 0, 0);
    glVertex2f(311,391);
    glVertex2f(311,488);
    glEnd();
    // Doors ..............5...
    glBegin(GL_QUADS);
    glColor3ub(105,105,105);
    glVertex2f(293,410);
    glVertex2f(293,490);
    glVertex2f(288,489);
    glVertex2f(288,418);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0,0,0);  // Window
    glVertex2f(292,450);
    glVertex2f(292,475);
    glVertex2f(289,475);
    glVertex2f(289,455);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);   // Border
    glColor3ub(0, 0, 0);
    glVertex2f(293,410);
    glVertex2f(293,490);
    glVertex2f(288,489);
    glVertex2f(288,418);
    glVertex2f(293,410);
    glVertex2f(288,418);
    glVertex2f(293,490);
    glVertex2f(288,489);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);   // Partition
    glColor3ub(195, 0, 0);
    glVertex2f(290.5,416);
    glVertex2f(290.5,488);
    glEnd();
    // Doors ..............6...
    glBegin(GL_QUADS);
    glColor3ub(105,105,105);
    glVertex2f(278,430);
    glVertex2f(278,490);
    glVertex2f(274,489);
    glVertex2f(274,436);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0,0,0);  // Window
    glVertex2f(277,458);
    glVertex2f(277,478);
    glVertex2f(275,478);
    glVertex2f(275,463);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);   // Border
    glColor3ub(0, 0, 0);
    glVertex2f(278,430);
    glVertex2f(278,490);
    glVertex2f(274,489);
    glVertex2f(274,436);
    glVertex2f(278,430);
    glVertex2f(274,436);
    glVertex2f(278,490);
    glVertex2f(274,489);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);   // Partition
    glColor3ub(195, 0, 0);
    glVertex2f(276,436);
    glVertex2f(276,488);
    glEnd();
    // Doors ..............7...
    glBegin(GL_QUADS);
    glColor3ub(105,105,105);
    glVertex2f(266,442);
    glVertex2f(266,490);
    glVertex2f(263,489);
    glVertex2f(263,446);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0,0,0);  // Window
    glVertex2f(265.5,463);
    glVertex2f(265.5,478);
    glVertex2f(263.5,478);
    glVertex2f(263.5,468);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);   // Border
    glColor3ub(0, 0, 0);
    glVertex2f(266,442);
    glVertex2f(266,490);
    glVertex2f(263,489);
    glVertex2f(263,446);
    glVertex2f(266,442);
    glVertex2f(263,446);
    glVertex2f(266,490);
    glVertex2f(263,489);
    glEnd();
    glLineWidth(0.5);
    glBegin(GL_LINES);   // Partition
    glColor3ub(195, 0, 0);
    glVertex2f(264.5,446);
    glVertex2f(264.5,488);
    glEnd();
    // Doors ..............8...
    glBegin(GL_QUADS);
    glColor3ub(105,105,105);
    glVertex2f(258,452);
    glVertex2f(258,490);
    glVertex2f(256,489);
    glVertex2f(256,456);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0,0,0);  // Window
    glVertex2f(257.5,468);
    glVertex2f(257.5,478);
    glVertex2f(256.5,478);
    glVertex2f(256.5,473);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);   // Border
    glColor3ub(0, 0, 0);
    glVertex2f(258,452);
    glVertex2f(258,490);
    glVertex2f(256,489);
    glVertex2f(256,456);
    glVertex2f(258,452);
    glVertex2f(256,456);
    glVertex2f(258,490);
    glVertex2f(256,489);
    glEnd();
    glLineWidth(0.5);
    glBegin(GL_LINES);   // Partition
    glColor3ub(195, 0, 0);
    glVertex2f(257,456);
    glVertex2f(257,488);
    glEnd();
    // Windows.....1...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(510,355);
    glVertex2f(510,485);
    glVertex2f(490,485);
    glVertex2f(490,365);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(510,355);
    glVertex2f(510,440);
    glVertex2f(490,445);
    glVertex2f(490,365);
    glEnd();
    // Windows.....2...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(485,365);
    glVertex2f(485,485);
    glVertex2f(465,485);
    glVertex2f(465,375);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(485,365);
    glVertex2f(485,440);
    glVertex2f(465,445);
    glVertex2f(465,375);
    glEnd();
    // Windows.....3...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(435,380);
    glVertex2f(435,480);
    glVertex2f(420,479);
    glVertex2f(420,390);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(435,380);
    glVertex2f(435,435);
    glVertex2f(420,442);
    glVertex2f(420,390);
    glEnd();
    // Windows.....4...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(415,390);
    glVertex2f(415,478);
    glVertex2f(400,479);
    glVertex2f(400,400);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(415,390);
    glVertex2f(415,435);
    glVertex2f(400,442);
    glVertex2f(400,400);
    glEnd();
    // Windows.....5...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(375,405);
    glVertex2f(375,478);
    glVertex2f(365,479);
    glVertex2f(365,415);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(375,405);
    glVertex2f(375,435);
    glVertex2f(365,442);
    glVertex2f(365,415);
    glEnd();
    // Windows.....6...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(360,415);
    glVertex2f(360,478);
    glVertex2f(350,479);
    glVertex2f(350,425);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(360,415);
    glVertex2f(360,440);
    glVertex2f(350,447);
    glVertex2f(350,425);
    glEnd();
    // Windows.....7...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(330,427);
    glVertex2f(330,478);
    glVertex2f(325,479);
    glVertex2f(325,432);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(330,427);
    glVertex2f(330,445);
    glVertex2f(325,452);
    glVertex2f(325,432);
    glEnd();
    // Windows.....8...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(322,435);
    glVertex2f(322,478);
    glVertex2f(317,479);
    glVertex2f(317,440);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(322,435);
    glVertex2f(322,450);
    glVertex2f(317,457);
    glVertex2f(317,440);
    glEnd();
    // Windows.....9...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(305,440);
    glVertex2f(305,478);
    glVertex2f(301,479);
    glVertex2f(301,445);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(305,440);
    glVertex2f(305,455);
    glVertex2f(301,460);
    glVertex2f(301,445);
    glEnd();
    // Windows.....10...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(299,448);
    glVertex2f(299,478);
    glVertex2f(295,479);
    glVertex2f(295,453);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(299,448);
    glVertex2f(299,458);
    glVertex2f(295,465);
    glVertex2f(295,453);
    glEnd();
    // Windows.....11...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(286,453);
    glVertex2f(286,478);
    glVertex2f(283,479);
    glVertex2f(283,458);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(286,453);
    glVertex2f(286,463);
    glVertex2f(283,467);
    glVertex2f(283,458);
    glEnd();
    // Windows.....12...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(282,457);
    glVertex2f(282,478);
    glVertex2f(279,479);
    glVertex2f(279,462);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(282,457);
    glVertex2f(282,468);
    glVertex2f(279,471);
    glVertex2f(279,462);
    glEnd();
    // Windows.....13...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(272,460);
    glVertex2f(272,478);
    glVertex2f(270,479);
    glVertex2f(270,463);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(272,460);
    glVertex2f(272,469);
    glVertex2f(270,472);
    glVertex2f(270,463);
    glEnd();
    // Windows.....14...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(269,463);
    glVertex2f(269,478);
    glVertex2f(267,479);
    glVertex2f(267,468);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(269,463);
    glVertex2f(269,473);
    glVertex2f(267,475);
    glVertex2f(267,468);
    glEnd();
    // Windows.....15...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(262,468);
    glVertex2f(262,478);
    glVertex2f(260.5,479);
    glVertex2f(260.5,471);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(262,468);
    glVertex2f(262,475);
    glVertex2f(260.5,477);
    glVertex2f(260.5,471);
    glEnd();
    // Windows.....15...
    glBegin(GL_QUADS);
    glColor3ub(46, 139, 127);
    glVertex2f(260,469);
    glVertex2f(260,478);
    glVertex2f(258.5,479);
    glVertex2f(258.5,472);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(36, 119, 107);
    glVertex2f(260,469);
    glVertex2f(260,475);
    glVertex2f(258.5,477);
    glVertex2f(258.5,472);
    glEnd();
    /// End Train

    } else if (scenario == '2') {
        // Scenario 2
        if (isDay) {
        // Day background
        glBegin(GL_QUADS);
        glColor3ub(255, 255, 147);   // Light Yellow
        glVertex2f(0,100);
        glVertex2f(800,100);
        glColor3ub(102, 204, 255);   // Light Blue
        glVertex2f(800,800);
        glVertex2f(0,800);
        glEnd();

        glColor3ub(253, 183, 77);    ///.........S U N.....................///
        circle(18,36,400,705);
        glColor3ub(253, 183, 77);
        circle(16.5,33,400,705);
        glColor3ub(253, 183, 77);
        circle(14.5,30,400,705);
        glColor3ub(253, 183, 77);
        circle(12.5,27,400,705);


        glColor3ub(232,241,255);        ///....Cloud.......1 covering sun....///
        circle(13,20,400,665);
        glColor3ub(252,254,255);
        circle(11,18,400,665);

        glColor3ub(232,241,255);
        circle(10,20,410,675);
        glColor3ub(252,254,255);
        circle(10,20,412,672);

        glColor3ub(232,241,255);
        circle(13,20,410,655);

        glColor3ub(221,229,247);
        circle(9,20,420,680);
        glColor3ub(252,254,255);
        circle(8,18,420,679);

        glColor3ub(232,241,255);
        circle(9,20,420,650);
        glColor3ub(252,254,255);
        circle(8,18,420,652);

        glColor3ub(221,229,247);
        circle(9,20,430,685);
        glColor3ub(252,254,255);
        circle(8,18,430,683);

        glColor3ub(232,241,255);
        circle(9,20,425,655);
        glColor3ub(252,254,255);
        circle(8,18,435,657);

        glColor3ub(232,241,255);
        circle(9,20,440,675);

        glColor3ub(221,229,247);
        circle(8,18,445,665);
        glColor3ub(252,254,255);
        circle(8,18,443,663);
        glColor3ub(252,254,255);
        circle(18,18,420,664);
        glColor3ub(252,254,255);
        circle(18,25,417,665);

    }
    else {
        // Night background
        glBegin(GL_QUADS);
        glColor3ub(102, 204, 255);   // Light Blue
        glVertex2f(0,100);
        glVertex2f(800,100);
        glColor3ub(25, 25, 112); // Dark Blue
        glVertex2f(800,800);
        glVertex2f(0,800);
        glEnd();

        glPointSize(1.5f);

        // Stars
        glBegin(GL_POINTS);
        glColor3ub(255, 255, 255); // White
        glVertex2f(100,700);
        glVertex2f(200,700);
        glVertex2f(250,660);
        glVertex2f(400,660);
        glVertex2f(100,780);
        glVertex2f(200,780);
        glVertex2f(250,680);
        glVertex2f(400,680);
        glVertex2f(700,700);
        glVertex2f(700,780);
        glVertex2f(750,780);
        glVertex2f(500,680);
        glVertex2f(600,700);
        glVertex2f(550,780);
        glVertex2f(450,660);
        glVertex2f(450,750);
        glVertex2f(800,780);
        glVertex2f(650,720);
        glVertex2f(750,700);
        glVertex2f(800,700);
        glVertex2f(420,750);
        glVertex2f(330,750);
        glVertex2f(230,780);
        glVertex2f(180,780);
        glVertex2f(150,780);
        glVertex2f(50,780);
        glVertex2f(20,720);
        glVertex2f(80,750);
        glVertex2f(840,780);
        glVertex2f(620,720);
        glVertex2f(780,700);
        glVertex2f(520,780);
        glVertex2f(480,680);
        glVertex2f(410,750);
        glVertex2f(420,780);
        glVertex2f(680,720);
        glVertex2f(780,760);
        glVertex2f(380,760);
        glVertex2f(150,780);
        glVertex2f(270,740);
        glVertex2f(290,730);
        glVertex2f(480,740);
        glVertex2f(840,770);
        glVertex2f(590,790);
        glVertex2f(710,770);
        glVertex2f(520,760);
        glVertex2f(460,680);
        glVertex2f(410,760);
        glVertex2f(430,740);
        glVertex2f(180,730);
        glVertex2f(280,730);
        glVertex2f(360,710);
        glVertex2f(150,710);
        glVertex2f(50,710);
        glVertex2f(60,760);
        glVertex2f(90,750);
        glVertex2f(810,730);
        glVertex2f(645,790);
        glVertex2f(677,790);
        glVertex2f(770,760);
        glVertex2f(210,730);
        glVertex2f(140,750);
        glVertex2f(110,730);
        glVertex2f(60,720);
        glVertex2f(30,760);
        glVertex2f(10,730);
        glVertex2f(780,735);
        glVertex2f(730,765);
        glVertex2f(790,730);
        glVertex2f(130,710);
        glVertex2f(225,780);
        glVertex2f(255,690);
        glVertex2f(655,720);
        glVertex2f(770,775);
        glEnd();

        // Moon
        glColor3ub(255, 255, 147);    ///.........Full Moon.....................///
        circle(18,36,400,705);
        glColor3ub(255, 255, 147);
        circle(16.5,33,400,705);
        glColor3ub(255, 255, 147);
        circle(14.5,30,400,705);
        glColor3ub(255, 255, 147);
        circle(12.5,27,400,705);

    }

    /// ........Store 1..........
    ///white part///
    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(70,90);
    glVertex2f(0,90);
    glVertex2f(0,200);
    glVertex2f(70,200);
    glEnd();
    glBegin(GL_QUADS);   /// Top
    glColor3ub(169, 169, 242);
    glVertex2f(57,215);
    glVertex2f(15,215);
    glVertex2f(15,200);
    glVertex2f(57,200);
    glEnd();

    ///
    glBegin(GL_QUADS);
    glColor3ub(165, 165, 165);
    glVertex2f(67,90);
    glVertex2f(3,90);
    glVertex2f(3,190);
    glVertex2f(67,190);
    glEnd();

    glLineWidth(4);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 100);
    glVertex2f(3,120);
    glVertex2f(67,120);
    glEnd();

    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 100);
    glVertex2f(3,135);
    glVertex2f(67,135);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 100);
    glVertex2f(3,150);
    glVertex2f(67,150);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 100);
    glVertex2f(3,165);
    glVertex2f(67,165);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 100);
    glVertex2f(3,180);
    glVertex2f(67,180);
    glEnd();

    /// signboard
    glColor3ub(255, 255, 255);
    glRasterPos2i(17,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'B');
    glColor3ub(255, 255, 255);
    glRasterPos2i(21,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'O');
    glColor3ub(255, 255, 255);
    glRasterPos2i(25,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'O');
    glColor3ub(255, 255, 255);
    glRasterPos2i(29,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'K');
    glColor3ub(255, 255, 255);
    glRasterPos2i(33,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,' ');
    glColor3ub(255, 255, 255);
    glRasterPos2i(37,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'S');
    glColor3ub(255, 255, 255);
    glRasterPos2i(41,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'T');
    glColor3ub(255, 255, 255);
    glRasterPos2i(45,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'O');
    glColor3ub(255, 255, 255);
    glRasterPos2i(49,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'R');
    glColor3ub(255, 255, 255);
    glRasterPos2i(53,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'E');
    /// End

    ///1st Building Design///
    ///white part///
    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(75,120);
    glVertex2f(135,120);
    glVertex2f(135,505);
    glVertex2f(75,505);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(77.5,120);        //1st Building main part 2
    glVertex2f(131,120);
    glVertex2f(131,490);
    glVertex2f(77.5,490);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(135,120);         //1st Building 2nd part 2
    glVertex2f(165,120);
    glVertex2f(165,450);
    glVertex2f(135,450);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(135,120);         //1st Building 2nd part 1
    glVertex2f(162.5,120);
    glVertex2f(162.5,440);
    glVertex2f(135,440);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(177,124,119);
    glVertex2f(137,400);   //part 2 1st Building 6th floor2..........outlook
    glVertex2f(162.5,400);
    glVertex2f(162.5,430);
    glVertex2f(137,430);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(123, 88, 71);
    glVertex2f(138,395);   //part 2 1st Building 6th floor2..........outlook
    glVertex2f(148,395);
    glVertex2f(148,430);
    glVertex2f(138,430);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(143,395);   //Door 1st Building 6th floor2..........outlook-1
    glVertex2f(144,395);
    glVertex2f(144,422);
    glVertex2f(143,422);
    glEnd();

/////////////****
    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(115,120); //1st Building floor1
    glVertex2f(167,120);
    glVertex2f(167,175);
    glVertex2f(115,175);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(115,175);   //1st Building 2nd floor1
    glVertex2f(167,175);
    glVertex2f(167,230);
    glVertex2f(115,230);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(115,230);   //1st Building 3rd floor1
    glVertex2f(167,230);
    glVertex2f(167,285);
    glVertex2f(115,285);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(115,285);   //1st Building 4th floor1
    glVertex2f(167,285);
    glVertex2f(167,340);
    glVertex2f(115,340);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(115,340);   //1st Building 5th floor1
    glVertex2f(167,340);
    glVertex2f(167,395);
    glVertex2f(115,395);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(115,395);   //1st Building 6th floor1
    glVertex2f(167,395);
    glVertex2f(167,450);
    glVertex2f(115,450);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(115,450);   //1st Building 7th floor1
    glVertex2f(167,450);
    glVertex2f(167,505);
    glVertex2f(115,505);
    glEnd();

     ///design of main building....blue and glass....

    glBegin(GL_QUADS);
    glColor3ub(50, 95, 115); // sea green color
    glVertex2f(77.5,450);  //7 1st Building main part3
    glVertex2f(92,450);
    glVertex2f(92,490);
    glVertex2f(77.5,490);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(50, 95, 115); // sea green color
    glVertex2f(77.5,395);  //6 1st Building main part3
    glVertex2f(92,395);
    glVertex2f(92,435);
    glVertex2f(77.5,435);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(50, 95, 115); // sea green color
    glVertex2f(77.5,340);  //5 1st Building main part3
    glVertex2f(92,340);
    glVertex2f(92,380);
    glVertex2f(77.5,380);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(50, 95, 115); // sea green color
    glVertex2f(77.5,285);  //4 1st Building main part3
    glVertex2f(92,285);
    glVertex2f(92,325);
    glVertex2f(77.5,325);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(50, 95, 115); // sea green color
    glVertex2f(77.5,230);  //3 1st Building main part3
    glVertex2f(92,230);
    glVertex2f(92,270);
    glVertex2f(77.5,270);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(50, 95, 115); // sea green color
    glVertex2f(77.5,175);  //2 1st Building main part3
    glVertex2f(92,175);
    glVertex2f(92,215);
    glVertex2f(77.5,215);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(50, 95, 115); // sea green color
    glVertex2f(77.5,120);  //1 1st Building main part3
    glVertex2f(92,120);
    glVertex2f(92,160);
    glVertex2f(77.5,160);
    glEnd();
    /////////.....................
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(120,450);  //7 1st Building main part3
    glVertex2f(131,450);
    glVertex2f(131,490);
    glVertex2f(120,490);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(120,395);  //6 1st Building main part3
    glVertex2f(131,395);
    glVertex2f(131,435);
    glVertex2f(120,435);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(120,340);  //5 1st Building main part3
    glVertex2f(131,340);
    glVertex2f(131,380);
    glVertex2f(120,380);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(120,285);  //4 1st Building main part3
    glVertex2f(131,285);
    glVertex2f(131,325);
    glVertex2f(120,325);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(120,230);  //3 1st Building main part3
    glVertex2f(131,230);
    glVertex2f(131,270);
    glVertex2f(120,270);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(120,175);  //2 1st Building main part3
    glVertex2f(131,175);
    glVertex2f(131,215);
    glVertex2f(120,215);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(110,120);  //door
    glVertex2f(131,120);
    glVertex2f(131,160);
    glVertex2f(110,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 77);
    glVertex2f(120,120);  //door 1 main
    glVertex2f(121,120);
    glVertex2f(121,160);
    glVertex2f(120,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(121,130);  //door 1 main
    glVertex2f(122,130);
    glVertex2f(122,150);
    glVertex2f(121,150);
    glEnd();

    //////////............................

    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(75,450);  //7 1st Building main part3
    glVertex2f(135,450);
    glVertex2f(135,451);
    glVertex2f(75,451);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(75,395);  //6 1st Building main part3
    glVertex2f(162.5,395);
    glVertex2f(162.5,396);
    glVertex2f(75,396);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(75,340);  //5 1st Building main part3
    glVertex2f(135,340);
    glVertex2f(135,341);
    glVertex2f(75,341);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(75,285);  //4 1st Building main part3
    glVertex2f(135,285);
    glVertex2f(135,286);
    glVertex2f(75,286);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(75,229);  //3 1st Building main part3
    glVertex2f(135,229);
    glVertex2f(135,230);
    glVertex2f(75,230);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(75,175);  //2 1st Building main part3
    glVertex2f(135,175);
    glVertex2f(135,176);
    glVertex2f(75,176);
    glEnd();

    ///////...............................
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(75,435);  //7 1st Building main part3
    glVertex2f(135,435);
    glVertex2f(135,436);
    glVertex2f(75,436);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(75,380);  //6 1st Building main part3
    glVertex2f(135,380);
    glVertex2f(135,381);
    glVertex2f(75,381);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(75,325);  //5 1st Building main part3
    glVertex2f(135,325);
    glVertex2f(135,326);
    glVertex2f(75,326);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(75,270);  //4 1st Building main part3
    glVertex2f(135,270);
    glVertex2f(135,271);
    glVertex2f(75,271);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(75,215);  //3 1st Building main part3
    glVertex2f(135,215);
    glVertex2f(135,216);
    glVertex2f(75,216);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(75,160);  //2 1st Building main part3
    glVertex2f(135,160);
    glVertex2f(135,161);
    glVertex2f(75,161);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(89, 89, 89);
    glVertex2f(165,120);  // part2 last black line
    glVertex2f(166,120);
    glVertex2f(166,490);
    glVertex2f(165,490);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(135,450);  //7 2nd part3
    glVertex2f(162.5,450);
    glVertex2f(162.5,490);
    glVertex2f(135,490);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(135,395);  //6 2nd part3
    glVertex2f(162.5,395);
    glVertex2f(162.5,435);
    glVertex2f(135,435);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(135,340);  //5 part3
    glVertex2f(162.5,340);
    glVertex2f(162.5,380);
    glVertex2f(135,380);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(135,285);  //4 2nd part3
    glVertex2f(162.5,285);
    glVertex2f(162.5,325);
    glVertex2f(135,325);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(135,230);  //3 2nd part3
    glVertex2f(162.5,230);
    glVertex2f(162.5,270);
    glVertex2f(135,270);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(135,175);  //2 2nd part3
    glVertex2f(162.5,175);
    glVertex2f(162.5,215);
    glVertex2f(135,215);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(135,120);  //1 1st Building main part3
    glVertex2f(162.5,120);
    glVertex2f(162.5,160);
    glVertex2f(135,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 77);
    glVertex2f(142,120);  //1 main part3
    glVertex2f(143,120);
    glVertex2f(143,160);
    glVertex2f(142,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 77);
    glVertex2f(152,120);  //1 main part3
    glVertex2f(153,120);
    glVertex2f(153,160);
    glVertex2f(152,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(143,130);  //1 main part3
    glVertex2f(144,130);
    glVertex2f(144,150);
    glVertex2f(143,150);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(153,130);  ///1 main part3
    glVertex2f(154,130);
    glVertex2f(154,150);
    glVertex2f(153,150);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(0, 26, 51);
    glVertex2f(135,120);   ///partition of Blue line
    glVertex2f(136,120);
    glVertex2f(136,490);
    glVertex2f(135,490);
    glEnd();

///End 1st Building//

      ///2nd Building Design///Top
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);///2nd Building main part 2
    glVertex2f(183.5,440);
    glVertex2f(255.2,440);
    glVertex2f(255.2,472);
    glVertex2f(183.5,472);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(50, 95, 115);
    glVertex2f(183.5,440);        ///2nd Building main part 2
    glVertex2f(255.2,440);
    glVertex2f(255.2,467);
    glVertex2f(183.5,467);
    glEnd();
    ///white part///
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);   ///2nd Building main part 2
    glVertex2f(175,119);
    glVertex2f(263.5,119);
    glVertex2f(263.5,442);
    glVertex2f(175,442);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(50, 95, 115);
    glVertex2f(177.5,119);        ///2nd Building main part 2
    glVertex2f(261,119);
    glVertex2f(261,434);
    glVertex2f(177.5,434);
    glEnd();

    ///floor divided y+40//
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(175,150);  ///2nd Building 1st floor1
    glVertex2f(263,150);
    glVertex2f(263,154);
    glVertex2f(175,154);
    glEnd();
    //floor divided
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(175,190);  ///2nd Building 2nd floor1
    glVertex2f(263,190);
    glVertex2f(263,193);
    glVertex2f(175,193);
    glEnd();
    //floor divided
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(175,230);  ///2nd Building 3rd floor1
    glVertex2f(263,230);
    glVertex2f(263,234);
    glVertex2f(175,234);
    glEnd();
    //floor divided
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(175,270);  ///2nd Building 4th floor1
    glVertex2f(263,270);
    glVertex2f(263,273);
    glVertex2f(175,273);
    glEnd();
    //floor divided
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(175,310);  ///2nd Building 5th floor1
    glVertex2f(263,310);
    glVertex2f(263,314);
    glVertex2f(175,314);
    glEnd();
    //floor divided
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(175,310);  ///2nd Building 6th floor1
    glVertex2f(263,310);
    glVertex2f(263,314);
    glVertex2f(175,314);
    glEnd();
    //floor divided
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(175,350);  ///2nd Building 7th floor1
    glVertex2f(263,350);
    glVertex2f(263,353);
    glVertex2f(175,353);
    glEnd();
    //floor divided
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(175,390);  ///2nd Building 8th floor1
    glVertex2f(263,390);
    glVertex2f(263,394);
    glVertex2f(175,394);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(191,119);  /// 2nd Building white line vertical
    glVertex2f(191.5,119);
    glVertex2f(191.5,440);
    glVertex2f(191,440);
    glEnd();
     glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(205,119);  /// 2nd Building white line vertical
    glVertex2f(205.5,119);
    glVertex2f(205.5,440);
    glVertex2f(205,440);
    glEnd();
     glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(219,119);  /// 2nd Building white line vertical
    glVertex2f(219.5,119);
    glVertex2f(219.5,440);
    glVertex2f(219,440);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(233,119);  /// 2nd Building white line vertical
    glVertex2f(233.5,119);
    glVertex2f(233.5,440);
    glVertex2f(233,440);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(247,119);  /// 2nd Building white line vertical
    glVertex2f(247.5,119);
    glVertex2f(247.5,440);
    glVertex2f(247,440);
    glEnd();

    ///Door
    glBegin(GL_QUADS);
    glColor3ub(0, 26, 51);
    glVertex2f(205,140);  ///2nd Building 1st floor1
    glVertex2f(233,140);
    glVertex2f(233,144);
    glVertex2f(205,144);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 26, 51);
    glVertex2f(232,119);  /// 2nd Building white line vertical
    glVertex2f(233.6,119);
    glVertex2f(233.6,140);
    glVertex2f(232,140);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 26, 51);
    glVertex2f(218,119);  /// 2nd Building white line vertical
    glVertex2f(219.6,119);
    glVertex2f(219.6,140);
    glVertex2f(218,140);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 26, 51);
    glVertex2f(205,119);  ///2nd Building white line vertical
    glVertex2f(206.6,119);
    glVertex2f(206.6,140);
    glVertex2f(205,140);
    glEnd();
    ///End 2nd Building///

    /// signboard
    glColor3ub(255, 255, 255);
    glRasterPos2i(203,455);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'H');
    glColor3ub(255, 255, 255);
    glRasterPos2i(208,455);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'O');
    glColor3ub(255, 255, 255);
    glRasterPos2i(213,455);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'S');
    glColor3ub(255, 255, 255);
    glRasterPos2i(217,455);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'P');
    glColor3ub(255, 255, 255);
    glRasterPos2i(221,455);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'I');
    glColor3ub(255, 255, 255);
    glRasterPos2i(225,455);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'T');
    glColor3ub(255, 255, 255);
    glRasterPos2i(229,455);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'A');
    glColor3ub(255, 255, 255);
    glRasterPos2i(233,455);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'L');
    ///End//

    /////////////////
    ///3rd building main part/////
    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(270,120);
    glVertex2f(357,120);
    glVertex2f(357,395);
    glVertex2f(270,395);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(272.5,120);        //3rd building main part 2
    glVertex2f(354,120);
    glVertex2f(354,380);
    glVertex2f(272.5,380);
    glEnd();

   ///....1st floor design............

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(275,125);   //part 2 3rd building 1st floor red.........
    glVertex2f(351,125);
    glVertex2f(351,155);
    glVertex2f(275,155);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(351,125);   //part 2 3rd building 1st floor.......red
    glVertex2f(337,125);
    glVertex2f(337,155);
    glVertex2f(351,155);
    glEnd();

    //Door and window
    glBegin(GL_QUADS);
    glColor3ub(123, 88, 71);
    glVertex2f(275,120);   //d2 3rd building 1st floor
    glVertex2f(285,120);
    glVertex2f(285,155);
    glVertex2f(275,155);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(279,132);   //d2 3rd building 1st floor
    glVertex2f(280,132);
    glVertex2f(280,147);
    glVertex2f(279,147);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(293,131);   //w1 3rd building 1st floor2
    glVertex2f(313,131);
    glVertex2f(313,147);
    glVertex2f(293,147);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(128,197,215);
    glVertex2f(293.5,132);   //w1 3rd building 1st floor2
    glVertex2f(312.5,132);
    glVertex2f(312.5,146);
    glVertex2f(293.5,146);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(303.1,131);   //w1 3rd building 1st floor2
    glVertex2f(304,131);
    glVertex2f(304,147);
    glVertex2f(303.1,147);
    glEnd();

     glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(323,131);   //w2 3rd building 1st floor2
    glVertex2f(343,131);
    glVertex2f(343,147);
    glVertex2f(323,147);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(128,197,215);
    glVertex2f(323.5,132);   //w2 3rd building 1st floor2
    glVertex2f(342.5,132);
    glVertex2f(342.5,146);
    glVertex2f(323.5,146);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(333.1,131);   //w2 3rd building 1st floor2
    glVertex2f(334,131);
    glVertex2f(334,147);
    glVertex2f(333.1,147);
    glEnd();

    //floor divided
    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(272.5,160);  //3rd building 1st floor1
    glVertex2f(354,160);
    glVertex2f(354,175);
    glVertex2f(272.5,175);
    glEnd();

       ///....2nd floor design............///y+55

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(275,180);   //part 2 3rd building 2nd floor red.........
    glVertex2f(351,180);
    glVertex2f(351,210);
    glVertex2f(275,210);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(351,180);   //part 2 3rd building 2nd floor.......red
    glVertex2f(334,180);
    glVertex2f(334,210);
    glVertex2f(351,210);
    glEnd();

    //Door and window
    glBegin(GL_QUADS);
    glColor3ub(123, 88, 71);
    glVertex2f(275,175);   //d2 3rd building 2nd floor
    glVertex2f(285,175);
    glVertex2f(285,210);
    glVertex2f(275,210);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(279,187);   //d2 3rd building 2nd floor
    glVertex2f(280,187);
    glVertex2f(280,202);
    glVertex2f(279,202);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(293,186);   //w1 3rd building 2nd floor2
    glVertex2f(313,186);
    glVertex2f(313,202);
    glVertex2f(293,202);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(128,197,215);
    glVertex2f(293.5,187);   //w1 3rd building 2nd floor2
    glVertex2f(312.5,187);
    glVertex2f(312.5,201);
    glVertex2f(293.5,201);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(303.1,186);   //w1 3rd building 2nd floor2
    glVertex2f(304,186);
    glVertex2f(304,202);
    glVertex2f(303.1,202);
    glEnd();

     glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(323,186);   //w2 3rd building 2nd floor2
    glVertex2f(343,186);
    glVertex2f(343,202);
    glVertex2f(323,202);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(128,197,215);
    glVertex2f(323.5,187);   //w2 3rd building 2nd floor2
    glVertex2f(342.5,187);
    glVertex2f(342.5,201);
    glVertex2f(323.5,201);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(333.1,186);   //w2 3rd building 2nd floor2
    glVertex2f(334,186);
    glVertex2f(334,202);
    glVertex2f(333.1,202);
    glEnd();

    //floor divided
    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(272.5,215);  //3rd building 2nd floor1
    glVertex2f(354,215);
    glVertex2f(354,230);
    glVertex2f(272.5,230);
    glEnd();

    ///....3rd floor design............///y+55

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(275,235);   //part 2 3rd building 3rd floor red.........
    glVertex2f(351,235);
    glVertex2f(351,265);
    glVertex2f(275,265);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(351,235);   //part 2 3rd building 3rd floor.......red
    glVertex2f(334,235);
    glVertex2f(334,265);
    glVertex2f(351,265);
    glEnd();

    //Door and window
    glBegin(GL_QUADS);
    glColor3ub(123, 88, 71);
    glVertex2f(275,230);   //d2 3rd building 3rd floor
    glVertex2f(285,230);
    glVertex2f(285,265);
    glVertex2f(275,265);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(279,242);   //d2 3rd building 2nd floor
    glVertex2f(280,242);
    glVertex2f(280,257);
    glVertex2f(279,257);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(293,241);   //w1 3rd building 3rd floor2
    glVertex2f(313,241);
    glVertex2f(313,257);
    glVertex2f(293,257);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(128,197,215);
    glVertex2f(293.5,242);   //w1 3rd building 2nd floor2
    glVertex2f(312.5,242);
    glVertex2f(312.5,256);
    glVertex2f(293.5,256);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(303.1,241);   //w1 3rd building 3rd floor2
    glVertex2f(304,241);
    glVertex2f(304,257);
    glVertex2f(303.1,257);
    glEnd();

     glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(323,241);   //w2 3rd building 3rd floor2
    glVertex2f(343,241);
    glVertex2f(343,257);
    glVertex2f(323,257);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(128,197,215);
    glVertex2f(323.5,242);   //w2 3rd building 3rd floor2
    glVertex2f(342.5,242);
    glVertex2f(342.5,256);
    glVertex2f(323.5,256);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(333.1,241);   //w2 3rd building 3rd floor2
    glVertex2f(334,241);
    glVertex2f(334,257);
    glVertex2f(333.1,257);
    glEnd();

    //floor divided
    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(272.5,270);  //3rd building 3rd floor1
    glVertex2f(354,270);
    glVertex2f(354,285);
    glVertex2f(272.5,285);
    glEnd();

    ///....4th floor design............///y+55 korchi

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(275,290);   //part 2 3rd building 4th floor red.........
    glVertex2f(351,290);
    glVertex2f(351,320);
    glVertex2f(275,320);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(351,290);   //part 2 3rd building 4th floor.......red
    glVertex2f(334,290);
    glVertex2f(334,320);
    glVertex2f(351,320);
    glEnd();

    //Door and window
    glBegin(GL_QUADS);
    glColor3ub(123, 88, 71);
    glVertex2f(275,285);   //d2 3rd building 4th floor
    glVertex2f(285,285);
    glVertex2f(285,320);
    glVertex2f(275,320);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(279,297);   //d2 3rd building 5th floor
    glVertex2f(280,297);
    glVertex2f(280,312);
    glVertex2f(279,312);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(293,296);   //w1 3rd building 4th floor2
    glVertex2f(313,296);
    glVertex2f(313,312);
    glVertex2f(293,312);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(128,197,215);
    glVertex2f(293.5,297);   //w1 3rd building 4th floor2
    glVertex2f(312.5,297);
    glVertex2f(312.5,311);
    glVertex2f(293.5,311);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(303.1,296);   //w1 3rd building 4th floor2
    glVertex2f(304,296);
    glVertex2f(304,312);
    glVertex2f(303.1,312);
    glEnd();

     glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(323,297);   //w2 3rd building 4th floor2
    glVertex2f(343,297);
    glVertex2f(343,312);
    glVertex2f(323,312);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(128,197,215);
    glVertex2f(323.5,297);   //w2 3rd building 4th floor2
    glVertex2f(342.5,297);
    glVertex2f(342.5,311);
    glVertex2f(323.5,311);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(333.1,297);   //w2 3rd building 4th floor2
    glVertex2f(334,297);
    glVertex2f(334,312);
    glVertex2f(333.1,312);
    glEnd();

     //floor divided
    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(272.5,325);  //3rd building 4th floor1
    glVertex2f(354,325);
    glVertex2f(354,340);
    glVertex2f(272.5,340);
    glEnd();

    ///....5th floor design............///y+55

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(275,345);   //part 2 3rd building 5th floor red.........
    glVertex2f(351,345);
    glVertex2f(351,375);
    glVertex2f(275,375);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(351,345);   //part 2 3rd building 5th floor.......red
    glVertex2f(334,345);
    glVertex2f(334,375);
    glVertex2f(351,375);
    glEnd();

    //Door and window
    glBegin(GL_QUADS);
    glColor3ub(123, 88, 71);
    glVertex2f(275,340);   //d2 3rd building 5th floor
    glVertex2f(285,340);
    glVertex2f(285,375);
    glVertex2f(275,375);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(279,352);   //d2 3rd building 5th floor
    glVertex2f(280,352);
    glVertex2f(280,367);
    glVertex2f(279,367);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(293,351);   //w1 3rd building 5th floor2
    glVertex2f(313,351);
    glVertex2f(313,367);
    glVertex2f(293,367);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(128,197,215);
    glVertex2f(293.5,352);   //w1 3rd building 5th floor2
    glVertex2f(312.5,352);
    glVertex2f(312.5,366);
    glVertex2f(293.5,366);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(303.1,351);   //w1 3rd building 5th floor2
    glVertex2f(304,351);
    glVertex2f(304,367);
    glVertex2f(303.1,367);
    glEnd();

     glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(323,352);   //w2 3rd building 4th floor2
    glVertex2f(343,352);
    glVertex2f(343,367);
    glVertex2f(323,367);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(128,197,215);
    glVertex2f(323.5,352);   //w2 3rd building 5th floor2
    glVertex2f(342.5,352);
    glVertex2f(342.5,366);
    glVertex2f(323.5,366);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(333.1,352);   //w2 3rd building 5th floor2
    glVertex2f(334,352);
    glVertex2f(334,367);
    glVertex2f(333.1,367);
    glEnd();
    ///End 3rd building//

    ///Tower 3rd Building//
    glBegin(GL_QUADS);
    glColor3ub(140, 140, 140);
    glVertex2f(343,395);
    glVertex2f(344,395);
    glVertex2f(344,520);
    glVertex2f(343,520);
    glEnd();

    glColor3ub(102, 102, 102);
    circle(3,6,343,500);
    glColor3ub(217, 217, 217);
    circle(2.5,5,343,500);
    glColor3ub(102, 102, 102);
    circle(2,4,346,485);
    glColor3ub(217, 217, 217);
    circle(1.5,3,346,485);
    //Tower End//

       ///4th Building Design///
    ///....4th Building main part-1
    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(370,120);
    glVertex2f(430,120);
    glVertex2f(430,505);
    glVertex2f(370,505);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(372.5,120);        //4th Building main part 2
    glVertex2f(426,120);
    glVertex2f(426,490);
    glVertex2f(372.5,490);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(430,120);         //4th Building 2nd part 2
    glVertex2f(460,120);
    glVertex2f(460,450);
    glVertex2f(430,450);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(430,120);         //4th Building 2nd part 1
    glVertex2f(457.5,120);
    glVertex2f(457.5,440);
    glVertex2f(430,440);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(177,124,119);
    glVertex2f(433,400);   //part 2 4th Building 6th floor2..........outlook
    glVertex2f(457.5,400);
    glVertex2f(457.5,430);
    glVertex2f(433,430);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(123, 88, 71);
    glVertex2f(433,395);   //part 2 4th Building 6th floor2..........outlook
    glVertex2f(443,395);
    glVertex2f(443,430);
    glVertex2f(433,430);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(438,395);   //Door 4th Building 6th floor2..........outlook-1
    glVertex2f(439,395);
    glVertex2f(439,422);
    glVertex2f(438,422);
    glEnd();

/////////////****
    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(410,120);  //4th Building 1st floor1
    glVertex2f(517,120);
    glVertex2f(517,175);
    glVertex2f(410,175);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(410,175);   //4th Building 2nd floor1
    glVertex2f(517,175);
    glVertex2f(517,230);
    glVertex2f(410,230);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(410,230);   //4th Building 3rd floor1
    glVertex2f(517,230);
    glVertex2f(517,285);
    glVertex2f(410,285);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(410,285);   //4th Building 4th floor1
    glVertex2f(517,285);
    glVertex2f(517,340);
    glVertex2f(410,340);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(410,340);   //4th Building 5th floor1
    glVertex2f(517,340);
    glVertex2f(517,395);
    glVertex2f(410,395);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(410,395);   //4th Building 6th floor1
    glVertex2f(517,395);
    glVertex2f(517,450);
    glVertex2f(410,450);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(410,450);   //4th Building 7th floor1
    glVertex2f(517,450);
    glVertex2f(517,505);
    glVertex2f(410,505);
    glEnd();


    glBegin(GL_QUADS);              ///SIRI GHORE.//
    glColor3ub(204, 204, 204);
    glVertex2f(410,505);
    glVertex2f(440,505);
    glVertex2f(440,545);
    glVertex2f(410,545);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(412,505);
    glVertex2f(438,505);
    glVertex2f(438,540);
    glVertex2f(412,540);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(123, 88, 71);
    glVertex2f(420,505);
    glVertex2f(430,505);
    glVertex2f(430,535);
    glVertex2f(420,535);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(425,513);
    glVertex2f(426,513);
    glVertex2f(426,522);
    glVertex2f(425,522);
    glEnd();


    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(430,450);   //part 2 4th Building 7th floor2 white
    glVertex2f(514,450);
    glVertex2f(514,490);
    glVertex2f(430,490);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(460,395);   //part 2 4th Building 6th floor2
    glVertex2f(514,395);
    glVertex2f(514,435);
    glVertex2f(460,435);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(460,340);   //part 2 4th Building 5th floor2
    glVertex2f(514,340);
    glVertex2f(514,380);
    glVertex2f(460,380);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(460,285);   //part 2 4th Building 4th floor2
    glVertex2f(514,285);
    glVertex2f(514,325);
    glVertex2f(460,325);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(460,230);   //part 2 4th Building 3rd floor2
    glVertex2f(514,230);
    glVertex2f(514,270);
    glVertex2f(460,270);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(460,175);   //part 2 4th Building 2nd floor2
    glVertex2f(514,175);
    glVertex2f(514,215);
    glVertex2f(460,215);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(460,120);  //part 2 4th Building 1st floor2
    glVertex2f(514,120);
    glVertex2f(514,160);
    glVertex2f(460,160);
    glEnd();

    ///design of main building....red and glass..............

    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(372.5,450);  //7 4th Building main part3
    glVertex2f(387,450);
    glVertex2f(387,490);
    glVertex2f(372.5,490);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(372.5,395);  //6 4th Building main part3
    glVertex2f(387,395);
    glVertex2f(387,435);
    glVertex2f(372.5,435);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(372.5,340);  //5 4th Building main part3
    glVertex2f(387,340);
    glVertex2f(387,380);
    glVertex2f(372.5,380);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(372.5,285);  //4 4th Building main part3
    glVertex2f(387,285);
    glVertex2f(387,325);
    glVertex2f(372.5,325);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(372.5,230);  //3 4th Building main part3
    glVertex2f(387,230);
    glVertex2f(387,270);
    glVertex2f(372.5,270);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(372.5,175);  //2 4th Building main part3
    glVertex2f(387,175);
    glVertex2f(387,215);
    glVertex2f(372.5,215);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(372.5,120);  //1 4th Building main part3
    glVertex2f(387,120);
    glVertex2f(387,160);
    glVertex2f(372.5,160);
    glEnd();
    /////////.....................
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(415,450);  //7 4th Building main part3
    glVertex2f(426,450);
    glVertex2f(426,490);
    glVertex2f(415,490);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(415,395);  //6 4th Building main part3
    glVertex2f(426,395);
    glVertex2f(426,435);
    glVertex2f(415,435);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(415,340);  //5 4th Building main part3
    glVertex2f(426,340);
    glVertex2f(426,380);
    glVertex2f(415,380);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(415,285);  //4 4th Building main part3
    glVertex2f(426,285);
    glVertex2f(426,325);
    glVertex2f(415,325);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(415,230);  //3 4th Building main part3
    glVertex2f(426,230);
    glVertex2f(426,270);
    glVertex2f(415,270);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(415,175);  //2 4th Building main part3
    glVertex2f(426,175);
    glVertex2f(426,215);
    glVertex2f(415,215);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(405,120);  //door
    glVertex2f(426,120);
    glVertex2f(426,160);
    glVertex2f(405,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 77);
    glVertex2f(415,120);  //door 1 main
    glVertex2f(416,120);
    glVertex2f(416,160);
    glVertex2f(415,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(416,130);  //door 1 main
    glVertex2f(417,130);
    glVertex2f(417,150);
    glVertex2f(416,150);
    glEnd();

    //////////............................

    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(370,450);  //7 4th Building main part3
    glVertex2f(430,450);
    glVertex2f(430,451);
    glVertex2f(370,451);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(370,395);  //6 4th Building main part3
    glVertex2f(457.5,395);
    glVertex2f(457.5,396);
    glVertex2f(370,396);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(370,340);  //5 4th Building main part3
    glVertex2f(430,340);
    glVertex2f(430,341);
    glVertex2f(370,341);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(370,285);  //4 4th Building main part3
    glVertex2f(430,285);
    glVertex2f(430,286);
    glVertex2f(370,286);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(370,229);  //3 4th Building main part3
    glVertex2f(430,229);
    glVertex2f(430,230);
    glVertex2f(370,230);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(370,175);  //2 4th Building main part3
    glVertex2f(430,175);
    glVertex2f(430,176);
    glVertex2f(370,176);
    glEnd();

    ///////...............................
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(370,435);  //7 4th Building main part3
    glVertex2f(430,435);
    glVertex2f(430,436);
    glVertex2f(370,436);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(370,380);  //6 4th Building main part3
    glVertex2f(430,380);
    glVertex2f(430,381);
    glVertex2f(370,381);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(370,325);  //5 4th Building main part3
    glVertex2f(430,325);
    glVertex2f(430,326);
    glVertex2f(370,326);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(370,270);  //4  main part3
    glVertex2f(430,270);
    glVertex2f(430,271);
    glVertex2f(370,271);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(370,215);  //3 4th Building main part3
    glVertex2f(430,215);
    glVertex2f(430,216);
    glVertex2f(370,216);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(370,160);  //2 4th Building main part3
    glVertex2f(430,160);
    glVertex2f(430,161);
    glVertex2f(370,161);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(89, 89, 89);
    glVertex2f(460,120);  // part2
    glVertex2f(461,120);
    glVertex2f(461,450);
    glVertex2f(460,450);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(430,395);  //6 4th Building main part3
    glVertex2f(440,395);
    glVertex2f(440,415);
    glVertex2f(430,415);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(448,395);  //6 4th Building main part3
    glVertex2f(457.5,395);
    glVertex2f(457.5,415);
    glVertex2f(448,415);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(57,80,80);
    glVertex2f(440,400);  //6 4th Building main part3
    glVertex2f(448,400);
    glVertex2f(448.5,402);
    glVertex2f(440,402);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(57,80,80);
    glVertex2f(440,409);  //6 4th Building main part3
    glVertex2f(448,409);
    glVertex2f(448.5,411);
    glVertex2f(440,411);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(430,340);  //5 2nd part2
    glVertex2f(457.5,340);
    glVertex2f(457.5,380);
    glVertex2f(430,380);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(430,285);  //4 2nd part3
    glVertex2f(457.5,285);
    glVertex2f(457.5,325);
    glVertex2f(430,325);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(430,230);  //3 2nd part3
    glVertex2f(457.5,230);
    glVertex2f(457.5,270);
    glVertex2f(430,270);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(430,175);  //2 2nd part3
    glVertex2f(457.5,175);
    glVertex2f(457.5,215);
    glVertex2f(430,215);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(430,120);  //1 4th Building main part3
    glVertex2f(457.5,120);
    glVertex2f(457.5,160);
    glVertex2f(430,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 77);
    glVertex2f(437,120);  //1 4th Building main part3
    glVertex2f(438,120);
    glVertex2f(438,160);
    glVertex2f(437,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 77);
    glVertex2f(447,120);  //1 4th Building main part3
    glVertex2f(448,120);
    glVertex2f(448,160);
    glVertex2f(447,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(438,130);  //1 4th Building main part3
    glVertex2f(439,130);
    glVertex2f(439,150);
    glVertex2f(438,150);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(242, 242, 242);
    glVertex2f(448,130);  //1 4th Building main part3
    glVertex2f(449,130);
    glVertex2f(449,150);
    glVertex2f(448,150);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(0, 26, 51);
    glVertex2f(430,120);   //partation
    glVertex2f(431,120);
    glVertex2f(431,505);
    glVertex2f(430,505);
    glEnd();

    //..7th Floor design...................

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(433,455);   //part 2 4th Building 7th floor2
    glVertex2f(511,455);
    glVertex2f(511,485);
    glVertex2f(433,485);
    glEnd();

    //....door.....window
    glBegin(GL_QUADS);
    glColor3ub(123, 88, 71);
    glVertex2f(433,450);   //d1 4th Building 7th floor2
    glVertex2f(443,450);
    glVertex2f(443,485);
    glVertex2f(433,485);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(438,460);   //d1 4th Building 7th floor2
    glVertex2f(439,460);
    glVertex2f(439,475);
    glVertex2f(438,475);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(453,462);   //w1 4th Building 7th floor2
    glVertex2f(473,462);
    glVertex2f(473,478);
    glVertex2f(453,478);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(453.5,463);   //w1 4th Building 7th floor2
    glVertex2f(472.5,463);
    glVertex2f(472.5,477);
    glVertex2f(453.5,477);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(463,462);   //w1 4th Building 7th floor2
    glVertex2f(464,462);
    glVertex2f(464,478);
    glVertex2f(463,478);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(483,462);   //w2 4th Building 7th floor2
    glVertex2f(503,462);
    glVertex2f(503,478);
    glVertex2f(483,478);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(483.5,463);   //w2 4th Building 7th floor2
    glVertex2f(502.5,463);
    glVertex2f(502.5,477);
    glVertex2f(483.5,477);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(493,462);   //w2 4th Building 7th floor2
    glVertex2f(494,462);
    glVertex2f(494,478);
    glVertex2f(493,478);
    glEnd();


    //....6th Floor Design..........Door window

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(461,400);   //part 2 4th Building 6th floor2..........Inlook
    glVertex2f(511,400);
    glVertex2f(511,430);
    glVertex2f(461,430);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(461,407);   //w1 4th Building 6th floor2
    glVertex2f(473,407);
    glVertex2f(473,423);
    glVertex2f(461,423);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(461,408);   //w1 4th Building 6th floor2
    glVertex2f(472.5,408);
    glVertex2f(472.5,422);
    glVertex2f(461,422);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(463,407);   //w1 4th Building 6th floor2
    glVertex2f(464,407);
    glVertex2f(464,423);
    glVertex2f(463,423);
    glEnd();


    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(483,407);   //w2 4th Building 6th floor2
    glVertex2f(503,407);
    glVertex2f(503,423);
    glVertex2f(483,423);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(483.5,408);   //w2 4th Building 6th floor2
    glVertex2f(502.5,408);
    glVertex2f(502.5,422);
    glVertex2f(483.5,422);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(493,407);   //w2 4th Building 6th floor2
    glVertex2f(494,407);
    glVertex2f(494,423);
    glVertex2f(493,423);
    glEnd();


    ///5th floor......design

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(461,345);   //part 2 4th Building 5th floor2.........
    glVertex2f(511,345);
    glVertex2f(511,375);
    glVertex2f(461,375);
    glEnd();


    ///....door.....window


    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(461,352);   //w1 4th Building 5th floor2
    glVertex2f(473,352);
    glVertex2f(473,368);
    glVertex2f(461,368);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(461,353);   //w1 4th Building 5th floor2
    glVertex2f(472.5,353);
    glVertex2f(472.5,367);
    glVertex2f(461,367);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(463,352);   //w1 4th Building 5th floor2
    glVertex2f(464,352);
    glVertex2f(464,368);
    glVertex2f(463,368);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(483,352);   //w2 4th Building 5th floor2
    glVertex2f(503,352);
    glVertex2f(503,368);
    glVertex2f(483,368);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(483.5,353);   //w2 4th Building 5th floor2
    glVertex2f(502.5,353);
    glVertex2f(502.5,367);
    glVertex2f(483.5,367);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(493,352);   //w2 4th Building 5th floor2
    glVertex2f(494,352);
    glVertex2f(494,368);
    glVertex2f(493,368);
    glEnd();


    ///....4TH floor design............

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(461,290);   //part 2 4th Building 5th floor2.........
    glVertex2f(511,290);
    glVertex2f(511,320);
    glVertex2f(461,320);
    glEnd();


    ///....door.....window


    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(461,297);   //w1 4th Building 4th floor2
    glVertex2f(473,297);
    glVertex2f(473,313);
    glVertex2f(461,313);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(461,298);   //w1 4th Building 4th floor2
    glVertex2f(472.5,298);
    glVertex2f(472.5,312);
    glVertex2f(461,312);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(463,297);   //w1 4th Building 4th floor2
    glVertex2f(464,297);
    glVertex2f(464,313);
    glVertex2f(463,313);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(483,297);   //w2 4th Building 4th floor2
    glVertex2f(503,297);
    glVertex2f(503,313);
    glVertex2f(483,313);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(483.5,298);   //w2 4th Building 4th floor2
    glVertex2f(502.5,298);
    glVertex2f(502.5,312);
    glVertex2f(483.5,312);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(493,297);   //w2 4th Building 4th floor2
    glVertex2f(494,297);
    glVertex2f(494,313);
    glVertex2f(493,313);
    glEnd();


    ///....3rd floor design............

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(461,235);   //part 2 4th Building 3th floor2.........
    glVertex2f(511,235);
    glVertex2f(511,265);
    glVertex2f(461,265);
    glEnd();

    ///....door.....window


    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(461,242);   //w1 4th Building 3rd floor2
    glVertex2f(473,242);
    glVertex2f(473,258);
    glVertex2f(461,258);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(461,243);   //w1 4th Building 3rd floor2
    glVertex2f(472.5,243);
    glVertex2f(472.5,257);
    glVertex2f(461,257);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(463,242);   //w1 4th Building 3rd floor2
    glVertex2f(464,242);
    glVertex2f(464,258);
    glVertex2f(463,258);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(483,242);   //w2 4th Building 3rd floor2
    glVertex2f(503,242);
    glVertex2f(503,258);
    glVertex2f(483,258);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(483.5,243);   //w2 4th Building 3rd floor2
    glVertex2f(502.5,243);
    glVertex2f(502.5,257);
    glVertex2f(483.5,257);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(493,242);   //w2 4th Building 3rd floor2
    glVertex2f(494,242);
    glVertex2f(494,258);
    glVertex2f(493,258);
    glEnd();


    ///....2nd floor design............

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(461,180);   //part 2 4th Building 2nd floor2.........
    glVertex2f(511,180);
    glVertex2f(511,210);
    glVertex2f(461,210);
    glEnd();


    ///....door.....window

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(461,187);   //w1 4th Building 2nd floor2
    glVertex2f(473,187);
    glVertex2f(473,203);
    glVertex2f(461,203);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(461,188);   //w1 4th Building 2nd floor2
    glVertex2f(472.5,188);
    glVertex2f(472.5,202);
    glVertex2f(461,202);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(463,187);   //w1 4th Building 2nd floor2
    glVertex2f(464,187);
    glVertex2f(464,203);
    glVertex2f(463,203);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(483,187);   //w2 4th Building 2nd floor2
    glVertex2f(503,187);
    glVertex2f(503,203);
    glVertex2f(483,203);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(483.5,188);   //w2 4th Building 2nd floor2
    glVertex2f(502.5,188);
    glVertex2f(502.5,202);
    glVertex2f(483.5,202);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(493,187);   //w2 4th Building 2nd floor2
    glVertex2f(494,187);
    glVertex2f(494,203);
    glVertex2f(493,203);
    glEnd();


    ///....1st floor design............

    glBegin(GL_QUADS);
    glColor3ub(200, 120, 130);
    glVertex2f(461,125);   //part 2 4th Building 1st floor red.........
    glVertex2f(511,125);
    glVertex2f(511,155);
    glVertex2f(461,155);
    glEnd();


    ///....door.....window

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(461,132);   //w1 4th Building 1st floor2
    glVertex2f(473,132);
    glVertex2f(473,148);
    glVertex2f(461,148);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(461,133);   //w1 4th Building 1st floor2
    glVertex2f(472.5,133);
    glVertex2f(472.5,147);
    glVertex2f(461,147);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(463,132);   //w1 4th Building 1st floor2
    glVertex2f(464,132);
    glVertex2f(464,148);
    glVertex2f(463,148);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(483,132);   //w2 4th Building 1st floor2
    glVertex2f(503,132);
    glVertex2f(503,148);
    glVertex2f(483,148);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(483.5,133);   //w2 4th Building 1st floor2
    glVertex2f(502.5,133);
    glVertex2f(502.5,147);
    glVertex2f(483.5,147);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(493,132);   //w2 4th Building 1st floor2
    glVertex2f(494,132);
    glVertex2f(494,148);
    glVertex2f(493,148);
    glEnd();
    /// End 4th Building ///


    /// ........Store 2..........
    ///white part///
    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(590,90);
    glVertex2f(520,90);
    glVertex2f(520,200);
    glVertex2f(590,200);
    glEnd();
    glBegin(GL_QUADS);   /// Top
    glColor3ub(0, 0, 0);
    glVertex2f(577,215);
    glVertex2f(535,215);
    glVertex2f(535,200);
    glVertex2f(577,200);
    glEnd();

    ///
    glBegin(GL_QUADS);
    glColor3ub(165, 165, 165);
    glVertex2f(587,90);
    glVertex2f(523,90);
    glVertex2f(523,190);
    glVertex2f(587,190);
    glEnd();

    glLineWidth(4);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 100);
    glVertex2f(523,120);
    glVertex2f(587,120);
    glEnd();

    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 100);
    glVertex2f(523,135);
    glVertex2f(587,135);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 100);
    glVertex2f(523,150);
    glVertex2f(587,150);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 100);
    glVertex2f(523,165);
    glVertex2f(587,165);
    glEnd();
    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(100, 100, 100);
    glVertex2f(523,180);
    glVertex2f(587,180);
    glEnd();

    /// signboard
    glColor3ub(255, 255, 255);
    glRasterPos2i(537,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'E');
    glColor3ub(255, 255, 255);
    glRasterPos2i(541,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'L');
    glColor3ub(255, 255, 255);
    glRasterPos2i(545,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'E');
    glColor3ub(255, 255, 255);
    glRasterPos2i(549,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'C');
    glColor3ub(255, 255, 255);
    glRasterPos2i(553,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'T');
    glColor3ub(255, 255, 255);
    glRasterPos2i(557,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'O');
    glColor3ub(255, 255, 255);
    glRasterPos2i(561,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'N');
    glColor3ub(255, 255, 255);
    glRasterPos2i(565,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'I');
    glColor3ub(255, 255, 255);
    glRasterPos2i(569,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'C');
    glColor3ub(255, 255, 255);
    glRasterPos2i(573,205);
    glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_10,'S');
    /// End ///

        ///5th Building Design///
///white part///
    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(595,120);
    glVertex2f(655,120);
    glVertex2f(655,505);
    glVertex2f(595,505);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(597.5,120);        //5th Building main part 2
    glVertex2f(651,120);
    glVertex2f(651,490);
    glVertex2f(597.5,490);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(655,120);         //5th Building 2nd part 2
    glVertex2f(685,120);
    glVertex2f(685,450);
    glVertex2f(655,450);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(655,120);         //5th Building 2nd part 1
    glVertex2f(682.5,120);
    glVertex2f(682.5,440);
    glVertex2f(655,440);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(177,124,119);
    glVertex2f(657,400);   //part 2 5th Building 6th floor2..........outlook
    glVertex2f(682.5,400);
    glVertex2f(682.5,430);
    glVertex2f(657,430);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(123, 88, 71);
    glVertex2f(658,395);   //part 2 5th Building 6th floor2..........outlook
    glVertex2f(668,395);
    glVertex2f(668,430);
    glVertex2f(658,430);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(663,395);   //Door 5th Building 6th floor2..........outlook-1
    glVertex2f(664,395);
    glVertex2f(664,422);
    glVertex2f(663,422);
    glEnd();

/////////////****
    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(635,120); //5th Building floor1
    glVertex2f(687,120);
    glVertex2f(687,175);
    glVertex2f(635,175);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(635,175);   //5th Building 2nd floor1
    glVertex2f(687,175);
    glVertex2f(687,230);
    glVertex2f(635,230);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(635,230);   //5th Building 3rd floor1
    glVertex2f(687,230);
    glVertex2f(687,285);
    glVertex2f(635,285);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(635,285);   //5th Building 4th floor1
    glVertex2f(687,285);
    glVertex2f(687,340);
    glVertex2f(635,340);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(635,340);   //5th Building 5th floor1
    glVertex2f(687,340);
    glVertex2f(687,395);
    glVertex2f(635,395);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(635,395);   //5th Building 6th floor1
    glVertex2f(687,395);
    glVertex2f(687,450);
    glVertex2f(635,450);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(204, 204, 204);
    glVertex2f(635,450);   //5th Building 7th floor1
    glVertex2f(687,450);
    glVertex2f(687,505);
    glVertex2f(635,505);
    glEnd();

     ///design of main building....red and glass....

    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(597.5,450);  //7 5th Building main part3
    glVertex2f(612,450);
    glVertex2f(612,490);
    glVertex2f(597.5,490);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(597.5,395);  //6 5th Building main part3
    glVertex2f(612,395);
    glVertex2f(612,435);
    glVertex2f(597.5,435);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(597.5,340);  //5 5th Building main part3
    glVertex2f(612,340);
    glVertex2f(612,380);
    glVertex2f(597.5,380);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(597.5,285);  //4 5th Building main part3
    glVertex2f(612,285);
    glVertex2f(612,325);
    glVertex2f(597.5,325);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(597.5,230);  //3 5th Building main part3
    glVertex2f(612,230);
    glVertex2f(612,270);
    glVertex2f(597.5,270);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(597.5,175);  //2 5th Building main part3
    glVertex2f(612,175);
    glVertex2f(612,215);
    glVertex2f(597.5,215);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(220, 110, 130); // Muted rose pink
    glVertex2f(597.5,120);  //1 5th Building main part3
    glVertex2f(612,120);
    glVertex2f(612,160);
    glVertex2f(597.5,160);
    glEnd();
    /////////.....................
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(640,450);  //7 5th Building main part3
    glVertex2f(651,450);
    glVertex2f(651,490);
    glVertex2f(640,490);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(640,395);  //6 5th Building main part3
    glVertex2f(651,395);
    glVertex2f(651,435);
    glVertex2f(640,435);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(640,340);  //5 5th Building main part3
    glVertex2f(651,340);
    glVertex2f(651,380);
    glVertex2f(640,380);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(640,285);  //4 5th Building main part3
    glVertex2f(651,285);
    glVertex2f(651,325);
    glVertex2f(640,325);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(640,230);  //3 5th Building main part3
    glVertex2f(651,230);
    glVertex2f(651,270);
    glVertex2f(640,270);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(640,175);  //2 5th Building main part3
    glVertex2f(651,175);
    glVertex2f(651,215);
    glVertex2f(640,215);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(630,120);  //door
    glVertex2f(651,120);
    glVertex2f(651,160);
    glVertex2f(630,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 77);
    glVertex2f(640,120);  //door 1 main
    glVertex2f(641,120);
    glVertex2f(641,160);
    glVertex2f(640,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(641,130);  //door 1 main
    glVertex2f(642,130);
    glVertex2f(642,150);
    glVertex2f(641,150);
    glEnd();

    //////////............................

    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(595,450);  //7 5th Building main part3
    glVertex2f(655,450);
    glVertex2f(655,451);
    glVertex2f(595,451);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(595,395);  //6 5th Building main part3
    glVertex2f(682.5,395);
    glVertex2f(682.5,396);
    glVertex2f(595,396);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(595,340);  //5 5th Building main part3
    glVertex2f(655,340);
    glVertex2f(655,341);
    glVertex2f(595,341);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(595,285);  //4 5th Building main part3
    glVertex2f(655,285);
    glVertex2f(655,286);
    glVertex2f(595,286);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(595,229);  //3 5th Building main part3
    glVertex2f(655,229);
    glVertex2f(655,230);
    glVertex2f(595,230);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(595,175);  //2 5th Building main part3
    glVertex2f(655,175);
    glVertex2f(655,176);
    glVertex2f(595,176);
    glEnd();

    ///////...............................
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(595,435);  //7 5th Building main part3
    glVertex2f(655,435);
    glVertex2f(655,436);
    glVertex2f(595,436);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(595,380);  //6 5th Building main part3
    glVertex2f(655,380);
    glVertex2f(655,381);
    glVertex2f(595,381);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(595,325);  //5 5th Building main part3
    glVertex2f(655,325);
    glVertex2f(655,326);
    glVertex2f(595,326);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(595,270);  //4 5th Building main part3
    glVertex2f(655,270);
    glVertex2f(655,271);
    glVertex2f(595,271);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(595,215);  //3 5th Building main part3
    glVertex2f(655,215);
    glVertex2f(655,216);
    glVertex2f(595,216);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(179, 179, 179);
    glVertex2f(595,160);  //2 5th Building main part3
    glVertex2f(655,160);
    glVertex2f(655,161);
    glVertex2f(595,161);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(89, 89, 89);
    glVertex2f(685,120);  // part2 last black line
    glVertex2f(686,120);
    glVertex2f(686,490);
    glVertex2f(685,490);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(655,450);  //7 2nd part3
    glVertex2f(682.5,450);
    glVertex2f(682.5,490);
    glVertex2f(655,490);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(655,395);  //6 2nd part3
    glVertex2f(682.5,395);
    glVertex2f(682.5,435);
    glVertex2f(655,435);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(655,340);  //5 part3
    glVertex2f(682.5,340);
    glVertex2f(682.5,380);
    glVertex2f(655,380);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(655,285);  //4 2nd part3
    glVertex2f(682.5,285);
    glVertex2f(682.5,325);
    glVertex2f(655,325);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(655,230);  //3 2nd part3
    glVertex2f(682.5,230);
    glVertex2f(682.5,270);
    glVertex2f(655,270);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(85,119,119);
    glVertex2f(655,175);  //2 2nd part3
    glVertex2f(682.5,175);
    glVertex2f(682.5,215);
    glVertex2f(655,215);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(143,175,175);
    glVertex2f(655,120);  //1 5th Building main part3
    glVertex2f(682.5,120);
    glVertex2f(682.5,160);
    glVertex2f(655,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 77);
    glVertex2f(662,120);  //1 main part3
    glVertex2f(663,120);
    glVertex2f(663,160);
    glVertex2f(662,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 77);
    glVertex2f(672,120);  //1 main part3
    glVertex2f(673,120);
    glVertex2f(673,160);
    glVertex2f(672,160);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(663,130);  //1 main part3
    glVertex2f(664,130);
    glVertex2f(664,150);
    glVertex2f(663,150);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(250, 245, 235);
    glVertex2f(673,130);  ///1 main part3
    glVertex2f(674,130);
    glVertex2f(674,150);
    glVertex2f(673,150);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(0, 26, 51);
    glVertex2f(655,120);   ///partation of Blue line
    glVertex2f(656,120);
    glVertex2f(656,490);
    glVertex2f(655,490);
    glEnd();

///End 5th Building//

     glBegin(GL_QUADS);
    glColor3ub(90,147,48);
    glVertex2f(0,100);        ///building font area
    glVertex2f(800,100);
    glVertex2f(800,119.5);
    glVertex2f(0,119.5);
    glEnd();

    glBegin(GL_QUADS);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(0,80);        ///building back area
    glVertex2f(800,80);
    glVertex2f(800,100);
    glVertex2f(0,100);
    glEnd();

    glBegin(GL_QUADS);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(0,30);
    glVertex2f(800,30);
    glVertex2f(800,80);
    glVertex2f(0,80);
    glEnd();


    // Update position for animation
    if (c <= -100) {
           c = 800; // Reset to the starting position
      } else {
           c = c - 0.3; // Move left
      }

    /// ...........Bus..............
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 139); // Dark blue
    glVertex2f(10 + c, 148);  // Bus top
    glVertex2f(5 + c, 148);
    glVertex2f(5 + c, 150);
    glVertex2f(10 + c, 150);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(26, 26, 0); // Front glass
    glVertex2f(4 + c, 139);
    glVertex2f(6 + c, 139);
    glVertex2f(6 + c, 150);
    glVertex2f(4 + c, 150);
    glEnd();

    // Main body of the bus
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 139); // Dark blue
    glVertex2f(10 + c, 130);
    glVertex2f(90 + c, 130);
    glVertex2f(90 + c, 155);
    glVertex2f(10 + c, 155);
    glEnd();

    // Lower part
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 139); // Dark blue
    glVertex2f(8 + c, 105);
    glVertex2f(90 + c, 105);
    glVertex2f(90 + c, 130);
    glVertex2f(8 + c, 130);
    glEnd();

    // Top part
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 0); // Black
    glVertex2f(11 + c, 153);
    glVertex2f(89 + c, 153);
    glVertex2f(89 + c, 130);
    glVertex2f(11 + c, 130);
    glEnd();

    // Windows
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255); // Window 1
    glVertex2f(40 + c, 135);
    glVertex2f(48 + c, 135);
    glVertex2f(48 + c, 150);
    glVertex2f(40 + c, 150);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255); // Window 2
    glVertex2f(50 + c, 135);
    glVertex2f(58 + c, 135);
    glVertex2f(58 + c, 150);
    glVertex2f(50 + c, 150);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255); // Window 3
    glVertex2f(60 + c, 135);
    glVertex2f(68 + c, 135);
    glVertex2f(68 + c, 150);
    glVertex2f(60 + c, 150);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255); // Window 4
    glVertex2f(78 + c, 135);
    glVertex2f(70 + c, 135);
    glVertex2f(70 + c, 150);
    glVertex2f(78 + c, 150);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255); // Window 5
    glVertex2f(88 + c, 135);
    glVertex2f(80 + c, 135);
    glVertex2f(80 + c, 150);
    glVertex2f(88 + c, 150);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255); // Window 6
    glVertex2f(12 + c, 135);
    glVertex2f(18 + c, 135);
    glVertex2f(18 + c, 150);
    glVertex2f(12 + c, 150);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255); // Window 7
    glVertex2f(20 + c, 135);
    glVertex2f(28 + c, 135);
    glVertex2f(28 + c, 150);
    glVertex2f(20 + c, 150);
    glEnd();

    // Door
    glBegin(GL_QUADS);
    glColor3ub(230, 247, 255);
    glVertex2f(38 + c, 105);
    glVertex2f(30 + c, 105);
    glVertex2f(30 + c, 145);
    glVertex2f(38 + c, 145);
    glEnd();

    // Wheels
    glColor3ub(0, 0, 0); // Back wheel
    circle(5, 10, 25 + c, 105);
    glColor3ub(255, 255, 255);
    circle(3, 6, 25 + c, 105);

    glColor3ub(0, 0, 0); // Front wheel
    circle(5, 10, 78 + c, 105);
    glColor3ub(255, 255, 255);
    circle(3, 6, 78 + c, 105);

    // Display text
    glColor3ub(255, 255, 255); // White text
    glRasterPos2i(50 + c, 115);
    glutBitmapCharacter(GLUT_BITMAP_9_BY_15, 'B');
    glutBitmapCharacter(GLUT_BITMAP_9_BY_15, 'U');
    glutBitmapCharacter(GLUT_BITMAP_9_BY_15, 'S');
    /// End ///

    glLineWidth(1);
    glBegin(GL_LINES);//Road top bar
	glColor3f(1.0,1.0,1.0);
    glVertex2i(0,81);
    glVertex2i(800,81);
    glEnd();

    glLineWidth(2);
    glBegin(GL_LINES);//Road middle bar
	glColor3f(1.0,1.0,1.0);
    glVertex2i(0,62);
    glVertex2i(800,62);
    glEnd();

    glLineWidth(1);
    glBegin(GL_LINES);//Road Bottom bar
	glColor3f(1.0,1.0,1.0);
    glVertex2i(0,39);
    glVertex2i(800,39);
    glEnd();

    ///
    glBegin(GL_QUADS);
    glColor3ub(90, 147, 48);
    glVertex2f(0,82);
    glVertex2f(800,82);
    glVertex2f(800,90);
    glVertex2f(0,90);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(90, 147, 48);
    glVertex2f(0,38);
    glVertex2f(800,38);
    glVertex2f(800,0);
    glVertex2f(0,0);
    glEnd();


    glBegin(GL_TRIANGLE_FAN);  ///Bottom tree1   ///
    glColor3ub(75,35,5);
    glVertex3f(680,0,0);
    glVertex3f(685,0,0);
    glVertex3f(685,20,0);
    glVertex3f(680,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(675,10,0);
    glVertex3f(690,10,0);
    glVertex3f(682.5,40,0);
    glVertex3f(682.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(676,15,0);
    glVertex3f(689,15,0);
    glVertex3f(682.5,45,0);
    glVertex3f(682.5,45,0);
    glEnd();


    glBegin(GL_TRIANGLE_FAN);  ///Bottom tree2   ///
    glColor3ub(75,35,5);
    glVertex3f(580,0,0);
    glVertex3f(585,0,0);
    glVertex3f(585,20,0);
    glVertex3f(580,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(575,10,0);
    glVertex3f(590,10,0);
    glVertex3f(582.5,40,0);
    glVertex3f(582.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(576,15,0);
    glVertex3f(589,15,0);
    glVertex3f(582.5,45,0);
    glVertex3f(582.5,45,0);
    glEnd();

     glBegin(GL_TRIANGLE_FAN);  ///Bottom tree3   ///
    glColor3ub(75,35,5);
    glVertex3f(480,0,0);
    glVertex3f(485,0,0);
    glVertex3f(485,20,0);
    glVertex3f(480,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(475,10,0);
    glVertex3f(490,10,0);
    glVertex3f(482.5,40,0);
    glVertex3f(482.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(476,15,0);
    glVertex3f(489,15,0);
    glVertex3f(482.5,45,0);
    glVertex3f(482.5,45,0);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///Bottom tree4   ///
    glColor3ub(75,35,5);
    glVertex3f(380,0,0);
    glVertex3f(385,0,0);
    glVertex3f(385,20,0);
    glVertex3f(380,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(375,10,0);
    glVertex3f(390,10,0);
    glVertex3f(382.5,40,0);
    glVertex3f(382.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(376,15,0);
    glVertex3f(389,15,0);
    glVertex3f(382.5,45,0);
    glVertex3f(382.5,45,0);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///Bottom tree5   ///
    glColor3ub(75,35,5);
    glVertex3f(280,0,0);
    glVertex3f(285,0,0);
    glVertex3f(285,20,0);
    glVertex3f(280,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(275,10,0);
    glVertex3f(290,10,0);
    glVertex3f(282.5,40,0);
    glVertex3f(282.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(276,15,0);
    glVertex3f(289,15,0);
    glVertex3f(282.5,45,0);
    glVertex3f(282.5,45,0);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///Bottom tree6   ///
    glColor3ub(75,35,5);
    glVertex3f(180,0,0);
    glVertex3f(185,0,0);
    glVertex3f(185,20,0);
    glVertex3f(180,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(175,10,0);
    glVertex3f(190,10,0);
    glVertex3f(182.5,40,0);
    glVertex3f(182.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(176,15,0);
    glVertex3f(189,15,0);
    glVertex3f(182.5,45,0);
    glVertex3f(182.5,45,0);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///Bottom tree7   ///
    glColor3ub(75,35,5);
    glVertex3f(80,0,0);
    glVertex3f(85,0,0);
    glVertex3f(85,20,0);
    glVertex3f(80,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(75,10,0);
    glVertex3f(90,10,0);
    glVertex3f(82.5,40,0);
    glVertex3f(82.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(76,15,0);
    glVertex3f(89,15,0);
    glVertex3f(82.5,45,0);
    glVertex3f(82.5,45,0);
    glEnd();
    ///End///


    ///....Right side circle tree 1 ///
    glColor3ub(139, 146, 22);
    circle(3,6,98,101);
    glColor3ub(139, 146, 22);
    circle(5,12,93,111);
    glColor3ub(139, 146, 22);
    circle(5,12,103,111);
    glColor3ub(139, 146, 22);
    circle(5,12,108,106);
    glColor3ub(139, 146, 22);
    circle(5,12,88,121);


    glColor3ub(181, 106, 76);
    circle(5,12,93,123);
    glColor3ub(139, 146, 22);
    circle(5,12,94,123);
    glColor3ub(139, 146, 22);
    circle(5,12,98,141);
    glColor3ub(139, 146, 22);
    circle(4,10,93,136);
    glColor3ub(181, 106, 76);
    circle(4,10,95,134);

    glColor3ub(139, 146, 22);
    circle(4,10,96,133);

    glColor3ub(139, 146, 22);
    circle(5,12,108,131);
    glColor3ub(139, 146, 22);
    circle(5,12,103,131);
    glColor3ub(181, 106, 76);
    circle(5,12,102,126);
    glColor3ub(139, 146, 22);
    circle(5,12,101,125);
    glColor3ub(139, 146, 22);
    circle(5,12,113,121);
    glColor3ub(181, 106, 76);
    circle(5,12,108,116);
    glColor3ub(139, 146, 22);
    circle(5,12,107,116);
    glColor3ub(139, 146, 22);
    circle(5,12,98,119);
    glColor3ub(139, 146, 22);
    circle(5,12,110,141);



    glColor3ub(227, 91, 137);         ///Full........ .........comp.
    circle(1,2,98,119);
    glColor3ub(227, 91, 137);
    circle(1,2,98,133);
    glColor3ub(227, 91, 137);
    circle(1,2,108,133);
    glColor3ub(227, 91, 137);
    circle(1,2,113,128);
    glColor3ub(227, 91, 137);
    circle(1,2,87,119);
    glColor3ub(227, 91, 137);
    circle(1,2.5,93,134);
    glColor3ub(227, 91, 137);
    circle(1,1.5,94,110);
    glColor3ub(227, 91, 137);
    circle(1,2.5,108,106);
    glColor3ub(227, 91, 137);
    circle(1,3,113,119);
    glColor3ub(227, 91, 137);
    circle(1,3,103,103);



    glBegin(GL_TRIANGLE_FAN);  ///tree 1.........   ///
    glColor3ub(75, 35, 5);
    glVertex2f(103,90);
    glVertex2f(106,90);
    glVertex2f(105,100);
    glVertex2f(100,130);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);  ///tree 1.........   ///
    glColor3ub(75, 35, 5);
    glVertex2f(103,90);
    glVertex2f(106,90);
    glVertex2f(102,100);
    glVertex2f(96,110);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///tree 1.........  ///
    glColor3ub(75, 35, 5);
    glVertex2f(102,90);
    glVertex2f(106,90);
    glVertex2f(107,110);
    glVertex2f(110,140);
    glEnd();
///End Right side circle tree 1///


      ///....Right side circle tree 2  ///
    glColor3ub(139, 146, 22);
    circle(3,6,468,101);
    glColor3ub(139, 146, 22);
    circle(5,12,463,111);
    glColor3ub(139, 146, 22);
    circle(5,12,473,111);
    glColor3ub(139, 146, 22);
    circle(5,12,478,106);
    glColor3ub(139, 146, 22);
    circle(5,12,458,121);


    glColor3ub(181, 106, 76);
    circle(5,12,463,123);
    glColor3ub(139, 146, 22);
    circle(5,12,464,123);
    glColor3ub(139, 146, 22);
    circle(5,12,468,141);
    glColor3ub(139, 146, 22);
    circle(4,10,463,136);
    glColor3ub(181, 106, 76);
    circle(4,10,465,134);

    glColor3ub(139, 146, 22);
    circle(4,10,466,133);

    glColor3ub(139, 146, 22);
    circle(5,12,478,131);
    glColor3ub(139, 146, 22);
    circle(5,12,473,131);
    glColor3ub(181, 106, 76);
    circle(5,12,472,126);
    glColor3ub(139, 146, 22);
    circle(5,12,471,125);
    glColor3ub(139, 146, 22);
    circle(5,12,483,121);
    glColor3ub(181, 106, 76);
    circle(5,12,478,116);
    glColor3ub(139, 146, 22);
    circle(5,12,477,116);
    glColor3ub(139, 146, 22);
    circle(5,12,468,119);
    glColor3ub(139, 146, 22);
    circle(5,12,480,141);



    glColor3ub(227, 91, 137);         ///Full........ .........comp.
    circle(1,2,468,119);
    glColor3ub(227, 91, 137);
    circle(1,2,468,133);
    glColor3ub(227, 91, 137);
    circle(1,2,478,133);
    glColor3ub(227, 91, 137);
    circle(1,2,483,128);
    glColor3ub(227, 91, 137);
    circle(1,2,457,119);
    glColor3ub(227, 91, 137);
    circle(1,2.5,463,134);
    glColor3ub(227, 91, 137);
    circle(1,1.5,464,110);
    glColor3ub(227, 91, 137);
    circle(1,2.5,478,106);
    glColor3ub(227, 91, 137);
    circle(1,3,483,119);
    glColor3ub(227, 91, 137);
    circle(1,3,473,103);



    glBegin(GL_TRIANGLE_FAN);  ///tree 2.........  ///
    glColor3ub(75, 35, 5);
    glVertex2f(473,90);
    glVertex2f(476,90);
    glVertex2f(475,100);
    glVertex2f(470,130);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);  ///tree 2.........  ///
    glColor3ub(75, 35, 5);
    glVertex2f(473,90);
    glVertex2f(476,90);
    glVertex2f(472,100);
    glVertex2f(466,110);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///tree 2.........  ///
    glColor3ub(75, 35, 5);
    glVertex2f(472,90);
    glVertex2f(476,90);
    glVertex2f(477,110);
    glVertex2f(480,140);
    glEnd();
///End Right side circle tree 2///

///....Left side circle tree ///
    glColor3ub(139, 146, 22);
    circle(3,6,280,101);
    glColor3ub(139, 146, 22);
    circle(5,12,275,111);
    glColor3ub(139, 146, 22);
    circle(5,12,285,111);
    glColor3ub(139, 146, 22);
    circle(5,12,290,106);
    glColor3ub(139, 146, 22);
    circle(5,12,270,121);


    glColor3ub(181, 106, 76);
    circle(5,12,275,123);
    glColor3ub(139, 146, 22);
    circle(5,12,276,123);
    glColor3ub(139, 146, 22);
    circle(5,12,280,141);
    glColor3ub(139, 146, 22);
    circle(4,10,275,136);
    glColor3ub(181, 106, 76);
    circle(4,10,277,134);

    glColor3ub(139, 146, 22);
    circle(4,10,278,133);

    glColor3ub(139, 146, 22);
    circle(5,12,290,131);
    glColor3ub(139, 146, 22);
    circle(5,12,285,131);
    glColor3ub(181, 106, 76);
    circle(5,12,284,126);
    glColor3ub(139, 146, 22);
    circle(5,12,283,125);
    glColor3ub(139, 146, 22);
    circle(5,12,295,121);
    glColor3ub(181, 106, 76);
    circle(5,12,290,116);
    glColor3ub(139, 146, 22);
    circle(5,12,289,116);
    glColor3ub(139, 146, 22);
    circle(5,12,280,119);
    glColor3ub(139, 146, 22);
    circle(5,12,292,141);



    glColor3ub(227, 91, 137);         ///Full......... .........comp.
    circle(1,2,280,119);
    glColor3ub(227, 91, 137);
    circle(1,2,280,133);
    glColor3ub(227, 91, 137);
    circle(1,2,290,133);
    glColor3ub(227, 91, 137);
    circle(1,2,295,128);
    glColor3ub(227, 91, 137);
    circle(1,2,269,119);
    glColor3ub(227, 91, 137);
    circle(1,2.5,275,134);
    glColor3ub(227, 91, 137);
    circle(1,1.5,276,110);
    glColor3ub(227, 91, 137);
    circle(1,2.5,290,106);
    glColor3ub(227, 91, 137);
    circle(1,3,295,119);
    glColor3ub(227, 91, 137);
    circle(1,3,285,103);


    glBegin(GL_TRIANGLE_FAN);  ///tree.........   ///
    glColor3ub(75, 35, 5);
    glVertex2f(285,90);
    glVertex2f(288,90);
    glVertex2f(287,100);
    glVertex2f(282,130);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);  ///tree.........   ///
    glColor3ub(75, 35, 5);
    glVertex2f(285,90);
    glVertex2f(288,90);
    glVertex2f(284,100);
    glVertex2f(278,110);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///tree.........   ///
    glColor3ub(75, 35, 5);
    glVertex2f(284,90);
    glVertex2f(288,90);
    glVertex2f(289,110);
    glVertex2f(292,140);
    glEnd();
///End Left side circle tree///



    glBegin(GL_TRIANGLE_FAN);  ///tree.........beside 3rd Building........3   ///
    glColor3ub(139,99,47);
    glVertex2f(680,90);
    glVertex2f(685,90);
    glVertex2f(685,100);
    glVertex2f(680,100);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex2f(675,100);
    glVertex2f(690,100);
    glVertex2f(682.5,130);
    glVertex2f(682.5,130);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex2f(676,110);
    glVertex2f(689,110);
    glVertex2f(682.5,140);
    glVertex2f(682.5,140);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex2f(677,122);
    glVertex2f(688,122);
    glVertex2f(682.5,155);
    glVertex2f(682.5,155);
    glEnd();


    glBegin(GL_TRIANGLE_FAN);  ///tree.........beside 3rd Building........4   ///
    glColor3ub(139,99,47);
    glVertex2f(690,90);
    glVertex2f(695,90);
    glVertex2f(695,105);
    glVertex2f(690,105);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0,99,47);
    glVertex2f(685,105);
    glVertex2f(700,105);
    glVertex2f(692.5,135);
    glVertex2f(692.5,135);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex2f(686,115);
    glVertex2f(699,115);
    glVertex2f(692.5,145);
    glVertex2f(692.5,145);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex2f(687,127);
    glVertex2f(698,127);
    glVertex2f(692.5,165);
    glVertex2f(692.5,165);
    glEnd();


    glColor3ub(139, 146, 22);     ///....tree.........beside 3rd Building........6 ///
    circle(3,6,625,100);
    glColor3ub(139, 146, 22);
    circle(5,12,620,110);
    glColor3ub(139, 146, 22);
    circle(5,12,630,110);
    glColor3ub(139, 146, 22);
    circle(5,12,635,105);
    glColor3ub(139, 146, 22);
    circle(5,12,615,120);


    glColor3ub(181, 106, 76);
    circle(5,12,620,122);
    glColor3ub(139, 146, 22);
    circle(5,12,621,122);
    glColor3ub(139, 146, 22);
    circle(5,12,625,140);
    glColor3ub(139, 146, 22);
    circle(4,10,620,135);
    glColor3ub(181, 106, 76);
    circle(4,10,622,133);

    glColor3ub(139, 146, 22);
    circle(4,10,623,132);

    glColor3ub(139, 146, 22);
    circle(5,12,635,130);
    glColor3ub(139, 146, 22);
    circle(5,12,630,130);
    glColor3ub(181, 106, 76);
    circle(5,12,629,125);
    glColor3ub(139, 146, 22);
    circle(5,12,628,124);
    glColor3ub(139, 146, 22);
    circle(5,12,640,120);
    glColor3ub(181, 106, 76);
    circle(5,12,635,115);
    glColor3ub(139, 146, 22);
    circle(5,12,634,115);
    glColor3ub(139, 146, 22);
    circle(5,12,625,118);
    glColor3ub(139, 146, 22);
    circle(5,12,637,140);



    glColor3ub(227, 91, 137);         ///Full..........3rd Building.........comp.
    circle(1,2,625,118);
    glColor3ub(227, 91, 137);
    circle(1,2,625,138);
    glColor3ub(227, 91, 137);
    circle(1,2,635,138);
    glColor3ub(227, 91, 137);
    circle(1,2,630,127);
    glColor3ub(227, 91, 137);
    circle(1,2,614,118);
    glColor3ub(227, 91, 137);
    circle(1,2.5,620,133);
    glColor3ub(227, 91, 137);
    circle(1,1.5,621,109);
    glColor3ub(227, 91, 137);
    circle(1,2.5,635,105);
    glColor3ub(227, 91, 137);
    circle(1,3,640,118);
    glColor3ub(227, 91, 137);
    circle(1,3,635,120);


    glBegin(GL_TRIANGLE_FAN);  ///tree.........beside 3rd Building........6   ///
    glColor3ub(75,35,5);
    glVertex2f(630,90);
    glVertex2f(633,90);
    glVertex2f(632,100);
    glVertex2f(627,130);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);  ///tree.........beside 3rd Building........6   ///
    glColor3ub(75,35,5);
    glVertex2f(630,90);
    glVertex2f(633,90);
    glVertex2f(629,100);
    glVertex2f(623,110);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///tree.........beside 3rd Building........6   ///
    glColor3ub(75,35,5);
    glVertex2f(629,90);
    glVertex2f(633,90);
    glVertex2f(634,110);
    glVertex2f(637,140);
    glEnd();


    glColor3ub(232,241,255);        ///....Cloud.......1 covering sun....///
    circle(13,20,400,665);
    glColor3ub(252,254,255);
    circle(11,18,400,665);

    glColor3ub(232,241,255);
    circle(10,20,410,675);
    glColor3ub(252,254,255);
    circle(10,20,412,672);

    glColor3ub(232,241,255);
    circle(13,20,410,655);

    glColor3ub(221,229,247);
    circle(9,20,420,680);
    glColor3ub(252,254,255);
    circle(8,18,420,679);

    glColor3ub(232,241,255);
    circle(9,20,420,650);
    glColor3ub(252,254,255);
    circle(8,18,420,652);

    glColor3ub(221,229,247);
    circle(9,20,430,685);
    glColor3ub(252,254,255);
    circle(8,18,430,683);

    glColor3ub(232,241,255);
    circle(9,20,425,655);
    glColor3ub(252,254,255);
    circle(8,18,435,657);

    glColor3ub(232,241,255);
    circle(9,20,440,675);

    glColor3ub(221,229,247);
    circle(8,18,445,665);
    glColor3ub(252,254,255);
    circle(8,18,443,663);
    glColor3ub(252,254,255);
    circle(18,18,420,664);
    glColor3ub(252,254,255);
    circle(18,25,417,665);


    glColor3ub(232,241,255);        ///....Cloud.......2.....///
    circle(13,20,p+200,745);
    glColor3ub(252,254,255);
    circle(11,18,p+200,745);

    glColor3ub(232,241,255);
    circle(10,20,p+210,755);
    glColor3ub(252,254,255);
    circle(10,20,p+212,762);

    glColor3ub(232,241,255);
    circle(13,20,p+210,735);

    glColor3ub(221,229,247);
    circle(9,20,p+220,750);
    glColor3ub(252,254,255);
    circle(8,18,p+220,759);

    glColor3ub(232,241,255);
    circle(9,20,p+220,756);
    glColor3ub(252,254,255);
    circle(8,18,p+220,752);

    glColor3ub(232,241,255);
    circle(9,20,p+230,765);
    glColor3ub(252,254,255);
    circle(8,18,p+230,761);

    glColor3ub(232,241,255);
    circle(9,20,p+225,745);
    glColor3ub(252,254,255);
    circle(8,18,p+235,747);

    glColor3ub(232,241,255);
    circle(9,20,p+240,755);

    glColor3ub(221,229,247);
    circle(8,18,p+243,745);
    glColor3ub(252,254,255);
    circle(8,18,p+240,743);
    glColor3ub(173,197,224);
    circle(8,18,p+230,733);
    glColor3ub(252,254,255);
    circle(8,18,p+230,738);
    glColor3ub(173,197,224);
    circle(8,18,p+220,723);
    glColor3ub(252,254,255);
    circle(8,18,p+220,728);



    glColor3ub(252,254,255);
    circle(23,16,p+242,744);
    glColor3ub(173,197,224);
    circle(21,20,p+240,720);
    glColor3ub(252,254,255);
    circle(21,21,p+238,723);


    glColor3ub(252,254,255);
    circle(18,18,p+210,744);
    glColor3ub(252,254,255);
    circle(18,25,p+220,745);

    glColor3ub(173,197,224);
    circle(10,20,p+235,715);
    glColor3ub(252,254,255);
    circle(10,20,p+235,719);



    glColor3ub(173,197,224);        ///....Cloud.......3.....///
    circle(9,15,p+20,685);
    glColor3ub(252,254,255);
    circle(6,14,p+21,685);

    glColor3ub(232,241,255);
    circle(7,16,p+30,695);
    glColor3ub(252,254,255);
    circle(7,14,p+32,692);

    glColor3ub(252,254,255);
    circle(12,16,p+28,680);

    glColor3ub(221,229,247);
    circle(10,15,p+45,690);
    glColor3ub(252,254,255);
    circle(9,13,p+43,685);
    glColor3ub(252,254,255);
    circle(15,18,p+48,670);

    glColor3ub(173,197,224);
    circle(6,14,p+30,680);
    glColor3ub(252,254,255);
    circle(6,13,p+30,677);

    glColor3ub(173,197,224);
    circle(6,14,p+38,668);
    glColor3ub(252,254,255);
    circle(6,13,p+36,667);


    glColor3ub(252,254,255);
    circle(11,15,p+29,668);

     ///....Cloud.......4.....///

    glColor3ub(173,197,224);
    circle(9,15,590,695);
    glColor3ub(252,254,255);
    circle(6,14,591,695);

    glColor3ub(232,241,255);
    circle(7,16,600,705);
    glColor3ub(252,254,255);
    circle(7,14,602,702);

    glColor3ub(252,254,255);
    circle(12,16,598,690);

    glColor3ub(221,229,247);
    circle(10,15,615,700);
    glColor3ub(252,254,255);
    circle(9,13,613,695);
    glColor3ub(252,254,255);
    circle(15,18,618,680);

    glColor3ub(173,197,224);
    circle(6,14,600,690);
    glColor3ub(252,254,255);
    circle(6,13,600,687);

    glColor3ub(173,197,224);
    circle(6,14,608,678);
    glColor3ub(252,254,255);
    circle(6,13,606,677);


    glColor3ub(252,254,255);
    circle(11,15,599,678);


    if(p<= 800)
        p = p + 0.1;
    else
        p = -10;


    ///..........B U S...........1

    if(j<= 800)
        j = j + 0.3;
    else
        j = -250;

    // Second floor
    glBegin(GL_QUADS);
    glColor3ub(255, 0, 0); // Pure red
    glVertex2f(j+10,105);  //.....bus
    glVertex2f(j+90,105);
    glVertex2f(j+90,155);
    glVertex2f(j+10,155);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(0, 51, 0);
    glVertex2f(j+11,131);  //top..........
    glVertex2f(j+89,131);
    glVertex2f(j+89,152);
    glVertex2f(j+11,152);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 51, 0);
    glVertex2f(j+11,125);
    glVertex2f(j+89,125);
    glVertex2f(j+89,130);
    glVertex2f(j+11,130);
    glEnd();


    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+12,135);  //window..........
    glVertex2f(j+20,135);
    glVertex2f(j+20,150);
    glVertex2f(j+12,150);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+22,135);  //window..........
    glVertex2f(j+30,135);
    glVertex2f(j+30,150);
    glVertex2f(j+22,150);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+32,135);  //window..........
    glVertex2f(j+40,135);
    glVertex2f(j+40,150);
    glVertex2f(j+32,150);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+42,135);  //window..........
    glVertex2f(j+50,135);
    glVertex2f(j+50,150);
    glVertex2f(j+42,150);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+52,135);  //window..........
    glVertex2f(j+60,135);
    glVertex2f(j+60,150);
    glVertex2f(j+52,150);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 247, 255);
    glVertex2f(j+62,135);  //window..........
    glVertex2f(j+70,135);
    glVertex2f(j+70,150);
    glVertex2f(j+62,150);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+72,135);  //window..........
    glVertex2f(j+80,135);
    glVertex2f(j+80,150);
    glVertex2f(j+72,150);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+82,135);  //window..........
    glVertex2f(j+88,135);
    glVertex2f(j+88,150);
    glVertex2f(j+82,150);
    glEnd();


    // First floor
    glBegin(GL_QUADS);
    glColor3ub(255, 0, 0); // Pure red
    glVertex2f(j+90,98);  //bus...................
    glVertex2f(j+95,98);
    glVertex2f(j+95,100);
    glVertex2f(j+90,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(26, 26, 0);
    glVertex2f(j+94,89);   // bus font glass
    glVertex2f(j+96,89);
    glVertex2f(j+96,100);
    glVertex2f(j+94,100);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(255, 0, 0); // Pure red
    glVertex2f(j+10,80);  //.....bus
    glVertex2f(j+90,80);
    glVertex2f(j+90,105);
    glVertex2f(j+10,105);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(255, 0, 0); // Pure red
    glVertex2f(j+10,55);  //top..........lowerpart
    glVertex2f(j+90,55);
    glVertex2f(j+90,80);
    glVertex2f(j+10,80);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(0, 51, 0);
    glVertex2f(j+11,81);  //top..........
    glVertex2f(j+89,81);
    glVertex2f(j+89,102);
    glVertex2f(j+11,102);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(0, 51, 0);
    glVertex2f(j+11,75);
    glVertex2f(j+89,75);
    glVertex2f(j+89,80);
    glVertex2f(j+11,80);
    glEnd();


    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+12,85);  //window..........
    glVertex2f(j+20,85);
    glVertex2f(j+20,100);
    glVertex2f(j+12,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+22,85);  //window..........
    glVertex2f(j+30,85);
    glVertex2f(j+30,100);
    glVertex2f(j+22,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+32,85);  //window..........
    glVertex2f(j+40,85);
    glVertex2f(j+40,100);
    glVertex2f(j+32,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+42,85);  //window..........
    glVertex2f(j+50,85);
    glVertex2f(j+50,100);
    glVertex2f(j+42,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+52,85);  //window..........
    glVertex2f(j+60,85);
    glVertex2f(j+60,100);
    glVertex2f(j+52,100);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(230, 247, 255);
    glVertex2f(j+62,55);  //..door..........
    glVertex2f(j+70,55);
    glVertex2f(j+70,95);
    glVertex2f(j+62,95);
    glEnd();


    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+72,85);  //window..........
    glVertex2f(j+80,85);
    glVertex2f(j+80,100);
    glVertex2f(j+72,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(j+82,85);  //window..........
    glVertex2f(j+88,85);
    glVertex2f(j+88,100);
    glVertex2f(j+82,100);
    glEnd();


    glColor3ub(0,0,0);          //....chaka....back
    circle(5,10,j+25,55);
    glColor3ub(255,255,255);
    circle(3,6,j+25,55);

    glColor3ub(0,0,0);
    circle(5,10,j+78,55);
    glColor3ub(255,255,255);
    circle(3,6,j+78,55);

    glColor3ub(255, 200, 50);
    glRasterPos2i(j+43,110);

    glutBitmapCharacter(GLUT_BITMAP_9_BY_15,'B');
    glutBitmapCharacter(GLUT_BITMAP_9_BY_15,'R');
    glutBitmapCharacter(GLUT_BITMAP_9_BY_15,'T');
    glutBitmapCharacter(GLUT_BITMAP_9_BY_15,'C');



    if(k<= 850)
        k = k + 0.7;
    else
        k = -160;

        // .........PLANE......... //

    // Body
    glBegin(GL_POLYGON);
    glColor3ub(255, 255, 255);
    glVertex2f(k + 15, 640);
    glVertex2f(k + 2, 657);
    glVertex2f(k + 2, 660);
    glVertex2f(k + 70, 660);
    glVertex2f(k + 80, 645);
    glVertex2f(k + 75, 640);
    glEnd();
    glBegin(GL_POLYGON);
    glColor3ub(127, 153, 178);
    glVertex2f(k + 70, 640);
    glVertex2f(k + 65, 645);
    glVertex2f(k + 11, 645);
    glVertex2f(k + 15, 640);
    glEnd();

    // Tail
    glBegin(GL_POLYGON);
    glColor3ub(127, 153, 178);
    glVertex2f(k + 5, 660);
    glVertex2f(k + 5, 675);
    glVertex2f(k + 12, 675);
    glVertex2f(k + 14, 667);
    glVertex2f(k + 20, 660);
    glEnd();

    glBegin(GL_POLYGON);
    glColor3ub(127, 153, 178);
    glVertex2f(k + 2, 657);
    glVertex2f(k, 650);
    glVertex2f(k + 5, 650);
    glVertex2f(k + 10, 657);
    glEnd();

    // Wings
    glBegin(GL_POLYGON);
    glColor3ub(127, 153, 178);
    glVertex2f(k + 35, 665);
    glVertex2f(k + 40, 665);  // Adjusted to align with the body
    glVertex2f(k + 45, 660);  // Adjusted to align with the body
    glVertex2f(k + 37, 660);
    glEnd();

    glBegin(GL_POLYGON);
    glColor3ub(127, 153, 178);
    glVertex2f(k + 50, 647);  // Wing starting point
    glVertex2f(k + 40, 647);  // Wing end point
    glVertex2f(k + 32, 630);  // Wing bottom point
    glVertex2f(k + 38, 630);  // Wing bottom point
    glEnd();

    // Windows
    glPointSize(3);
    glBegin(GL_POINTS);
    glColor3ub(0, 0, 0);
    glVertex2f(k + 22, 652);
    glVertex2f(k + 25, 652);
    glVertex2f(k + 28, 652);
    glVertex2f(k + 31, 652);
    glVertex2f(k + 34, 652);
    glVertex2f(k + 37, 652);
    glVertex2f(k + 40, 652);
    glVertex2f(k + 43, 652);
    glVertex2f(k + 46, 652);
    glVertex2f(k + 49, 652);
    glVertex2f(k + 52, 652);
    glVertex2f(k + 55, 652);
    glVertex2f(k + 58, 652);
    glEnd();

    // Front glass
    glBegin(GL_POLYGON);
    glColor3ub(0, 0, 0);
    glVertex2f(k + 65, 655);
    glVertex2f(k + 65, 650);
    glVertex2f(k + 76, 650);
    glVertex2f(k + 73, 655);
    glEnd();

    glLineWidth(0.5);
    glBegin(GL_LINES);
    glColor3ub(255, 255, 255);
    glVertex2f(k + 72, 655);
    glVertex2f(k + 72, 650);
    glEnd();
    glBegin(GL_LINES);
    glColor3ub(255, 255, 255);
    glVertex2f(k + 68.5, 655);
    glVertex2f(k + 68.5, 650);
    glEnd();
    /// End ///

    if(b<= 800)
        b = b + 0.3;
    else
        b = -100;

        ///..........B U S...........2

    glBegin(GL_QUADS);
    glColor3ub(255, 200, 50); // Orangish-yellow
    glVertex2f(b+90,98);  //bus...................
    glVertex2f(b+95,98);
    glVertex2f(b+95,100);
    glVertex2f(b+90,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(26, 26, 0);
    glVertex2f(b+94,89);   // bus font glass
    glVertex2f(b+96,89);
    glVertex2f(b+96,100);
    glVertex2f(b+94,100);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(255, 200, 50); // Orangish-yellow
    glVertex2f(b+10,80);  //.....bus
    glVertex2f(b+90,80);
    glVertex2f(b+90,105);
    glVertex2f(b+10,105);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(255, 200, 50); // Orangish-yellow
    glVertex2f(b+10,55);  //top..........lowerpart
    glVertex2f(b+92,55);
    glVertex2f(b+92,80);
    glVertex2f(b+10,80);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(0, 51, 0);
    glVertex2f(b+11,81);  //top..........
    glVertex2f(b+89,81);
    glVertex2f(b+89,102);
    glVertex2f(b+11,102);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+12,85);  //window..........
    glVertex2f(b+20,85);
    glVertex2f(b+20,100);
    glVertex2f(b+12,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+22,85);  //window..........
    glVertex2f(b+30,85);
    glVertex2f(b+30,100);
    glVertex2f(b+22,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+32,85);  //window..........
    glVertex2f(b+40,85);
    glVertex2f(b+40,100);
    glVertex2f(b+32,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+42,85);  //window..........
    glVertex2f(b+50,85);
    glVertex2f(b+50,100);
    glVertex2f(b+42,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+52,85);  //window..........
    glVertex2f(b+60,85);
    glVertex2f(b+60,100);
    glVertex2f(b+52,100);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(230, 247, 255);
    glVertex2f(b+62,55);  //..door..........
    glVertex2f(b+70,55);
    glVertex2f(b+70,95);
    glVertex2f(b+62,95);
    glEnd();


    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+72,85);  //window..........
    glVertex2f(b+80,85);
    glVertex2f(b+80,100);
    glVertex2f(b+72,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+82,85);  //window..........
    glVertex2f(b+88,85);
    glVertex2f(b+88,100);
    glVertex2f(b+82,100);
    glEnd();

    glColor3ub(255, 255, 204);          //....chaka....back
    circle(4,8,b+45,65);
    glColor3ub(255, 255, 204);
    circle(2,4,b+55,75);
    glColor3ub(255, 255, 204);
    circle(3,6,b+15,75);
    glColor3ub(255, 255, 204);
    circle(2,4,b+35,65);
    glColor3ub(255, 255, 204);
    circle(2,4,b+75,75);


    glColor3ub(0,0,0);          //....chaka....back
    circle(5,10,b+25,55);
    glColor3ub(255,255,255);
    circle(3,6,b+25,55);

    glColor3ub(0,0,0);
    circle(5,10,b+78,55);
    glColor3ub(255,255,255);
    circle(3,6,b+78,55);

    glColor3ub(255, 0, 0); // Pure red
    glRasterPos2i(b+40,65);

    glutBitmapCharacter(GLUT_BITMAP_9_BY_15,'B');
    glutBitmapCharacter(GLUT_BITMAP_9_BY_15,'U');
    glutBitmapCharacter(GLUT_BITMAP_9_BY_15,'S');

    /// Metro rail runway
    glBegin(GL_QUADS);
    glColor3f(0.4,0.4,0.4);
    glVertex2f(0,280);
    glVertex2f(800,280);
    glVertex2f(800,350);
    glVertex2f(0,350);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.5,0.5,0.5);
    glVertex2f(0,310);
    glVertex2f(800,310);
    glVertex2f(800,340);
    glVertex2f(0,340);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.3,0.3,0.3);
    glVertex2f(200,280);
    glVertex2f(200,310);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.3,0.3,0.3);
    glVertex2f(450,280);
    glVertex2f(450,310);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.3,0.3,0.3);
    glVertex2f(690,280);
    glVertex2f(690,310);
    glEnd();

    glLineWidth(4);    ///
    glBegin(GL_LINES);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(190,350);
    glVertex2f(190,450);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(191,450);
    glVertex2f(179,440);
    glEnd();
    glBegin(GL_LINES);    ///
    glColor3f(0.2,0.2,0.2);
    glVertex2f(380,350);
    glVertex2f(380,450);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(381,450);
    glVertex2f(369,440);
    glEnd();
    glBegin(GL_LINES);   ///
    glColor3f(0.2,0.2,0.2);
    glVertex2f(570,350);
    glVertex2f(570,450);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(571,450);
    glVertex2f(559,440);
    glEnd();

    glBegin(GL_QUADS);        /// ......Pillar 1...... ///
    glColor3f(0.5, 0.5, 0.5);
    glVertex2f(50,250);
    glVertex2f(100,250);
    glVertex2f(100,280);
    glVertex2f(50,280);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.4,0.4,0.4);
    glVertex2f(65,250);
    glVertex2f(85,250);
    glVertex2f(85,38);
    glVertex2f(65,38);
    glEnd();

    glBegin(GL_QUADS);        /// ......Pillar 2...... ///
    glColor3f(0.5,0.5,0.5);
    glVertex2f(300,250);
    glVertex2f(350,250);
    glVertex2f(350,280);
    glVertex2f(300,280);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.4,0.4,0.4);
    glVertex2f(315,250);
    glVertex2f(335,250);
    glVertex2f(335,38);
    glVertex2f(315,38);
    glEnd();

    glBegin(GL_QUADS);        /// ......Pillar 3...... ///
    glColor3f(0.5,0.5,0.5);
    glVertex2f(550,250);
    glVertex2f(600,250);
    glVertex2f(600,280);
    glVertex2f(550,280);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.4,0.4,0.4);
    glVertex2f(565,250);
    glVertex2f(585,250);
    glVertex2f(585,38);
    glVertex2f(565,38);
    glEnd();
    /// End ///

    // Update position based on metroStop and metroSpeed
    if (!metroStop) {
        if (a <= 900) {
            a += metroSpeed; // Move the metro forward
        } else {
            a = -250; // Reset position
        }
    }

    /// Metro Rail Train
    glBegin(GL_QUADS);     // 1st partition
    glColor3f(0.95,0.95,0.97);
    glVertex2f(19+a,400);
    glVertex2f(100+a,400);
    glVertex2f(100+a,340);
    glVertex2f(19+a,340);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.95,0.95,0.97);
    glVertex2f(100+a,400);
    glVertex2f(100+a,340);
    glVertex2f(110+a,340);
    glVertex2f(110+a,400);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.18,0.55,0.34);
    glVertex2f(19+a,384);
    glVertex2f(19+a,391);
    glVertex2f(100+a,391);
    glVertex2f(100+a,384);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.18,0.55,0.34);
    glVertex2f(100+a,400);
    glVertex2f(100+a,370);
    glVertex2f(110+a,370);
    glVertex2f(110+a,400);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.8,0,0);
    glVertex2f(100+a,350);
    glVertex2f(100+a,340);
    glVertex2f(110+a,340);
    glVertex2f(110+a,350);
    glEnd();
    glPointSize(8);
    glBegin(GL_POINTS);
    glColor3f(0,0.8,0);
    glVertex2f(105+a,360);
    glEnd();
    glPointSize(4);
    glBegin(GL_POINTS);
    glColor3f(1,0,0);
    glVertex2f(105+a,360);
    glEnd();

    // 2nd Partition
    glBegin(GL_QUADS);
    glColor3f(0.95,0.95,0.97);
    glVertex2f(16+a,400);
    glVertex2f(-71+a,400);
    glVertex2f(-71+a,340);
    glVertex2f(16+a,340);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.18,0.55,0.34);
    glVertex2f(16+a,384);
    glVertex2f(16+a,391);
    glVertex2f(-71+a,391);
    glVertex2f(-71+a,384);
    glEnd();
    glLineWidth(2);     // Joint
    glBegin(GL_LINES);
    glColor3f(0.3,0.3,0.3);
    glVertex2f(16+a,350);
    glVertex2f(19+a,350);
    glEnd();

    // 3rd Partition
    glBegin(GL_QUADS);
    glColor3f(0.95,0.95,0.97);
    glVertex2f(-74+a,400);
    glVertex2f(-162+a,400);
    glVertex2f(-162+a,340);
    glVertex2f(-74+a,340);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.18,0.55,0.34);
    glVertex2f(-74+a,384);
    glVertex2f(-74+a,391);
    glVertex2f(-162+a,391);
    glVertex2f(-162+a,384);
    glEnd();
    glLineWidth(2);     // Joint
    glBegin(GL_LINES);
    glColor3f(0.3,0.3,0.3);
    glVertex2f(-71+a,350);
    glVertex2f(-74+a,350);
    glEnd();

    // Front Window
    glBegin(GL_QUADS);
    glColor3f(0.75,0.75,0.75);
    glVertex2f(101+a,390);
    glVertex2f(101+a,375);
    glVertex2f(109+a,375);
    glVertex2f(109+a,390);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(101+a,375);
    glVertex2f(101+a,390);
    glVertex2f(109+a,375);
    glVertex2f(109+a,390);
    glVertex2f(101+a,390);
    glVertex2f(109+a,390);
    glVertex2f(101+a,375);
    glVertex2f(109+a,375);
    glEnd();
    glBegin(GL_LINES);    // Partition
    glColor3f(0,0,0);
    glVertex2f(103+a,375);
    glVertex2f(103+a,390);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);    // Black header
    glColor3f(0,0,0);
    glVertex2f(103+a,395);
    glVertex2f(107+a,395);
    glEnd();
    glPointSize(1.5);   // Front lights
    glBegin(GL_POINTS);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(101+a,360);
    glVertex2f(101+a,355);
    glVertex2f(109+a,360);
    glVertex2f(109+a,355);
    glEnd();

    // Doors
    glBegin(GL_QUADS);   // ....1.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(98+a,345);
    glVertex2f(98+a,375);
    glVertex2f(93+a,375);
    glVertex2f(93+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(98+a,375);
    glVertex2f(98+a,345);
    glVertex2f(93+a,375);
    glVertex2f(93+a,345);
    glVertex2f(98+a,345);
    glVertex2f(93+a,345);
    glVertex2f(98+a,375);
    glVertex2f(93+a,375);
    glEnd();
    glLineWidth(4);    // Window
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(95.5+a,360);
    glVertex2f(95.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....2.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(79+a,345);
    glVertex2f(79+a,375);
    glVertex2f(69+a,375);
    glVertex2f(69+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(79+a,375);
    glVertex2f(79+a,345);
    glVertex2f(69+a,375);
    glVertex2f(69+a,345);
    glVertex2f(79+a,345);
    glVertex2f(69+a,345);
    glVertex2f(79+a,375);
    glVertex2f(69+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(74+a,345);
    glVertex2f(74+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(71.5+a,360);
    glVertex2f(71.5+a,370);
    glVertex2f(76.5+a,360);
    glVertex2f(76.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....3.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(45+a,345);
    glVertex2f(45+a,375);
    glVertex2f(55+a,375);
    glVertex2f(55+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(55+a,375);
    glVertex2f(55+a,345);
    glVertex2f(45+a,375);
    glVertex2f(45+a,345);
    glVertex2f(55+a,345);
    glVertex2f(45+a,345);
    glVertex2f(55+a,375);
    glVertex2f(45+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(50+a,345);
    glVertex2f(50+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(47.5+a,360);
    glVertex2f(47.5+a,370);
    glVertex2f(52.5+a,360);
    glVertex2f(52.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....4.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(31+a,345);
    glVertex2f(31+a,375);
    glVertex2f(21+a,375);
    glVertex2f(21+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(31+a,375);
    glVertex2f(31+a,345);
    glVertex2f(21+a,375);
    glVertex2f(21+a,345);
    glVertex2f(31+a,345);
    glVertex2f(21+a,345);
    glVertex2f(31+a,375);
    glVertex2f(21+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(26+a,345);
    glVertex2f(26+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(23.5+a,360);
    glVertex2f(23.5+a,370);
    glVertex2f(28.5+a,360);
    glVertex2f(28.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....5.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(13+a,345);
    glVertex2f(13+a,375);
    glVertex2f(3+a,375);
    glVertex2f(3+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(13+a,375);
    glVertex2f(13+a,345);
    glVertex2f(3+a,375);
    glVertex2f(3+a,345);
    glVertex2f(13+a,345);
    glVertex2f(3+a,345);
    glVertex2f(13+a,375);
    glVertex2f(3+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(8+a,345);
    glVertex2f(8+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(5.5+a,360);
    glVertex2f(5.5+a,370);
    glVertex2f(10.5+a,360);
    glVertex2f(10.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....6.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-11+a,345);
    glVertex2f(-11+a,375);
    glVertex2f(-21+a,375);
    glVertex2f(-21+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-11+a,375);
    glVertex2f(-11+a,345);
    glVertex2f(-21+a,375);
    glVertex2f(-21+a,345);
    glVertex2f(-11+a,345);
    glVertex2f(-21+a,345);
    glVertex2f(-11+a,375);
    glVertex2f(-21+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-16+a,345);
    glVertex2f(-16+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-13.5+a,360);
    glVertex2f(-13.5+a,370);
    glVertex2f(-18.5+a,360);
    glVertex2f(-18.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....7.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-35+a,345);
    glVertex2f(-35+a,375);
    glVertex2f(-45+a,375);
    glVertex2f(-45+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-35+a,375);
    glVertex2f(-35+a,345);
    glVertex2f(-45+a,375);
    glVertex2f(-45+a,345);
    glVertex2f(-35+a,345);
    glVertex2f(-45+a,345);
    glVertex2f(-35+a,375);
    glVertex2f(-45+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-40+a,345);
    glVertex2f(-40+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-37.5+a,360);
    glVertex2f(-37.5+a,370);
    glVertex2f(-42.5+a,360);
    glVertex2f(-42.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....8.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-59+a,345);
    glVertex2f(-59+a,375);
    glVertex2f(-69+a,375);
    glVertex2f(-69+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-59+a,375);
    glVertex2f(-59+a,345);
    glVertex2f(-69+a,375);
    glVertex2f(-69+a,345);
    glVertex2f(-59+a,345);
    glVertex2f(-69+a,345);
    glVertex2f(-59+a,375);
    glVertex2f(-69+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-64+a,345);
    glVertex2f(-64+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-61.5+a,360);
    glVertex2f(-61.5+a,370);
    glVertex2f(-66.5+a,360);
    glVertex2f(-66.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....9.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-77+a,345);
    glVertex2f(-77+a,375);
    glVertex2f(-87+a,375);
    glVertex2f(-87+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-77+a,375);
    glVertex2f(-77+a,345);
    glVertex2f(-87+a,375);
    glVertex2f(-87+a,345);
    glVertex2f(-77+a,345);
    glVertex2f(-87+a,345);
    glVertex2f(-77+a,375);
    glVertex2f(-87+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-82+a,345);
    glVertex2f(-82+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-79.5+a,360);
    glVertex2f(-79.5+a,370);
    glVertex2f(-84.5+a,360);
    glVertex2f(-84.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....10.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-101+a,345);
    glVertex2f(-101+a,375);
    glVertex2f(-111+a,375);
    glVertex2f(-111+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-101+a,375);
    glVertex2f(-101+a,345);
    glVertex2f(-111+a,375);
    glVertex2f(-111+a,345);
    glVertex2f(-101+a,345);
    glVertex2f(-111+a,345);
    glVertex2f(-101+a,375);
    glVertex2f(-111+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-106+a,345);
    glVertex2f(-106+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-103.5+a,360);
    glVertex2f(-103.5+a,370);
    glVertex2f(-108.5+a,360);
    glVertex2f(-108.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....11.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-125+a,345);
    glVertex2f(-125+a,375);
    glVertex2f(-135+a,375);
    glVertex2f(-135+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-125+a,375);
    glVertex2f(-125+a,345);
    glVertex2f(-135+a,375);
    glVertex2f(-135+a,345);
    glVertex2f(-125+a,345);
    glVertex2f(-135+a,345);
    glVertex2f(-125+a,375);
    glVertex2f(-135+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-130+a,345);
    glVertex2f(-130+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-127.5+a,360);
    glVertex2f(-127.5+a,370);
    glVertex2f(-132.5+a,360);
    glVertex2f(-132.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....12.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-149+a,345);
    glVertex2f(-149+a,375);
    glVertex2f(-159+a,375);
    glVertex2f(-159+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-149+a,375);
    glVertex2f(-149+a,345);
    glVertex2f(-159+a,375);
    glVertex2f(-159+a,345);
    glVertex2f(-149+a,345);
    glVertex2f(-159+a,345);
    glVertex2f(-149+a,375);
    glVertex2f(-159+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-154+a,345);
    glVertex2f(-154+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-151.5+a,360);
    glVertex2f(-151.5+a,370);
    glVertex2f(-156.5+a,360);
    glVertex2f(-156.5+a,370);
    glEnd();

    // Windows
    glBegin(GL_QUADS);   // ....1.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(82+a,360);
    glVertex2f(82+a,373);
    glVertex2f(90+a,373);
    glVertex2f(90+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....2.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(66+a,360);
    glVertex2f(66+a,373);
    glVertex2f(58+a,373);
    glVertex2f(58+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....3.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(42+a,360);
    glVertex2f(42+a,373);
    glVertex2f(34+a,373);
    glVertex2f(34+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....4.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(0+a,360);
    glVertex2f(0+a,373);
    glVertex2f(-8+a,373);
    glVertex2f(-8+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....5.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-24+a,360);
    glVertex2f(-24+a,373);
    glVertex2f(-32+a,373);
    glVertex2f(-32+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....6.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-48+a,360);
    glVertex2f(-48+a,373);
    glVertex2f(-56+a,373);
    glVertex2f(-56+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....7.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-90+a,360);
    glVertex2f(-90+a,373);
    glVertex2f(-98+a,373);
    glVertex2f(-98+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....8.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-114+a,360);
    glVertex2f(-114+a,373);
    glVertex2f(-122+a,373);
    glVertex2f(-122+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....9.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-138+a,360);
    glVertex2f(-138+a,373);
    glVertex2f(-146+a,373);
    glVertex2f(-146+a,360);
    glEnd();
    /// End Train ///

    glLineWidth(4);
    glBegin(GL_LINES);   ///
    glColor3f(0.2,0.2,0.2);
    glVertex2f(180,340);
    glVertex2f(180,440);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(370,340);
    glVertex2f(370,440);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(560,340);
    glVertex2f(560,440);
    glEnd();      ///

    }
    else if (scenario == '3') {
        // Scenario 3
        if (isDay) {
        // Day background
        glBegin(GL_QUADS);
        glColor3ub(255, 255, 147);   // Light Yellow
        glVertex2f(0,100);
        glVertex2f(800,100);
        glColor3ub(102, 204, 255);   // Light Blue
        glVertex2f(800,800);
        glVertex2f(0,800);
        glEnd();

        glColor3ub(253, 183, 77);    ///.........S U N.....................///
        circle(30,48,400,155);
        glColor3ub(253, 183, 77);
        circle(28.5,45,400,155);
        glColor3ub(253, 183, 77);
        circle(26.5,42,400,155);
        glColor3ub(253, 183, 77);
        circle(24.5,39,400,155);

    }
    else {
        // Night background
        glBegin(GL_QUADS);
        glColor3ub(220, 130, 20);   // Orange
        glVertex2f(0,50);
        glVertex2f(800,50);
        glColor3ub(102, 204, 225);   // Light Blue
        glVertex2f(800,800);
        glVertex2f(0,800);
        glEnd();

        glColor3ub(200, 100, 0);    ///.........S U N.....................///
        circle(30,48,400,145);
        glColor3ub(200, 100, 0);
        circle(28.5,45,400,145);
        glColor3ub(200, 100, 0);
        circle(26.5,42,400,145);
        glColor3ub(200, 100, 0);
        circle(24.5,39,400,145);

    }


    glBegin(GL_QUADS);        /// Lack area
    glColor3f(0.529, 0.808, 0.922);
    glVertex2f(0,140);
    glVertex2f(800,140);
    glVertex2f(800,90);
    glVertex2f(0,90);
    glEnd();

      /// Lack backside
    glBegin(GL_QUADS);
    glColor3ub(90,147,48);
    glVertex2f(0,140);
    glVertex2f(800,140);
    glVertex2f(800,150);
    glVertex2f(0,150);
    glEnd();

    // Update position for animation
    if (d >= 850) {
           d = 100; // Reset to the starting position
      } else {
           d = d + 0.1; // Move Right
      }

    /// Boat
    glBegin(GL_QUADS);
    glColor3ub(65,35,5);
    glVertex2f(150+d,125);
    glVertex2f(160+d,110);
    glVertex2f(200+d,110);
    glVertex2f(210+d,125);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(180, 150, 10);
    glVertex2f(150+d,125);
    glVertex2f(160+d,120);
    glVertex2f(200+d,120);
    glVertex2f(210+d,125);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);
    glColor3ub(65,35,5);
    glVertex2f(170+d,135);
    glVertex2f(152+d,105);
    glEnd();
    glColor3ub(0, 0, 0);  // Man 1
    circle(1.5,2.5,163+d,130);
    glColor3ub(20, 20, 20);
    circle(2,5,163+d,123.5);
    glColor3ub(0, 0, 0);  // Man 2
    circle(1.5,2.5,193+d,130);
    glColor3ub(20, 20, 20);
    circle(2,5,193+d,123.5);
    glColor3ub(0, 0, 0);  // Man 3
    circle(1.5,2.5,197+d,130);
    glColor3ub(20, 20, 20);
    circle(2,5,197+d,123.5);
    /// End

    ///  Road
    glBegin(GL_QUADS);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(0,81);
    glVertex2f(800,81);
    glVertex2f(800,39);
    glVertex2f(0,39);
    glEnd();

    glLineWidth(1);
    glBegin(GL_LINES);//Road top bar
	glColor3f(1.0,1.0,1.0);
    glVertex2i(0,81);
    glVertex2i(800,81);
    glEnd();

    glLineWidth(2);
    glBegin(GL_LINES);//Road middle bar
	glColor3f(1.0,1.0,1.0);
    glVertex2i(0,62);
    glVertex2i(800,62);
    glEnd();

    glLineWidth(1);
    glBegin(GL_LINES);//Road Bottom bar
	glColor3f(1.0,1.0,1.0);
    glVertex2i(0,39);
    glVertex2i(800,39);
    glEnd();

    ///
    glBegin(GL_QUADS);
    glColor3ub(90, 147, 48);
    glVertex2f(0,82);
    glVertex2f(800,82);
    glVertex2f(800,90);
    glVertex2f(0,90);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(90, 147, 48);
    glVertex2f(0,38);
    glVertex2f(800,38);
    glVertex2f(800,0);
    glVertex2f(0,0);
    glEnd();


    glBegin(GL_TRIANGLE_FAN);  ///Bottom tree1   ///
    glColor3ub(75,35,5);
    glVertex3f(680,0,0);
    glVertex3f(685,0,0);
    glVertex3f(685,20,0);
    glVertex3f(680,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(675,10,0);
    glVertex3f(690,10,0);
    glVertex3f(682.5,40,0);
    glVertex3f(682.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(676,15,0);
    glVertex3f(689,15,0);
    glVertex3f(682.5,45,0);
    glVertex3f(682.5,45,0);
    glEnd();


    glBegin(GL_TRIANGLE_FAN);  ///Bottom tree2   ///
    glColor3ub(75,35,5);
    glVertex3f(580,0,0);
    glVertex3f(585,0,0);
    glVertex3f(585,20,0);
    glVertex3f(580,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(575,10,0);
    glVertex3f(590,10,0);
    glVertex3f(582.5,40,0);
    glVertex3f(582.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(576,15,0);
    glVertex3f(589,15,0);
    glVertex3f(582.5,45,0);
    glVertex3f(582.5,45,0);
    glEnd();

     glBegin(GL_TRIANGLE_FAN);  ///Bottom tree3   ///
    glColor3ub(75,35,5);
    glVertex3f(480,0,0);
    glVertex3f(485,0,0);
    glVertex3f(485,20,0);
    glVertex3f(480,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(475,10,0);
    glVertex3f(490,10,0);
    glVertex3f(482.5,40,0);
    glVertex3f(482.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(476,15,0);
    glVertex3f(489,15,0);
    glVertex3f(482.5,45,0);
    glVertex3f(482.5,45,0);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///Bottom tree4   ///
    glColor3ub(75,35,5);
    glVertex3f(380,0,0);
    glVertex3f(385,0,0);
    glVertex3f(385,20,0);
    glVertex3f(380,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(375,10,0);
    glVertex3f(390,10,0);
    glVertex3f(382.5,40,0);
    glVertex3f(382.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(376,15,0);
    glVertex3f(389,15,0);
    glVertex3f(382.5,45,0);
    glVertex3f(382.5,45,0);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///Bottom tree5   ///
    glColor3ub(75,35,5);
    glVertex3f(280,0,0);
    glVertex3f(285,0,0);
    glVertex3f(285,20,0);
    glVertex3f(280,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(275,10,0);
    glVertex3f(290,10,0);
    glVertex3f(282.5,40,0);
    glVertex3f(282.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(276,15,0);
    glVertex3f(289,15,0);
    glVertex3f(282.5,45,0);
    glVertex3f(282.5,45,0);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///Bottom tree6   ///
    glColor3ub(75,35,5);
    glVertex3f(180,0,0);
    glVertex3f(185,0,0);
    glVertex3f(185,20,0);
    glVertex3f(180,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(175,10,0);
    glVertex3f(190,10,0);
    glVertex3f(182.5,40,0);
    glVertex3f(182.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(176,15,0);
    glVertex3f(189,15,0);
    glVertex3f(182.5,45,0);
    glVertex3f(182.5,45,0);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///Bottom tree7   ///
    glColor3ub(75,35,5);
    glVertex3f(80,0,0);
    glVertex3f(85,0,0);
    glVertex3f(85,20,0);
    glVertex3f(80,20,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(75,10,0);
    glVertex3f(90,10,0);
    glVertex3f(82.5,40,0);
    glVertex3f(82.5,40,0);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex3f(76,15,0);
    glVertex3f(89,15,0);
    glVertex3f(82.5,45,0);
    glVertex3f(82.5,45,0);
    glEnd();
    ///End///


    ///....Right side circle tree 1 ///
    glColor3ub(0, 153, 51);
    circle(3,6,98,101);
    glColor3ub(0, 153, 51);
    circle(5,12,93,111);
    glColor3ub(0, 153, 51);
    circle(5,12,103,111);
    glColor3ub(0, 153, 51);
    circle(5,12,108,106);
    glColor3ub(0, 153, 51);
    circle(5,12,88,121);


    glColor3ub(0, 102, 0);
    circle(5,12,93,123);
    glColor3ub(0, 153, 51);
    circle(5,12,94,123);
    glColor3ub(0, 153, 51);
    circle(5,12,98,141);
    glColor3ub(0, 153, 51);
    circle(4,10,93,136);
    glColor3ub(0, 102, 0);
    circle(4,10,95,134);

    glColor3ub(0, 153, 51);
    circle(4,10,96,133);

    glColor3ub(0, 153, 51);
    circle(5,12,108,131);
    glColor3ub(0, 153, 51);
    circle(5,12,103,131);
    glColor3ub(0, 102, 0);
    circle(5,12,102,126);
    glColor3ub(0, 153, 51);
    circle(5,12,101,125);
    glColor3ub(0, 153, 51);
    circle(5,12,113,121);
    glColor3ub(0, 102, 0);
    circle(5,12,108,116);
    glColor3ub(0, 153, 51);
    circle(5,12,107,116);
    glColor3ub(0, 153, 51);
    circle(5,12,98,119);
    glColor3ub(0, 153, 51);
    circle(5,12,110,141);



    glColor3ub(255, 255, 255);         ///Full........ .........comp.
    circle(1,2,98,119);
    glColor3ub(255, 255, 255);
    circle(1,2,98,133);
    glColor3ub(255, 255, 255);
    circle(1,2,108,133);
    glColor3ub(255, 255, 255);
    circle(1,2,113,128);
    glColor3ub(255, 255, 255);
    circle(1,2,87,119);
    glColor3ub(255, 255, 255);
    circle(1,2.5,93,134);
    glColor3ub(255, 255, 255);
    circle(1,1.5,94,110);
    glColor3ub(255, 255, 255);
    circle(1,2.5,108,106);
    glColor3ub(255, 255, 255);
    circle(1,3,113,119);
    glColor3ub(255, 255, 255);
    circle(1,3,103,103);



    glBegin(GL_TRIANGLE_FAN);  ///tree 1.........   ///
    glColor3ub(75, 35, 5);
    glVertex2f(103,90);
    glVertex2f(106,90);
    glVertex2f(105,100);
    glVertex2f(100,130);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);  ///tree 1.........   ///
    glColor3ub(75, 35, 5);
    glVertex2f(103,90);
    glVertex2f(106,90);
    glVertex2f(102,100);
    glVertex2f(96,110);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///tree 1.........  ///
    glColor3ub(75, 35, 5);
    glVertex2f(102,90);
    glVertex2f(106,90);
    glVertex2f(107,110);
    glVertex2f(110,140);
    glEnd();
///End Right side circle tree 1///


      ///....Right side circle tree 2  ///
    glColor3ub(0, 153, 51);
    circle(3,6,468,101);
    glColor3ub(0, 153, 51);
    circle(5,12,463,111);
    glColor3ub(0, 153, 51);
    circle(5,12,473,111);
    glColor3ub(0, 153, 51);
    circle(5,12,478,106);
    glColor3ub(0, 153, 51);
    circle(5,12,458,121);


    glColor3ub(0, 102, 0);
    circle(5,12,463,123);
    glColor3ub(0, 153, 51);
    circle(5,12,464,123);
    glColor3ub(0, 153, 51);
    circle(5,12,468,141);
    glColor3ub(0, 153, 51);
    circle(4,10,463,136);
    glColor3ub(0, 102, 0);
    circle(4,10,465,134);

    glColor3ub(0, 153, 51);
    circle(4,10,466,133);

    glColor3ub(0, 153, 51);
    circle(5,12,478,131);
    glColor3ub(0, 153, 51);
    circle(5,12,473,131);
    glColor3ub(0, 102, 0);
    circle(5,12,472,126);
    glColor3ub(0, 153, 51);
    circle(5,12,471,125);
    glColor3ub(0, 153, 51);
    circle(5,12,483,121);
    glColor3ub(0, 102, 0);
    circle(5,12,478,116);
    glColor3ub(0, 153, 51);
    circle(5,12,477,116);
    glColor3ub(0, 153, 51);
    circle(5,12,468,119);
    glColor3ub(0, 153, 51);
    circle(5,12,480,141);



    glColor3ub(255, 255, 255);         ///Full........ .........comp.
    circle(1,2,468,119);
    glColor3ub(255, 255, 255);
    circle(1,2,468,133);
    glColor3ub(255, 255, 255);
    circle(1,2,478,133);
    glColor3ub(255, 255, 255);
    circle(1,2,483,128);
    glColor3ub(255, 255, 255);
    circle(1,2,457,119);
    glColor3ub(255, 255, 255);
    circle(1,2.5,463,134);
    glColor3ub(255, 255, 255);
    circle(1,1.5,464,110);
    glColor3ub(255, 255, 255);
    circle(1,2.5,478,106);
    glColor3ub(255, 255, 255);
    circle(1,3,483,119);
    glColor3ub(255, 255, 255);
    circle(1,3,473,103);



    glBegin(GL_TRIANGLE_FAN);  ///tree 2.........  ///
    glColor3ub(75, 35, 5);
    glVertex2f(473,90);
    glVertex2f(476,90);
    glVertex2f(475,100);
    glVertex2f(470,130);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);  ///tree 2.........  ///
    glColor3ub(75, 35, 5);
    glVertex2f(473,90);
    glVertex2f(476,90);
    glVertex2f(472,100);
    glVertex2f(466,110);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///tree 2.........  ///
    glColor3ub(75, 35, 5);
    glVertex2f(472,90);
    glVertex2f(476,90);
    glVertex2f(477,110);
    glVertex2f(480,140);
    glEnd();
///End Right side circle tree 2///

///....Left side circle tree ///
    glColor3ub(0, 153, 51);
    circle(3,6,280,101);
    glColor3ub(0, 153, 51);
    circle(5,12,275,111);
    glColor3ub(0, 153, 51);
    circle(5,12,285,111);
    glColor3ub(0, 153, 51);
    circle(5,12,290,106);
    glColor3ub(0, 153, 51);
    circle(5,12,270,121);


    glColor3ub(0, 102, 0);
    circle(5,12,275,123);
    glColor3ub(0, 153, 51);
    circle(5,12,276,123);
    glColor3ub(0, 153, 51);
    circle(5,12,280,141);
    glColor3ub(0, 153, 51);
    circle(4,10,275,136);
    glColor3ub(0, 102, 0);
    circle(4,10,277,134);

    glColor3ub(0, 153, 51);
    circle(4,10,278,133);

    glColor3ub(0, 153, 51);
    circle(5,12,290,131);
    glColor3ub(0, 153, 51);
    circle(5,12,285,131);
    glColor3ub(0, 102, 0);
    circle(5,12,284,126);
    glColor3ub(0, 153, 51);
    circle(5,12,283,125);
    glColor3ub(0, 153, 51);
    circle(5,12,295,121);
    glColor3ub(0, 102, 0);
    circle(5,12,290,116);
    glColor3ub(0, 153, 51);
    circle(5,12,289,116);
    glColor3ub(0, 153, 51);
    circle(5,12,280,119);
    glColor3ub(0, 153, 51);
    circle(5,12,292,141);



    glColor3ub(255, 255, 255);         ///Full......... .........comp.
    circle(1,2,280,119);
    glColor3ub(255, 255, 255);
    circle(1,2,280,133);
    glColor3ub(255, 255, 255);
    circle(1,2,290,133);
    glColor3ub(255, 255, 255);
    circle(1,2,295,128);
    glColor3ub(255, 255, 255);
    circle(1,2,269,119);
    glColor3ub(255, 255, 255);
    circle(1,2.5,275,134);
    glColor3ub(255, 255, 255);
    circle(1,1.5,276,110);
    glColor3ub(255, 255, 255);
    circle(1,2.5,290,106);
    glColor3ub(255, 255, 255);
    circle(1,3,295,119);
    glColor3ub(255, 255, 255);
    circle(1,3,285,103);


    glBegin(GL_TRIANGLE_FAN);  ///tree.........   ///
    glColor3ub(75, 35, 5);
    glVertex2f(285,90);
    glVertex2f(288,90);
    glVertex2f(287,100);
    glVertex2f(282,130);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);  ///tree.........   ///
    glColor3ub(75, 35, 5);
    glVertex2f(285,90);
    glVertex2f(288,90);
    glVertex2f(284,100);
    glVertex2f(278,110);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///tree.........   ///
    glColor3ub(75, 35, 5);
    glVertex2f(284,90);
    glVertex2f(288,90);
    glVertex2f(289,110);
    glVertex2f(292,140);
    glEnd();
///End Left side circle tree///



    glBegin(GL_TRIANGLE_FAN);  ///tree.........beside 3rd Building........3   ///
    glColor3ub(139,99,47);
    glVertex2f(680,90);
    glVertex2f(685,90);
    glVertex2f(685,100);
    glVertex2f(680,100);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex2f(675,100);
    glVertex2f(690,100);
    glVertex2f(682.5,130);
    glVertex2f(682.5,130);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex2f(676,110);
    glVertex2f(689,110);
    glVertex2f(682.5,140);
    glVertex2f(682.5,140);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex2f(677,122);
    glVertex2f(688,122);
    glVertex2f(682.5,155);
    glVertex2f(682.5,155);
    glEnd();


    glBegin(GL_TRIANGLE_FAN);  ///tree.........beside 3rd Building........4   ///
    glColor3ub(139,99,47);
    glVertex2f(690,90);
    glVertex2f(695,90);
    glVertex2f(695,105);
    glVertex2f(690,105);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0,99,47);
    glVertex2f(685,105);
    glVertex2f(700,105);
    glVertex2f(692.5,135);
    glVertex2f(692.5,135);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex2f(686,115);
    glVertex2f(699,115);
    glVertex2f(692.5,145);
    glVertex2f(692.5,145);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(0, 102, 0);
    glVertex2f(687,127);
    glVertex2f(698,127);
    glVertex2f(692.5,165);
    glVertex2f(692.5,165);
    glEnd();


    glColor3ub(0, 153, 51);      ///....tree.........beside 3rd Building........6 ///
    circle(3,6,625,100);
    glColor3ub(0, 153, 51);
    circle(5,12,620,110);
    glColor3ub(0, 153, 51);
    circle(5,12,630,110);
    glColor3ub(0, 153, 51);
    circle(5,12,635,105);
    glColor3ub(0, 153, 51);
    circle(5,12,615,120);


    glColor3ub(0, 102, 0);
    circle(5,12,620,122);
    glColor3ub(0, 153, 51);
    circle(5,12,621,122);
    glColor3ub(0, 153, 51);
    circle(5,12,625,140);
    glColor3ub(0, 153, 51);
    circle(4,10,620,135);
    glColor3ub(0, 102, 0);
    circle(4,10,622,133);

    glColor3ub(0, 153, 51);
    circle(4,10,623,132);

    glColor3ub(0, 153, 51);
    circle(5,12,635,130);
    glColor3ub(0, 153, 51);
    circle(5,12,630,130);
    glColor3ub(0, 102, 0);
    circle(5,12,629,125);
    glColor3ub(0, 153, 51);
    circle(5,12,628,124);
    glColor3ub(0, 153, 51);
    circle(5,12,640,120);
    glColor3ub(0, 102, 0);
    circle(5,12,635,115);
    glColor3ub(0, 153, 51);
    circle(5,12,634,115);
    glColor3ub(0, 153, 51);
    circle(5,12,625,118);
    glColor3ub(0, 153, 51);
    circle(5,12,637,140);



    glColor3ub(255, 255, 255);         ///Full..........3rd Building.........comp.
    circle(1,2,625,118);
    glColor3ub(255, 255, 255);
    circle(1,2,625,138);
    glColor3ub(255, 255, 255);
    circle(1,2,635,138);
    glColor3ub(255, 255, 255);
    circle(1,2,630,127);
    glColor3ub(255, 255, 255);
    circle(1,2,614,118);
    glColor3ub(255, 255, 255);
    circle(1,2.5,620,133);
    glColor3ub(255, 255, 255);
    circle(1,1.5,621,109);
    glColor3ub(255, 255, 255);
    circle(1,2.5,635,105);
    glColor3ub(255, 255, 255);
    circle(1,3,640,118);
    glColor3ub(255, 255, 255);
    circle(1,3,635,120);


    glBegin(GL_TRIANGLE_FAN);  ///tree.........beside 3rd Building........6   ///
    glColor3ub(75,35,5);
    glVertex2f(630,90);
    glVertex2f(633,90);
    glVertex2f(632,100);
    glVertex2f(627,130);
    glEnd();
    glBegin(GL_TRIANGLE_FAN);  ///tree.........beside 3rd Building........6   ///
    glColor3ub(75,35,5);
    glVertex2f(630,90);
    glVertex2f(633,90);
    glVertex2f(629,100);
    glVertex2f(623,110);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);  ///tree.........beside 3rd Building........6   ///
    glColor3ub(75,35,5);
    glVertex2f(629,90);
    glVertex2f(633,90);
    glVertex2f(634,110);
    glVertex2f(637,140);
    glEnd();


    glColor3ub(232,241,255);        ///....Cloud.......1 covering sun....///
    circle(13,20,400,665);
    glColor3ub(252,254,255);
    circle(11,18,400,665);

    glColor3ub(232,241,255);
    circle(10,20,410,675);
    glColor3ub(252,254,255);
    circle(10,20,412,672);

    glColor3ub(232,241,255);
    circle(13,20,410,655);

    glColor3ub(221,229,247);
    circle(9,20,420,680);
    glColor3ub(252,254,255);
    circle(8,18,420,679);

    glColor3ub(232,241,255);
    circle(9,20,420,650);
    glColor3ub(252,254,255);
    circle(8,18,420,652);

    glColor3ub(221,229,247);
    circle(9,20,430,685);
    glColor3ub(252,254,255);
    circle(8,18,430,683);

    glColor3ub(232,241,255);
    circle(9,20,425,655);
    glColor3ub(252,254,255);
    circle(8,18,435,657);

    glColor3ub(232,241,255);
    circle(9,20,440,675);

    glColor3ub(221,229,247);
    circle(8,18,445,665);
    glColor3ub(252,254,255);
    circle(8,18,443,663);
    glColor3ub(252,254,255);
    circle(18,18,420,664);
    glColor3ub(252,254,255);
    circle(18,25,417,665);


    glColor3ub(232,241,255);        ///....Cloud.......2.....///
    circle(13,20,p+200,745);
    glColor3ub(252,254,255);
    circle(11,18,p+200,745);

    glColor3ub(232,241,255);
    circle(10,20,p+210,755);
    glColor3ub(252,254,255);
    circle(10,20,p+212,762);

    glColor3ub(232,241,255);
    circle(13,20,p+210,735);

    glColor3ub(221,229,247);
    circle(9,20,p+220,750);
    glColor3ub(252,254,255);
    circle(8,18,p+220,759);

    glColor3ub(232,241,255);
    circle(9,20,p+220,756);
    glColor3ub(252,254,255);
    circle(8,18,p+220,752);

    glColor3ub(232,241,255);
    circle(9,20,p+230,765);
    glColor3ub(252,254,255);
    circle(8,18,p+230,761);

    glColor3ub(232,241,255);
    circle(9,20,p+225,745);
    glColor3ub(252,254,255);
    circle(8,18,p+235,747);

    glColor3ub(232,241,255);
    circle(9,20,p+240,755);

    glColor3ub(221,229,247);
    circle(8,18,p+243,745);
    glColor3ub(252,254,255);
    circle(8,18,p+240,743);
    glColor3ub(173,197,224);
    circle(8,18,p+230,733);
    glColor3ub(252,254,255);
    circle(8,18,p+230,738);
    glColor3ub(173,197,224);
    circle(8,18,p+220,723);
    glColor3ub(252,254,255);
    circle(8,18,p+220,728);



    glColor3ub(252,254,255);
    circle(23,16,p+242,744);
    glColor3ub(173,197,224);
    circle(21,20,p+240,720);
    glColor3ub(252,254,255);
    circle(21,21,p+238,723);


    glColor3ub(252,254,255);
    circle(18,18,p+210,744);
    glColor3ub(252,254,255);
    circle(18,25,p+220,745);

    glColor3ub(173,197,224);
    circle(10,20,p+235,715);
    glColor3ub(252,254,255);
    circle(10,20,p+235,719);



    glColor3ub(173,197,224);        ///....Cloud.......3.....///
    circle(9,15,p+20,685);
    glColor3ub(252,254,255);
    circle(6,14,p+21,685);

    glColor3ub(232,241,255);
    circle(7,16,p+30,695);
    glColor3ub(252,254,255);
    circle(7,14,p+32,692);

    glColor3ub(252,254,255);
    circle(12,16,p+28,680);

    glColor3ub(221,229,247);
    circle(10,15,p+45,690);
    glColor3ub(252,254,255);
    circle(9,13,p+43,685);
    glColor3ub(252,254,255);
    circle(15,18,p+48,670);

    glColor3ub(173,197,224);
    circle(6,14,p+30,680);
    glColor3ub(252,254,255);
    circle(6,13,p+30,677);

    glColor3ub(173,197,224);
    circle(6,14,p+38,668);
    glColor3ub(252,254,255);
    circle(6,13,p+36,667);


    glColor3ub(252,254,255);
    circle(11,15,p+29,668);

     ///....Cloud.......4.....///

    glColor3ub(173,197,224);
    circle(9,15,590,695);
    glColor3ub(252,254,255);
    circle(6,14,591,695);

    glColor3ub(232,241,255);
    circle(7,16,600,705);
    glColor3ub(252,254,255);
    circle(7,14,602,702);

    glColor3ub(252,254,255);
    circle(12,16,598,690);

    glColor3ub(221,229,247);
    circle(10,15,615,700);
    glColor3ub(252,254,255);
    circle(9,13,613,695);
    glColor3ub(252,254,255);
    circle(15,18,618,680);

    glColor3ub(173,197,224);
    circle(6,14,600,690);
    glColor3ub(252,254,255);
    circle(6,13,600,687);

    glColor3ub(173,197,224);
    circle(6,14,608,678);
    glColor3ub(252,254,255);
    circle(6,13,606,677);


    glColor3ub(252,254,255);
    circle(11,15,599,678);


    if(p<= 800)
        p = p + 0.1;
    else
        p = -10;


    // Update position for animation
    if (c <= -100) {
           c = 800; // Reset to the starting position
      } else {
           c = c - 0.3; // Move left
      }

    /// ...........C A R  1..............
    // Main body of the bus
    glBegin(GL_QUADS);
    glColor3ub(255, 255, 255); // White
    glVertex2f(15 + c, 95);
    glVertex2f(45 + c, 95);
    glVertex2f(40 + c, 115);
    glVertex2f(20 + c, 115);
    glEnd();

    // Lower part
    glBegin(GL_QUADS);
    glColor3ub(255, 255, 255); // White
    glVertex2f(10 + c, 75);
    glVertex2f(50 + c, 75);
    glVertex2f(50 + c, 95);
    glVertex2f(10 + c, 95);
    glEnd();

    // Top part
    glBegin(GL_QUADS);
    glColor3ub(0, 0, 0); // Black
    glVertex2f(21 + c, 113);
    glVertex2f(39 + c, 113);
    glVertex2f(44 + c, 95);
    glVertex2f(16 + c, 95);
    glEnd();

    // Windows
    glBegin(GL_QUADS);
    glColor3ub(125, 125, 125); // Gray // Window 1
    glVertex2f(19 + c, 100);
    glVertex2f(28 + c, 100);
    glVertex2f(28 + c, 110);
    glVertex2f(22 + c, 110);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(125, 125, 125); // Gray // Window 2
    glVertex2f(32 + c, 100);
    glVertex2f(41 + c, 100);
    glVertex2f(38 + c, 110);
    glVertex2f(32 + c, 110);
    glEnd();

    // Doors
    glLineWidth(1);
    glBegin(GL_LINES);
    glColor3ub(0, 0, 0);
    glVertex2f(17 + c, 80);
    glVertex2f(17 + c, 100);
    glVertex2f(29.5 + c, 80);
    glVertex2f(29.5 + c, 100);
    glVertex2f(30.5 + c, 80);
    glVertex2f(30.5 + c, 100);
    glVertex2f(43 + c, 80);
    glVertex2f(43 + c, 100);
    glVertex2f(17 + c, 80);
    glVertex2f(29.5 + c, 80);
    glVertex2f(30.5 + c, 80);
    glVertex2f(43 + c, 80);
    glVertex2f(28 + c, 88);
    glVertex2f(28 + c, 92);
    glVertex2f(41.5 + c, 88);
    glVertex2f(41.5 + c, 92);
    glEnd();

    glLineWidth(1);    ///
    glBegin(GL_LINES);
    glColor3ub(255, 255, 255);
    glVertex2f(30 + c, 95);
    glVertex2f(30 + c, 113);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(255, 255, 255); // Front glass
    glVertex2f(16 + c, 95);
    glVertex2f(18 + c, 95);
    glVertex2f(18 + c, 105);
    glVertex2f(16 + c, 105);
    glEnd();

    // Front light
    glBegin(GL_QUADS);
    glColor3ub(126, 126, 126);   // Gray
    glVertex2f(10 + c, 90);
    glVertex2f(13 + c, 90);
    glVertex2f(13 + c, 85);
    glVertex2f(10 + c, 85);
    glEnd();

    // Back light
    glBegin(GL_QUADS);
    glColor3ub(255, 0, 0);   // Red
    glVertex2f(50 + c, 90);
    glVertex2f(47 + c, 90);
    glVertex2f(47 + c, 85);
    glVertex2f(50 + c, 85);
    glEnd();

    // Wheels
    glColor3ub(0, 0, 0); // Back wheel
    circle(4, 8, 18 + c, 75);
    glColor3ub(255, 255, 255);
    circle(2.5, 5, 18 + c, 75);

    glColor3ub(0, 0, 0); // Front wheel
    circle(4, 8, 42 + c, 75);
    glColor3ub(255, 255, 255);
    circle(2.5, 5, 42 + c, 75);

    if(k<= 850)
        k = k + 0.7;
    else
        k = -160;

        // .........PLANE......... //

    // Body
    glBegin(GL_POLYGON);
    glColor3ub(255, 255, 255);
    glVertex2f(k + 15, 640);
    glVertex2f(k + 2, 657);
    glVertex2f(k + 2, 660);
    glVertex2f(k + 70, 660);
    glVertex2f(k + 80, 645);
    glVertex2f(k + 75, 640);
    glEnd();
    glBegin(GL_POLYGON);
    glColor3ub(127, 153, 178);
    glVertex2f(k + 70, 640);
    glVertex2f(k + 65, 645);
    glVertex2f(k + 11, 645);
    glVertex2f(k + 15, 640);
    glEnd();

    // Tail
    glBegin(GL_POLYGON);
    glColor3ub(127, 153, 178);
    glVertex2f(k + 5, 660);
    glVertex2f(k + 5, 675);
    glVertex2f(k + 12, 675);
    glVertex2f(k + 14, 667);
    glVertex2f(k + 20, 660);
    glEnd();

    glBegin(GL_POLYGON);
    glColor3ub(127, 153, 178);
    glVertex2f(k + 2, 657);
    glVertex2f(k, 650);
    glVertex2f(k + 5, 650);
    glVertex2f(k + 10, 657);
    glEnd();

    // Wings
    glBegin(GL_POLYGON);
    glColor3ub(127, 153, 178);
    glVertex2f(k + 35, 665);
    glVertex2f(k + 40, 665);  // Adjusted to align with the body
    glVertex2f(k + 45, 660);  // Adjusted to align with the body
    glVertex2f(k + 37, 660);
    glEnd();

    glBegin(GL_POLYGON);
    glColor3ub(127, 153, 178);
    glVertex2f(k + 50, 647);  // Wing starting point
    glVertex2f(k + 40, 647);  // Wing end point
    glVertex2f(k + 32, 630);  // Wing bottom point
    glVertex2f(k + 38, 630);  // Wing bottom point
    glEnd();

    // Windows
    glPointSize(3);
    glBegin(GL_POINTS);
    glColor3ub(0, 0, 0);
    glVertex2f(k + 22, 652);
    glVertex2f(k + 25, 652);
    glVertex2f(k + 28, 652);
    glVertex2f(k + 31, 652);
    glVertex2f(k + 34, 652);
    glVertex2f(k + 37, 652);
    glVertex2f(k + 40, 652);
    glVertex2f(k + 43, 652);
    glVertex2f(k + 46, 652);
    glVertex2f(k + 49, 652);
    glVertex2f(k + 52, 652);
    glVertex2f(k + 55, 652);
    glVertex2f(k + 58, 652);
    glEnd();

    // Front glass
    glBegin(GL_POLYGON);
    glColor3ub(0, 0, 0);
    glVertex2f(k + 65, 655);
    glVertex2f(k + 65, 650);
    glVertex2f(k + 76, 650);
    glVertex2f(k + 73, 655);
    glEnd();

    glLineWidth(0.5);
    glBegin(GL_LINES);
    glColor3ub(255, 255, 255);
    glVertex2f(k + 72, 655);
    glVertex2f(k + 72, 650);
    glEnd();
    glBegin(GL_LINES);
    glColor3ub(255, 255, 255);
    glVertex2f(k + 68.5, 655);
    glVertex2f(k + 68.5, 650);
    glEnd();
    /// End ///

    if(b<= 800)
        b = b + 0.3;
    else
        b = -100;

        ///..........B U S...........1

    glBegin(GL_QUADS);
    glColor3ub(235, 0, 0); // Red
    glVertex2f(b+90,98);  //bus...................
    glVertex2f(b+95,98);
    glVertex2f(b+95,100);
    glVertex2f(b+90,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(26, 26, 0);
    glVertex2f(b+94,89);   // bus font glass
    glVertex2f(b+96,89);
    glVertex2f(b+96,100);
    glVertex2f(b+94,100);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(235, 0, 0); // Red
    glVertex2f(b+10,80);  //.....bus
    glVertex2f(b+90,80);
    glVertex2f(b+90,105);
    glVertex2f(b+10,105);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(235, 0, 0); // Red
    glVertex2f(b+10,55);  //top..........lowerpart
    glVertex2f(b+92,55);
    glVertex2f(b+92,80);
    glVertex2f(b+10,80);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(0, 51, 0);
    glVertex2f(b+11,81);  //top..........
    glVertex2f(b+89,81);
    glVertex2f(b+89,102);
    glVertex2f(b+11,102);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+12,85);  //window..........
    glVertex2f(b+20,85);
    glVertex2f(b+20,100);
    glVertex2f(b+12,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+22,85);  //window..........
    glVertex2f(b+30,85);
    glVertex2f(b+30,100);
    glVertex2f(b+22,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+32,85);  //window..........
    glVertex2f(b+40,85);
    glVertex2f(b+40,100);
    glVertex2f(b+32,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+42,85);  //window..........
    glVertex2f(b+50,85);
    glVertex2f(b+50,100);
    glVertex2f(b+42,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+52,85);  //window..........
    glVertex2f(b+60,85);
    glVertex2f(b+60,100);
    glVertex2f(b+52,100);
    glEnd();

    glBegin(GL_QUADS);
    glColor3ub(230, 247, 255);
    glVertex2f(b+62,55);  //..door..........
    glVertex2f(b+70,55);
    glVertex2f(b+70,95);
    glVertex2f(b+62,95);
    glEnd();


    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+72,85);  //window..........
    glVertex2f(b+80,85);
    glVertex2f(b+80,100);
    glVertex2f(b+72,100);
    glEnd();
    glBegin(GL_QUADS);
    glColor3ub(230, 255, 255);
    glVertex2f(b+82,85);  //window..........
    glVertex2f(b+88,85);
    glVertex2f(b+88,100);
    glVertex2f(b+82,100);
    glEnd();

    glColor3ub(255, 255, 204);          //....chaka....back
    circle(4,8,b+45,65);
    glColor3ub(255, 255, 204);
    circle(2,4,b+55,75);
    glColor3ub(255, 255, 204);
    circle(3,6,b+15,75);
    glColor3ub(255, 255, 204);
    circle(2,4,b+35,65);
    glColor3ub(255, 255, 204);
    circle(2,4,b+75,75);


    glColor3ub(0,0,0);          //....chaka....back
    circle(5,10,b+25,55);
    glColor3ub(255,255,255);
    circle(3,6,b+25,55);

    glColor3ub(0,0,0);
    circle(5,10,b+78,55);
    glColor3ub(255,255,255);
    circle(3,6,b+78,55);

    glColor3ub(0, 51, 0); // Green
    glRasterPos2i(b+40,65);

    glutBitmapCharacter(GLUT_BITMAP_9_BY_15,'B');
    glutBitmapCharacter(GLUT_BITMAP_9_BY_15,'U');
    glutBitmapCharacter(GLUT_BITMAP_9_BY_15,'S');

    /// Metro rail runway
    glBegin(GL_QUADS);
    glColor3f(0.4,0.4,0.4);
    glVertex2f(0,280);
    glVertex2f(800,280);
    glVertex2f(800,350);
    glVertex2f(0,350);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.5,0.5,0.5);
    glVertex2f(0,310);
    glVertex2f(800,310);
    glVertex2f(800,340);
    glVertex2f(0,340);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.3,0.3,0.3);
    glVertex2f(200,280);
    glVertex2f(200,310);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.3,0.3,0.3);
    glVertex2f(450,280);
    glVertex2f(450,310);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.3,0.3,0.3);
    glVertex2f(690,280);
    glVertex2f(690,310);
    glEnd();

    glLineWidth(4);    ///
    glBegin(GL_LINES);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(190,350);
    glVertex2f(190,450);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(191,450);
    glVertex2f(179,440);
    glEnd();
    glBegin(GL_LINES);    ///
    glColor3f(0.2,0.2,0.2);
    glVertex2f(380,350);
    glVertex2f(380,450);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(381,450);
    glVertex2f(369,440);
    glEnd();
    glBegin(GL_LINES);   ///
    glColor3f(0.2,0.2,0.2);
    glVertex2f(570,350);
    glVertex2f(570,450);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(571,450);
    glVertex2f(559,440);
    glEnd();



    glBegin(GL_QUADS);        /// ......Pillar 1...... ///
    glColor3f(0.5, 0.5, 0.5);
    glVertex2f(50,250);
    glVertex2f(100,250);
    glVertex2f(100,280);
    glVertex2f(50,280);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.4,0.4,0.4);
    glVertex2f(65,250);
    glVertex2f(85,250);
    glVertex2f(85,38);
    glVertex2f(65,38);
    glEnd();

    glBegin(GL_QUADS);        /// ......Pillar 2...... ///
    glColor3f(0.5,0.5,0.5);
    glVertex2f(300,250);
    glVertex2f(350,250);
    glVertex2f(350,280);
    glVertex2f(300,280);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.4,0.4,0.4);
    glVertex2f(315,250);
    glVertex2f(335,250);
    glVertex2f(335,38);
    glVertex2f(315,38);
    glEnd();

    glBegin(GL_QUADS);        /// ......Pillar 3...... ///
    glColor3f(0.5,0.5,0.5);
    glVertex2f(550,250);
    glVertex2f(600,250);
    glVertex2f(600,280);
    glVertex2f(550,280);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.4,0.4,0.4);
    glVertex2f(565,250);
    glVertex2f(585,250);
    glVertex2f(585,38);
    glVertex2f(565,38);
    glEnd();
    /// End ///

    // Update position based on metroStop and metroSpeed
    if (!metroStop) {
        if (a <= 900) {
            a += metroSpeed; // Move the metro forward
        } else {
            a = -250; // Reset position
        }
    }

    /// Metro Rail Train
    glBegin(GL_QUADS);     // 1st partition
    glColor3f(0.95,0.95,0.97);
    glVertex2f(19+a,400);
    glVertex2f(100+a,400);
    glVertex2f(100+a,340);
    glVertex2f(19+a,340);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.95,0.95,0.97);
    glVertex2f(100+a,400);
    glVertex2f(100+a,340);
    glVertex2f(110+a,340);
    glVertex2f(110+a,400);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.18,0.55,0.34);
    glVertex2f(19+a,384);
    glVertex2f(19+a,391);
    glVertex2f(100+a,391);
    glVertex2f(100+a,384);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.18,0.55,0.34);
    glVertex2f(100+a,400);
    glVertex2f(100+a,370);
    glVertex2f(110+a,370);
    glVertex2f(110+a,400);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.8,0,0);
    glVertex2f(100+a,350);
    glVertex2f(100+a,340);
    glVertex2f(110+a,340);
    glVertex2f(110+a,350);
    glEnd();
    glPointSize(8);
    glBegin(GL_POINTS);
    glColor3f(0,0.8,0);
    glVertex2f(105+a,360);
    glEnd();
    glPointSize(4);
    glBegin(GL_POINTS);
    glColor3f(1,0,0);
    glVertex2f(105+a,360);
    glEnd();

    // 2nd Partition
    glBegin(GL_QUADS);
    glColor3f(0.95,0.95,0.97);
    glVertex2f(16+a,400);
    glVertex2f(-71+a,400);
    glVertex2f(-71+a,340);
    glVertex2f(16+a,340);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.18,0.55,0.34);
    glVertex2f(16+a,384);
    glVertex2f(16+a,391);
    glVertex2f(-71+a,391);
    glVertex2f(-71+a,384);
    glEnd();
    glLineWidth(2);     // Joint
    glBegin(GL_LINES);
    glColor3f(0.3,0.3,0.3);
    glVertex2f(16+a,350);
    glVertex2f(19+a,350);
    glEnd();

    // 3rd Partition
    glBegin(GL_QUADS);
    glColor3f(0.95,0.95,0.97);
    glVertex2f(-74+a,400);
    glVertex2f(-162+a,400);
    glVertex2f(-162+a,340);
    glVertex2f(-74+a,340);
    glEnd();
    glBegin(GL_QUADS);
    glColor3f(0.18,0.55,0.34);
    glVertex2f(-74+a,384);
    glVertex2f(-74+a,391);
    glVertex2f(-162+a,391);
    glVertex2f(-162+a,384);
    glEnd();
    glLineWidth(2);     // Joint
    glBegin(GL_LINES);
    glColor3f(0.3,0.3,0.3);
    glVertex2f(-71+a,350);
    glVertex2f(-74+a,350);
    glEnd();

    // Front Window
    glBegin(GL_QUADS);
    glColor3f(0.75,0.75,0.75);
    glVertex2f(101+a,390);
    glVertex2f(101+a,375);
    glVertex2f(109+a,375);
    glVertex2f(109+a,390);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(101+a,375);
    glVertex2f(101+a,390);
    glVertex2f(109+a,375);
    glVertex2f(109+a,390);
    glVertex2f(101+a,390);
    glVertex2f(109+a,390);
    glVertex2f(101+a,375);
    glVertex2f(109+a,375);
    glEnd();
    glBegin(GL_LINES);    // Partition
    glColor3f(0,0,0);
    glVertex2f(103+a,375);
    glVertex2f(103+a,390);
    glEnd();
    glLineWidth(2);
    glBegin(GL_LINES);    // Black header
    glColor3f(0,0,0);
    glVertex2f(103+a,395);
    glVertex2f(107+a,395);
    glEnd();
    glPointSize(1.5);   // Front lights
    glBegin(GL_POINTS);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(101+a,360);
    glVertex2f(101+a,355);
    glVertex2f(109+a,360);
    glVertex2f(109+a,355);
    glEnd();

    // Doors
    glBegin(GL_QUADS);   // ....1.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(98+a,345);
    glVertex2f(98+a,375);
    glVertex2f(93+a,375);
    glVertex2f(93+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(98+a,375);
    glVertex2f(98+a,345);
    glVertex2f(93+a,375);
    glVertex2f(93+a,345);
    glVertex2f(98+a,345);
    glVertex2f(93+a,345);
    glVertex2f(98+a,375);
    glVertex2f(93+a,375);
    glEnd();
    glLineWidth(4);    // Window
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(95.5+a,360);
    glVertex2f(95.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....2.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(79+a,345);
    glVertex2f(79+a,375);
    glVertex2f(69+a,375);
    glVertex2f(69+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(79+a,375);
    glVertex2f(79+a,345);
    glVertex2f(69+a,375);
    glVertex2f(69+a,345);
    glVertex2f(79+a,345);
    glVertex2f(69+a,345);
    glVertex2f(79+a,375);
    glVertex2f(69+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(74+a,345);
    glVertex2f(74+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(71.5+a,360);
    glVertex2f(71.5+a,370);
    glVertex2f(76.5+a,360);
    glVertex2f(76.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....3.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(45+a,345);
    glVertex2f(45+a,375);
    glVertex2f(55+a,375);
    glVertex2f(55+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(55+a,375);
    glVertex2f(55+a,345);
    glVertex2f(45+a,375);
    glVertex2f(45+a,345);
    glVertex2f(55+a,345);
    glVertex2f(45+a,345);
    glVertex2f(55+a,375);
    glVertex2f(45+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(50+a,345);
    glVertex2f(50+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(47.5+a,360);
    glVertex2f(47.5+a,370);
    glVertex2f(52.5+a,360);
    glVertex2f(52.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....4.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(31+a,345);
    glVertex2f(31+a,375);
    glVertex2f(21+a,375);
    glVertex2f(21+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(31+a,375);
    glVertex2f(31+a,345);
    glVertex2f(21+a,375);
    glVertex2f(21+a,345);
    glVertex2f(31+a,345);
    glVertex2f(21+a,345);
    glVertex2f(31+a,375);
    glVertex2f(21+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(26+a,345);
    glVertex2f(26+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(23.5+a,360);
    glVertex2f(23.5+a,370);
    glVertex2f(28.5+a,360);
    glVertex2f(28.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....5.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(13+a,345);
    glVertex2f(13+a,375);
    glVertex2f(3+a,375);
    glVertex2f(3+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(13+a,375);
    glVertex2f(13+a,345);
    glVertex2f(3+a,375);
    glVertex2f(3+a,345);
    glVertex2f(13+a,345);
    glVertex2f(3+a,345);
    glVertex2f(13+a,375);
    glVertex2f(3+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(8+a,345);
    glVertex2f(8+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(5.5+a,360);
    glVertex2f(5.5+a,370);
    glVertex2f(10.5+a,360);
    glVertex2f(10.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....6.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-11+a,345);
    glVertex2f(-11+a,375);
    glVertex2f(-21+a,375);
    glVertex2f(-21+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-11+a,375);
    glVertex2f(-11+a,345);
    glVertex2f(-21+a,375);
    glVertex2f(-21+a,345);
    glVertex2f(-11+a,345);
    glVertex2f(-21+a,345);
    glVertex2f(-11+a,375);
    glVertex2f(-21+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-16+a,345);
    glVertex2f(-16+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-13.5+a,360);
    glVertex2f(-13.5+a,370);
    glVertex2f(-18.5+a,360);
    glVertex2f(-18.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....7.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-35+a,345);
    glVertex2f(-35+a,375);
    glVertex2f(-45+a,375);
    glVertex2f(-45+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-35+a,375);
    glVertex2f(-35+a,345);
    glVertex2f(-45+a,375);
    glVertex2f(-45+a,345);
    glVertex2f(-35+a,345);
    glVertex2f(-45+a,345);
    glVertex2f(-35+a,375);
    glVertex2f(-45+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-40+a,345);
    glVertex2f(-40+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-37.5+a,360);
    glVertex2f(-37.5+a,370);
    glVertex2f(-42.5+a,360);
    glVertex2f(-42.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....8.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-59+a,345);
    glVertex2f(-59+a,375);
    glVertex2f(-69+a,375);
    glVertex2f(-69+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-59+a,375);
    glVertex2f(-59+a,345);
    glVertex2f(-69+a,375);
    glVertex2f(-69+a,345);
    glVertex2f(-59+a,345);
    glVertex2f(-69+a,345);
    glVertex2f(-59+a,375);
    glVertex2f(-69+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-64+a,345);
    glVertex2f(-64+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-61.5+a,360);
    glVertex2f(-61.5+a,370);
    glVertex2f(-66.5+a,360);
    glVertex2f(-66.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....9.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-77+a,345);
    glVertex2f(-77+a,375);
    glVertex2f(-87+a,375);
    glVertex2f(-87+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-77+a,375);
    glVertex2f(-77+a,345);
    glVertex2f(-87+a,375);
    glVertex2f(-87+a,345);
    glVertex2f(-77+a,345);
    glVertex2f(-87+a,345);
    glVertex2f(-77+a,375);
    glVertex2f(-87+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-82+a,345);
    glVertex2f(-82+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-79.5+a,360);
    glVertex2f(-79.5+a,370);
    glVertex2f(-84.5+a,360);
    glVertex2f(-84.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....10.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-101+a,345);
    glVertex2f(-101+a,375);
    glVertex2f(-111+a,375);
    glVertex2f(-111+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-101+a,375);
    glVertex2f(-101+a,345);
    glVertex2f(-111+a,375);
    glVertex2f(-111+a,345);
    glVertex2f(-101+a,345);
    glVertex2f(-111+a,345);
    glVertex2f(-101+a,375);
    glVertex2f(-111+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-106+a,345);
    glVertex2f(-106+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-103.5+a,360);
    glVertex2f(-103.5+a,370);
    glVertex2f(-108.5+a,360);
    glVertex2f(-108.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....11.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-125+a,345);
    glVertex2f(-125+a,375);
    glVertex2f(-135+a,375);
    glVertex2f(-135+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-125+a,375);
    glVertex2f(-125+a,345);
    glVertex2f(-135+a,375);
    glVertex2f(-135+a,345);
    glVertex2f(-125+a,345);
    glVertex2f(-135+a,345);
    glVertex2f(-125+a,375);
    glVertex2f(-135+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-130+a,345);
    glVertex2f(-130+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-127.5+a,360);
    glVertex2f(-127.5+a,370);
    glVertex2f(-132.5+a,360);
    glVertex2f(-132.5+a,370);
    glEnd();

    glBegin(GL_QUADS);     // ....12.....
    glColor3f(0.85,0.85,0.85);
    glVertex2f(-149+a,345);
    glVertex2f(-149+a,375);
    glVertex2f(-159+a,375);
    glVertex2f(-159+a,345);
    glEnd();
    glLineWidth(1);     // borders
    glBegin(GL_LINES);
    glColor3f(0,0,0);
    glVertex2f(-149+a,375);
    glVertex2f(-149+a,345);
    glVertex2f(-159+a,375);
    glVertex2f(-159+a,345);
    glVertex2f(-149+a,345);
    glVertex2f(-159+a,345);
    glVertex2f(-149+a,375);
    glVertex2f(-159+a,375);
    glEnd();
    glBegin(GL_LINES);     // partition
    glColor3f(1,0,0);
    glVertex2f(-154+a,345);
    glVertex2f(-154+a,375);
    glEnd();
    glLineWidth(4);    // Windows
    glBegin(GL_LINES);
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-151.5+a,360);
    glVertex2f(-151.5+a,370);
    glVertex2f(-156.5+a,360);
    glVertex2f(-156.5+a,370);
    glEnd();

    // Windows
    glBegin(GL_QUADS);   // ....1.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(82+a,360);
    glVertex2f(82+a,373);
    glVertex2f(90+a,373);
    glVertex2f(90+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....2.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(66+a,360);
    glVertex2f(66+a,373);
    glVertex2f(58+a,373);
    glVertex2f(58+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....3.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(42+a,360);
    glVertex2f(42+a,373);
    glVertex2f(34+a,373);
    glVertex2f(34+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....4.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(0+a,360);
    glVertex2f(0+a,373);
    glVertex2f(-8+a,373);
    glVertex2f(-8+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....5.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-24+a,360);
    glVertex2f(-24+a,373);
    glVertex2f(-32+a,373);
    glVertex2f(-32+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....6.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-48+a,360);
    glVertex2f(-48+a,373);
    glVertex2f(-56+a,373);
    glVertex2f(-56+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....7.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-90+a,360);
    glVertex2f(-90+a,373);
    glVertex2f(-98+a,373);
    glVertex2f(-98+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....8.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-114+a,360);
    glVertex2f(-114+a,373);
    glVertex2f(-122+a,373);
    glVertex2f(-122+a,360);
    glEnd();
    glBegin(GL_QUADS);   // ....9.....
    glColor3f(0.55,0.55,0.55);
    glVertex2f(-138+a,360);
    glVertex2f(-138+a,373);
    glVertex2f(-146+a,373);
    glVertex2f(-146+a,360);
    glEnd();
    /// End Train ///

    glLineWidth(4);
    glBegin(GL_LINES);   ///
    glColor3f(0.2,0.2,0.2);
    glVertex2f(180,340);
    glVertex2f(180,440);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(370,340);
    glVertex2f(370,440);
    glEnd();
    glBegin(GL_LINES);
    glColor3f(0.2,0.2,0.2);
    glVertex2f(560,340);
    glVertex2f(560,440);
    glEnd();      ///

    /// Left corner big tree
    glColor3ub(139, 146, 22);
    circle(8,22,0,70);
    glColor3ub(139, 146, 22);
    circle(8,22,10,90);
    glColor3ub(139, 146, 22);
    circle(8,22,13,60);
    glColor3ub(139, 146, 22);
    circle(7,25,22,70);
    glColor3ub(139, 146, 22);
    circle(8,22,30,70);
    glColor3ub(139, 146, 22);
    circle(10,40,0,170);

    glColor3ub(139, 146, 22);
    circle(9,22,30,215);
    glColor3ub(139, 146, 22);
    circle(8,15,30,213);

    glColor3ub(139, 146, 22);
    circle(9,22,45,205);
    glColor3ub(139, 146, 22);
    circle(9,22,45,200);
    glColor3ub(139, 146, 22);
    circle(8,15,45,195);

    glColor3ub(139, 146, 22);
    circle(9,22,55,155);
    glColor3ub(139, 146, 22);
    circle(9,32,50,175);

    glColor3ub(139, 146, 22);
    circle(9,22,59,145);
    glColor3ub(139, 146, 22);
    circle(9,22,56,175);
    glColor3ub(139, 146, 22);
    circle(9,22,63,115);
    glColor3ub(139, 146, 22);
    circle(9,22,50,100);
    glColor3ub(139, 146, 22);
    circle(9,22,58,85);
    glColor3ub(139, 146, 22);
    circle(9,22,49,70);
    glColor3ub(139, 146, 22);
    circle(9,22,38,60);


    glColor3ub(0, 77, 26);
    circle(10,20,55,110);
    glColor3ub(139, 146, 22);
    circle(9.5,19,55,110);


    glColor3ub(0, 77, 26);
    circle(10,20,55,125);
    glColor3ub(139, 146, 22);
    circle(9.5,20,55,125);


    glColor3ub(0, 77, 26);
    circle(10,20,50,138);
    glColor3ub(139, 146, 22);
    circle(9.5,20,50,138);


    glColor3ub(139, 146, 22);
    circle(10,20,27,50);


    glColor3ub(139, 146, 22);
    circle(35,70,20,120);
    glColor3ub(139, 146, 22);    ///
    circle(15,30,30,175);


    glColor3ub(0, 77, 26);
    circle(10,20,42,145);
    glColor3ub(139, 146, 22);
    circle(9.5,20,42,144);


    glColor3ub(0, 77, 26);
    circle(10,20,30,145);
    glColor3ub(139, 146, 22);
    circle(10,20,30,144);


    glColor3ub(0, 77, 26);
    circle(10,18,42,183);
    glColor3ub(139, 146, 22);
    circle(10,18,42,182);


    glColor3ub(0, 77, 26);
    circle(10,20,30,100);
    glColor3ub(139, 146, 22);
    circle(10,20,30,99);

    glColor3ub(0, 77, 26);
    circle(10,20,20,100);
    glColor3ub(139, 146, 22);
    circle(10,20,20,99);

    glColor3ub(0, 77, 26);
    circle(10,20,40,75);
    glColor3ub(139, 146, 22);
    circle(10,20,40,76);


    glColor3ub(139, 146, 22);
    circle(9,22,20,200);
    glColor3ub(0, 77, 26);
    circle(9,21,20,190);
    glColor3ub(139, 146, 22);
    circle(9,21,20,189);


    glColor3ub(139, 146, 22);
    circle(9,22,10,175);
    glColor3ub(0, 77, 26);
    circle(9,20,10,165);
    glColor3ub(139, 146, 22);
    circle(9,20,10.5,164);


    ///........Tree........D-1........///
    glBegin(GL_TRIANGLE_FAN);
    glColor3ub(75,35,5);
    glVertex2f(13,0);
    glVertex2f(21,0);
    glVertex2f(21,20);
    glVertex2f(20,30);
    glVertex2f(18,40);
    glVertex2f(16,50);
    glVertex2f(17,60);
    glVertex2f(18,65);
    glVertex2f(20,70);
    glVertex2f(22,70);
    glVertex2f(21,67);
    glVertex2f(20,65);
    glVertex2f(18,60);
    glVertex2f(16,50);
    glVertex2f(13,40);
    glVertex2f(16,50);
    glVertex2f(18,60);
    glVertex2f(20,65);
    glVertex2f(22,70);
    glVertex2f(22,80);
    glVertex2f(18,70);
    glEnd();


    glBegin(GL_TRIANGLE_FAN);  ///........Tree........D-2.......///
    glColor3ub(75,35,5);
    glVertex2f(15,45);
    glVertex2f(19,50);
    glVertex2f(14,60);
    glVertex2f(14,70);
    glVertex2f(13,80);
    glVertex2f(10,90);
    glVertex2f(12,90);
    glVertex2f(12,80);
    glVertex2f(11,70);
    glVertex2f(11,60);
    glEnd();

    glBegin(GL_TRIANGLE_FAN);   ///tree...................D-3 p2  ///
    glColor3ub(75,35,5);
    glVertex2f(31,60);
    glVertex2f(29,60);
    glVertex2f(28,40);
    glVertex2f(25,40);
    glEnd();


    glBegin(GL_TRIANGLE_FAN);  ///tree..................D-3 p1   ///
    glColor3ub(75,35,5);
    glVertex2f(16,20);
    glVertex2f(21,20);
    glVertex2f(24.5,40);
    glVertex2f(28,40);
    glEnd();
    /// End Tree ///

    }
    glutSwapBuffers();
}

void specialKeys(int key, int x, int y) {
    switch (key) {
        case GLUT_KEY_UP:
            if (metroSpeed >= 0) metroStop = false;
            metroSpeed += 0.3;
            break;
        case GLUT_KEY_DOWN:
            if (metroSpeed > 0) metroSpeed -= 0.3;
            if (metroSpeed <= 0) metroStop = true;
            break;
    }
    glutPostRedisplay();
}

void keyboard(unsigned char key, int x, int y) {

    switch(key)
    {
    case '1':
        scenario = key; // Set the scenario
        PlaySound(NULL, NULL, 0);
        PlaySound(TEXT("platform.wav"), NULL,SND_ASYNC|SND_FILENAME|SND_LOOP);
        break;

    case '2':
        scenario = key; // Set the scenario
        PlaySound(NULL, NULL, 0);
        PlaySound(TEXT("metro.wav"), NULL,SND_ASYNC|SND_FILENAME|SND_LOOP);
        break;

    case '3':
        scenario = key; // Set the scenario
        PlaySound(NULL, NULL, 0);
        PlaySound(TEXT("metro.wav"), NULL,SND_ASYNC|SND_FILENAME|SND_LOOP);
        break;

    case 'd':
        isDay = true;
        break;

    case 'n':
        isDay = false;
        break;

    case '+':
        glutFullScreen();
        break;

    case '-':
        glutReshapeWindow(1450,750);
        glutInitWindowPosition(50,50);
        break;

    case 'x':
        PlaySound(NULL, NULL, 0);
        exit(0);
        break;
    }

    glutPostRedisplay(); // Request redraw
}

void update(int value) {
    glutPostRedisplay(); // Redraw the screen
    glutTimerFunc(16, update, 0);
}

void initOpenGL() {
    glClearColor(0.0, 0.0, 0.0, 1.0); // Black background
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    gluOrtho2D(0, 700, 0, 800); // Set up a 2D orthographic projection
}

int main(int argc, char **argv) {
    cout << "Press 1 : For Scenario 1 " << endl << endl;
    cout << "Press 2 : For Scenario 2 " << endl << endl;
    cout << "Press 3 : For Scenario 3 " << endl << endl;
    cout << "Press d : For Day " << endl << endl;
    cout << "Press n : For Night " << endl << endl;
    cout << "Press UP Arrow : For Speed up " << endl << endl;
    cout << "Press Down Arrow : For Speed Down " << endl << endl;
    cout << "Press + : For Full Screen " << endl << endl;
    cout << "Press - : For Restore Screen " << endl << endl;
    cout << "Press x : For Hide Screen " << endl << endl;

    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB);
    glutInitWindowSize(1450, 750);
    glutInitWindowPosition(50,50);
    glutCreateWindow("Bangladesh Metro Rail");

    initOpenGL();
    glutDisplayFunc(display);
    glutKeyboardFunc(keyboard);
    glutSpecialFunc(specialKeys);
    glutTimerFunc(0, update, 0);

    glutMainLoop();
    return 0;
}
