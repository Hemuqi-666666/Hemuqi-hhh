# Assignment #C: 五味杂陈 

Updated 1148 GMT+8 Dec 10, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 1115. 取石子游戏

dfs, https://www.acwing.com/problem/content/description/1117/

思路：



代码：

```python
import math

def wythoff(a, b):
    if a > b:
        a, b = b, a  # Make sure a <= b.
    k = b - a
    ak = k * (math.sqrt(5) + 1) / 2  # ak is the k-th element in the Beatty sequence.
    return 1 if a != int(ak) else 0

while True:
    try:
        a, b = map(int, input().split())
    except:
        break

    ans = wythoff(a, b)

    print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-6.png)




### 25570: 洋葱

Matrices, http://cs101.openjudge.cn/practice/25570

思路：



代码：

```python
DIRECTIONS = ((0, 1), (1, 0), (0, -1), (-1, 0))
n = int(input())
N = 0
onion = [[-1e9 for i in range(n + 2)]] + [[-1e9] + list(map(int, input().split())) + [-1e9] for i in range(n)] + [[-1e9 for i in range(n + 2)]]
dx, dy = DIRECTIONS[0]
x, y = 1, 0
layer = [0 for i in range(n // 2 + 1)]
for i in range(1, 1 + n * n):
    if onion[x + dx][y + dy] == -1e9:
        N += 1
        dx, dy = DIRECTIONS[N % 4]
    x, y = x + dx, y + dy
    layer[N // 4] += onion[x][y]
    onion[x][y] = -1e9
print(max(layer))
```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](image-7.png)




### 1526C1. Potions(Easy Version)

greedy, dp, data structures, brute force, *1500, https://codeforces.com/problemset/problem/1526/C1

思路：



代码：

```python
import heapq


def max_potions(n, potions):
    # 当前健康值
    health = 0
    # 已经饮用的药水效果列表，用作最小堆
    consumed = []

    for potion in potions:
        # 尝试饮用当前药水
        health += potion
        heapq.heappush(consumed, potion)
        if health < 0:
            # 如果饮用后健康值为负，且堆中有元素
            if consumed:
                health -= consumed[0]
                heapq.heappop(consumed)


    return len(consumed)

n = int(input())
potions = list(map(int, input().split()))
print(max_potions(n, potions))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-8.png)




### 22067: 快速堆猪

辅助栈，http://cs101.openjudge.cn/practice/22067/

思路：



代码：

```python
class MinStack:
    def __init__(self):
        self.stack = []          # 主栈
        self.min_stack = []      # 辅助栈，用来保存每个状态下的最小值

    def push(self, x):
        self.stack.append(x)
        if not self.min_stack or x <= self.min_stack[-1]:
            self.min_stack.append(x)

    def pop(self):
        if self.stack:  # 如果主栈非空才执行pop
            top = self.stack.pop()
            if top == self.min_stack[-1]:
                self.min_stack.pop()

    def min(self):
        if self.min_stack:
            return self.min_stack[-1]
        else:
            return None  # 栈为空时返回None

# 使用 MinStack 类
min_stack = MinStack()

while True:
    try:
        command = input().strip()
        if command.startswith('push'):
            value = int(command.split()[1])
            min_stack.push(value)
        elif command.startswith('pop'):
            min_stack.pop()  # 空栈时不进行任何操作
        elif command.startswith('min'):
            min_value = min_stack.min()
            if min_value is not None:
                print(min_value)  # 只有在栈非空时才打印最小值
    except EOFError:
        break
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-9.png)




### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/

思路：



代码：

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### 04129: 变换的迷宫

bfs, http://cs101.openjudge.cn/practice/04129/

思路：



代码：

```python
import heapq
from math import inf

# 四个基本方向：右、下、左、上
DIRECTIONS = [(0, 1), (1, 0), (-1, 0), (0, -1)]

def find_shortest_path(grid, start, end, dimensions, cycle_length):
    """
    寻找从起点到终点的最短路径。
    
    :param grid: 地图信息（0为空地，1为石头）
    :param start: 起点坐标 (x, y)
    :param end: 终点坐标 (x, y)
    :param dimensions: 地图尺寸 (rows, cols)
    :param cycle_length: 穿过石头的时间周期
    :return: 最短时间或 "Oop!" 表示无法到达
    """
    rows, cols = dimensions
    visited = [[[False] * cols for _ in range(rows)] for _ in range(cycle_length)]
    priority_queue = [(0,) + start]  # 初始时间为0加上起点坐标
    
    while priority_queue:
        time, x, y = heapq.heappop(priority_queue)
        if (x, y) == end:  # 到达终点
            return time
        
        for dx, dy in DIRECTIONS:
            nx, ny = x + dx, y + dy
            new_time = time + 1
            
            if not (0 <= nx < rows and 0 <= ny < cols):  # 检查是否在地图内
                continue
                
            if grid[nx][ny] == 1 and new_time % cycle_length == 0 and not visited[new_time % cycle_length][nx][ny]:  # 穿石头
                visited[new_time % cycle_length][nx][ny] = True
                heapq.heappush(priority_queue, (new_time, nx, ny))
            elif grid[nx][ny] == 0 and not visited[new_time % cycle_length][nx][ny]:  # 普通空地
                visited[new_time % cycle_length][nx][ny] = True
                heapq.heappush(priority_queue, (new_time, nx, ny))
                
    return "Oop!"

def main():
    test_cases = int(input())
    results = []
    
    for _ in range(test_cases):
        rows, cols, cycle_length = map(int, input().split())
        grid = []
        start = None
        end = None
        
        for i in range(rows):
            line = input()
            row = []
            for j, char in enumerate(line):
                if char == "S":
                    start = (i, j)
                    row.append(0)  # 起点当空地
                elif char == "E":
                    end = (i, j)
                    row.append(0)  # 终点当空地
                elif char == "#":
                    row.append(1)  # 石头
                else:
                    row.append(0)  # 空地
            grid.append(row)
            
        result = find_shortest_path(grid, start, end, (rows, cols), cycle_length)
        results.append(result)

    for result in results:
        print(result)

if __name__ == "__main__":
    main()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-10.png)




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
正在纠结下学期还要不要报这个班的数算，感觉这个学期太摆导致和同学差的有点多。纠结。。。。





