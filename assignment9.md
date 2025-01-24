# Assignment #9: dfs, bfs, & dp

Updated 2107 GMT+8 Nov 19, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 18160: 最大连通域面积

dfs similar, http://cs101.openjudge.cn/practice/18160

思路：



代码：

```python
direction=[[-1,-1],[-1,0],[-1,1],[0,-1],[0,1],[1,-1],[1,0],[1,1]]
area=0
def dfs(x,y):
    global area
    if m[x][y]=='.':
        return
    if m[x][y]=='W':
        m[x][y]='.'
        area+=1
        for i in direction:
            dfs(x+i[0],y+i[1])

T=int(input())
for _ in range(T):
    N,M=map(int,input().split())
    m=[['.']*(M+2) for _ in range(N+2)]
    for i in range(1,N+1):
        m[i][1:-1]=input()

    count=0
    for i in range(1,N+1):
        for j in range(1,M+1):
            if m[i][j]=='W':
                area=0
                dfs(i,j)
                count=max(count,area)

    print(count)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image.png)




### 19930: 寻宝

bfs, http://cs101.openjudge.cn/practice/19930

思路：



代码：

```python
import heapq
def bfs(x, y):
    d = [[-1, 0], [1, 0], [0, 1], [0, -1]]
    queue = []
    heapq.heappush(queue, [0, x, y])
    check = set()
    check.add((x, y))
    while queue:
        step, x, y = map(int, heapq.heappop(queue))
        if martix[x][y] == 1:
            return step
        for i in range(4):
            dx, dy = x + d[i][0], y + d[i][1]
            if martix[dx][dy] != 2 and (dx, dy) not in check:
                heapq.heappush(queue, [step + 1, dx, dy])
                check.add((dx, dy))
    return "NO"


m, n = map(int, input().split())
martix = [[2] * (n + 2)] + [[2] + list(map(int, input().split())) + [2] for i in range(m)] + [[2] * (n + 2)]
print(bfs(1, 1))
```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](image-1.png)




### 04123: 马走日

dfs, http://cs101.openjudge.cn/practice/04123

思路：



代码：

```python
maxn = 10;
sx = [-2,-1,1,2, 2, 1,-1,-2]
sy = [ 1, 2,2,1,-1,-2,-2,-1]

ans = 0;
 
def Dfs(dep: int, x: int, y: int):
    #是否已经全部走完
    if n*m == dep:
        global ans
        ans += 1
        return
    
    #对于每个可以走的点
    for r in range(8):
        s = x + sx[r]
        t = y + sy[r]
        if chess[s][t]==False and 0<=s<n and 0<=t<m :
            chess[s][t]=True
            Dfs(dep+1, s, t)
            chess[s][t] = False; #回溯
 

for _ in range(int(input())):
    n,m,x,y = map(int, input().split())
    chess = [[False]*maxn for _ in range(maxn)]  #False表示没有走过
    ans = 0
    chess[x][y] = True
    Dfs(1, x, y)
    print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-2.png)




### sy316: 矩阵最大权值路径

dfs, https://sunnywhy.com/sfbj/8/1/316

思路：



代码：

```python
def dfs(x, y, now_value):
    global max_value, opt_path
    # 如果到达右下角，更新最大权值和最优路径
    if x == n - 1 and y == m - 1:
        if now_value > max_value:
            max_value = now_value
            opt_path = temp_path[:]
        return
    
    # 标记当前位置为已访问
    visited[x][y] = True
    
    # 尝试向四个方向移动
    for dx, dy in directions:
        next_x, next_y = x + dx, y + dy
        if 0 <= next_x < n and 0 <= next_y < m and not visited[next_x][next_y]:
            next_value = now_value + maze[next_x][next_y]
            temp_path.append((next_x, next_y))
            dfs(next_x, next_y, next_value)
            temp_path.pop()  # 回溯
    
    # 取消当前位置的访问标记
    visited[x][y] = False

# 读取输入
n, m = map(int, input().split())
maze = [list(map(int, input().split())) for _ in range(n)]

# 初始化变量
max_value = float('-inf')
opt_path = []
temp_path = [(0, 0)]
visited = [[False] * m for _ in range(n)]
directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]

# 从左上角开始DFS搜索
dfs(0, 0, maze[0][0])

# 输出最优路径
for x, y in opt_path:
    print(x + 1, y + 1)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-9.png)






### LeetCode62.不同路径

dp, https://leetcode.cn/problems/unique-paths/

思路：



代码：

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        mi = min(m-1, n-1)
        if not mi:
            return 1
        else:
            methods = 1
            for i in range(mi):
                methods *= (m+n-2-i)
            for i in range(mi):
                methods = methods//(i+1)   
            return methods
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-10.png)




### sy358: 受到祝福的平方

dfs, dp, https://sunnywhy.com/sfbj/8/3/539

思路：



代码：

```python
def is_blessed_id(A):
    # 预处理所有可能的平方数
    squares = set()
    i = 1
    while i * i <= 10**9:
        squares.add(i * i)
        i += 1
    
    # 将数字A转换为数字列表
    digits = list(map(int, str(A)))
    
    # DFS函数，判断是否可以分割成平方数
    def dfs(idx):
        if idx == len(digits):
            return True
        
        num = 0
        for i in range(idx, len(digits)):
            num = num * 10 + digits[i]
            if num in squares:
                if dfs(i + 1):
                    return True
        return False
    
    # 调用DFS函数，判断是否可以分割成平方数
    return "Yes" if dfs(0) else "No"

# 读取输入
A = int(input())
# 输出结果
print(is_blessed_id(A))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-11.png)




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

连通陆地问题挺有意思的，第一次接触DFS，感觉应该可以减少很多计算时间，同时还学到了global的用法，不过不知道为什么我一开始提交总是有CE，直到我在最前面加了area=0，那我的global是干啥用的。。。
寻宝题没思路，其实我一开始想到的是用dp，但是感觉会很麻烦。。。直接看的答案，学了heapq，但是不会用。。。但至少还是学了怎么避免重复访问相同的节点，也算是有收获(?)
马走日写了，感觉没什么问题，就是不对，遂复制粘贴。注意回溯。
不喜欢用leetcode写题，感觉像是写八股文。







