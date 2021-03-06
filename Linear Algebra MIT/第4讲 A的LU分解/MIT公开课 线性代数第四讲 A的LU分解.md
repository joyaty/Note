# MIT公开课 线性代数第四讲 A的LU分解

L为lower，意为下三角矩阵，U为upper，意为上三角矩阵。



假设存在矩阵A且可逆，矩阵B且可逆，则存在
$$
ABB^{-1}A^{-1} = I
$$
将矩阵A转置可以得到：
$$
AA^{-1} = I 
$$

$$
(A^{-1})^{T}A^{T} = I
$$

A转置的逆等于A的逆的装置。对于单个矩阵A，转置和逆两种计算的顺序可以互换。



重新审视消元，先考虑一个2*2矩阵的实例：
$$
\left[
\begin{matrix}
1 & 0 \\
-4 & 1 \\
\end{matrix}
\right]
\left[
\begin{matrix}
2 & 1 \\
8 & 7 \\
\end{matrix}
\right]
=
\left[
\begin{matrix}
2 & 1 \\
0 & 3 \\
\end{matrix}
\right]
\tag{4.1}
$$
消元过程 EA = L 描述为4.1的矩阵乘法问题。

现在考虑用A=LU描述上面的消元过程，可得
$$
\left[
\begin{matrix}
2 & 1 \\
8 & 7 \\
\end{matrix}
\right]
=
\left[
\begin{matrix}
1 & 0 \\
4 & 1 \\
\end{matrix}
\right]
\left[
\begin{matrix}
2 & 1 \\
0 & 3 \\
\end{matrix}
\right]
\tag{4.2}
$$
L为E的逆矩阵。

扩展：有时候会将A=LU拓展为A=LDU的形式，即U分解为一个对角矩阵和一个对角线都是1的U，将4.2扩展为LDU可得
$$
\left[
\begin{matrix}
2 & 1 \\
8 & 7 \\
\end{matrix}
\right]
=
\left[
\begin{matrix}
1 & 0 \\
4 & 1 \\
\end{matrix}
\right]
\left[
\begin{matrix}
2 & 0 \\
0 & 3 \\
\end{matrix}
\right]
\left[
\begin{matrix}
1 & 1/2 \\
0 & 1 \\
\end{matrix}
\right]
\tag{4.3}
$$
对于3 * 3矩阵消元，可以得到：
$$
E_{32}E_{31}E_{21}A = U
\tag{4.4}
$$
转化为A=LU的形式，可得：
$$
A = (E_{21})^{'}(E_{31})^{'}(E_{32})^{'}U \\
L = (E_{21})^{'}(E_{31})^{'}(E_{32})^{'}
\tag{4.5}
$$
在考虑一个3 * 3消元矩阵的例子，假设3 * 3矩阵只有两个消元矩阵，即3个消元矩阵中又在一个单位矩阵，可计算最终的消元矩阵E
$$
E = E_{32}E_{21}
\\
\left[
\begin{matrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & -5 & 1 \\
\end{matrix}
\right]
\left[
\begin{matrix}
1 & 0 & 0 \\
-2 & 1 & 0 \\
0 & 0 & 1 \\
\end{matrix}
\right]
=
\left[
\begin{matrix}
1 & 0 & 0 \\
-2 & 1 & 0 \\
10 & -5 & 1 \\
\end{matrix}
\right]
\tag{4.6}
$$
可以看到最终消元矩阵中在31位多了一个10，这是因为消元过程中 第一步将行二减去了两倍的行 一得到新行二，之后又将行三减去了五倍的新行二，从而累积的。

在让我看看看逆的形式，即:
$$
L = (E_{21})^{'}(E_{32})^{'}
\\
\left[
\begin{matrix}
1 & 0 & 0 \\
2 & 1 & 0 \\
0 & 0 & 1 \\
\end{matrix}
\right]
\left[
\begin{matrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 5 & 1 \\
\end{matrix}
\right]
=
\left[
\begin{matrix}
1 & 0 & 0 \\
2 & 1 & 0 \\
0 & 5 & 1 \\
\end{matrix}
\right]
$$
可以看到，E中的倍数累积在L中不存在，即消元过程中产生的倍数在L中不会相互影响。这是L的一个重要特性

综上可得结论，对于A=LU，不存在换行操作的情况下，消元过程中产生的消元倍数可以直接填到L中。



 考虑消元过程中的总的步数

假设一个N * N矩阵，每个位置都不为0，消元过程操作本质是每次的一次乘法和一次加法达到消元目的。因此将一次乘法和一次加法综合为一次操作，则需要多少次？

只考虑第一步，将N * N矩阵消元到(N - 1) * (N - 1)矩阵，可以发现，除了矩阵第一行，余下所有行和列的元素都发生了一次操作，最终将第一列的各行元素都变换成为0，则此时操作数达到了 n * (n-1)，约等于n的平方。

递归思想考虑N-1的矩阵，可得操作数为n-1的平方。

综上可得，总次数Count(结合微积分计算)：
$$
Count = n^{2} + (n-1)^{2} + ... + 2^{2} + 1^{2} = 1/3(n^3)
\tag{4.8}
$$
右侧结果向量的操作次数(包括消元过程和回代过程)为n的平方。



矩阵的转置