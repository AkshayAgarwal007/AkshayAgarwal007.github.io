---
title:  "Layout Management in PyQt5"
date:   2016-07-01 12:58:00
description: Layout Management PyQt5
---



Layout Management is an important aspect of App Development. It deals with how various widgets are placed in the application window. There are two ways we can do it, either by using absolute positioning or using layout classes. 

#### Absolute Positioning

In absolute positioning the programmer specifies the size and position of the widgets in pixels. This is the most basic way of doing layout management but is not often used as the application looks different in different platforms and the position of the widgets remains static as we resize the window. Simply, it's not flexible.

{% highlight python %}

import sys
from PyQt5.QtWidgets import QWidget, QLabel, QApplication


class Layout(QWidget):
    
    def __init__(self):
        super().__init__()
        
        self.initUI()
        
        
    def initUI(self):
        
        lbl1 = QLabel('200px from left and 180px from top', self)
        lbl1.move(200, 180)      
        
        self.setGeometry(200, 200, 640, 360)
        self.setWindowTitle('Absolute Positioning')    
        self.show()
        
        
if __name__ == '__main__':
    
    app = QApplication(sys.argv)
    lt = Layout()
    sys.exit(qApp.exec_())
    
    
{% endhighlight %}

Following will be the output of the program. 

![Absolute Positioning](../../assets/images/ss2.png)

Whoa! it's successfully placed at the center vertically. But wait, try to resize the window. Now you can clearly see one of the demerits of absolute positioning, the position of the widgets remains static as you resize the window which is something you would not want in a GUI application.

Now let's understand the code. I'll explain you only those lines which are new or have something do with layout management. For understanding the rest of the code please check my article on [App Development with Python - I](#).

{% highlight python %}
lbl1 = QLabel('200px from left and 180px from top', self)
{% endhighlight %}

Here we create a QLabel object. It's simply a label that provides a text or image display.

{% highlight python %}
lbl1.move(200, 180) 
{% endhighlight %}


The move() function is used for absolute positioning. It takes the x and y coordinates of where you want to place the widget as arguments. The top left corner of the window is assigned a coordinate of (0,0). We try to place the label in the center vertically. Let's do some maths for the same. Since the height of the window is 360px, placing the label at the center vertically is same as placing it at the coordinate (x,360/2=180). So in order to place the label at the coordinate (200,180) we pass the same x and y positions inside the move() function. We do the same in the code below.


#### Box Layout

Box layout is a flexible way of doing layout management and is generally used. The QHBoxLayout and QVBoxLayout are layout classes used to align the widgets vertically and horizontally.

{% highlight python %}

import sys
from PyQt5.QtWidgets import (QWidget, QPushButton, QLabel, QHBoxLayout, QVBoxLayout, QApplication)


class Layout(QWidget):
    
    def __init__(self):
        super().__init__()
        
        self.initUI()
        
        
    def initUI(self):
        
        lbl = QLabel("Try to Resize and See the Magic")

        hbox = QHBoxLayout()
        hbox.addStretch(1)
        hbox.addWidget(lbl)
        hbox.addStretch(1)

        vbox = QVBoxLayout()
        vbox.addStretch(1)
        vbox.addLayout(hbox)
        vbox.addStretch(1)
        
        self.setLayout(vbox)    
        
        self.setGeometry(200, 200, 640, 360)
        self.setWindowTitle('Box Layout')    
        self.show()
        
        
if __name__ == '__main__':
    
    app = QApplication(sys.argv)
    lt = Layout()
    sys.exit(qApp.exec_())
        
{% endhighlight %}

Following will be the output of the program. 

![Box Layout](../../assets/images/ss3.png)

Let's try to understand what's happening in the code.

{% highlight python %}
lbl = QLabel("Try to Resize and See the Magic")
{% endhighlight %}


Again we create a QLabel object lbl (a label).

{% highlight python %}
hbox = QHBoxLayout()
hbox.addStretch(1)
hbox.addWidget(lbl)
hbox.addStretch(1)
{% endhighlight %}

Here we create a Horizontal Box Layout (hbox) and add a stretch factor and the label to it. The stretch factor adds a stretchable space before and after the label which adjusts itself depending upon the size of the window.

{% highlight python %}
vbox = QVBoxLayout()
vbox.addStretch(1)
vbox.addLayout(hbox)
vbox.addStretch(1)

self.setLayout(vbox)  
{% endhighlight %}

We create a Vertical Box Layout and put the hbox inside it. Here also we add a stretch factor similar to what we did in case of the horizontal layout in order to keep the horizontal box vertically at the center. 

{% highlight python %}
self.setLayout(vbox)  
{% endhighlight %}

Lastly using the setLayout() method we set the layout of the window by passing the vertical box as an argument.  



#### GridLayout 

Grid layout takes the space made available to it, divides it up into rows and columns, and puts each widget it manages into the correct cell. Let's try to understand it with the help of a simple example of a login form.

{% highlight python %}

import sys
from PyQt5.QtWidgets import (QWidget, QLabel, QLineEdit, QGridLayout, QApplication, QPushButton)


class loginForm(QWidget):
    
    def __init__(self):
        super().__init__()
        
        self.initUI()
        
        
    def initUI(self):
        
        uname = QLabel('Enter Your Username')
        passwd = QLabel('Enter Your Password')

        unameEdit = QLineEdit()
        passwdEdit = QLineEdit()
        passwdEdit.setEchoMode(QLineEdit.PasswordEchoOnEdit)
        
        btn = QPushButton('Submit')

        grid = QGridLayout()
        grid.setSpacing(20)

        grid.addWidget(uname, 1, 0)
        grid.addWidget(unameEdit, 1, 1)

        grid.addWidget(passwd, 2, 0)
        grid.addWidget(passwdEdit, 2, 1)

        grid.addWidget(btn, 3, 0, 1, 2)
        
        self.setLayout(grid) 
        
        self.setGeometry(300, 300, 350, 300)
        self.setWindowTitle('Login Form')    
        self.show()
        
        
if __name__ == '__main__':
    
    qApp = QApplication(sys.argv)
    w = loginForm()
    sys.exit(qApp.exec_())
{% endhighlight %}

Following will be the output of the program.

![Login Form](../../assets/images/login.png)

Let's try to understand he code.

{% highlight python %}
uname = QLabel('Enter Your Username')
passwd = QLabel('Enter Your Password')
{% endhighlight %}

Firstly we create two labels uname and passwd.

{% highlight python %}
unameEdit = QLineEdit()
passwdEdit = QLineEdit()
passwdEdit.setEchoMode(QLineEdit.Password)
btn = QPushButton('Submit')
{% endhighlight %}

Here we create two QLineEdit objects. A line edit allows the user to enter and edit a single line of plain text. Then we call the setEchoMode() method. The setEchoMode() method is used to determine how the text entered in the line edit is displayed to the user. We provide it with QLineEdit.Password which is an enum constant as an argument. QLineEdit.Password  is used if you want to display asterisks instead of the characters actually entered. FInally we create a button. The QPushButton class is used to create buttons.

{% highlight python %}
grid = QGridLayout()
grid.setSpacing(20)
{% endhighlight %}

We create a grid layout and add the spacing between the widgets in the layout to 20px.

{% highlight python %}
grid.addWidget(uname,0, 0)
grid.addWidget(unameEdit, 0, 1)

grid.addWidget(passwd, 1, 0)
grid.addWidget(passwdEdit, 1, 1)

grid.addWidget(btn, 3, 0, 1, 2)
{% endhighlight %}

Now we start adding the widgets to the grid layout using the addWidget() method. The method takes the widget you want to add and the row and column number in order as arguments. We divide the entire layout into a grid of 3*2 cells. We place the labels for username and password at row1, col1 and row2, col1 and the line edits for username and pasword at row1, col2 and row2, col2 respectively. Finally we add the submit button to the third row and make it span 2 columns. Note we can also provide the row and column span as arguments to the addWidget() method.

#### Let's mix them all together

We often need to combine several layout classes together to give our UI components a desired alignment. Below you can see a code for a login form that makes use of both the box layout and the grid layout.

{% highlight python %}

import sys
from PyQt5.QtWidgets import (QWidget, QLabel, QLineEdit, QGridLayout, QApplication, QPushButton, QHBoxLayout, QVBoxLayout)


class loginForm(QWidget):
    
    def __init__(self):
        super().__init__()
        
        self.initUI()
        
        
    def initUI(self):
        
        uname = QLabel('Enter Your Username')
        passwd = QLabel('Enter Your Password')

        unameEdit = QLineEdit()
        passwdEdit = QLineEdit()
        passwdEdit.setEchoMode(QLineEdit.Password)
        
        btn = QPushButton('Submit')

        grid = QGridLayout()
        grid.setSpacing(20)

        grid.addWidget(uname, 0, 0)
        grid.addWidget(unameEdit, 0, 1)

        grid.addWidget(passwd, 1, 0)
        grid.addWidget(passwdEdit, 1, 1)

        hbox1 = QHBoxLayout()
        hbox1.addStretch(1)
        hbox1.addLayout(grid)
        hbox1.addStretch(1)
        
        hbox2 = QHBoxLayout()
        hbox2.addStretch(1)
        hbox2.addWidget(btn)
        hbox2.addStretch(1)
        
        vbox = QVBoxLayout()
        vbox.addStretch(2)
        vbox.addLayout(hbox1)
        vbox.addStretch(1)
        vbox.addLayout(hbox2)
        vbox.addStretch(2)
        
        self.setLayout(vbox) 
        
        self.setGeometry(300, 300, 640, 360)
        self.setWindowTitle('Login Form')    
        self.show()
        
        
if __name__ == '__main__':
    
    qApp = QApplication(sys.argv)
    w = loginForm()
    sys.exit(qApp.exec_())
{% endhighlight %}

Following will be the output of the program.

![Hybrid Login Form](../../assets/images/hybrid.png)

I am not going to make you understand this code. I'm leaving this as an exercise for you. If you face any problems in understanding this, just go through the entire article once again and you'll surely get it.