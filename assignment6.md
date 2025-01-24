# Assignment #6: Recursion and DP

Updated 2201 GMT+8 Oct 29, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### sy119: 汉诺塔

recursion, https://sunnywhy.com/sfbj/4/3/119  

思路：



代码：

```python
def hanoi(n,A,B,C):
    if n==1:
        print(f'{A}->{C}')
        return
    hanoi(n-1,A,C,B)
    print(f'{A}->{C}')
    hanoi(n-1,B,A,C)
n=int(input())
print(2**n-1)
hanoi(n,'A','B','C')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image.png)




### sy132: 全排列I

recursion, https://sunnywhy.com/sfbj/4/3/132

思路：



代码：

```python
n=int(input())
l=[]
for i in range(1,n+1):
    l.append(f'{i}')

def arrange(l):
    if len(l)==1:
        yield l[0]
    else:
        for i in range(len(l)):
            new_l=l[:i]+l[i+1:]
            for rest in arrange(new_l):
                yield l[i] + ' ' + rest

for ans in arrange(l):
    print(ans)

```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](image-1.png)




### 02945: 拦截导弹 

dp, http://cs101.openjudge.cn/2024fallroutine/02945

思路：



代码：

```python
k=int(input())
heights=list(map(int,input().split()))

def count(heights,k):
    dp=[1]*k
    for i in range(k):
        for j in range(i):
            if heights[i]<=heights[j]:
                dp[i]=max(dp[i],dp[j]+1)
    res=max(dp)
    return res

print(count(heights,k))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-2.png)




### 23421: 小偷背包 

dp, http://cs101.openjudge.cn/practice/23421

思路：



代码：

```python
N,B=map(int,input().split())
prices=list(map(int,input().split()))
weights=list(map(int,input().split()))

dp=[[0 for _ in range(B+1)] for _ in range(N+1)]
for i in range(1,N+1):
    for w in range(1,B+1):
        if weights[i-1]>w:
            dp[i][w]=dp[i-1][w]
        else:
            dp[i][w]=max(dp[i-1][w-weights[i-1]]+prices[i-1],dp[i-1][w])
print(dp[N][B])



```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-3.png)




### 02754: 八皇后

dfs and similar, http://cs101.openjudge.cn/practice/02754

思路：



代码：

```python
def is_safe(board,x,y):
    for i in range(x):
        if board[i][y]==1:
            return False
    i=x-1
    j=y-1
    while i>=0 and j>=0:
        if board[i][j]==1:
            return False
        i-=1
        j-=1
    i=x-1
    j=y+1
    while i>=0 and j<=7:
        if board[i][j]==1:
            return False
        i-=1
        j+=1
    return True

def solve(board,x,solutions):
    if x==8:
        solutions.append([board[i].copy() for i in range(8)])
        return
    for y in range(8):
        if is_safe(board,x,y):
            board[x][y]=1
            solve(board,x+1,solutions)
            board[x][y]=0

board=[[0]*8 for _ in range(8)]
solutions=[]
solve(board,0,solutions)

s=[]
for solution in solutions:
    a=[]
    for x in range(8):
        for y in range(8):
            if solution[x][y]==1:
                a.append(y+1)
    s.append(a)

n=int(input())
no=[]
for i in range(n):
    no.append(int(input()))
for i in no:
    print(*s[i-1],sep='')

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-4.png)




### 189A. Cut Ribbon 

brute force, dp 1300 https://codeforces.com/problemset/problem/189/A

思路：



代码：

```python
n,a,b,c=map(int,input().split())
lengths=[a,b,c]
dp=[-1]*(n+1)
dp[0]=0
for i in lengths:
    if i<=n:
        dp[i]=1
for i in range(1,n+1):
    for length in lengths:
        if i>=length and dp[i-length]!=-1:
            dp[i]=max(dp[i],dp[i-length]+1)
print(dp[n])

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-5.png)




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
感觉这次作业相当难，以前没有接触过递推和dp，前面几道题目只能看答案，然后慢慢理解他们的思路是什么，感觉好大概明白了，同时也向同学请教了很多，感觉很有收获。八皇后那道题给的答案其实只是最后代码的一部分，我花了很多时间去完善整个代码，虽然中途很崩溃，还专门发了朋友圈表达我的强烈情感，但是最后完成的时候超有成就感。最后一题是我在看了取硬币的代码后自己模仿的，很快就完成了。可能掌握的还不是很扎实，可以再找点例题看看，甚至放进cheatsheet里面。




