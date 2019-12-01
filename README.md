# nealrycompleteproject
from tkinter import *
import pymongo
from  tkinter import colorchooser
root =Tk()
n = StringVar()
a= StringVar()
q=StringVar()
nu=IntVar()
g=StringVar()
d1= StringVar()
d2=StringVar()
u1=StringVar()
u2=StringVar()
crt1=StringVar()
crt2=StringVar()
def create():
    uri = "mongodb://127.0.0.1:27017"
    connection = pymongo.MongoClient(uri)
    database = connection['glau']
    collection = database['student1']
    data = {"age":23}
    collection.insert_one(data)
def insert():
    uri = "mongodb://127.0.0.1:27017"
    connection = pymongo.MongoClient(uri)
    database = connection['glau']
    collection = database['student1']
    data = [
        {"name":n.get()},
        {"address":a.get()},
        {"qualification":q.get()},
        {"number":nu.get()},
        {"gender":g.get()}

    ]
    collection.insert_many(data)
def change_color():
    clr=colorchooser.askcolor()
    root.configure(background=clr[1])




def fetch():
    top=Toplevel()
    top.geometry('600x600')
    top.title("fetch the data")
    text=Text(top,font=10)
    text.pack(fill=BOTH,expand=1)


    uri = "mongodb://127.0.0.1:27017"
    connection = pymongo.MongoClient(uri)
    database = connection['glau']
    collection = database['student1']
    x = collection.find()
    for i in x:
        text.insert(INSERT,i)

def dele():
    uri = "mongodb://127.0.0.1:27017"
    connection = pymongo.MongoClient(uri)
    database = connection['glau']
    collection = database['student1']
    my={d1.get():d2.get()}
    mydoc = collection.delete_one(my)
def updat():
    uri = "mongodb://127.0.0.1:27017"
    connection = pymongo.MongoClient(uri)
    database = connection['glau']
    collection = database['student1']
    oldquery= {d1.get():d2.get()}
    newquery={"$set":{u1.get():u2.get()}}
    collection.update_one(oldquery,newquery)
def drop_c():
    uri = "mongodb://127.0.0.1:27017"
    connection = pymongo.MongoClient(uri)
    database = connection['glu']
    collection = database['student1']
    collection.drop()









name = Label(root ,text="Name",bg="white",font = 20,bd=4,fg="green")
name.grid(row = 0,column= 0)
namee=Entry(root,font=10,bg="white",textvariable=n)
namee.grid(row=0,column=3)


#address of the person
addr = Label(root ,text="Address",bg="white",font = 20,bd=4,fg="green")
addr.grid(row = 1,column= 0)
addre = Entry(root,font=20,bg="white",textvariable=a)
addre.grid(row=1,column=3)



#qualification
quali = Label(root ,text="Qualification",bg="white",font = 20,bd=4,fg="red")
quali.grid(row = 2,column= 0)
qualie = Entry(root,font=20,bg="white",textvariable=q)
qualie.grid(row=2,column=3)

#number of the person
number = Label(root ,text="Mobile Number",bg="white",font = 20,bd=4,fg="red")
number.grid(row = 3,column= 0)
numbere = Entry(root,font=20,bg="white",textvariable=nu)
numbere.grid(row=3,column=3)


#gender of the person
gender = Label(root ,text="gender",bg="white",font = 20,bd=4,fg="red")
gender.grid(row = 4,column= 0)
gendere = Entry(root,font=20,bg="white",textvariable=g)
gendere.grid(row=4,column=3)


#change color
bt= Button(root,text="change color",font=10,command=change_color)
bt.grid(row=7,column=0)

#insert button
ins = Button(root,text="insert",font=10,activebackground="yellow",
activeforeground="red",command=insert)
ins.grid(row=7,column=2)


#create the database
cr = Button(root,text="create",font=10,activebackground="yellow",
activeforeground="red",command=create)
cr.grid(row=8,column=0)

c1=Entry(root,font=10,bg="white",textvariable=crt1)
c1.grid(row=8,column=3)
c2=Entry(root,font=10,bg="white",textvariable=crt2)
c2.grid(row=9,column=3)
databa = Label(root ,text="database",bg="white",font = 20,bd=4,fg="green")
databa.grid(row = 8,column= 4)
collec = Label(root ,text="collectiion",bg="white",font = 20,bd=4,fg="green")
collec.grid(row = 9,column= 4)


#delete the cllection
de= Button(root,text="delete",font=10,activebackground="yellow",activeforeground="red",command=dele)
de.grid(row=10,column=0)
de1= Entry(root,font=10,textvariable=d1)
de1.grid(row=10,column=3)
de2= Entry(root,font=10,textvariable=d2)
de2.grid(row=11,column=3)
ke1 = Label(root ,text="key",bg="white",font = 20,bd=4,fg="green")
ke1.grid(row = 10,column= 4)
ke2 = Label(root ,text="value",bg="white",font = 20,bd=4,fg="green")
ke2.grid(row = 11,column= 4)


#fetch the data
fet = Button(root,text="fetch",font=10,activebackground="yellow",
activeforeground="red",command=fetch)
fet.grid(row=7,column=5)

root.title("Ragitrationform")


#update the collection
upd = Button(root,text="update",font=10,activebackground="yellow",
activeforeground="red",command=updat)
upd.grid(row=12,column=0)
upe = Entry(root,font=20,bg="white",textvariable=u1)
upe.grid(row=12,column=3)
upe1 = Entry(root,font=20,bg="white",textvariable=u2)
upe1.grid(row=13,column=3)
ke1 = Label(root ,text="ukey",bg="white",font = 20,bd=4,fg="green")
ke1.grid(row = 12,column= 4)
ke2 = Label(root ,text="uvalue",bg="white",font = 20,bd=4,fg="green")
ke2.grid(row = 13,column= 4)


#drop the collection
drp = Button(root,text="dropcollection",font=10,activebackground="yellow",
activeforeground="red",command=drop_c)
drp.grid(row=14,column=0)

#drop the database
drp = Button(root,text="dropdatabse",font=10,activebackground="yellow",
activeforeground="red")
drp.grid(row=15,column=0)
root.geometry('600x600')
root.mainloop()
