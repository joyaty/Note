# MIT公开课 线性代数第一讲 方程组的集合解释

行图像（Row picture）

列图像（Column picture）

实例，两个未知数，两个方程组
$$
\begin{cases}
2x - y = 0 \\
-x + 2y = 3 \\
\end{cases}
\tag{1.1}
$$
方程组的矩阵形式：
$$
\left[
\begin{matrix}
2 & -1 \\
-1 & 2 \\
\end{matrix}
\right]
\left[
\begin{matrix}
x \\
y \\
\end{matrix}
\right]
= 
\left[
\begin{matrix}
0 \\
3 \\
\end{matrix}
\right]
\tag{1.2}
$$

抽象为：
$$
Ax = b
\tag{1.3}
$$
一次取一行，作用于XY平面，可以得到方程组行图像：

设点A（0， 0），B（1，2），可得2x-y = 0的直线，设点C（-3，0），D(-1, 1)，可得-x+2y = 3的直线。直线上的点即为所代表的方程的所有解，两条直线的交点即为方程组的解。

![](/Users/joyaty/Documents/Notes/Linear Algebra MIT/第一讲 方程组的集合解释/images/RowPicture.png)



列图像（Column picture）
$$
x
\left[
\begin{matrix}
2 \\
-1 \\
\end{matrix}
\right]
+
y
\left[
\begin{matrix}
-1 \\
-2 \\
\end{matrix}
\right]
=
\left[
\begin{matrix}
0 \\
3 \\
\end{matrix}
\right]
\tag{1.4}
$$
列图像寻找正确的x,y，将矩阵A的各个列向量，通过线性组合，得到等号右边的向量。（列向量的线性组合）

问：现在考虑任意的右侧向量，能否得到矩阵A的各个列向量的线性组合（x,y）？

答：只要矩阵A的各个列向量分量不平行，即可通过列向量的线性组合，得到任意的右侧向量(充满二维平面)。



实例，3个未知数，3个方程：
$$
\begin{cases}
2x - y = 0 \\
-x + 2y - z = -1 \\
-3y + 4z = 4 \\
\end{cases}
\tag{1.5}
$$
矩阵形式
$$
\left[
\begin{matrix}
2 & -1 & 0  \\
-1 & 2 & -1 \\
0 & -3 & 4 \\
\end{matrix}
\right]
\left[
\begin{matrix}
x \\
y \\
z \\
\end{matrix}
\right]
= 
\left[
\begin{matrix}
0 \\
-1 \\
4 \\
\end{matrix}
\right]
\tag{1.6}
$$
行图像几何意义：每个方程的解构成一个三维空间平面，3个方程的解平面在三维空间相交于一点，此点即代表方程组的解。

列图像方程组
$$
x
\left[
\begin{matrix}
2 \\
-1 \\
0 \\
\end{matrix}
\right]
+
y
\left[
\begin{matrix}
-1 \\
-2 \\
-3 \\
\end{matrix}
\right]
+
z
\left[
\begin{matrix}
0 \\
-1 \\
4 \\
\end{matrix}
\right]
=
\left[
\begin{matrix}
0 \\
-1 \\
4 \\
\end{matrix}
\right]
\tag{1.7}
$$
列图像几何意义：三维向量在三维空间的线性组合，得到右侧向量。只要三个三维向量不在同一平面，则可通过线性组合，得到任意的右侧向量，使充满三维空间



**本讲核心：矩阵A*向量x = 向量b，即Ax = b，应该看做矩阵A的各个列向量基于向量b各个分量的线性组合。(Ax is a combination of the columns of A.)**

