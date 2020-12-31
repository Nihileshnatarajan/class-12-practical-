# class-12-practical-
#SARA AIRLINE ONLINE RESERVATION

import os
import platform
import random
import mysql.connector
import pandas as pd
import datetime
global z
global prows
global brows
mydb=mysql.connector.connect(user='root',password='pass',host='localhost',database='airline')
mycursor=mydb.cursor()
mydb.commit()
mycursor.execute('drop database airline')
mycursor.execute('create database if not exists airline')
mycursor.execute('use airline')
mycursor.execute('create table pdata(custname varchar(50),addr varchar(90),jrdate date)')
print('WELCOME TO SARA AIRLINE ONLINE RESERVATION\n')
print('Please Fill in Every Details , Enter and Check Every Option\n')
mycursor.execute('create table travloc(b_station varchar(40),l_station varchar(40),takeofftime varchar(50),flytime varchar(30))')
query1='insert into travloc values(%s,%s,%s,%s)'
dat=[('USA,Washington,D.C.','India,Chennai','Monday,08:20:00','48 Hours'),
     ('USA,New york','India,Chennai','Monday,16:40:00','40 Hours'),
     ('Dubai','USA,New york','Tuesday,12:30:00','36 Hours'),
     ('India,Delhi','Canada,Gander','Tuesday,14:10:00','52 Hours'),
     ('India,Delhi','Canada,Hamilton','Thursday,10:40:00','56 Hours'),
     ('Australia,Sydney','USA,Washington,D.C.','Wednesday,12:50:00','70 Hours'),
     ('India,Chennai','Sri lanka,Colombo','Friday,20:10:00','18 Hours'),
     ('India,Chennai','USA,Washington,D.C.','Thursday,18:40:00','48 Hours'),
     ('India,Chennai','USA,New york','Friday,16:40:00','40 Hours'),
     ('Canada,Gander','India,Delhi','Sunday,12:40:00','52 Hours'),
     ('USA,Washington,D.C.','Australia,Sydney','Sunday,16:30:00','70 Hours'),
     ('India,Delhi','Japan,Nairo','Wednesday,17:20:00','28 Hours'),
     ('Japan,Nairo','India,Delhi','Sunday,7:30:00','28 Hours')]
mycursor.executemany(query1,dat)
    
def registercust():
    print('Incomplete registration will cancel your Reservation!\n')
    print('You Can Also Cancel Your Reservation If Your Boarding Station And Destination Is Not Available\n')
    print('Following are the Planes Available:\n')
    sbl='select*from travloc'
    mycursor.execute(sbl)
    go=mycursor.fetchall()
    print('Boarding Station , Landing Station , Takeoff Time , Fly Time\n')
    for c in go:
        print(c)
    usin=int(input('\nEnter 1 To Continue Reservation Or 2 To Exit:'))
    if usin==1:
        L=[]
        name=input('\nEnter name:')
        L.append(name)
        addr=input('Enter address:')
        L.append(addr)
        jr_date=input('Enter date of journey(year-month-day):')
        L.append(jr_date)
        print('Customer Details are as follows:\n')
        cust=(L)
        sql='insert into pdata(custname,addr,jrdate) values(%s,%s,%s)'
        mycursor.execute(sql,cust)
        mydb.commit()       
        sq='select custname,addr,jrdate from pdata'
        mycursor.execute(sq)
        rows=mycursor.fetchall()
        for x in rows:
            print('Name , Address , Boarding Date\n')
            print(x)
    else:
        quit()

mycursor.execute('create table passdetails(name varchar(50) primary key,destination varchar(30),board varchar(40))')

def location():
    global p
    k=[]
    print('The Following Are The Available Boarding Stations And Destinations\n')
    print('Boarding Station  ,  Landing Station\n')
    sq='select b_station,l_station from travloc'
    mycursor.execute(sq)
    rows=mycursor.fetchall()
    for r in rows:
        print(r)
    mycursor.execute('alter table pdata add column destination varchar(40)')
    mycursor.execute('alter table pdata add column board varchar(40)')
    q=input('\nEnter your Name:')
    k.append(q)
    a=input('Enter Your Destination(PLEASE TYPE AS IT IS IN THE ABOVE LIST) or x to exit:')
    k.append(a)
    t=input('Enter Your Boarding Station:')
    k.append(t)
    v=(k)
    n='insert into passdetails(name,destination,board) values(%s,%s,%s)'
    mycursor.execute(n,v)
    mydb.commit()
    if a=='India,Chennai':
        if t=='USA,Washington,D.C.':
            s='select*from travloc where b_station like "%D.C."'
            mycursor.execute(s)
            w=mycursor.fetchall()
            print('\nBoarding Station, Landing Station, Takeoff Time, Fly Time\n')
            for j in w:
                print('\n',j)
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.destination=passdetails.destination')
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.board=passdetails.board')
            sml='select custname,board,destination from pdata'
            mycursor.execute(sml)
            p=mycursor.fetchall()
            print('\nName, Boarding Station, Landing Station\n')
            for b in p:
                print('\n',b)
        elif t=='USA,New york':
            s='select*from travloc where b_station like "%york"'
            mycursor.execute(s)
            w=mycursor.fetchall()
            print('\nBoarding Station, Landing Station, Takeoff Time, Fly Time\n')
            for j in w:
                print('\n',j)
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.destination=passdetails.destination')
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.board=passdetails.board')
            sml='select custname,board,destination from pdata'
            mycursor.execute(sml)
            p=mycursor.fetchall()
            print('\nName, Boarding Station, Landing Station\n')
            for b in p:
                print('\n',b)
    elif a=='USA,New york':
        if t=='Dubai':
            s='select*from travloc where b_station like "%bai"'
            mycursor.execute(s)
            w=mycursor.fetchall()
            print('\nBoarding Station, Landing Station, Takeoff Time, Fly Time\n')
            for j in w:
                print('\n',j)
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.destination=passdetails.destination')
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.board=passdetails.board')
            sml='select custname,board,destination from pdata'
            mycursor.execute(sml)
            p=mycursor.fetchall()
            print('\nName, Boarding Station, Landing Station\n')
            for b in p:
                print('\n',b)
        elif t=='India,Chennai':
            s='select*from travloc where b_station like "%Chennai"'
            mycursor.execute(s)
            w=mycursor.fetchall()
            print('\nBoarding Station, Landing Station, Takeoff Time, Fly Time\n')
            for j in w:
                print('\n',j)
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.destination=passdetails.destination')
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.board=passdetails.board')
            sml='select custname,board,destination from pdata'
            mycursor.execute(sml)
            p=mycursor.fetchall()
            print('\nName, Boarding Station, Landing Station\n')
            for b in p:
                print('\n',b)
    elif a=='Canada,Gander':
        s='select*from travloc where l_station like "%Gander"'
        mycursor.execute(s)
        w=mycursor.fetchall()
        print('\nBoarding Station, Landing Station, Takeoff Time, Fly Time\n')
        for j in w:
            print('\n',j)
        mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.destination=passdetails.destination')
        mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.board=passdetails.board')
        sml='select custname,board,destination from pdata'
        mycursor.execute(sml)
        p=mycursor.fetchall()
        print('\nName, Boarding Station, Landing Station\n')
        for b in p:
            print('\n',b)
    elif a=='Canada,Hamilton':
        s='select*from travloc where l_station like "%Hamilton"'
        mycursor.execute(s)
        w=mycursor.fetchall()
        print('\nBoarding Station, Landing Station, Takeoff Time, Fly Time\n')
        for j in w:
            print('\n',j)
        mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.destination=passdetails.destination')
        mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.board=passdetails.board')
        sml='select custname,board,destination from pdata'
        mycursor.execute(sml)
        p=mycursor.fetchall()
        print('\nName, Boarding Station, Landing Station\n')
        for b in p:
            print('\n',b)
    elif a=='USA,Washington,D.C.':
        if t=='India,Chennai':
            s='select*from travloc where b_station like "%Chennai"'
            mycursor.execute(s)
            w=mycursor.fetchall()
            print('\nBoarding Station, Landing Station, Takeoff Time, Fly Time\n')
            for j in w:
                print('\n',j)
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.destination=passdetails.destination')
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.board=passdetails.board')
            sml='select custname,board,destination from pdata'
            mycursor.execute(sml)
            p=mycursor.fetchall()
            print('\nName, Boarding Station, Landing Station\n')
            for b in p:
                print('\n',b)
        elif t=='Australia,Sydney':
            s='select*from travloc where b_station like "%Sydney"'
            mycursor.execute(s)
            w=mycursor.fetchall()
            print('\nBoarding Station, Landing Station, Takeoff Time, Fly Time\n')
            for j in w:
                print('\n',j)
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.destination=passdetails.destination')
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.board=passdetails.board')
            sml='select custname,board,destination from pdata'
            mycursor.execute(sml)
            p=mycursor.fetchall()
            print('\nName, Boarding Station, Landing Station\n')
            for b in p:
                print('\n',b)            
    elif a=='Sri lanka,Colombo':
        s='select*from travloc where l_station like "%Colombo"'
        mycursor.execute(s)
        w=mycursor.fetchall()
        print('\nBoarding Station, Landing Station, Takeoff Time, Fly Time\n')
        for j in w:
            print('\n',j)
        mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.destination=passdetails.destination')
        mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.board=passdetails.board')
        sml='select custname,board,destination from pdata'
        mycursor.execute(sml)
        p=mycursor.fetchall()
        print('\nName, Boarding Station, Landing Station\n')
        for b in p:
            print('\n',b)
    elif a=='India,Delhi':
        if t=='Canada,Gander':
            s='select*from travloc where b_station like "%Gander"'
            mycursor.execute(s)
            w=mycursor.fetchall()
            print('\nBoarding Station, Landing Station, Takeoff Time, Fly Time\n')
            for j in w:
                print('\n',j)
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.destination=passdetails.destination')
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.board=passdetails.board')
            sml='select custname,board,destination from pdata'
            mycursor.execute(sml)
            p=mycursor.fetchall()
            print('\nName, Boarding Station, Landing Station\n')
            for b in p:
                print('\n',b)
        elif t=='Japan,Nairo':
            s='select*from travloc where b_station like "%Nairo"'
            mycursor.execute(s)
            w=mycursor.fetchall()
            print('\nBoarding Station, Landing Station, Takeoff Time, Fly Time\n')
            for j in w:
                print('\n',j)
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.destination=passdetails.destination')
            mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.board=passdetails.board')
            sml='select custname,board,destination from pdata'
            mycursor.execute(sml)
            p=mycursor.fetchall()
            print('\nName, Boarding Station, Landing Station\n')
            for b in p:
                print('\n',b)            
    elif a=='Australia,Sydney':
        s='select*from travloc where l_station like "%Sydney"'
        mycursor.execute(s)
        w=mycursor.fetchall()
        print('\nBoarding Station, Landing Station, Takeoff Time, Fly Time\n')
        for j in w:
            print('\n',j)
        mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.destination=passdetails.destination')
        mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.board=passdetails.board')
        sml='select custname,board,destination from pdata'
        mycursor.execute(sml)
        p=mycursor.fetchall()
        print('\nName, Boarding Station, Landing Station\n')
        for b in p:
            print('\n',b)
    elif a=='Japan,Nairo':
        s='select*from travloc where l_station like "%Nairo"'
        mycursor.execute(s)
        w=mycursor.fetchall()
        print('\nBoarding Station, Landing Station, Takeoff Time, Fly Time\n')
        for j in w:
            print('\n',j)
        mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.destination=passdetails.destination')
        mycursor.execute('update pdata inner join passdetails on pdata.custname=passdetails.name set pdata.board=passdetails.board')
        sml='select custname,board,destination from pdata'
        mycursor.execute(sml)
        p=mycursor.fetchall()
        print('\nName, Boarding Station, Landing Station\n')
        for b in p:
            print('\n',b)
    elif a=='x':
        exit()
    else:
        print('Sorry! That Destination is not Available')
    return p

def classtypeview():
    ch=int(input('Enter 1 to see seats available or not:'))
    if ch==1:
        sql='select * from pdata'
        mycursor.execute(sql)
        rows=mycursor.fetchall()
        for x in rows:
            print(x)
        if len(rows) < 200:
            a=(200-len(rows)+1)
            print('There are',a,'seats available!')
        else:
            b=(200-len(rows))
            print('sorry! no more seats available',b,'left')

mycursor.execute('create table ticketprice(name varchar(40) primary key,rate int,Class char(20))')

def ticketprice():
    global prows
    a=[]
    print('We have the following rooms for you:-\n')
    print('1. type First class--->rs 6000 PN\-')
    print('2. type Business class--->rs 4000 PN\-')
    print('3. type Economy class--->rs 2000 PN\-\n')
    x=int(input('Enter your choice:'))
    r=input('Enter Your Name:')
    a.append(r)
    if x==1:
        print('you have opted First class.\n')
        s=6000
        a.append(s)
        b='First class'
        a.append(b)
        z=(a)
        sql='insert into ticketprice(name,rate,class) values(%s,%s,%s)'
        mycursor.execute(sql,z)
        sq='select*from ticketprice'
        mycursor.execute(sq)
        rows=mycursor.fetchall()                         
        mycursor.execute('alter table pdata add column rate int')
        mycursor.execute('alter table pdata add column class char(20)')
        mycursor.execute('update pdata inner join ticketprice on pdata.custname=ticketprice.name set pdata.rate=ticketprice.rate')
        mycursor.execute('update pdata inner join ticketprice on pdata.custname=ticketprice.name set pdata.class=ticketprice.class')
        msql='select custname,rate,class from pdata'
        mycursor.execute(msql)
        prows=mycursor.fetchall()
        mydb.commit()
        for p in prows:
            print('Name , Rate , Class\n')
            print(p)
    elif x==2:
        print('you have opted Business class.\n')
        s=4000
        a.append(s)
        c='Business class'
        a.append(c)
        x=(a)
        sql='insert into ticketprice(name,rate,class) values(%s,%s,%s)'
        mycursor.execute(sql,x)
        sq='select*from ticketprice'
        mycursor.execute(sq)
        rows=mycursor.fetchall()                         
        mycursor.execute('alter table pdata add column class char(20)')
        mycursor.execute('alter table pdata add column rate int')
        mycursor.execute('update pdata inner join ticketprice on pdata.custname=ticketprice.name set pdata.rate=ticketprice.rate')
        mycursor.execute('update pdata inner join ticketprice on pdata.custname=ticketprice.name set pdata.class=ticketprice.class')
        msql='select custname,rate,class from pdata'
        mycursor.execute(msql)
        prows=mycursor.fetchall()
        mydb.commit()
        for p in prows:
            print('Name , Rate , Class\n')
            print(p)
    elif x==3:
        print('you have opted Economy class.\n')
        s=2000
        a.append(s)
        d='Economy class'
        a.append(d)
        y=(a)
        sql='insert into ticketprice(name,rate,class) values(%s,%s,%s)'
        mycursor.execute(sql,y)
        sq='select*from ticketprice'
        mycursor.execute(sq)
        rows=mycursor.fetchall()                         
        mycursor.execute('alter table pdata add column class char(20)')
        mycursor.execute('alter table pdata add column rate int')
        mycursor.execute('update pdata inner join ticketprice on pdata.custname=ticketprice.name set pdata.rate=ticketprice.rate')
        mycursor.execute('update pdata inner join ticketprice on pdata.custname=ticketprice.name set pdata.class=ticketprice.class')
        msql='select custname,rate,class from pdata'
        mycursor.execute(msql)
        prows=mycursor.fetchall()
        mydb.commit()
        for p in prows:
            print('Name , Rate , Class\n')
            print(p)
    else:
        print('Please select a class type.')
    print('\nyour room rent is = Rs.',s,'/-\n')
    return prows

mycursor.execute('create table food(available varchar(70),cost char(10))')
query2='insert into food values(%s,%s)'
da=[('1.  Tea and Noodles','70/-'),
    ('2.  Coffee and Pasta','80/-'),
    ('3.  Colddrink and Noodles','90/-'),
    ('4.  Samosa and Coffee','40/-'),
    ('5.  Sandwich and Pasta','90/-'),
    ('6.  Popcorn and Pasta','70/-'),
    ('7.  Icecream and Noodles','80/-'),
    ('8.  Milk and Cake','60/-'),
    ('9.  Noodles and Cake','50/-'),
    ('10. Pasta and Tea','50/-'),
    ('11. Burger and Colddrink','40/-'),
    ('12. Cake and Colddrink','50/-'),
    ('13. Chocolate , Icecream and Pasta','120/-')]
mycursor.executemany(query2,da)

mycursor.execute('create table custfood(name varchar(80) primary key,bill int)')            

def orderitem():
    print('HOME MADE FOODS ARE NOT ALLOWED TO BRING INTO AN AIRPLANE!')
    ch=int(input('Do you want to order food? Enter 1 for Yes and 2 for No:'))
    if ch==1:
        m=[]
        sql='select * from food'
        mycursor.execute(sql)
        rows=mycursor.fetchall()
        for x in rows:
            print(x)
        c=input('Please Enter your Name Here:')
        m.append(c)            
        print('What do you want to purchase from above list? Enter your choice.')
        d=int(input('Your choice:'))
        if d==1:
            print('You have ordered Tea and Noodles.')
            a=int(input('Enter quantity:'))
            s=70*a
            print('Your amount for Tea and Noodles is: Rs.',s,'\n')
            m.append(s)
        elif d==2:
            print('You have ordered Coffee and Pasta.')
            a=int(input('Enter quantity:'))
            s=80*a
            print('Your amount for Coffee and Pasta is: Rs.',s,'\n')
            m.append(s)
        elif d==3:
            print('You have ordered Colddrink and Noodles.')
            a=int(input('Enter quantity:'))
            s=90*a
            print('Your amount for Colddrink and Noodles is: Rs.',s,'\n')
            m.append(s)
        elif d==4:
            print('You have ordered Samosa and Coffee.')
            a=int(input('Enter quantity:'))
            s=40*a
            print('Your amount for Samosa and Coffee is: Rs.',s,'\n')
            m.append(s)
        elif d==5:
            print('You have ordered Sandwich and Pasta.')
            a=int(input('Enter quantity:'))
            s=90*a
            print('Your amount for Sandwich and Pasta is: Rs.',s,'\n')
            m.append(s)
        elif d==6:
            print('You have ordered Popcorn and Pasta.')
            a=int(input('Enter quantity:'))
            s=70*a
            print('Your amount for Popcorn and Pasta is: Rs.',s,'\n')
            m.append(s)
        elif d==7:
            print('You have ordered Icecream and Noodles.')
            a=int(input('Enter quantity:'))
            s=80*a
            print('Your amount for Icecream and Noodles is: Rs.',s,'\n')
            m.append(s)
        elif d==8:
            print('You have ordered Milk and Cake.')
            a=int(input('Enter quantity:'))
            s=60*a
            print('Your amount for Milk and Cake is: Rs.',s,'\n')
            m.append(s)
        elif d==9:
            print('You have ordered Noodles and Cake.')
            a=int(input('Enter quantity:'))
            s=50*a
            print('Your amount for Noodles and Cake is: Rs.',s,'\n')
            m.append(s)
        elif d==10:
            print('You have ordered Pasta and Tea.')
            a=int(input('Enter quantity:'))
            s=50*a
            print('Your amount for Pasta and Tea is: Rs.',s,'\n')
            m.append(s)
        elif d==11:
            print('You have ordered Burger and Colddrink.')
            a=int(input('Enter quantity:'))
            s=40*a
            print('Your amount for Burger and Colddrink is: Rs.',s,'\n')
            m.append(s)
        elif d==12:
            print('You have ordered Cake and Colddrink.')
            a=int(input('Enter quantity:'))
            s=50*a
            print('Your amount for Cake and Colddrink is: Rs.',s,'\n')
            m.append(s)
        elif d==13:
            print('You have ordered Chocolate , Icecream and Pasta.')
            a=int(input('Enter quantity:'))
            s=120*a
            print('Your amount for Chocolate , Icecream and Pasta is: Rs.',s,'\n')
            m.append(s)
        else:
            print('Please enter your choice from the menu.')
        n=(m)
        sql='insert into custfood(name,bill) values(%s,%s)'
        mycursor.execute(sql,n)
        mydb.commit()
        mycursor.execute('alter table pdata add column foodbill int default null')
        mycursor.execute('update pdata inner join custfood on pdata.custname=custfood.name set pdata.foodbill=custfood.bill')
        e='select custname,foodbill from pdata'
        mycursor.execute(e)
        f=mycursor.fetchall()
        mydb.commit()
        for y in f:
            print('Name , Foodbill\n')
            print(y)
    elif ch==2:
        mycursor.execute('alter table pdata add column foodbill int default null')
        
mycursor.execute('create table luggage(name varchar(50) primary key,luggagebill int default null)')

def luggagebill():
    
    global brows
    b=[]
    print()
    print('First 25KG is Free , you have to pay for extra luggage\n')
    print('It will be Rs. 100/- for 1KG\n')
    print('Do you want to see rate for luggage?')
    ch=int(input('Enter 1 for Yes or 2 for No:'))
    if ch==1:
        c=input('Enter Your Name Please:')
        b.append(c)
        y=int(input('Enter your weight,of extra luggage:'))
        z=y*100
        print('Your Luggage bill:',z,'/-\n')
        b.append(z)
        c=(b)
        sql='insert into luggage(name,luggagebill) values(%s,%s)'
        mycursor.execute(sql,c)
        mycursor.execute('alter table pdata add column luggagebill int default null')
        mycursor.execute('update pdata inner join luggage on pdata.custname=luggage.name set pdata.luggagebill=luggage.luggagebill')
        sw='select custname,luggagebill from pdata'
        mycursor.execute(sw)
        brows=mycursor.fetchall()
        mydb.commit()
        for x in brows:
            print('Name  ,  Luggage Bill')
            print(x)
    elif ch==2:
        mycursor.execute('alter table pdata add column luggagebill int default null')
        return

def ticketamount():
    a=input('Enter Your Name:')
    print('Your Luggage bill:')
    sql='select luggagebill from pdata'
    mycursor.execute(sql)
    r=mycursor.fetchall()
    for i in r:
        print('Rs',i,'/-')
    print('Your Food bill:')
    sq='select foodbill from pdata'
    mycursor.execute(sq)
    p=mycursor.fetchall()
    for j in p:
        print('Rs',j,'/-')    
    print('Your Ticket Amount:')
    s='select rate from pdata'
    mycursor.execute(s)
    q=mycursor.fetchall()
    for k in q:
        print('Rs',k,'/-')
    print('\nYOU HAVE SUCCESSFULLY COMPLETED THE RESERVATION')
    print('\nPLEASE RECEIVE YOUR TICKET FROM THE AIRPORT , THANK YOU')

def Menuset():
    print('Enter 1: To Enter Customer Data.')
    print('Enter 2: To Enter Your Boarding Station And Destination.')
    print('Enter 3: To View Seat Availability.')
    print('Enter 4: For Class Type.')
    print('Enter 5: For Food Bill.')
    print('Enter 6: For Luggage Bill.')
    print('Enter 7: For Complete Amount.')
    print('Enter 8: Exit.')
    

    userinput=int(input('\nEnter your choice:'))
    if userinput==1:
        registercust()
    elif userinput==2:
        location()
    elif userinput==3:
        classtypeview()
    elif userinput==4:
        ticketprice()
    elif userinput==5:
        orderitem()
    elif userinput==6:
        luggagebill()
    elif userinput==7:
        ticketamount()
    elif userinput==8:
        quit()
    else:
        print('Enter correct choice.')

Menuset()
def runagain():
    runagn=input('\nPlease Enter 1 to Fill other Details or 0 to Exit:')
    while runagn=='1':
        if platform.system=='windows':
            print(os.system('cls'))
        else:
            print(os.system('clear'))
        Menuset()
        runagn=input('\nPlease Enter 1 to Fill other Details or 0 to Exit:')
runagain()

#SEAT NUMBER
#REMOVE DROP TABLE PDATA TO SAVE DATAS
