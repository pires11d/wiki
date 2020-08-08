# Python - Plotando gráficos
> Autor: Lucas Joshua Pires


## 1. Gráficos com **matplotlib**
- Gráficos 1D
~~~py
import matplotlib.pyplot as plt
import numpy as np

# Numerical data:
x = np.linspace(-10, 10, 100)
s = np.linspace(0.5, 50, 100)
y = x**2

# Simple graphs:
plt.plot(x,y)
plt.scatter(x,y)
plt.stackplot(x,y)
plt.bar(x,y)
plt.polar(x,y)
plt.pie([10, 30, 1, 5], explode = (0,0,0.1,0), labels = ('Frogs', 'Hogs', 'Dogs', 'Logs')

# Histograms:
plt.hist(x, bins = 20, range=(0,255))
plt.hist2d(x,y, bins = (10,20), range = ((0,10),(20,50)))
plt.hexbin(x,y, gridsize = (10,20), extent = (0,10,20,50))
~~~

- Gráficos 2D
~~~py
import matplotlib.pyplot as plt
import numpy as np

# Numerical data
x = np.linspace(-10, 10)
y = np.linspace(-10, 10)
X, Y = np.meshgrid(x, y)
Z = X**2+Y**2

plt.contour(X,Y,Z, 30,  cmap = 'jet')
plt.contourf(X,Y,Z)
plt.pcolor(X,Y,Z,)
plt.quiver(X,Y,Z)
plt.streamplot(X,Y,Z,W)
plt.violinplot()

# Layout adjusting:
plt.tight_layout()
plt.subplot(2,2,1) --> plt.subplot(2,2,4)
plt.colorbar()
plt.axis('tight')
plt.xlabel('X')
plt.ylabel('Y')
plt.xlim(xmin,xmax)
plt.ylim(ymin,ymax)
plt.xscale
plt.yscale
plt.xticks([-1,0,1])
plt.yticks([-1,0,1])

#Don't forget to show graph!
plt.show()
~~~
		
## 2. Gráficos com **seaborn**
- Distribuição bivariável
~~~py
import seaborn as sns
from pydataset import data
import matplotlib.pyplot as plt

# Numerical data:
dados = data('winter')

# Plot types:
sns.lmplot(x='NO',y='NO2',data=dados)
sns.residplot(x='NO',y='NO2',data=dados)
sns.jointplot(x='NO',y='NO2',data=dados)
sns.boxplot(x='NO',data=dados)
sns.regplot(x='NO', y='NO2', scatter=None, order=2)
sns.stripplot(x='NO',data=dados, jitter=True, orient='h')
sns.swarmplot(x='NO',data=dados)
sns.violinplot(x='NO',data=dados, inner=None)
~~~

- Distribuição multivariável
~~~py
import seaborn as sns
from pydataset import data
import matplotlib.pyplot as plt

# Numerical data:
dados = data('winter')

# Plot types:
sns.jointplot(x='xlabel',y='ylabel', data=dados)
	kind = 'kde', 'resid', 'scatter', 'reg', 'hex'
sns.pairplot(dados)
sns.heatmap(dados[1:10][:])
~~~
	
## 3. Processando imagens com **matplotlib**
~~~py
import matplotlib.pyplot as plt

# Load default image:
image1 = plt.imread('image1.jpg')
print(image1.shape)
plt.imgshow(image1)
plt.axis('off')
plt.show()

# Adjusting size:
plt.imshow(image1, aspect=2.0, extent=(-2,2,-1,1)
or	
pmin, pmax = image1.min(), image1.max()
image2 = 256*(image1-pmin) / (pmax-pmin)
	
# Set colormap:
image2 = image1.mean(axis=2)
print(image2.shape)
plt.set_cmap('gray')
plt.imshow(image2, cmap='gray')
plt.axis('off')
plt.show()

# Pixel histogram:
pixels = image1.flatten()
plt.hist(pixels, bins = 64, range=(0,255))
plt.twinx()
~~~
