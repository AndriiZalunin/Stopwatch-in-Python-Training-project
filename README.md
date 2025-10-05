# Stopwatch (Training project)
## Overview

The program allows you to start/stop/restart the timer using buttons.

## More detailed overview

Initially, all objects used are declared in the `__init__` function.
```Python
import sys
from PyQt5.QtWidgets import QApplication, QWidget, QPushButton, QLabel, QVBoxLayout, QHBoxLayout
from PyQt5.QtCore import QTimer, QTime, Qt

class Stopwatch(QWidget):
    def __init__(self):
        super().__init__()
        self.time = QTime(0,0,0,0)
        self.time_label = QLabel("00:00:00.00",self)
        self.start_button = QPushButton("Start",self)
        self.stop_button = QPushButton("Stop",self)
        self.reset_button = QPushButton("Reset",self)
        self.timer = QTimer(self)
        self.initUI()
```
Next, in `initUI`, widgets are placed using a combination of `QVBoxLayout`
and `QHBoxLayout` objects, CSS styles are applied, and functions are bound to the necessary buttons.
Also `update_display` function is called for the `timer` object, which
displays the time in a specific format every 10 milliseconds.
```Python
def format_time(self, time):
    hours = time.hour()
    minutes = time.minute()
    seconds = time.second()
    milliseconds = time.msec() // 10
    return f"{hours:02}:{minutes:02}:{seconds:02}.{milliseconds:02}"

def update_display(self):
    self.time = self.time.addMSecs(10)
    self.time_label.setText(self.format_time(self.time))
```
Functions with the same names have been created for the corresponding buttons: 
`start`, `stop`, and `reset`.
```Python
def start(self):
    self.timer.start(10)

def stop(self):
    self.timer.stop()

def reset(self):
    self.timer.stop()
    self.time = QTime(0,0,0,0)
    self.time_label.setText(self.format_time(self.time))
```