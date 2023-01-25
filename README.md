# CGP_TaskPerformance


import pygame
from pygame.locals import *
from OpenGL.GL import *
from OpenGL.GLU import *
import OpenGL.GL as GL


def draw_square_head():
    glBegin(GL_TRIANGLES)
    glTexCoord2f(0.5, 1)    
    glVertex3f(1, 2, 1)
    glTexCoord2f(0, 0)
    glVertex3f(-1, 2, 1)
    glTexCoord2f(1, 0)
    glVertex3f(-1, 1, 1)

    glTexCoord2f(0.5, 1)  
    glVertex3f(-1, 1, 1)
    glTexCoord2f(0, 0)
    glVertex3f(1, 1, 1)
    glTexCoord2f(1, 0)
    glVertex3f(1, 2, 1)
    glEnd()


def draw_square():

    glBegin(GL_TRIANGLES)
    glTexCoord2f(0.5, 1)    
    glVertex3f(1, 1, 1)
    glTexCoord2f(0, 0)
    glVertex3f(-1, 1, 1)
    glTexCoord2f(1, 0)
    glVertex3f(-1, -1, 1)

    glTexCoord2f(0.5, 1)  
    glVertex3f(-1, -1, 1)
    glTexCoord2f(0, 0)
    glVertex3f(1, -1, 1)
    glTexCoord2f(1, 0)
    glVertex3f(1, 1, 1)
    glEnd()
    

def draw_cube():
  
    glPushMatrix()
    draw_square()
    glPopMatrix()

    glPushMatrix()
    glRotatef(90, 0, 1, 0)
    draw_square()
    glPopMatrix()

    glPushMatrix()
    glRotatef(-90, 1, 0, 0)
    draw_square()
    glPopMatrix()

    glPushMatrix()
    glRotatef(180, 0, 1, 0)
    draw_square()
    glPopMatrix()

    glPushMatrix()
    glRotatef(-90, 0, 1, 0)
    draw_square()
    glPopMatrix()

    glPushMatrix()
    glRotatef(90, 1, 0, 0)
    draw_square()
    glPopMatrix()

def draw_cube_hat():
   
    glPushMatrix()
    draw_square_head()
    glPopMatrix()

    glPushMatrix()
    glRotatef(90, 0, 1, 0)
    draw_square_head()
    glPopMatrix()

    glPushMatrix()
    glRotatef(-90, 1, 0, 0)
    draw_square_head()
    glPopMatrix()

    glPushMatrix()
    glRotatef(180, 0, 1, 0)
    draw_square_head()
    glPopMatrix()

    glPushMatrix()
    glRotatef(-90, 0, 1, 0)
    draw_square_head()
    glPopMatrix()
  

def add_texture_head():
    image = pygame.image.load('snowman.jpg')
    data = pygame.image.tostring(image, 'RGBA')
    texID = glGenTextures(1)
    glBindTexture(GL_TEXTURE_2D, texID)
    glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, image.get_width(), image.get_height(), 0, GL_RGBA, GL_UNSIGNED_BYTE, data)
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR)
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR)
    glEnable(GL_TEXTURE_2D)
    
def main():
    pygame.init()
    display =(800,600)
    pygame.display.set_mode(display,DOUBLEBUF|OPENGL)
    pygame.display.set_caption("06 Lab Exercise 01 Theerd Figura Arroza")
    
    glEnable(GL_DEPTH_TEST)
    
    gluPerspective(45, display[0]/display[1], 0.1, 50.0)
    glTranslatef(0.0, 0.0, -7)
    while True:
        for event in pygame.event.get():
            if event.type==pygame.QUIT:
                pygame.quit()
                quit()        

        glRotatef(1, 0, 1, 0)    
        glClear(GL_COLOR_BUFFER_BIT|GL_DEPTH_BUFFER_BIT)
        
        draw_cube_hat()
        draw_cube()
        pygame.display.flip()
        pygame.time.wait(15)
        
main()



















