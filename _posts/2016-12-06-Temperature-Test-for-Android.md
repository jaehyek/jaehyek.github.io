---
layout: post
title:  "Temperature Test for Android"
categories: Qt
comments: true
tags:  Qt Python Temperature Test Android
author: Jaehyek
---
## Descriptions of how to setup the Qt5 and  how to make scripts

### 1. download and install the "Qt 5.7.0 for Windows 64-bit (VS 2015, 918 MB)" 
please refer to here [here](https://www.qt.io/download-open-source/#section-2)

### 2. install the pyserial 
Anaconda python 3.5  will have it already. 

### 3. install the PyQt5 like below
```
C:\>pip install PyQt5
Collecting PyQt5
  Downloading PyQt5-5.7-cp35-none-win_amd64.whl (68.1MB)
    100% |################################| 68.1MB 13kB/s
Collecting sip (from PyQt5)
  Downloading sip-4.18.1-cp35-none-win_amd64.whl (46kB)
    100% |################################| 51kB 1.7MB/s
Installing collected packages: sip, PyQt5
Successfully installed PyQt5-5.7 sip-4.18.1
``` 

please refer to [PyQt5 Reference Guide](http://pyqt.sourceforge.net/Docs/PyQt5/)

### 4. create the UI file of Qt5 using Qt Creator  like below imaage.

![QtUI](/img/Qt/QtUI.jpg)

### 5. Qt programming for Android Phone Temperature Test 

** import and  _main__ **

```
from PyQt5.QtWidgets import QDialog, QMessageBox
from PyQt5.QtWidgets import QApplication, QWidget
from PyQt5.QtCore import *
import matplotlib.pyplot as plt

if __name__ == "__main__":
    app = QApplication(sys.argv)
    myapp = GUIForm()
    myapp.show()
    app.exec()
    #sys.exit(app.exec_())
    myapp.Update_data()
```

** GUIForm class, QThread, QTimer **

```
class GUIForm(QDialog):
    def __init__(self, parent=None):
        QWidget.__init__(self,parent)
        self.ui = Ui_Dialog()
        self.ui.setupUi(self)
        self.first_draw_flag = False
        
        self.path_battery_temp = "/sys/class/power_supply/battery/temp"
        self.path_cpu_temp     = "/sys/class/thermal/thermal_zone12/temp"
        self.path_battery_capacity = "/sys/class/power_supply/battery/capacity"
        
        self.art_script_thread = QThread()
        self.get_temp_thread = QThread()     
           
        self.myTimer1 = QTimer()
        self.myTimer2 = QTimer()
        self.myTimer3 = QTimer()
        self.myTimer4 = QTimer()           
```

### Final. run the Python scripts.  Below is the working screen .

![QtTempTest](/img/Qt/QtTempTest.jpg)

