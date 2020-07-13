# Matlab_arrowPlot
提供一种Matlab绘制直线箭头以及非线性箭头的方式，可用以绘制坐标轴箭头。

该仓库包含两个Matlab函数：

* `arrow.m`：绘制任意两点间的直线箭头，可应用于二维或三维图形
* `arrowPlot.m`：绘制任意曲线的趋势非线型箭头，只能应用于二维图形



### `arrow.m`

该函数的作用是绘制任意两点间的直线箭头，可应用于二维或三维图形。我多用此函数来绘制图形的坐标轴箭头，绘制坐标轴箭头是一个困扰我很久的问题，网上大部分方法往往差强人意，所以下面我据此来举例，如下图所示，我希望绘制以下图形的三维坐标轴。

![](/img/mat7.png)

#### 绘制坐标轴箭头

`arrow.m`函数绘制命令如下`arrow([x1 y1],[x2 y2])`，(三维也同理)表示绘制从(x1,y1)到(x2,y2)的箭头，非框图坐标是大家自己定义的坐标轴。还有两个我通常使用的命令，`BaseAngle`设置箭头的夹角，我通常设置30，以及`LineWidth`设置1即可。

下面我们来绘制上图的坐标轴，比如x轴绘制从(0,0,0)到(25,0,0)，y轴绘制从(0,-3,0)到(0,3,0)，z轴绘制从(0,0,-3)到(0,0,3)，好让我们直接来看代码。

```matlab
clear,clc
x = linspace(0,20,1000); 
y1 = 2*cos(x);
z1 = 2*sin(x);
y2 = sin(x);
z2 = cos(x);
figure(3);
plot3(x,y1,z1,'r','LineWidth',1.5);
hold on
plot3(x,y2,z2,'b:','LineWidth',1.5);
grid on
set(gca,'XLim',[0 25]);
set(gca,'YLim',[-3 3]);
set(gca,'ZLim',[-3 3]);
xlabel('x'); ylabel('y');zlabel('z');
arrow([0 0 0],[25 0 0],'BaseAngle',30,'LineWidth',1); % x轴绘制从(0,0,0)到(25,0,0)
arrow([0 -3 0],[0 3 0],'BaseAngle',30,'LineWidth',1); % y轴绘制从(0,-3,0)到(0,3,0)
arrow([0 0 -3],[0 0 3],'BaseAngle',30,'LineWidth',1); % z轴绘制从(0,0,-3)到(0,0,3)
set(gca,'Fontname','Monospaced','Fontsize',10,'FontWeight','bold');
title('三维例子：x\sim y_1,y_2 \sim z_1,z_2');
```

效果如下图所示，再次强调不光是坐标轴箭头，坐标空间任意两点的箭头都可以绘制：

![](/img/mat8.png)

### `arrowPlot.m`

#### 绘制非线型箭头

在我们绘图的过程中，我们还有另外一种情况，就是我们想表示某条曲线的变化趋势，比如$sin(x)$，我们希望在正弦函数上绘制一些箭头来表示，同样我找到了开源的绘制代码。

使用`arrowPlot.m`函数绘制非线型箭头，`arrowPlot(x,y)`代表绘制x,y曲线上的箭头，常用的命令还有`number`代表曲线上的箭头个数，`LineWidth`代表线宽，`color`代表颜色。

例如以下的example：

```matlab
clear,clc
t = [0:0.01:20];
x = t.*cos(t);
y = t.*sin(t);
arrowPlot(x, y, 'number', 5, 'color', 'r', 'LineWidth', 1)
```

效果图如下图所示，可惜的是此函数暂不支持三维图形的箭头绘制：

![](/img/mat9.png)