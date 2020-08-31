# MIT公开课 线性代数第二讲 矩阵消元



消元法求解方程组实例
$$
\begin{cases}
x + 2y + z = 2 \\
3x + 8y + z = 12 \\
4y + z = 2 \\
\end{cases}
\tag{1.1}
$$
根据方程组矩阵形式抽象Ax = b，可得矩阵A
$$
\left[
\begin{matrix}
1 & 2 & 1 \\
3 & 8 & 1 \\
0 & 4 & 1 \\
\end{matrix}
\right]
\tag{1.2}
$$
第一步进行消元

1列1的矩阵元素，即1，很容易得到消元参数为3，讲行1 * 3，可得到第一步的消元矩阵：
$$
\left[
\begin{matrix}
1 & 2 & 1 \\
0 & 2 & -2 \\
0 & 4 & 1 \\
\end{matrix}
\right]
\tag{1.3}
$$
同上，消去行2列2的矩阵元素，可得第二步消元结果的矩阵：
$$
\left[
\begin{matrix}
1 & 2 & 1 \\
0 & 2 & -2 \\
0 & 0 & 5 \\
\end{matrix}
\right]
\tag{1.4}
$$
此时得到一个上三角矩阵，消元结束，我们称得到的最终矩阵为U.

可以得到了三个主元，1/2/5，注意主元不能为0，如果发现主元为0，可以通过行交换避免，找到一行可以使本行主元不为0即可。

第二部进行回代

我们将右侧向量b代入到矩阵A中，得到增广矩阵：
$$
\left[
\begin{array}{ccc|c}
1 & 2 & 1 & 2 \\
3 & 8 & 1 & 12 \\
0 & 4 & 1 & 2 \\
\end{array}
\right]
\tag{1.5}
$$
同样代入到第一步的消元中，得到
$$
\left[
\begin{array}{ccc|c}
1 & 2 & 1 & 2 \\
3 & 8 & 1 & 12 \\
0 & 4 & 1 & 2 \\
\end{array}
\right]
\rightarrow
\left[
\begin{array}{ccc|c}
1 & 2 & 1 & 2 \\
0 & 2 & -2 & 6 \\
0 & 4 & 1 & 2 \\
\end{array}
\right]
\rightarrow
\left[
\begin{array}{ccc|c}
1 & 2 & 1 & 2 \\
0 & 2 & -2 & 6 \\
0 & 0 & 5 & -10 \\
\end{array}
\right]
\tag{1.6}
$$
我们称得到的增广矩阵中右侧向量的那一列为c.

则Ax = b，通过消元，得到了 Ux = c.

即方程组
$$
\begin{cases}
x + 2y + z = 2 \\
2y - 2z = 6 \\
5z = -10 \\
\end{cases}
\tag{1.7}
$$
由此很容易回代求解，x = 2, y = 1, z = -2。



接下来用矩阵来描述消元过程。

拓展，矩阵列变化，矩阵右乘一个向量，即：
$$
\left[
\begin{matrix}
a & b & c \\
d & e & f \\
g & h & i \\
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
x * col1 + y * col2 + z * col3 
\tag{1.8}
$$
矩阵行变换，矩阵左乘一个向量，即
$$
\left[
\begin{matrix}
x & y & z
\end{matrix}
\right]
\left[
\begin{matrix}
a & b & c \\
d & e & f \\
g & h & i \\
\end{matrix}
\right]
= 
x * row1 + y * row2 + z * row3
\tag{1.9}
$$
**注意，在进行矩阵乘法时，注意用整个向量来思考。**



我们可以很方便的用行变换来描述上述消元过程。

例如，第一步消元过程中，我们将行2 减去 3倍的行一，得到第一步的消元结果，则可用行变换的矩阵描述：
$$
\left[
\begin{matrix}
1 & 0 & 0 \\
-3 & 1 & 0 \\
0 & 0 & 1 \\
\end{matrix}
\right]
\left[
\begin{matrix}
1 & 2 & 1 \\
3 & 8 & 1 \\
0 & 4 & 1 \\
\end{matrix}
\right]
=
\left[
\begin{matrix}
1 & 2 & 1 \\
0 & 2 & -2 \\
0 & 4 & 1 \\
\end{matrix}
\right]
\tag{1.10}
$$
我们记1.10中左乘的矩阵为，它描述在2行1列做消元
$$
E_{21}
$$
同理，第二步的消元过程，用矩阵描述：
$$
\left[
\begin{matrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & -2 & 1 \\
\end{matrix}
\right]
\left[
\begin{matrix}
1 & 2 & 1 \\
0 & 2 & -2 \\
0 & 4 & 1 \\
\end{matrix}
\right]
=
\left[
\begin{matrix}
1 & 2 & 1 \\
0 & 2 & -2 \\
0 & 0 & 5 \\
\end{matrix}
\right]
\tag{1.11}
$$
同理记1.11中左乘矩阵为，它描述在3行2列做消元
$$
E_{32}
$$
由此可得抽象为：
$$
E_{32}(E_{21}A) = U
\tag{1.12}
$$
根据结合律（P.S. 矩阵乘法满足结合律，不满足交换律）
$$
（E_{32}E_{21}）A = U
\tag{1.13}
$$
则和得到一个描述消元过程的矩阵E，令
$$
EA = U
\tag{1.14}
$$
我们称E为初等矩阵。



消元过程中还有可能用到另一矩阵，即进行换行变换使，可以使用置换矩阵，置换矩阵也是另一种初等矩阵。

置换行，基于行变换事项，左乘置换矩阵，即
$$
\left[
\begin{matrix}
0 & 1 \\
1 & 0 \\
\end{matrix}
\right]
\left[
\begin{matrix}
a & b \\
c & c \\
\end{matrix}
\right]
=
\left[
\begin{matrix}
c & d \\
a & b \\
\end{matrix}
\right]
$$
置换列，基于列变化思想，右侧置换矩阵，即
$$
\left[
\begin{matrix}
a & b \\
c & d \\
\end{matrix}
\right]
\left[
\begin{matrix}
0 & 1 \\
1 & 0 \\
\end{matrix}
\right]
=
\left[
\begin{matrix}
b & a \\
d & c \\
\end{matrix}
\right]
$$


矩阵的逆

我们举例1.10中消元矩阵的逆
$$
\left[
\begin{matrix}
1 & 0 & 0 \\
-3 & 1 & 0 \\
0 & 0 & 1 \\
\end{matrix}
\right]
$$
该矩阵描述了行2 减去 3倍的 行1 进行消元。

矩阵的逆的含义即为取消这次消元，使得取消消元，即该消元矩阵左乘某个矩阵，得到单位矩阵。

则很容易得到应该是 行2 加上 3倍的 行一 来进行取消消元。这可得消元矩阵的逆：
$$
\left[
\begin{matrix}
1 & 0 & 0 \\
3 & 1 & 0 \\
0 & 0 & 1 \\
\end{matrix}
\right]
\left[
\begin{matrix}
1 & 0 & 0 \\
-3 & 1 & 0 \\
0 & 0 & 1 \\
\end{matrix}
\right]
=
\left[
\begin{matrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1 \\
\end{matrix}
\right]
$$
记做
$$
E^{-1}E = I
\tag{1.15}
$$

