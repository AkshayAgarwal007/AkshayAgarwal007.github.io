---
title:  "Basics of App Development with Python - I"
date:   2016-06-23 12:58:00
description: App Development Python
---

In this article we will be focusing on basics of App Development with Python. We'll be making use of the PyQt5 library for the same. I often find people struggle with making GUI apps and it's because they straight away start with some advanced stuff. This article is apt to get you started if you're a beginner.

### What is PyQt5?

PyQt5 is a set of Python Bindings for the cross platform application framework Qt (pronounced /ˈkjuːt/ "cute", or unofficially as Q-T cue-tee). Qt is currently being developed by the Qt Company and the Qt Project whereas PyQt5 is developed by Riverbank Computing. 
Some notable applications that use PyQt5 are Anki, Dropbox, Spyder, Puddletag etc.

Apart from PyQt5 some other modules that are used for GUI development using Python are PySide, Tkinter, wxPython, PyGTK etc. 

Note that "PySide was released by Nokia in 2009 after they failed to reach an agreement with PyQt developers to change its licensing terms to include LGPL as an alternative license." as qouted from *Wikipedia*. Both are bindings of the same Qt library and are almost similar in features with a few unimportant differences.

### Installing PyQt5

The easiest way to download PyQt5 is by using the [installer](https://riverbankcomputing.com/software/pyqt/download5). I will recommend you to have Python 3.5 installed. The installer will automatically add all the PyQt5 extras to the Python installation automatically. Note that choose the 64-bit installer or 32-bit installer depending on whether you have a 64-bit or a 32-bit version of Python installed.

If you're a Linux user, installing PyQt5 should be a very straight forward process for you. If facing any problems, you can go through a few references online and you'll easily have it downloaded. But, installing packages is always a menace on Windows. So if you are facing any issues with installing PyQt5 on Windows, I will advice you to use [WinPython](https://winpython.github.io/). It's a portable distribution of the Python programming language containing many 3rd party packages such as IPython, Spyder and PyQt itself. It's clean and won't mess around with anything that's already installed.

### Let's Write Some Code
Let's have a look at *main.py*, your first program using PyQt5.

{% highlight python %}
import sys
from PyQt5.QtWidgets import QApplication, QWidget


if __name__ == '__main__':
    
    qApp =   QApplication( )
    
    w = QWidget()
    w.resize(640, 360)
    w.move(500, 500)
    w.setWindowTitle('My First Program')
    w.show()
    
    sys.exit(qApp.exec_())
{% endhighlight %}

Create a folder named *tuts* inside your WinPython folder and save the above program as *main.py* there. Open the command prompt from within the WinPython folder. CD into the tuts folder. Then run the program.
{% highlight cmd %}
> python main.py
{% endhighlight %}

 Following will be the output of the program.   

![Output Window](../../assets/images/ss1.png)

Woah! We have an application window ready with merely some 10 lines of code. You can play around with the window, resize it, maximise it, minimise it, this is the power of PyQt5. Now let's understand the code line by line.

{% highlight python %}

import sys
from PyQt5.QtWidgets import QApplication, QWidget

{% endhighlight %}

Initially we import do all the necessary imports.  The sys module provides a number of functions and variables that can be used to manipulate different parts of the Python runtime environment. The basic widgets are located in the PyQt5.QtWidgets module.

{% highlight python %}

if __name__ == '__main__':

{% endhighlight %}

`'__main__'` is the name of the scope in which top-level code executes. A module's `__name__`   is set equal to `'__main__'`, if the python interpreter is running the module as the main program. If the module is being imported from another module, `__name__` will be se to the module's name. With the above code, everything you put inside the *if* block will execute only when you're running it as the primary module.

{% highlight python %}

qApp =  QApplication(sys.argv)

{% endhighlight %}

Here we create a QApplication object. Every PyQt5 application must have a QApplication object. The QApplication class manages the GUI application's control flow and main settings. Moreover there is only one QApplication object for any GUI application using Qt no matter how many window are there at an instant. It also provides the event loop. It must be created before any objects related to the user interface are created. The sys.argv list contains the arguments passed from the command line and is required sine Qt can be configured from the command line. 

{% highlight python %}

w = QWidget()

{% endhighlight %}

The QWidget class is the base class for all user interfaces objects in PyQt5. We create an object w of the QWidget class by calling its default constructor. The default constructor has no parent and the widget with no parent is called a window.

{% highlight python %}

w.resize(640, 360)

{% endhighlight %}

Then we resize the window to an height of 640px and a width of 360px by using the resize() method.

{% highlight python %}

w.move(500, 500)

{% endhighlight %}

Then we move the entire window to a position on the screen 500px from the left and 500px from the top.

{% highlight python %}

w.setWindowTitle('My First Program')

{% endhighlight %}

Here we set the title of the window which is displayed on the titlebar.

{% highlight python %}

w.show()

{% endhighlight %}

When we create a QWidget object a widget is created in the memory and nothing is displayed on the screen. In order to display the widget on the screen the show() method is used. Try running the program by commenting out the above line of code and you'll be surprises to see that the program executes successfully but nothing is displayed. Quite interesting isn't it?

{% highlight python %}

sys.exit(qApp.exec_())

{% endhighlight %}

Finally we start the event loop by calling qApp.exec_(). Event handling starts here. An event is generated when the user interacts (key presses or mouse clicks) with the application or can be generated by the system (timers) and gets added to the queue. The event loop continuously checks for events and passes it to the event's associated method for processing. The event loop is destroyed when the exit() method is called or the main widget is destroyed. The sys.exit() ensures a clean exit and the environment is informed how the application ended.

Note that the exec_() method has an underscore and that is because exec is a reserved keyword and hence cannot be used.  

The event loop is the heart of every GUI application and that is what makes it different from traditional batch processing programs.

![Diagram](../../assets/images/diagram.png)

Now let's look at the same code with an object oriented approach.

{% highlight python %}

import sys
from PyQt5.QtWidgets import QApplication, QWidget

class OOWidget(QWidget):
    
    def __init__(self):
        super().__init__()
        
        self.initUI()
        
        
    def initUI(self):
        
        self.setGeometry(300, 300, 300, 220)
        self.setWindowTitle('Object Oriented Approach')       
    
        self.show()
        
        
if __name__ == '__main__':
    
    qApp = QApplication(sys.argv)
    w = OOWidget()
    sys.exit(qApp.exec_())  

{% endhighlight %}

Now let's try to understand the difference from the previous one

{% highlight python %}

class OOWidget(QWidget):
    
    def __init__(self):
        super().__init__()
        
{% endhighlight %}

Here we create a class OOWidget that inherits from the QWidget class.  `__init__` is a constructor method in Python. So we are calling two constructors, one for the OOWidget class and the other for the QWidget class. super() returns a proxy object to handle the delegated call to `__init__` i.e calling the constructor of the parent class.

{% highlight python %}

self.initUI()
        
{% endhighlight %}

It's a user defined function inside which we'll place the code to create the GUI interface.

{% highlight python %}

self.setGeometry(300, 300, 300, 220)

{% endhighlight %}

The first two arguments to the setGeometry() method are the x and y positions of the window. The third and fourth arguments are the width and height of the window respectively.

{% highlight python %}

if __name__ == '__main__':
    
    qApp = QApplication(sys.argv)
    w = OOWidget()
    sys.exit(qApp.exec_())

{% endhighlight %}


Then we create application object and the OOWidget object and begin the event loop by calling qApp.exec_().

### Centering the Window on the Screen

{% highlight python %}

import sys
from PyQt5.QtWidgets import QWidget, QDesktopWidget, QApplication


class centerWidget(QWidget):
    
    def __init__(self):
        super().__init__()
        
        self.initUI()
        
        
    def initUI(self):               
        
        self.resize(640, 360)
        self.center()
        self.setWindowTitle('Centered Window')    
        self.show()
        
        
    def center(self):
        
        fg = self.frameGeometry()
        cp = QDesktopWidget().availableGeometry().center()
        fg.moveCenter(cp)
        self.move(fg.topLeft())
        
        
if __name__ == '__main__':
    
    qApp =  QApplication(sys.argv)
    w = centerWidget()
    sys.exit(qApp.exec_())  
    
{% endhighlight %}

Now let's understand the code line by line. 

{% highlight python %}

import sys
from PyQt5.QtWidgets import QWidget, QDesktopWidget, QApplication

{% endhighlight %}



Firstly we make the necessary import as always. Here we import the QDesktopWdiget class that provides information about the user's desktop such as its total size, geometry of screen etc. 

{% highlight python %}

self.center()

{% endhighlight %}

Now we  define a custom method center() inside which we'll place the code for centering the windows on the screen.

{% highlight python %}

fg = self.frameGeometry()

{% endhighlight %}

![geometry](../../assets/images/geometry.png)

Here we get the geometry of the main window including any window frame using the frameGeometry() method.

{% highlight python %}

cp = QDesktopWidget().availableGeometry().center()

{% endhighlight %}

Now we fetch the available geometry of the screen. What is available depends upon the platform (for example it excludes the dock and menu bar on OS X, or the task bar on Windows)

{% highlight python %}

fg.moveCenter(cp)

{% endhighlight %}

We already have a rectangle specifying the geometry of the main window. Using the moveCenter() method we set the center of the main window as the center of the screen.

{% highlight python %}

self.move(fg.topLeft())

{% endhighlight %}

Now we move the top-left point of main window to the top-left point of the rectangle specifying the geometry of the main window using the move method. Note that this works because move() is an overloaded fuction that can be called with either a pair of integers or PyQt5.QtCore.QPoint object as an argument.
    
This is all I wanted to cover in this article. This is the first article from the series **Basics of App Development with Python**. If you liked the article and are interested in App development with Python please subscribe to the blog and stay tuned for the upcoming articles.