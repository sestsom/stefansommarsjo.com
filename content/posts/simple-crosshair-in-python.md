+++
author = "Stefan Sommarsjö"
title = "Testing simple crosshair in Python"
date = "2023-02-04"
description = "Code for crosshair in python"
thumbnail = "/img/random/pythoncross.jpg"
twitter_creator = "@sestsom"
images = "/img/random/pythoncross.jpg"

tags = [
    "Python",
]
categories = [
    "Developing",
    "Coding",
]
series = ["Coding"]
aliases = ["simple-crosshair-in-python"]
draft = false
+++
Playing around in python just to see if it works. It's nothing complicated nor fancy but it does what I thought it would do. Thing is, I don't even play Fortnite, or any other game for that matter :-).

{{< gallery >}}
  {{< figure src="/img/random/pythoncross.jpg" caption="Crosshair in Python" >}}
{{< /gallery >}}
<!--more-->

```python
import tkinter as tk
import win32api
import win32gui
import win32con

root = tk.Tk()
root.attributes("-topmost", True)
root.config(bg='white')
root.overrideredirect(True)

canvas = tk.Canvas(root, width=100, height=100, bg='white')
canvas.pack()

cross_width = 40
cross_height = 40
cross_horizontal = canvas.create_line(0, 50, 100, 50, width=3, fill="red")
cross_vertical = canvas.create_line(50, 0, 50, 100, width=3, fill="red")

root.update_idletasks()
hWindow = win32gui.GetForegroundWindow()


exStyle = win32api.GetWindowLong(hWindow, win32con.GWL_EXSTYLE)
exStyle |= win32con.WS_EX_LAYERED
win32api.SetWindowLong(hWindow, win32con.GWL_EXSTYLE, exStyle)

# Set the transparency level (255 is fully opaque, 0 is fully transparent)
win32gui.SetLayeredWindowAttributes(hWindow, 0x00ffffff, 128, win32con.LWA_COLORKEY | win32con.LWA_ALPHA)

def move_cross(event):
    x, y = event.x_root, event.y_root
    root.geometry("+{}+{}".format(x, y))

root.bind("<B1-Motion>", move_cross)

root.mainloop()
```