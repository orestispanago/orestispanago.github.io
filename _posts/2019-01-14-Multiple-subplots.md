---
title: "Multiple subplots with python"
date: 2019-01-14
tags: [python, data, visualization]
header:
  image: #""
excerpt: "Plot non-square number of subplots with matplotlib"
---
Plotting multiple subplots in one figure is commonly used in data reporting tasks.
However, notice that a non-square number of plots generates blank axis.


```python
import matplotlib.pyplot as plt
import numpy as np
```

Let's generate some data


```python
x = np.linspace(0,1,10)
y = x**2
```

Let's assume that we need to plot 7 subplots in a 3-row layout.


```python
fig,axes = plt.subplots(nrows=3,ncols=3,figsize=(12,9),dpi=100)
for i in range(7):
	axes[i//3][i%3].plot(x,y,label='$x^2$')
	axes[i//3][i%3].plot(y,x,label='$\sqrt{x}$')
	axes[i//3][i%3].legend()
	axes[i//3][i%3].set_title('Plot '+str(i))
	axes[i//3][i%3].set_ylabel('Row '+ str(i//3))
	axes[i//3][i%3].set_xlabel('Col '+ str(i%3))
plt.tight_layout()
plt.show()
```


![png](/images/Multiple-subplots/output_5_0.png)


Notice the blank axes at the lower right corner of the figure.
To gert rid of them, we can set all axes off and set on after plotting


```python
fig,axes = plt.subplots(nrows=3,ncols=3,figsize=(12,9),dpi=100)
[axi.set_axis_off() for axi in axes.ravel()] # Makes all  axes invisible
for i in range(7):
	axes[i//3][i%3].plot(x,y,label='$x^2$')
	axes[i//3][i%3].plot(y,x,label='$\sqrt{x}$')
	axes[i//3][i%3].legend()
	axes[i//3][i%3].set_title('Plot '+str(i))
	axes[i//3][i%3].set_ylabel('Row '+ str(i//3))
	axes[i//3][i%3].set_xlabel('Col '+ str(i%3))
	axes[i//3][i%3].set_axis_on() # makes axes with plot visible
plt.tight_layout()
plt.show()
```


![png](/images/Multiple-subplots/output_7_0.png)
