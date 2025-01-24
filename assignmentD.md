# Assignment #D: 十全十美 

Updated 1254 GMT+8 Dec 17, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 02692: 假币问题

brute force, http://cs101.openjudge.cn/practice/02692

思路：



代码：

```python
status = [0]*12
left = ['' for _ in range(3)]
right = ['' for _ in range(3)]
result = ['' for _ in range(3)]

def Balanced():
    for j in range(3):
        leftW = rightW = 0
        for k in range(len(left[j])):
            leftW += status[ord(left[j][k]) - ord('A')]
            rightW += status[ord(right[j][k]) - ord('A')]
    
        if leftW>rightW and result[j][0]!='u':
            return False
        if leftW == rightW and result[j][0]!='e':
            return False
        if leftW<rightW and result[j][0]!='d':
            return False
    
    return True

for _ in range(int(input())):
    for i in range(3):
        left[i], right[i], result[i] = input().split()
    
    for i in range(12):
        status[i] = 0
    
    i = 0
    for i in range(12):
        status[i] = 1
        if Balanced():
            break
        
        status[i] = -1
        if Balanced():
            break
        
        status[i] = 0
    
    print('{} is the counterfeit coin and it is {}.'.format( chr(i+ord('A')), \
                    "heavy" if status[i]>0 else "light"))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-11.png)




### 01088: 滑雪

dp, dfs similar, http://cs101.openjudge.cn/practice/01088

思路：



代码：

```python
import heapq

rows, cols = map(int, input().split())
matrix = [list(map(int, input().split())) for _ in range(rows)]

# 使用最小堆存储元素及其坐标
heap = [(matrix[i][j], i, j) for i in range(rows) for j in range(cols)]
heapq.heapify(heap)

# 每个点的L值初始化为1
dp = [[1] * cols for _ in range(rows)]

# 定义方向数组，用于遍历上下左右
directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]

# 记录最长递增路径长度
longest_path = 1

# 遍历堆中的元素，按高度从小到大处理
while heap:
    height, x, y = heapq.heappop(heap)
    for dx, dy in directions:
        nx, ny = x + dx, y + dy
        if 0 <= nx < rows and 0 <= ny < cols and matrix[nx][ny] < height:
            dp[x][y] = max(dp[x][y], dp[nx][ny] + 1)
    longest_path = max(longest_path, dp[x][y])

print(longest_path)
```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](image-12.png)




### 25572: 螃蟹采蘑菇

bfs, dfs, http://cs101.openjudge.cn/practice/25572/

思路：



代码：

```python
from collections import deque

# 定义四个方向：右、下、左、上
dire = [(0, 1), (1, 0), (0, -1), (-1, 0)]

def bfs(a, x1, y1, x2, y2):
    visit = set()  # 使用集合来避免重复访问
    queue = deque([(x1, y1, x2, y2)])
    visit.add((x1, y1, x2, y2))  # 初始点加入访问集合

    while queue:
        xa, ya, xb, yb = queue.popleft()
        # 遍历四个方向
        for xi, yi in dire:
            # 计算新位置
            nx1, ny1 = xa + xi, ya + yi
            nx2, ny2 = xb + xi, yb + yi

            # 判断新位置是否合法
            if 0 <= nx1 < a and 0 <= ny1 < a and 0 <= nx2 < a and 0 <= ny2 < a:
                if (nx1, ny1, nx2, ny2) not in visit and Matrix[nx1][ny1] != 1 and Matrix[nx2][ny2] != 1:
                    # 加入队列并标记访问
                    queue.append((nx1, ny1, nx2, ny2))
                    visit.add((nx1, ny1, nx2, ny2))
                    # 检查是否到达目标
                    if Matrix[nx1][ny1] == 9 or Matrix[nx2][ny2] == 9:
                        return True
    return False

# 读取输入
a = int(input())
Matrix = [list(map(int, input().split())) for _ in range(a)]

# 找到第一个和第二个 '5' 的位置
x1, y1, x2, y2 = -1, -1, -1, -1
found_first = False

for i in range(a):
    for j in range(a):
        if Matrix[i][j] == 5:
            if not found_first:
                x1, y1 = i, j
                Matrix[i][j] = 0  # 标记为已访问
                found_first = True
            else:
                x2, y2 = i, j
                Matrix[i][j] = 0  # 标记为已访问
                break
    if x2 != -1:  # 如果第二个 5 已经找到
        break

# 运行 BFS 检查是否可以从 (x1, y1) 到 (x2, y2)
check = bfs(a, x1, y1, x2, y2)
print('yes' if check else 'no')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-13.png)




### 27373: 最大整数

dp, http://cs101.openjudge.cn/practice/27373/

思路：



代码：

```python
def f(string):
    if string=='':
        return 0
    else:
        return int(string)
m=int(input())#最大位数
n=int(input())#正整数数量
l=input().split()
#冒泡排序
for i in range(n):
    for j in range(n-1-i):
        if l[j] + l[j+1] > l[j+1] + l[j]:
            l[j],l[j+1] = l[j+1],l[j]
weight=[]#每个元素的位数
for num in l:
    weight.append(len(num))
#dp[i][j]在前i数中选择，不超过j位，最大可能数值
dp=[['']*(m+1) for _ in range(n+1)]
for k in range(m+1):
    dp[0][k]=''#无法组成整数
for q in range(n+1):
    dp[q][0]=''#无法组成整数
for i in range(1,n+1):
    for j in range(1,m+1):
        if weight[i-1]>j:#不能选第i个，因为会超位数
            dp[i][j]=dp[i-1][j]
        else:#可以选第i个也可以不选
                dp[i][j]=str(max(f(dp[i-1][j]),int(l[i-1]+dp[i-1][j-weight[i-1]])))
print(dp[n][m])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-14.png)




### 02811: 熄灯问题

brute force, http://cs101.openjudge.cn/practice/02811

思路：



代码：

```python
X = [[0,0,0,0,0,0,0,0]]
Y = [[0,0,0,0,0,0,0,0]]
for _ in range(5):
    X.append([0] + [int(x) for x in input().split()] + [0])
    Y.append([0 for x in range(8)])    
X.append([0,0,0,0,0,0,0,0])
Y.append([0,0,0,0,0,0,0,0])

import copy
for a in range(2):
    Y[1][1] = a
    for b in range(2):
        Y[1][2] = b
        for c in range(2):
            Y[1][3] = c
            for d in range(2):
                Y[1][4] = d
                for e in range(2):
                    Y[1][5] = e
                    for f in range(2):
                        Y[1][6] = f
                        
                        A = copy.deepcopy(X)
                        B = copy.deepcopy(Y)
                        for i in range(1, 7):
                            if B[1][i] == 1:
                                A[1][i] = abs(A[1][i] - 1)
                                A[1][i-1] = abs(A[1][i-1] - 1)
                                A[1][i+1] = abs(A[1][i+1] - 1)
                                A[2][i] = abs(A[2][i] - 1)
                        for i in range(2, 6):
                            for j in range(1, 7):
                                if A[i-1][j] == 1:
                                    B[i][j] = 1
                                    A[i][j] = abs(A[i][j] - 1)
                                    A[i-1][j] = abs(A[i-1][j] - 1)
                                    A[i+1][j] = abs(A[i+1][j] - 1)
                                    A[i][j-1] = abs(A[i][j-1] - 1)
                                    A[i][j+1] = abs(A[i][j+1] - 1)
                        if A[5][1]==0 and A[5][2]==0 and A[5][3]==0 and A[5][4]==0 and A[5][5]==0 and A[5][6]==0:
                            for i in range(1, 6):
                                print(" ".join(repr(y) for y in [B[i][1],B[i][2],B[i][3],B[i][4],B[i][5],B[i][6] ]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-15.png)




### 08210: 河中跳房子

binary search, greedy, http://cs101.openjudge.cn/practice/08210/

思路：



代码：

```python
L,n,m = map(int,input().split())
rock = [0]
for i in range(n):
    rock.append(int(input()))
rock.append(L)

def check(x):
    num = 0
    now = 0
    for i in range(1, n+2):
        if rock[i] - now < x:
            num += 1
        else:
            now = rock[i]
            
    if num > m:
        return True
    else:
        return False
lo, hi = 0, L+1
ans = -1
while lo < hi:
    mid = (lo + hi) // 2
    
    if check(mid):
        hi = mid
    else:               # 返回False，有可能是num==m
        ans = mid       # 如果num==m, mid可能是答案
        lo = mid + 1
        
#print(lo-1)
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-16.png)




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
正在纠结下学期还要不要报这个班的数算，感觉这个学期太摆导致和同学差的有点多。纠结。。。。




