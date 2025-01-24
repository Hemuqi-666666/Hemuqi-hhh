# Assignment #A: dp & bfs

Updated 2 GMT+8 Nov 25, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### LuoguP1255 数楼梯

dp, bfs, https://www.luogu.com.cn/problem/P1255

思路：



代码：

```python
n=int(input())

def solve(n):
    dp=[0]*(n+1)
    dp[0]=1
    dp[1]=1
    if n==0:
        return 1
    if n==1:
        return 1
    else:
        for i in range(2,n+1):
            dp[i]=dp[i-1]+dp[i-2]
        return dp[n]
print(solve(n))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-3.png)




### 27528: 跳台阶

dp, http://cs101.openjudge.cn/practice/27528/

思路：



代码：

```python
n=int(input())

def solve(n):
    dp=[0]*(n+1)
    dp[0]=1
    dp[1]=1
    for i in range(2,n+1):
        dp[i]=sum(dp[:i])
    return dp[n]
print(solve(n))
```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](image-4.png)




### 474D. Flowers

dp, https://codeforces.com/problemset/problem/474/D

思路：



代码：

```python
MAX = 1000000007
t, k = map(int, input().split())
MOD = int(1e9+7)
MAXN = 100001
dp = [0]*MAXN
s = [0]*MAXN
dp[0] = 1
s[0] = 1
for i in range(1, MAXN):
    if i >= k:
        dp[i] = (dp[i-1]+dp[i-k]) % MOD
    else:
        dp[i] = dp[i-1] % MOD
    s[i] = (s[i-1]+dp[i]) % MOD

for _ in range(t):
    a, b = map(int, input().split())
    print((s[b]-s[a-1]+MOD) % MOD)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-6.png)




### LeetCode5.最长回文子串

dp, two pointers, string, https://leetcode.cn/problems/longest-palindromic-substring/

思路：



代码：

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n = len(s)
        if n == 0:
            return ""
        dp = [[False] * n for _ in range(n)]
        start, max_length = 0, 1
        for i in range(n):
            dp[i][i] = True
        for i in range(n - 1):
            if s[i] == s[i + 1]:
                dp[i][i + 1] = True
                start = i
                max_length = 2
        for length in range(3, n + 1):
            for i in range(n - length + 1):
                j = i + length - 1
                if s[i] == s[j] and dp[i + 1][j - 1]==True:
                    dp[i][j] = True
                    start = i
                    max_length = length

        return s[start:start + max_length]

if __name__ == "__main__":
    sol = Solution()
    print(sol.longestPalindrome("babad"))  
    print(sol.longestPalindrome("cbbd"))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-5.png)






### 12029: 水淹七军

bfs, dfs, http://cs101.openjudge.cn/practice/12029/

思路：



代码：

```python
K=int(input())
dirs=[[-1,0],[1,0],[0,-1],[0,1]]
water_height=0
real_height=0
def dfs(board,x,y,water_height,real_height):
    for point in points:
        dp[x][y]=board[x][y]
        water_height=dp[x][y]
        for dir in dirs:
            dx=x+dir[0]
            dy=y+dir[1]
            if 0<=dx<M and 0<=dy<N and board[dx][dy]<water_height:
                dfs(board,dx,dy,water_height,real_height)
            if dp[dx][dy]:
                realheight=max(real_height,dp[dx][dy])

for _ in range(K):
    M,N=map(int,input().split())
    board=[[0]*(N+2) for _ in range(M+2)]
    for i in range(1,M+1):
        board[i][1:-1]=list(map(int,input().split()))
    dp=[[False]*(M+2) for _ in range(M+2)]
    goal=list(map(int,input().split()))
    p=int(input())
    points=[]
    for _ in range(p):
        x,y=map(int,input().split())
        points.append((x,y))
        dfs(board,x,y,water_height,real_height)

    if dp[goal[0]][goal[1]]:
        print('YES')
    else:
        print('NO')

    #自己写的代码，然后RE了，看群里讨论应该是要引入sys，但是我不太会，就单纯学习一下吧。。。截图将是提交答案版
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-7.png)




### 02802: 小游戏

bfs, http://cs101.openjudge.cn/practice/02802/

思路：



代码：

```python
from collections import deque
from collections import defaultdict

def bfs(start, end, grid, h, w):
    queue = deque([start])
    in_queue = defaultdict(lambda: float('inf'))
    dirs = [(0, -1), (-1, 0), (0, 1), (1, 0)]
    min_x = float('inf')
    while queue:
        x, y, d, seg = queue.popleft()

        for i, (dx, dy) in enumerate(dirs):
            nx, ny = x + dx, y + dy

            new_seg = seg if i == d else seg + 1
            if (nx, ny) == end:
                min_x = min(min_x, new_seg)
                continue

            if (0 <= nx < h + 2 and 0 <= ny < w + 2 and new_seg<in_queue[(nx,ny,i)]
                    and grid[nx][ny] != 'X'):
                    in_queue[(nx, ny, i)] = new_seg
                    queue.append((nx, ny, i, new_seg))

    return min_x


board_num = 1
while True:
    w, h = map(int, input().split())
    if w == h == 0:
        break

    grid = [' ' * (w + 2)] + [' ' + input() + ' ' for _ in range(h)] + [' ' * (w + 2)]
    print(f"Board #{board_num}:")
    pair_num = 1
    while True:
        y1, x1, y2, x2 = map(int, input().split())
        if x1 == y1 == x2 == y2 == 0:
            break

        start = (x1, y1, -1, 0)
        end = (x2, y2)

        seg = bfs(start, end, grid, h, w)
        if seg == float('inf'):
            print(f"Pair {pair_num}: impossible.")
        else:
            print(f"Pair {pair_num}: {seg} segments.")
        pair_num += 1

    print()
    board_num += 1
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-8.png)




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

前两题简单。flower感觉和前两题没什么区别，就是容易超时，学习了一下答案的方法
回文序列那道题不太清楚平台的机制，但是还是学到了判断的方法，现在对dp数组什么时候用一元什么时候用二元有了进一步的认识。
最后两题难，已经失去思考的能力。





