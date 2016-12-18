---
layout: post
title:  "How to use Qt5"
categories: Qt
comments: true
tags:  Qt Python Temperature Test Android
author: Jaehyek
---

This page will describe a Qt5 programming procedure, and show how to use the Qt5 API 
during making the little project "Temperature Test for Android" 

### 0. Assume that Python 3.5 is already installed at your system. 

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

### 4. create the UI file of Qt5 using Qt Creator  like below image.

![QtUI](/img/2016-12-06-How-to-use-Qt5/QtUI.JPG)

### 5. Qt programming for Android Phone Temperature Test 

**import and  main** 

```
from PyQt5.QtWidgets import QDialog, QMessageBox
from PyQt5.QtWidgets import QApplication, QWidget
from PyQt5.QtCore import *

if __name__ == "__main__":
    app = QApplication(sys.argv)
    myapp = GUIForm()
    myapp.show()
    app.exec()
    #sys.exit(app.exec_())
    myapp.Update_data()
```

**GUIForm class, QThread, QTimer, click.connect**

```
class GUIForm(QDialog):
    def __init__(self, parent=None):
        QWidget.__init__(self,parent)
        self.ui = Ui_Dialog()
        self.ui.setupUi(self)
        self.first_draw_flag = False
        
        # directory name to read temperature
        self.path_battery_temp = "/sys/class/power_supply/battery/temp"
        self.path_cpu_temp     = "/sys/class/thermal/thermal_zone12/temp"
        self.path_battery_capacity = "/sys/class/power_supply/battery/capacity"
        
        self.art_script_thread = QThread()
        self.get_temp_thread = QThread()     
           
        self.myTimer1 = QTimer()
        self.myTimer2 = QTimer()
        self.myTimer3 = QTimer()
        self.myTimer4 = QTimer()

        # bind widgets to relative call-back functions
        self.ui.pushButton_run_1.clicked.connect(self.Run1)
        self.ui.pushButton_run_2.clicked.connect(self.Run2)
        self.ui.pushButton_run_3.clicked.connect(self.Run3)
        self.ui.pushButton_run_4.clicked.connect(self.Run4)
        self.ui.pushButton_copy_script_1.clicked.connect(self.Copy_script_to_Phone1)
        self.ui.pushButton_copy_script_2.clicked.connect(self.Copy_script_to_Phone2)
        self.ui.pushButton_copy_script_3.clicked.connect(self.Copy_script_to_Phone3)
        self.ui.pushButton_copy_script_4.clicked.connect(self.Copy_script_to_Phone4)
        self.ui.pushButton_init_1.clicked.connect(self.Init_Totcnt1)
        self.ui.pushButton_init_2.clicked.connect(self.Init_Totcnt2)
        self.ui.pushButton_init_3.clicked.connect(self.Init_Totcnt3)
        self.ui.pushButton_init_4.clicked.connect(self.Init_Totcnt4)
        self.ui.Ball_Crack.toggled.connect(self.btnstate1)		                   
        
        # load icon to label
        myPixmap = QtGui.QPixmap(os.getcwd() + "/phone.png")
        myScaledPixmap = myPixmap.scaled(self.ui.label_9.size(), Qt.KeepAspectRatio)
        self.ui.label_9.setPixmap(myScaledPixmap)        
```

**font change** 

```
    def btnstate1(self): 
            font = QtGui.QFont()
            font.setBold(True)
```

**clicking the run button and timer call-back functions** 

```
    def Run1(self):
        if self.equipped[0] == False:
            return        
        myInitParams = 0
        timerCallback = functools.partial(self.RunTempTest, myInitParams)

        if self.myTimer1.isActive():
            print("Timer1 Already Active")
            #self.myTimer1.stop()
        else:
            self.myTimer1.timeout.connect(timerCallback)
            self.myTimer1.start(self.periodic_time*1000) 
            
        # thread to run the art scripts
        self.art_script_thread = ART_Scrtipt(self.device[0], "ART_Temp_Test_Script.py")
        self.art_script_thread.start()  
```

**call the plot function triggered by timer** 

```
    def RunTempTest(self,  idx):
        global g_read_temp_flag
            
        if self.test_result[idx] == False:      #  Test Error
            return
        
        if g_read_temp_flag == True:
            self.PlotFunc(idx)
            
        if self.CpuTemp[idx] == 0:
            return 
```

**QThread running for transfer a ART script** 

```
class ART_Scrtipt(QThread):    # Power On/Off Thread
    def __init__(self, device_id,  test_script):
        QThread.__init__(self)
        self.device_id = device_id
        self.test_script = test_script
  
    def run(self):
        timestring = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime())
        str1 = '[' + timestring + ']  ' 
        print("%s Enter Test Script %s  !!!" % (str1,  self.device_id))	
        adbcmd.adbcmd(self.device_id, 'am broadcast -a "com.lge.art.ACTION_START_SCRIPT" --es "files" %s ' %(self.test_script))
        self.quit() 
```

**QThread running for reading temperature from phone** 

```
class Get_Temp_from_Phone(QThread):    # Power On/Off Thread
    def __init__(self, path_battery_temp,  path_cpu_temp):
        QThread.__init__(self)
        self.path_battery_temp = path_battery_temp
        self.path_cpu_temp = path_cpu_temp    # XO_THERM
        
    def run(self):
        global g_device
        global g_Cpu_Temp		
        global g_Bat_Temp
        global g_read_temp_flag
        
        # read temperature of a phone
        g_Bat_Temp[count] <= value
        g_Cpu_Temp[count] <= value 
        
    def stop(self):
         self.exit_thread =  1
         self.quit()
         
```


**plot the graph with temperature** 

```
    def PlotFunc(self,  idx):
        global g_Temp

        self.init_data()
        if idx == 0:
            pointer  = self.ui.widget_1.canvas
            X_data  = self.lstX1
            Y_data  = self.lstY1
            X1_data = self.lstX1_1
            Y1_data = self.lstY1_1 
        
        pointer.axes.clear()
        pointer.axes.set_xlabel('Time(sec)')
        pointer.axes.set_ylabel('Temperature($^{\circ}$C)')
        pointer.axes.xaxis.set_ticks_position('bottom')
        pointer.axes.yaxis.set_ticks_position('left')
        #pointer.axes.spines['top'].set_color('red')     
        pointer.axes.grid(color='b',  linewidth=1) 
        
        if self.ball_crack_flag == False:		
            pointer.axes.plot(self.X_upper_limit,   self.Y_upper_limit,   'r-',  linestyle = '--')   
            pointer.axes.plot(self.X_center_limit,  self.Y_center_limit,  'c',   linestyle = '-',  label='baseline')    
            pointer.axes.plot(self.X_bottom_limit, self.Y_bottom_limit, 'r-',  linestyle = '--')    
        else:
            pointer.axes.set_ylim(int(self.save_low_temp[idx]-2), int(self.save_high_temp[idx]+2))
            
        pointer.axes.plot(X1_data,  Y1_data,  'b-',  label='Temp', linewidth=1)   # , 'b-', , 'g-' ,  marker='o'
        
        pointer.draw()
         
```


### Final. run the Python scripts.  Below is the working screen .

![QtTempTest](/img/2016-12-06-How-to-use-Qt5/QtTempTest.JPG)

