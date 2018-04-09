# -*- coding: utf-8 -*-
"""
Created on Wed Mar 21 09:51:44 2018

@author: Jonny and Robert
"""
import math
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation
from math import sqrt
from matplotlib import style


G = 6.67 * math.pow(10,-11)

class Etoile(object):    
    def __init__(self,m,r,x,y):
        self.masse=m
        #en kg
        self.rayon=r
        #par rapport à la Terre(r de la terre=1.00:)
        self.positionx=x
        self.positiony=y
 
Rayon_terre= 6371000 #mètre
    
soleil= Etoile(1.9891*math.pow(10,30), 109.2*Rayon_terre,0,0)


class Planete(object):
    G = 6.67 * math.pow(10,-11)
    
    def __init__(self,n,m,r,x,y,vx,vy):
        self.name=n
        self.masse=m
        #en kg
        #http://www.astronoo.com/fr/articles/caracteristiques-des-planetes.html
        self.rayon=r
        #par rapport à la Terre(r de la terre=1.00)
        self.positionx=x
        self.positiony=y
        #en AU
        self.vx=vx
        self.vy=vy
        #vitesse initial en x et en y
        #en m/s?
        
AU=1.49578707*math.pow(10,10)
    
mercure= Planete("Mercure",0.3302*math.pow(10,24),0.382*Rayon_terre,0.387*AU,0,0,147360)#vitessey inventé

venus= Planete("Venus",4.8685*math.pow(10,24),0.949*Rayon_terre,0.723*AU,0,0,35020)

terre= Planete("Terre",5.9736*math.pow(10,24),1.00*Rayon_terre,1.00*AU,0,0,29790)

mars= Planete("Mars",0.6418*math.pow(10,24),0.532*Rayon_terre,1.523*AU,0,0,24077)

jupiter= Planete("Jupiter",1898.6*math.pow(10,24),11.209*Rayon_terre,5.20*AU,0,0,13057.2)

saturne= Planete("Saturne",568.46*math.pow(10,24),9.449*Rayon_terre,9.537*AU,0,0,9644.6)

uranus= Planete("Uranus",86.810*math.pow(10,24),4.007*Rayon_terre,19.229*AU,0,0,6800)

neptune= Planete("Neptune",102.43*math.pow(10,24),3.883*Rayon_terre,30.069*AU,0,0,15431.7)#vitessey inventé

pluton= Planete("Pluton",1.314*math.pow(10,22),0.178*Rayon_terre,39.445*AU,0,0,4740)

xdata=0
ydata=0

def mouvement(P):

    print("Position de " +P.name+ " en x: " + str(P.positionx))
    print("Position de " +P.name+ " en y: " + str(P.positiony))
    print("Vitesse de " +P.name+ " en x: " + str(P.vx))
    print("Vitesse de " +P.name+ " en y: " + str(P.vy))
    
    datasoleil = plt.Circle((soleil.positionx, soleil.positiony), soleil.rayon, color='orange')        
    
    fig = plt.figure()    
    ax=fig.add_subplot(1,1,1, aspect='equal')
    ax.set_facecolor('black')
    ax.add_artist(datasoleil)
    
    dt=10
    
    def func(i):
        xdata=[]
        ydata=[]
        t=0 
            
        
        for i in range(0,20000):
            t=t+dt
            d=sqrt((P.positionx)**2 + (P.positiony)**2)
            j=math.atan2(P.positiony, P.positionx)
            
            P.positionx = P.positionx + P.vx*dt + ((-G*soleil.masse*(dt)**2)/(d**2))*math.cos(j)
            P.positiony = P.positiony + P.vy*dt + ((-G*soleil.masse*(dt)**2)/(d**2))*math.sin(j)
            
            P.vx = P.vx + ((-G*soleil.masse*dt)/(d**2))*math.cos(j)
            P.vy = P.vy + ((-G*soleil.masse*dt)/(d**2))*math.sin(j)
            
            xdata.append(P.positionx)
            ydata.append(P.positiony)
        
        
        ax.plot(xdata,ydata, linewidth=2.0)

    ready=input("Ready ?")
    
    ani = animation.FuncAnimation(fig, func, interval=0.1)
    
    plt.xlim(-39.445*AU, 39.445*AU)
    plt.ylim(-39.445*AU, 39.445*AU)
    plt.grid(color='w', linestyle='--')
    plt.title('Orbite de ' + P.name, fontsize=14)
    plt.xlabel('x (m)', fontsize=13)
    plt.ylabel('y (m)', fontsize=13)
    plt.show()



def Run():
    exiT=0
    while not exiT==1:
        ch=input("Choissisez une planète: ")
        if ch=="mercure":
            mouvement(mercure)
            exiT=RE()
        elif ch=="venus" or ch=="Venus":
            mouvement(venus)
            exiT=RE()
        elif ch=="terre" or ch=="Terre":
            mouvement(terre)
            exiT=RE()
        elif ch=="mars" or ch=="Mars":
            mouvement(mars)
            exiT=RE()         
        elif ch=="jupiter" or ch=="Jupiter":
            mouvement(jupiter)
            exiT=RE()
        elif ch=="saturne" or ch=="Saturne":
            mouvement(saturne)
            exiT=RE()
        elif ch=="uranus" or ch=="Uranus":
            mouvement(uranus)
            exiT=RE()
        elif ch=="neptune" or ch=="Neptune":
            mouvement(neptune)
            exiT=RE()
        elif ch=="pluton" or ch=="Pluton":
            mouvement(pluton)
            exiT=RE()     
        else:
            print("Hein?")
      
def RE():
    while True:
        retry=input("Réessayer? o/n: ")
        if retry=="o":
            retry="?"
            return 0
        elif retry=="n":
            retry="?"
            print("ok then")
            return 1
        else:
            print("Heiin?")
        
Run()

sad=input("press enter to close this window")
