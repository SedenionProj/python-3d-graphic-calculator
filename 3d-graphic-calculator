import time
import pip
from math import sin, cos, sqrt

try:
    import keyboard
except:
    print("installing keyboard module...")
    pip.main(['install', "keyboard"])
    import keyboard

width, height = 120//2,30-1 #118,66   //   120,30 full screen

top,bottom,left,right=height//2,-height//2,-width//2,width//2

fpsMax = 60

light=" .'~=/F#@"

dernier=0

map = [[0 for _ in range(width)] for _ in range(height)]

def rotationx(x,y,z):
    y1=cos(xrot)*y-sin(xrot)*z
    z1=sin(xrot)*y+cos(xrot)*z
    return y1,z1

def rotationy(x,y,z):
    x1=cos(yrot)*x+sin(yrot)*z
    z1=-sin(yrot)*x+cos(yrot)*z
    return x1,z1

def projection(x,y,z):
    x1=(x*25)/(z)
    y1=(y*25)/(z)
    return x1,y1

def matrix(x,y,z):

    
    x1=x    #orthogonal space
    y1=-y
    z1=z

    x1+=xcam
    y1+=ycam
    z1+=zcam

    x1,z1=rotationy(x1,y1,z1)
    y1,z1=rotationx(x1,y1,z1)
    

    if z1>0:
        x1,y1=(projection(x1,y1,z1))
    else:
        return None
    
    x1+=right
    y1+=top

    x1=round(x1)
    y1=round(y1)

    if x1 < width and y1 < height and x1>=0 and y1>=0:
        return x1,y1

def clear():
    for y in range(height):
        for x in range(width):
            map[y][x]=0

def render():
    n=' '*width*2
    for y in range(height):
        for x in range(width):
            n+=light[map[y][x]]*2
    print(n,end='')

def lighting(x,y,z):
    x1=xlight-x
    y1=ylight-y
    z1=zlight-z
    n=sqrt(x1**2+y1**2+z1**2)
    if n>0:
        return round(((y1/n)*7))+1
    else:
        return 1

def draw(x,y,z):
    n = matrix(x,y,z)
    if not n==None:
        light = lighting(x,y,z)
        map[n[1]][n[0]]=light
    
xlight=0
ylight=10
zlight=0

xcam = 0
ycam = 10
zcam = -30

xrot=0
yrot=3.14

while True:
    clear()
    courent = time.time()
    dt = (courent-dernier)*10
    dernier=courent
    if keyboard.is_pressed("up arrow"):
        if xrot>-1.57:
            xrot-=0.1*dt
    if keyboard.is_pressed("down arrow"):
        if xrot<1.57:
            xrot+=0.1*dt
    if keyboard.is_pressed("left arrow"):
        yrot+=0.1*dt
    if keyboard.is_pressed("right arrow"):
        yrot-=0.1*dt
    if keyboard.is_pressed("z"):
        xcam-=-sin(yrot)*3*dt
        zcam-=cos(yrot)*3*dt
    if keyboard.is_pressed("s"):
        xcam+=-sin(yrot)*3*dt
        zcam+=cos(yrot)*3*dt
    if keyboard.is_pressed("q"):
        xcam+=cos(yrot)*3*dt
        zcam+=sin(yrot)*3*dt
    if keyboard.is_pressed("d"):
        xcam-=cos(yrot)*3*dt
        zcam-=sin(yrot)*3*dt
    if keyboard.is_pressed("space"):
        ycam+=5*dt
    if keyboard.is_pressed("shift"):
        ycam-=5*dt

    for x in range(-20,20):
        for z in range(-20,20):
            draw(x,0,z)

    render()
    
