# Assignment #B: Dec Mock Exam大雪前一天

Updated 1649 GMT+8 Dec 5, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）⽉考： AC6<mark>（请改为同学的通过数）</mark> 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E22548: 机智的股民老张

http://cs101.openjudge.cn/practice/22548/

思路：



代码：

```python
*a, = map(int, input().split())
min_price = float('inf')
max_profit = 0

for price in a:
    min_price = min(min_price, price)  # 更新最小值
    max_profit = max(max_profit, price - min_price)  # 更新最大利润

print(max_profit)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image.png)




### M28701: 炸鸡排

greedy, http://cs101.openjudge.cn/practice/28701/

思路：



代码：

```python
n, k = map(int, input().split())
t = list(map(int, input().split()))
t.sort()
s = sum(t)
while True:
    if t[-1] > s / k:
        s -= t.pop()
        k -= 1
    else:
        print(f'{s / k:.3f}')
        break
```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](image-1.png)




### M20744: 土豪购物

dp, http://cs101.openjudge.cn/practice/20744/

思路：



代码：

```python
a=list(map(int,input().split(",")))
n=len(a)
dp1,dp2=a[0],a[0]
ans=0
for i in range(1,n):
    dp1,dp2=max(a[i],dp1+a[i]),max(dp1,dp2+a[i])
    ans=max(ans,dp2)
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-2.png)




### T25561: 2022决战双十一

brute force, dfs, http://cs101.openjudge.cn/practice/25561/

思路：



代码：

```python
# 张俊龙，工学院
result = float("inf")
n, m = map(int, input().split())
store_prices = [input().split() for _ in range(n)]
you= [input().split() for _ in range(m)]
la=[0]*m
def dfs(i,sum1):
    global result
    if i==n:
        jian=0
        for i2 in range(m):
            store_j=0
            for k in you[i2]:
                a,b=map(int,k.split('-'))
                if la[i2]>=a:
                    store_j=max(store_j,b)
            jian+=store_j
        result=min(result,sum1-(sum1//300)*50-jian)
        return
    for i1 in store_prices[i]:
        idx,p=map(int,i1.split(':'))
        la[idx-1]+=p
        dfs(i+1,sum1+p)
        la[idx-1]-=p
dfs(0,0)
print(result)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-3.png)




### T20741: 两座孤岛最短距离

dfs, bfs, http://cs101.openjudge.cn/practice/20741/

思路：



代码：

```python
from collections import deque

def dfs(x, y, grid, n, queue, directions):
    """ Mark the connected component starting from (x, y) as visited using DFS. """
    grid[x][y] = 2  # Mark as visited
    queue.append((x, y))
    for dx, dy in directions:
        nx, ny = x + dx, y + dy
        if 0 <= nx < n and 0 <= ny < n and grid[nx][ny] == 1:
            dfs(nx, ny, grid, n, queue, directions)

def bfs(grid, n, queue, directions):
    """ Perform BFS to find the shortest path to another component. """
    distance = 0
    while queue:
        for _ in range(len(queue)):
            x, y = queue.popleft()
            for dx, dy in directions:
                nx, ny = x + dx, y + dy
                if 0 <= nx < n and 0 <= ny < n:
                    if grid[nx][ny] == 1:
                        return distance
                    elif grid[nx][ny] == 0:
                        grid[nx][ny] = 2  # Mark as visited
                        queue.append((nx, ny))
        distance += 1
    return distance

def main():
    n = int(input())
    grid = [list(map(int, input())) for _ in range(n)]
    directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
    queue = deque()

    # Start DFS from the first '1' found and use BFS from there
    for i in range(n):
        for j in range(n):
            if grid[i][j] == 1:
                dfs(i, j, grid, n, queue, directions)
                return bfs(grid, n, queue, directions)

if __name__ == "__main__":
    print(main())
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-5.png)




### T28776: 国王游戏

greedy, http://cs101.openjudge.cn/practice/28776

思路：



代码：

```python
from typing import List
def Solution(n:int, a:int, b:int, lst:List[List]) -> int:
    lst.sort(key=lambda x: (x[0] * x[1]))
    ans = 0
    for i in range(n):
        ans = max(ans, a // lst[i][1])
        a *= lst[i][0]
    return ans
if __name__ == "__main__":
    n = int(input())
    a, b = map(int, input().split())
    lst = []
    for i in range(n):
        lst.append([int(_) for _ in input().split()])
    # 时间复杂度O(nlogn)，空间复杂度O(n)

    print(Solution(n, a, b, lst))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-4.png)




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
正在纠结下学期还要不要报这个班的数算，感觉这个学期太摆导致和同学差的有点多。纠结。。。。




