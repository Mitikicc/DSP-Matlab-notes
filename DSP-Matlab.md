# DSP-Matlab-notes
for tests, for DSP — 信号分析处理与实验

2020-8-18

# 实验一 信号的产生和运算

**实验目的**：

熟悉 Matlab 软件环境和常用函数， 能够按照要求产生信号，对信号进行基本运算。 通过实验，加深理解连续和离散时间信号的时域表示。

**实验内容**：

基于 Matlab 环境， 产生常用的连续时间信号和离散时间序列（含正弦信号、指数信号、阶跃信号等），绘制信号波形，实现信号的加、乘、移位、卷积等基本运算。

**一．** **实验过程与结果分析：**

**1.**   单位样本和单位阶跃序列

使用如下Matlab命令，可产生长度为*N*的单位样本序列`u[n]`

```matlab
u = [1 zeros(1,N-1)];
```

延时*M*个样本且长度为*N*的单位样本序列`ud[n]`，可用如下Matlab命令产生，其中*M<N*:

```matlab
ud = [zeros(1,M) 1 zeros(1,N-M-1)];
```

同样，使用下面的MATLAB命令可产生长度为*N*的单位阶跃序列s[n]:

```matlab
s = [ones(1,N)];
```

产生延时单位阶跃序列的方法，类似于产生延时单位样本序列的方法。

程序P1_1产生并绘制了一个单位样本序列。

```matlab
% Program P1_1
% Generation of a Unit Sample Sequence 
clf;
% Generate a vector from -10 to 20
n = -10:20;
% Generate the unit sample sequence
u = [zeros(1,10) 1 zeros(1,20)];
% Plot the unit sample sequence
stem(n,u);
xlabel('Time index n');ylabel('Amplitude');
title('Unit Sample Sequence');
axis([-10 20 0 1.2]);
```

**问题****1.1****：**运行程序P1_1，以产生单位样本序列u[n]并显示它。

 ![image-20200818181013190](C:\Users\XiaoChen\AppData\Roaming\Typora\typora-user-images\image-20200818181013190.png)

**问题****1.2****：**命令clf, axis, title, xlabel和ylabel的作用是什么？

 clf: 清除上一次运行产生的图片

axis：规定横纵坐标范围

 xlabel：在x轴添加标签

 Ylabel：在y轴添加标签

**问题****1.3****：**修改程序P1_1，以产生带有延时11个样本的延迟单位样本序列`ud[n]`。运行修改的程序并显示产生的序列。

 

```matlab
% Program P1_1
% Generation of a Unit Sample Sequence 
clf;
% Generate a vector from -10 to 20
n = -10:20;
% 产生带有延时11个样本的延迟单位样本序列ud[n]
ud = [zeros(1,21) 1 zeros(1,9)];
% Plot the unit sample sequence
stem(n,u);
xlabel('Time index n');ylabel('Amplitude');
title('Unit Sample Sequence');
axis([-10 20 0 1.2]);
```

![image-20200818182432315](C:\Users\XiaoChen\AppData\Roaming\Typora\typora-user-images\image-20200818182432315.png)

**问题****1.4：**修改程序P1_1，以产生单位阶跃序列`s[n]`。运行修改的程序并显示产生的序列。

 

```matlab
% Program P1_1
% Generate a vector from -10 to 20
n = -10:20;
% 产生单位阶跃序列s[n]
u = [zeros(1,10),ones(1,21)];
% Plot 
stem(n,u);
xlabel('Time index n');ylabel('Amplitude');
title('Unit Sample Sequence');
axis([-10 20 0 1.2]);
```

![image-20200818183307510](C:\Users\XiaoChen\AppData\Roaming\Typora\typora-user-images\image-20200818183307510.png)

**问题****1.5****：**修改程序P1_1，以产生带有超前7个样本的延迟单位阶跃序列`sd[n]`。运行修改

的程序并显示产生的序列。

```matlab
% Program P1_1
% Generate a vector from -10 to 20
n = -10:20;
% 
u = [zeros(1,3),ones(1,28)];
% Plot 
stem(n,u);
xlabel('Time index n');ylabel('Amplitude');
title('Unit Sample Sequence');
axis([-10 20 0 1.2]);
```

![image-20200818184120873](C:\Users\XiaoChen\AppData\Roaming\Typora\typora-user-images\image-20200818184120873.png)

 





**2.**   指数序列

指数序列可使用MATLAB运算符 .^ 和exp 产生。

程序P1_2可生成一个复指数序列。

```matlab
% Program P1_2
% Generation of a complex exponential sequence
clf;
c = -(1/12)+(pi/6)*i;
K = 2;
n = 0:40;
x = K*exp(c*n);
subplot(2,1,1);
stem(n,real(x));
xlabel('Time index n');ylabel('Amplitude');
title('Real part');
subplot(2,1,2);
stem(n,imag(x));
xlabel('Time index n');ylabel('Amplitude');
title('Imaginary part');
```

程序P1_3可生成一个实指数序列。

```matlab
% Program P1_3
% Generation of a real exponential sequence
clf;
n = 0:35; a = 1.2; K = 0.2;
x = K*a.^n;
stem(n,x);
xlabel('Time index n');ylabel('Amplitude');
```

 

**问题****2.1****：**运行程序P1_2，以产生复指数序列。

 ![image-20200818184547723](C:\Users\XiaoChen\AppData\Roaming\Typora\typora-user-images\image-20200818184547723.png)

**问题****2.2****：**运算符real和imag的作用是什么？

 运算符real和imag的作用分别是提取运算数值x实部和虚部。

**问题****2.3****：**命令subplot的作用是什么？

 subplot（a，b，c），其中a代表图像分a行显示，b代表图像分b列显示，c代表第a行的第b列图像。

**问题****2.4****：**运行程序P1_3，以产生实指数序列。

![image-20200818185059551](C:\Users\XiaoChen\AppData\Roaming\Typora\typora-user-images\image-20200818185059551.png)



**3.**   **正弦序列**

实正弦序列，![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)，在MATLAB中可使用三角运算符cos和sin产生。

程序P1_4是产生一个正弦信号的简单示例。

```matlab
% Program P1_4
% Generation of a sinusoidal sequence
n = 0:40; 
f = 0.1;         
phase = 0;          
A = 1.5;        
arg = 2*pi*f*n - phase; 
x = A*cos(arg);
clf;        % Clear old graph
stem(n,x);       % Plot the generated sequence
axis([0 40 -2 2]);
grid; 
title('Sinusoidal Sequence');
xlabel('Time index n');
ylabel('Amplitude');
axis;
```

**问题****3.1****：**运行程序P1_4，以产生正弦序列并显示它。

 ![image-20200818185252447](C:\Users\XiaoChen\AppData\Roaming\Typora\typora-user-images\image-20200818185252447.png)

**问题****3.2****：**该序列的频率是多少？哪个参数控制该序列的相位？哪个参数控制该序列的振

幅？该序列的周期是多少？

​     频率f=0.1HZ，通过改变f的值可以改变频率。

​     Phase控制相位

​     A控制振幅

​     周期T=10s

**问题****3.3****：**修改程序P1_4，以产生长度为50、频率为0.08、振幅为2.5、相移为90度的

正弦序列并显示它。该序列的周期是多少？

T=12.5s

```matlab
% Program P1_4
% Generation of a sinusoidal sequence
n = 0:50; 
f = 0.1;         
phase = pi/2;          
A = 2.5;        
arg = 2*pi*f*n - phase; 
x = A*cos(arg);
clf;        % Clear old graph
stem(n,x);       % Plot the generated sequence
axis([0 40 -3 3]);
grid; 
title('Sinusoidal Sequence');
xlabel('Time index n');
ylabel('Amplitude');
axis;
```

![image-20200818185739527](C:\Users\XiaoChen\AppData\Roaming\Typora\typora-user-images\image-20200818185739527.png)

**问题****3.4****：**在程序P1_4中用plot命令代替stem命令，运行新程序。新图形与问题3.1中

产生的图形有什么区别？

![image-20200818185825421](C:\Users\XiaoChen\AppData\Roaming\Typora\typora-user-images\image-20200818185825421.png)

区别：离散变为连续



 

**4.**   **序列的简单运算**

数字信号处理的目的，是从一个或多个给定的离散时间信号中，产生一个具有我们所需

性质的信号。处理算法由诸如加法、标量乘法、时间反转、延时和乘积运算等基本运算的组合所组成。

数字信号处理应用的一个常见例子是从被加性噪声污染的信号中移除噪声。假定信号

![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)被噪声![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image004.png)所污染，得到了一个含有噪声的信号![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image006.png)。我们的目的是对![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image008.png)进行运算，产生一个合理逼近![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)的信号![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image010.png)。因此，对时刻*n*的样本附近的一些样本求平均，产生输出信号是一种简单有效的方法。例如，采用三点滑动平均算法的表达式如下:

![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

程序P1_5可用于实现上面的算法。

```matlab
% Program P1_5
% Signal Smoothing by Averaging
clf;
R = 51;
d = 0.8*(rand(R,1) - 0.5); % Generate random noise
m = 0:R-1;
s = 2*m.*(0.9.^m); % Generate uncorrupted signal
x = s + d'; % Generate noise corrupted signal
subplot(2,1,1);
plot(m,d','r-',m,s,'g--',m,x,'b-.');
xlabel('Time index n');ylabel('Amplitude');
legend('d[n] ','s[n] ','x[n] ');
x1 = [0 0 x];x2 = [0 x 0];x3 = [x 0 0];
y = (x1 + x2 + x3)/3;
subplot(2,1,2);
plot(m,y(2:R+1),'r-',m,s,'g--');
legend( 'y[n] ','s[n] ');
xlabel('Time index n');ylabel('Amplitude');
```

**问题****4.1****：**运行程序P1_5，以产生所有相关的信号。

 <img src="C:\Users\XiaoChen\AppData\Roaming\Typora\typora-user-images\image-20200818190917926.png" alt="image-20200818190917926" style="zoom: 67%;" />

**问题****4.2****：**使用语句x=s+d能产生被噪声污染的信号吗？若不能，为什么？

 不能，行向量不能直接和列向量相加

**问题****4.3****：**信号x1，x2和x3与信号x之间的关系是什么？

 x1在x前补两个0，是延时

x2是在x前后各补一个0，是为了和x1，x3相同长度。

x3在x后面补两个0，是x的超前

**问题****4.4****：**legend命令的作用是什么？

添加图示



**5.**   **卷积**

线性时不变离散系统，输出序列y[n]是输出序列x[n]和冲激响应(单位脉冲响应) h[n]的卷积

![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

假设待卷积的两个序列都为有限长序列，在MATLAB中可通过命令conv实现。

程序P1_6实现了该方法。

```matlab
% Program P1_6
clf;
h = [3 2 1 -2 1 0 -4 0 3];	% impulse response
x = [1 -2 3 -4 3 2 1];		% input sequence
y = conv(h,x);
n = 0:14;
stem(n,y);
xlabel('Time index n'); ylabel('Amplitude');
title('Output Obtained by Convolution'); grid;

```

**问题****5.1****：**运行程序P1_6，对序列h[n]和x[n]求卷积，生成y[n]。 

 ![image-20200818194211785](C:\Users\XiaoChen\AppData\Roaming\Typora\typora-user-images\image-20200818194211785.png)

**问题****5.2****：**修改程序P1_6，自己给定一长度为15的序列h[n]和一长度为10的序列x[n]，计

算h[n]和x[n]的卷积。

```matlab
clf;
h = [2 0 4 8 7 0 4 0 3 1 2 3 3 5 5];
x = [1 -2 3 -4 7 8 9 4 4 4];
y = conv(h,x);
n = 0:23;
stem(n,y);
xlabel('Time index n'); ylabel('Amplitude');
title('Output Obtained by Convolution'); grid;
```

![image-20200818195014114](C:\Users\XiaoChen\AppData\Roaming\Typora\typora-user-images\image-20200818195014114.png)



**6.**   **连续正弦信号**

实正弦信号![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)。由于MATLAB不能严格地产生一个连续时间信号，可用较密的离散点的连线来近似。

程序P1_7产生了一个实正弦信号![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)，*t*的单位为毫秒(ms)。

```matlab
% Program P1_7
clf;
t = 0:0.0005:1;
f = 13;
xa = cos(2*pi*f*t);
plot(t,xa);grid
xlabel('Time, msec');ylabel('Amplitude');
title('Continuous-time signal x_{a}(t)');
```

**问题****6.1****：**运行程序P1_7，产生连续时间正弦信号并显示它。

 ![image-20200818195252651](C:\Users\XiaoChen\AppData\Roaming\Typora\typora-user-images\image-20200818195252651.png)

**问题****6.2****：**正弦信号的频率是多少赫兹？

 F=13kHZ

**问题****6.3：** 若![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)，t的单位是毫秒，修改程序P1_7，画出![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)在![img](file:///C:/Users/XiaoChen/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)内的连续波形。

```matlab
clf;
t = 0:0.0005:9;
xa = cos(5*pi *t)+4*sin(2*pi*t).*sin(3*pi*t);
plot(t,xa);grid
xlabel('Time, msec');ylabel('Amplitude');
title('Continuous-time signal x_{a}(t)');
```

