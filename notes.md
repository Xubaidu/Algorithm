# 数学 07

[toc]

## 知识点

### 高斯消元

给定 $n$ 元一次线性方程组

$$
\left\{\begin{matrix}
a_{1,1}x_{1} + a_{1,2}x_{2} + .. + a_{1,n}x_{n} = b_{1}\\
a_{2,1}x_{1} + a_{2,2}x_{2} + .. + a_{2,n}x_{n} = b_{2}\\
\vdots\\
a_{n,1}x_{1} + a_{n,2}x_{2} + .. + a_{n,n}x_{n} = b_{n}\\
\end{matrix}\right.
$$

高斯消元可以在 $O(n^3)$ 时间复杂度内计算各个未知数的解，计算机会用浮点数存储答案

#### 线性代数知识回顾

在上述方程组中，未知数其实意义不大，我们主要关注系数，因此我们可以把上述的方程写成 **系数矩阵** 的形式

$$
\begin{bmatrix}
a_{1, 1} & a_{1, 2} & ... & a_{1,n}\\
a_{2, 1} & a_{2, 2} & ... & a_{2, n}\\
\vdots & \vdots & \vdots & \vdots\\
a_{n, 1} & a_{n, 2} & ... & a_{n, n}
\end{bmatrix}
$$

如果把 $b_{1},\ b_{2},\ ...,\ b_{n}$ 也添加上，便构成如下 **增广矩阵**

$$
\left[ \begin{array}{cccc|c}
a_{1, 1} & a_{1, 2} & ... & a_{1,n} & b_{1}\\
a_{2, 1} & a_{2, 2} & ... & a_{2, n} & b_{2}\\
\vdots & \vdots & \vdots & \vdots & \vdots\\
a_{n, 1} & a_{n, 2} & ... & a_{n, n} & b_{n}
\end{array} \right]
$$

高斯消元最终会把系数矩阵化为 **行阶梯矩阵**，即如下的形式

$$
\left[ \begin{array}{ccccc|c}
1 & a'_{1, 2} & a'_{1, 3} & ... & a'_{1,n} & b'_{1}\\
0 & 1 & a'_{2, 3} & ... & a'_{2, n} & b'_{2}\\
0 & 0 & 1 & ... & a'_{2, n} & b'_{3}\\
\vdots & \vdots & \vdots & \vdots & \vdots & \vdots\\
0 & 0 & ... & 1 & a'_{n - 1, n} & b'_{n - 1}\\
0 & 0 & ... & 0 & 1 & b'_{n}
\end{array} \right]
$$

我们要介绍的高斯约旦消元更是把系数矩阵化为如下形式的 **简化行阶梯矩阵**

$$
\left[ \begin{array}{ccccc|c}
1 & 0 & 0 & ... & 0 & b'_{1}\\
0 & 1 & 0 & ... & 0 & b'_{2}\\
0 & 0 & 1 & ... & 0 & b'_{3}\\
\vdots & \vdots & \vdots & \vdots & \vdots & \vdots\\
0 & 0 & ... & 1 & 0 & b'_{n - 1s}\\
0 & 0 & ... & 0 & 1 & b'_{n}
\end{array} \right]
$$


#### 从简单的方程组入手

给定二元一次方程

$$
\left\{\begin{matrix}
x + 3y = 16\\
x - 3y = 10
\end{matrix}\right.
$$

将两个方程相减，消元 $x$ 得到

$$
6y = 6
$$

从而计算出

$$
y = 1
$$

将 $y = 1$ 随意带入两个方程，都可以计算出 $x = 13$

#### 用系数矩阵表示三元一次方程组的消元过程
给定三元一次方程

$$
\left\{\begin{matrix}
x + 3y + 4z = 272\\
x - 3y - 5z = 170\\
x + 6y - 4z = 204\\
\end{matrix}\right.
$$

我们省略未知数，将其写成系数矩阵的形式，最后一列为等号右边的数值，具体如下所示

$$
\begin{bmatrix}
1 & 3 & 4 & 1\\
1 & -3 & -5 & 2\\
1 & 6 & -4 & 3
\end{bmatrix}
$$

我们手动模拟一下消元的过程

$$
\begin{aligned}
\begin{bmatrix}
1 & 3 & 4 & 1\\
1 & -3 & -5 & 2\\
1 & 6 & -4 & 3
\end{bmatrix}
& \xrightarrow[r_{3} - r_{1}]{r_{2} - r_{1}}
\begin{bmatrix}
1 & 3 & 4 & 1\\
0 & -6 & -9 & 1\\
0 & 3 & -8 & 1
\end{bmatrix}\\
& \xrightarrow[]{r_{2}\times -\frac{1}{6}}
\begin{bmatrix}
1 & 3 & 4 & 272\\
0 & 1 & \frac{3}{2} & 17\\
0 & 3 & -8 & -68
\end{bmatrix}\\
& \xrightarrow[r_{3} - 3r_{2}]{r_{1} - 3r_{2}}
\begin{bmatrix}
1 & 0 & -\frac{1}{2} & 221\\
0 & 1 & \frac{3}{2} & 17\\
0 & 0 & -\frac{17}{2} & -119
\end{bmatrix}\\
& \xrightarrow[]{r_{3}\times -\frac{2}{17}}
\begin{bmatrix}
1 & 0 & -\frac{1}{2} & 221\\
0 & 1 & \frac{3}{2} & 17\\
0 & 0 & 1 & 14
\end{bmatrix}\\
& \xrightarrow[r_{2} - \frac{3}{2}r_{3}]{r_{1} - (-\frac{1}{2})r_{3}}
\begin{bmatrix}
1 & 0 & 0 & 228\\
0 & 1 & 0 & -4\\
0 & 0 & 1 & 14
\end{bmatrix}\\
\end{aligned}
$$

从而计算出

$$
x = 228,\ y = -4,\ z = 14
$$

#### 消元法的一些优化

- 列主元，选取列中最大的元素所在行与当前行交换，这样最大程度保证精度

- 高斯约旦消元，将行阶梯矩阵继续化简为对角矩阵，这样可以直接计算出每一个未知数的结果

#### 高斯约旦消元算法

算法的步骤如下

- 枚举第 $j$ 列
  - 从第 $j + 1$ 行到第 $n$ 行，寻找 **绝对值最大** 的元素作为列主元，设其所在行为 $r$，与第 $j$ 行交换
  - 从第 $1$ 行到第 $n$ 行，把除去第 $j$ 行的每一行的第 $j$ 个元素消去，其他元素相应改变
  
注意，在寻找列主元的过程中，如果绝对值最大的元素都为 $0$ 时，则方程组无解

在计算机中，我们可以用 $\epsilon$ 来逼近 $0$

#### 高斯消元的应用

- 逆矩阵
- 矩阵树定理
- 期望 $dp$（本状态由前后状态转移而来）

### 插值

给定 $n$ 个点 $(x_{0}, y_{0}),\ (x_{1},\ y_{1}),\ (x_{2},\ y_{2}),\ ...,\ (x_{n},\ y_{n})$

可以用一个 $n$ 次多项式 $f(x)$ 来拟合这个曲线

#### 如何理解插值

插值，顾名思义，就是画一条曲线，穿针引线，把所有的值都插进去

从我们熟悉的低阶多项式理解

两点唯一确定一条直线

三点唯一确定一个抛物线

...

$n + 1$ 个点唯一确定一个 $n$ 次多项式

这样的多项式 $f(x)$ 一定 **唯一存在**，数学证明省略

#### 优秀的插值算法

具体如何还原多项式？

##### 高斯消元的局限性

直观的做法，设 $f(x) = a_{0} + a_{1}x + .. + a_{n}x^{n}$，将 $n + 1$ 个点代入，得到 $n + 1$ 元一次方程组，可以使用高斯消元在 $O(n^3)$ 时间范围内求解

不过这个时间复杂度有点高，我们需要寻求其他的办法

##### 拉格朗日插值

对每一个数对 $(x_{i},\ y_{i})$ 构造插值基函数

$$
\ell(x) = \prod_{i = 0,\ i\neq j}^{t - 1}\frac{x - x_{i}}{x_{j} - x_{i}} = \frac{x - x_{0}}{x_{j} - x_{0}}\cdot \frac{x - x_{1}}{x_{j} - x_{1}}\cdots \frac{x - x_{t - 1}}{x_{j} - x_{t - 1}}
$$

观察知道

$$
\ell(x) = \left\{\begin{matrix}
1 & x = x_{j} \\ 
0 & x\neq x_{j} 
\end{matrix}\right.
$$

进而构造拉格朗日多项式

$$
L(x) = \sum_{j=0}^{t-1} y_j \ell_j(x)
$$

由于 $f(x)$ 有且仅有一个，因此 $L(x) = f(x)$

拉格朗日插值法可以在 $O(n^2)$ 时间范围内计算答案

##### 举例理解拉格朗日插值

上述函数有点抽象，我们用例子来解释

给定二次函数 $f(x)$ 上 $3$ 个点 $(4,\ 10),\ (5,\ 8),\ (6,\ 3)$，考虑还原 $f(x)$

写出拉格朗日插值基函数

$$
\ell_{0}(x) = \frac{(x - 5)(x - 6)}{(4 - 5)(4 - 6)}$$

$$
\ell_{1}(x) = \frac{(x - 4)(x - 6)}{(5 - 4)(5 - 6)}
$$

$$
\ell_{2}(x) = \frac{(x - 4)(x - 5)}{(6 - 4)(6 - 5)}
$$

进而构造拉格朗日插值多项式

$$
\begin{aligned}
f(x) & = f(4)\cdot \ell_{0}(x) + f(5)\cdot \ell_{1}(x) + f(6)\cdot \ell_{2}(x) \\
& = 10\cdot \ell_{0}(x) + 8\cdot \ell_{1}(x) + 3\cdot \ell_{2}(x)
\end{aligned}
$$

我们可以发现，$f(4) = 10,\ f(5) = 8,\ f(6) = 1$

因此我们还原出了 $f(x)$

#### 插值的应用

求解 $\sum\limits_{i = 1}^{n}{i^k}$

## 题目选讲

### 2614. 高斯消元

#### 题意

给定一个 $n$ 元一次线性方程组，对其求解

$$
\left\{\begin{matrix}
a_{1,1}x_{1} + a_{1,2}x_{2} + .. + a_{1,n}x_{n} = b_{1}\\
a_{2,1}x_{1} + a_{2,2}x_{2} + .. + a_{2,n}x_{n} = b_{2}\\
\vdots\\
a_{n,1}x_{1} + a_{n,2}x_{2} + .. + a_{n,n}x_{n} = b_{n}\\
\end{matrix}\right.
$$

输入第一行一个数，表示 $n$

下面输入 $n$ 行，每行输入 $n + 1$ 个整数，表示 $a_{i,j}$ 和 $b_{i}$

最终输出 $1$ 行 $n$ 个数，依次表示 $x_{1},\ x_{2},\ ..,\ x_{n}$ （保留两位小数），注意行末没有空格

规定 $1\leq n\leq 100,\ |a_{i}|\leq 10^4,\ |b_{i}|\leq 10^4$

#### 题解

高斯消元模板题，直接上代码

```cpp
#include <bits/stdc++.h>
#define EPS 1e-7
using namespace std;

const int N = 1e2 + 7;
int n;
double mat[N][N], x[N];

void Gauss_jordan()
{
    for (int i = 1; i <= n; ++i) {
        // 在第 i 列寻找最大的数值作为主元
        int m = i;
        for (int j = i + 1; j <= n; ++j)
            if (fabs(mat[j][i]) > fabs(mat[m][i])) m = j;

        // 第 i 列全为 0，xi 无解
        if (fabs(mat[m][i]) < EPS) {
            printf("No Solution\n");
            return;
        }
        
        // 交换行
        if (m != i) swap(mat[i], mat[m]);

        //对每行进行消元，首项不一定为1
        for (int j = 1; j <= n; ++j)
            if (j != i) {
                double temp = mat[j][i] / mat[i][i];
                for (int k = i; k <= n + 1; ++k)
                    mat[j][k] -= temp * mat[i][k];
            }

    }
    for (int i = 1; i <= n; ++i) x[i] = mat[i][n + 1] / mat[i][i];
    for (int i = 1; i <= n; ++i) printf("%.2f%c", x[i], " \n"[i == n]);
}

int main() {
    cin >> n;
    for (int i = 1; i <= n; ++i)
        for (int j = 1; j <= n + 1; ++j)
            scanf("%lf", &mat[i][j]);
    Gauss_jordan();
    return 0;
}
```

### 2615. 拉格朗日插值

#### 题意

给定 $n$ 个点 $(x_{i},\ y_{i})$，拟合 $n - 1$ 次多项式 $f(x)$，给定 $k$，计算 $f(k)\ mod\ 998244353$

数据保证

$1\leq n\leq 10^3$

$1\leq x_{i},\ y_{i},\ k\leq 998244353$，并且 $x_{i}$ 两两不同

#### 题解

拉格朗日模板题，直接上代码

```cpp
#include <bits/stdc++.h>
typedef long long LL;
const int N = 2e3 + 7;
const int MOD = 998244353;
using namespace std;

LL qpow(LL a, LL b)
{
    if(!a) return 0;
    LL ans = 1;
    while(b) {
        if(b & 1) ans *= a, ans %= MOD;
        a *= a, a %= MOD, b >>= 1;
    }
    return ans;
}
LL inv(LL x) {return qpow(x, MOD - 2) % MOD;}
LL add(LL x, LL y) {return (x + y) % MOD;}
LL sub(LL x, LL y) {return ((x - y) % MOD + MOD) % MOD;}

LL k, n, x[N], y[N];

int main()
{
    scanf("%lld %lld", &k, &n);
    for(int i = 1; i <= k; ++i) scanf("%lld %lld", &x[i], &y[i]);
    LL res = 0;
    for(int j = 1; j <= k; ++j) {
        LL ans = y[j];
        for(int i = 1; i <= k; ++i) {
            if(i == j) continue;
            ans *= sub(n, x[i]), ans %= MOD;
            ans *= inv(sub(x[j], x[i])), ans %= MOD;
        }
        res += ans, res %= MOD;
    }
    printf("%lld\n", res);
    return 0;
}
```
