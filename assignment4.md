# Assignment #4: T-primes + 贪心

Updated 0337 GMT+8 Oct 15, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 34B. Sale

greedy, sorting, 900, https://codeforces.com/problemset/problem/34/B



思路：



代码

```python
# 
n,m=map(int,input().split())
sets=list(map(int,input().split()))
sets.sort()
total=0
for t in sets[:m]:
    if t<0:
        total+=t
print(-total)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![alt text](image-5.png)



### 160A. Twins

greedy, sortings, 900, https://codeforces.com/problemset/problem/160/A

思路：



代码

```python
n=int(input())
coins=list(map(int,input().split()))
s=sum(coins)
coins.sort(reverse=True)
take=[]
for j in range(n):
    take.append(coins[j])
    if (sum(take)>s-sum(take)):
        break
print(j+1)


```



代码运行截图 ==（至少包含有"Accepted"）==

![alt text](image-6.png)



### 1879B. Chips on the Board

constructive algorithms, greedy, 900, https://codeforces.com/problemset/problem/1879/B

思路：



代码

```python
t=int(input())
for i in range(t):
    n=int(input())
    a=list(map(int,input().split()))
    b=list(map(int,input().split()))
    a.sort()
    b.sort()
    s1=n*a[0]+sum(b)
    s2=n*b[0]+sum(a)
    print(min(s1,s2))

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![alt text](image-7.png)



### 158B. Taxi

*special problem, greedy, implementation, 1100, https://codeforces.com/problemset/problem/158/B

思路：



代码

```python
n=int(input())
l=list(map(int,input().split()))
a=l.count(1)
b=l.count(2)
c=l.count(3)
d=l.count(4)
if c>=a:
    print(d+c+(b+1)//2)
else:
    if b%2==0:
        print(d+c+b//2+(a-c+3)//4)
    else:
        if (a-c)<=2:
            print(d+c+b//2+1)
        else:
            print(d+c+(b+1)//2+(a-c+1)//4)


```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![alt text](image-8.png)



### *230B. T-primes（选做）

binary search, implementation, math, number theory, 1300, http://codeforces.com/problemset/problem/230/B

思路：



代码

```python


```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### *12559: 最大最小整数 （选做）

greedy, strings, sortings, http://cs101.openjudge.cn/practice/12559

思路：



代码

```python


```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

感觉这次作业整体难度不大，虽然但是我选做题没看懂。感觉慢慢地我的零基础好像可以通过做题的积累变成一基础了，也许是个好事！最后真的想浅浅吐槽一下GitHub，难以打开，即便它确实是个很不错的平台。
这次很开心的一点是我debug的速度和写题目的正确率有了很大的提升，看来还是要多问问老师和助教。加油！



