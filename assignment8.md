# Assignment #8: 田忌赛马来了

Updated 1021 GMT+8 Nov 12, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 12558: 岛屿周⻓

matices, http://cs101.openjudge.cn/practice/12558/ 

思路：



代码：

```python
n,m=map(int,input().split())
matrix=[[0]*(m+2)]

for _ in range(n):
    row=([0]+list(map(int,input().split()))+[0])
    matrix.append(row)
matrix.append([0]*(m+2))
count=0
for x in range(n+1):
    for y in range(m+1):
        surround=matrix[x][y-1]+matrix[x][y+1]+matrix[x-1][y]+matrix[x+1][y]
        if matrix[x][y]==1:
            if surround==1:
                count+=3
            if surround==2:
                count+=2
            if surround==3:
                count+=1
            if surround==4:
                count+=0
print(count)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image.png)




### LeetCode54.螺旋矩阵

matrice, https://leetcode.cn/problems/spiral-matrix/

与OJ这个题目一样的 18106: 螺旋矩阵，http://cs101.openjudge.cn/practice/18106

思路：



代码：

```python
n=int(input())
m=[[0]*n for _ in range(n)]
count=0
for t in range(n):
    count+=1
    m[0][t]=count
x=1
y=n
k=n-1
while k>0:
    for _ in range(k):
        x+=1
        count+=1
        m[x-1][y-1]=count
    for _ in range(k):
        y-=1
        count+=1
        m[x-1][y-1]=count
    k-=1
    for _ in range(k):
        x-=1
        count+=1
        m[x-1][y-1]=count
    for _ in range(k):
        y+=1
        count+=1
        m[x-1][y-1]=count
    k-=1
for i in range(n):
    print(*m[i])
```



代码运行截图 ==（至少包含有"Accepted"）==

![alt text](image-1.png)




### 04133:垃圾炸弹

matrices, http://cs101.openjudge.cn/practice/04133/

思路：



代码：

```python
d=int(input())
n=int(input())
m=[[0]*1025 for _ in range(1025)]
for _ in range(n):
    x,y,k=map(int,input().split())
    for i in range(max(x-d,0),min(x+d+1,1025)):
        for j in range(max(y-d,0),min(y+d+1,1025)):
            m[i][j]+=k
max_m=max(max(l) for l in m)
num_m=sum(l.count(max_m) for l in m)
print(num_m,max_m)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-2.png)




### LeetCode376.摆动序列

greedy, dp, https://leetcode.cn/problems/wiggle-subsequence/

与OJ这个题目一样的，26976:摆动序列, http://cs101.openjudge.cn/routine/26976/

思路：



代码：

```python
n=int(input())
l=list(map(int,input().split()))
dp=[[1,1] for _ in range(n)]
for i in range(1,n):
    if l[i]<l[i-1]:
        dp[i][0]=dp[i-1][1]+1
        dp[i][1]=dp[i-1][1]
    elif l[i]>l[i-1]:
        dp[i][1]=dp[i-1][0]+1
        dp[i][0]=dp[i-1][0]
    else:
        dp[i][1]=dp[i-1][1]
        dp[i][0]=dp[i-1][0]
print(max(dp[n-1][0],dp[n-1][1]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-3.png)




### CF455A: Boredom

dp, 1500, https://codeforces.com/contest/455/problem/A

思路：



代码：

```python
n=int(input())
a=list(map(int,input().split()))
count=[0]*(int(1e5)+1)
for i in a:
    count[i]+=1
dp=[[0,0] for _ in range(int(1e5)+1)]
for i in range(1,int(1e5)+1):
    dp[i][0]=max(dp[i-1][1],dp[i-1][0])
    dp[i][1]=dp[i-1][0]+i*count[i]
print(max(dp[int(1e5)][0],dp[int(1e5)][1]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-4.png)




### 02287: Tian Ji -- The Horse Racing

greedy, dfs http://cs101.openjudge.cn/practice/02287

思路：



代码：

```python
while True:
    n=int(input())
    if n==0:
        break
    a=list(map(int,input().split()))
    b=list(map(int,input().split()))
    a.sort(reverse=True)
    b.sort(reverse=True)
    dp=[[0]*(n+1) for _ in range(n+1)]#田用前i匹，王用前j匹，田赢的最大次数
    #记赢一局+2，输一局0，平局+1
    for i in range(1,n+1):
        for j in range(1,n+1):
            if a[i-1]>b[j-1]:#比较田第i匹和王第j匹
                dp[i][j]=max(dp[i-1][j],dp[i][j-1],dp[i-1][j-1]+2)
            if a[i-1]==b[j-1]:
                dp[i][j]=max(dp[i-1][j],dp[i][j-1],dp[i-1][j-1]+1)
            if a[i-1]<b[j-1]:
                dp[i][j]=max(dp[i-1][j],dp[i][j-1],dp[i-1][j-1])
    print(200*(dp[n][n]-n))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-5.png)




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

写螺旋矩阵那道题发现一个很有意思的点，初始化一个全为0的矩阵不能用[[0]*n]*n,生成出来的矩阵在对里面的元素进行赋值之后，矩阵的每一行都是一样的。
所以要用m=[[0]*n for _ in range(n)]
中间两道题感觉比较相似，都是要考虑不取和取两种情况，所以dp是一个二元数组。
田忌赛马那道题我只想到了用dp的方法做，不过一开始我一直是认为赢一局+1，输一局-1，平局+0，最后结果一直不对，后面看了题解才理解应该是+2、+0、+1，也算是一点积累。





