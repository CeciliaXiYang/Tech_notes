Python Plot

1) Load matplotlib: 
``
import matplotlib.pyplot as plt
%matplotlib inline
``

2) Change the distance from ticks to axis:  `ax.tick_param(axis = 'both', which = 'major', pad = 15)`

3) Change the distance from labels to axis: `plt.xlabel(labelpad = 15)`

4) Set the size of grids:
``
from matplotlib.ticker import MultipleLocator
spacing = 0.5
minorLocator = MultipleLocator(spacing)
ax.yaxis.set_minor_locator(minorLocator)
ax.xaxis.set_minor_locator(minorLocator)
ax.grid(linestyle = '--', which = 'minor')
``

5) Add notations for the data points:
``
notation = ['A', 'B', 'C']
for i, txt in enumerate(notation):
  ax.annotation(txt, (x[i], y[i] + 0.1), fontsize = 15)
``

6) Legend for scatters: 
``
pos_dots = plt.scatter(x_pos, y_pos, marker='x', s=100, color='r', lw=3.5)
neg_dots = plt.scatter(x_neg, y_neg, marker='o', s=100, color='r', lw=3.5)

lgd = plt.legend((pos_dots, neg_dots), ('Positive', 'Negative'), loc='upper center', bbox_to_anchor=(0.5, -0.1), fontsize=12)
``

7) Save figure to a file:
`plt.savefig('Figure', bbox_extra_artists=(lgd,), bbox_inches = 'tight')`

8) Set the range of axis:
``
ax.set_xlim([0,10])
ax.set_ylim([0,10])
``

9) Plot the with step:
`plt.step(x,y)`

10) Set fiture size:
`plt.figure(figsize=(8,6))`
