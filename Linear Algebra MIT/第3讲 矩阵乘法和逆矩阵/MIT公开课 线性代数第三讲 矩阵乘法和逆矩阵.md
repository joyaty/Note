# MIT公开课 线性代数第三讲 矩阵乘法和逆矩阵

### 矩阵乘法

价值存在m x n矩阵A，n x p矩阵B，AB = C，则C为m x p的矩阵。

矩阵C的第i行第j列元素等于矩阵A的第i行 点乘 矩阵B的第j列，用数学公式表示为
$$
C_{ij} = \sum_{k=1}^n({A_{ik} * B_{kj}})
$$
此为矩阵乘法的一般性法则。



使用矩阵的整行或整列来考虑矩阵的乘法，由前两讲已知：

矩阵右乘一个列向量，其意义可以视为矩阵A中各列基于右乘列向量的线性组合，最终得到一个列向量。

矩阵左乘一个行向量，其意义可以视为矩阵B中各行基于左侧行向量的线性组合，最终得到一个行向量。

拓展到矩阵乘法中，则可以视为矩阵C中的各列是矩阵A各列的线性组合，各行是矩阵B各行的线性组合。由此可以定义出矩阵乘法的两种方法，分别称为列方法和行方法。



矩阵乘法的一般性法则为左侧矩阵的行乘以右侧矩阵的列，得到矩阵C中某行某列的元素。那么我们反过来思考，左侧矩阵的列乘以右侧矩阵的行，将得到什么？根据矩阵乘法，mn矩阵 * np矩阵 = mp矩阵，则此时n = 1，因此左侧矩阵的列乘以右侧矩阵的行，将得到一个完整的mp矩阵，最终矩阵C为各个mp矩阵的和。例子：
$$
\left[
\begin{matrix}
2 \\
3 \\
4 \\
\end{matrix}
\right]
\left[
\begin{matrix}
1 & 6 \\
\end{matrix}
\right]
 = 
 \left[
\begin{matrix}
2 & 12 \\
3 & 18 \\
4 & 24 \\
\end{matrix}
\right]
$$


还可以分块对矩阵乘法进行计算，例如将矩阵 AB=C，各自分为4块子矩阵，则：
$$
\left[
\begin{matrix}
A_{1} & A_{2} \\
A_{3} & A_{4} \\
\end{matrix}
\right]
\left[
\begin{matrix}
B_{1} & B_{2} \\
B_{3} & B_{4} \\
\end{matrix}
\right]
 = 
 \left[
\begin{matrix}
A_{1}B_{1} + A_{2}B_{3} & A_{1}B_{2} + A_{2}B_{4} \\
A_{3}B_{1} + A_{4}B_{3} & A_{3}B_{2} + A_{4}B_{4} \\
\end{matrix}
\right]
$$


#### 矩阵的逆

I为单位矩阵，矩阵A的逆，定义为：
$$
A^{-1}A = I
$$
以上为左逆，或者：
$$
AA^{-1} = I
$$
以上为右逆，对于方阵(行列相等的矩阵)，左逆等于右逆，一般性矩阵，因行列不等无法相乘，故左逆不等于右逆。

对于存在逆矩阵的矩阵，我们称之为可逆矩阵，非奇异矩阵。否则称为不可逆矩阵，奇异矩阵。

判断矩阵不可逆的方法，如果能找着一个非0向量X，使得AX = 0，则矩阵A不可逆。例如：
$$
\left[
\begin{matrix}
1 & 3 \\
2 & 6 \\
\end{matrix}
\right]
 \left[
\begin{matrix}
-3 \\
1 \\
\end{matrix}
\right]
=
 \left[
\begin{matrix}
0 \\
0 \\
\end{matrix}
\right]
$$
P.S.  非奇异矩阵的很重要特性是矩阵中的各行各列都是不共线的，即矩阵包含此维度空间所有方向的信息。否则矩阵中至少有一对共线的向量，则矩阵是奇异的，不可逆的。



求取矩阵A的逆矩阵，设：
$$
\left[
\begin{matrix}
1 & 3 \\
2 & 7 \\
\end{matrix}
\right]
 \left[
\begin{matrix}
a & b \\
c & d \\
\end{matrix}
\right]
=
 \left[
\begin{matrix}
1 & 0 \\
0 & 1 \\
\end{matrix}
\right]
\tag{1.1}
$$
使用**Gause-Jordam方法**来求解逆矩阵

将1.1矩阵相乘看做两个方程组，可得：
$$
\left[
\begin{matrix}
1 & 3 \\
2 & 7 \\
\end{matrix}
\right]
\left[
\begin{matrix}
a \\
c \\
\end{matrix}
\right]
=
\left[
\begin{matrix}
1 \\
0 \\
\end{matrix}
\right]
\tag{1.2}
$$

$$
\left[
\begin{matrix}
1 & 3 \\
2 & 7 \\
\end{matrix}
\right]
 \left[
\begin{matrix}
b \\
d \\
\end{matrix}
\right]
=
 \left[
\begin{matrix}
0 \\
1 \\
\end{matrix}
\right]
\tag{1.3}
$$

将方程组1.2，1.3使用增广矩阵消元法综合求解，得：
$$
\left[
\begin{array}{cc|cc}
1 & 3 & 1 & 0 \\
2 & 7 & 0 & 1 \\
\end{array}
\right]
\rightarrow
\left[
\begin{array}{cc|cc}
1 & 3 & 1 & 0 \\
0 & 1 & -2 & 1 \\
\end{array}
\right]
\rightarrow
\left[
\begin{array}{cc|cc}
1 & 0 & 7 & -3 \\
0 & 1 & -2 & 1 \\
\end{array}
\right]
$$
通过综合消元，得到了
$$
AI 
\rightarrow 
IA^{-1}
$$
同时，A的逆矩阵也是方程组的消元矩阵

