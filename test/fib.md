### LeetCode 70 爬楼梯 climbing-stairs 
https://leetcode.cn/problems/climbing-stairs/discription/   
假设你正在爬楼梯。需要 n 阶你才能到达楼顶。    
每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？    
```
int climbStairs(int n) {}
```
这个问题其实非常简单，只要找到各阶之间的数量关系即可    
即：设： f(x) 表示爬到第 x 级台阶的方案数，考虑最后一步可能跨了一级台阶，也可能跨了两级台阶，所以我们可以列出如下式子：   
**f(x)=f(x−1)+f(x−2)**，f（1）=1，f（2）=1     
这是个很明显的递归方程，而且是斐波那契数列。我们可以轻易地用递归来计算。  

### LeetCode 509 斐波那契数 fibonacci-number
https://leetcode.cn/problems/fibonacci-number/description/  
已知斐波那契数列第0项、第1项分别为0、1。求第n项的值。
``` 
int fib(int n) {}
```
这道题很明显是属于递归。   
但是这道题在递归过程中会占用较多内存，而且递归算法的时间复杂度为O(2^n)，指数级的时间复杂度,所以需要我们进行算法优化    
#### 方法一：通项公式    
斐波那契数列的通项公式为    
$$f(n)=(1/\sqrt{5})*([(1+\sqrt{5})/2]^n-[(1-\sqrt{5})/2]^n)$$
这样我们可以直接用公式推导出第n项的结果
```
    int climbStairs(int n) {
        double sqrt5 = sqrt(5);
        double fibn = pow((1 + sqrt5) / 2, n + 1) - pow((1 - sqrt5) / 2, n + 1);
        return (int)round(fibn / sqrt5);
    }
```
#### 方法二：动态规划
斐波那契数列的递推关系公式为   
$$ f(n)=f(n-1)+f(n-2) $$
由于斐波那契数存在递推关系，因此可以使用动态规划求解。   
动态规划的状态转移方程即为上述递推关系，边界条件为F(0)和F(1)   
根据状态转移方程和边界条件，可以得到时间复杂度和空间复杂度都是 O(n) 的实现。   
由于 F(n) 只和 F(n−1) 与 F(n−2) 有关，因此可以使用「滚动数组思想」把空间复杂度优化成 O(1)   
```
    int fib(int n) {
        if(n<2) return n;
        int p=0,q=0,r=1;
        for(int i=2;i<=n;++i)
        {
            p=q;
            q=r;
            r=p+q;
        }
        return r;
    }
```
总结：  
这里形成的数列正好是斐波那契数列，答案要求的 f(n) 即是斐波那契数列的第 n 项（下标从 0 开始）。   
我们来总结一下斐波那契数列第 n 项的求解方法：   
- n 比较小的时候，可以直接使用过递归法求解，不做任何记忆化操作，时间复杂度是 O(2^n)，存在很多冗余计算。   
- 一般情况下，我们使用「记忆化搜索」或者「迭代」的方法，实现这个转移方程，时间复杂度和空间复杂度都可以做到 O(n)。
- 为了优化空间复杂度，我们可以不用保存 f(x−2)f(x - 2)f(x−2) 之前的项，我们只用三个变量来维护 f(x)、f(x−1) 和 f(x−2)，你可以理解成是把「滚动数组思想」应用在了动态规划中，也可以理解成是一种递推，这样把空间复杂度优化到了 O(1)。
- 随着 n 的不断增大 O(n) 可能已经不能满足我们的需要了，我们可以用「矩阵快速幂」的方法把算法加速到 O(log⁡n)。
- 我们也可以把 n 代入斐波那契数列的通项公式计算结果，但是如果我们用浮点数计算来实现，可能会产生精度误差。

 

### rongyao 多方案爬楼梯（超级斐波那契数列）
#### 从爬楼梯的角度描述：
每次爬楼梯的步数可以为x1，x2,x3……步（xi是整型），xi一共有几个未知，由cin输入   
已知楼梯共有x阶，求解一共有多少种拼接方法   
#### 从斐波那切数列角度描述：
已知存在一个数组int x[n],求解：   
函数f(x)=f(x-x1)+f(x-x2)+f(x-x3)+……+f(x-xn)   
其中，x[i]未知，甚至数组有多少个元素都未知，由cin输入
```
#include<iostream>
#include<vector>
using namespace std;
int super_fib(int m,vector<int>& x)
{
    int n=x.size();
    vector<int> dp(m+1,0);
    dp[0]=1;
    for(int i=0;i<n;i++)
    {
        for(int j=0;j<=m;j++)
        {
            dp[j]+=dp[j-x[i]];
        }
    }
    return dp[m];
}
int main()
{
    vector<int> x;
    int a;
    int num;
    cin>>a;
    while(cin>>num)
    {
        x.push_back(num);
    }
    int ans=super_fib(a,x);
    cout<<and<<endl;
}
```






