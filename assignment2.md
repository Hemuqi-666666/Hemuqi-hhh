# Assignment #2: 语法练习

Updated 0126 GMT+8 Sep 24, 2024

2024 fall, Complied by ==同学的姓名、院系==



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 263A. Beautiful Matrix

https://codeforces.com/problemset/problem/263/A



思路：



##### 代码

```python
# 
matrix=[]
for i in range(0,5):
    row=input().split()
    matrix.append(row)
m=-1
n=-1
for i in range(0,5):
    for j in range(0,5):
        if (matrix[i][j]=='1'):
            m=i
            n=j
if (m!=-1 and n!=-1):
    sum=abs(2-m)+abs(2-n)
    print(int(sum))
```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](263A.png)



### 1328A. Divisibility Problem

https://codeforces.com/problemset/problem/1328/A



思路：



##### 代码

```python
# 
t=int(input())
for i in range(t):
    a,b=map(int,input().split())
    x=a%b
    if (x==0):
        print('0')
    else :
        print(b-x)
```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](1328A.png)




### 427A. Police Recruits




思路：



##### 代码

```python
# 
n=int(input())
es=list(map(int,input().split()))
available=0
waiting=0
for e in es:
    if (e>0):
        available=available+e
    elif (available>=1):
        available=available-1
    else :
        waiting=waiting+1
print(waiting)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](427A.png)




### 02808: 校门外的树

http://cs101.openjudge.cn/practice/02808/



思路：



##### 代码

```python
# 
l,n=list(map(int,input().split()))
line=[1]*(l+1)
for t in range(n):
    s,e=list(map(int,input().split()))
    for j in range(s,e+1):
        line[j]=0
print(sum(line))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](02808.png)




### sy60: 水仙花数II

https://sunnywhy.com/sfbj/3/1/60



思路：



##### 代码

```python
# 
a,b=list(map(int,input().split()))
i=[]
for n in range(a,b+1):
    s=0
    z=n%10
    y=(n%100)//10
    x=n//100
    if (n==x**3+y**3+z**3):
       i.append(n)
if len(i)==0:
    print("NO")
else :
    for j in i[:-1]:
        print(j,end=' ')
    print(i[-1])
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](sy60.png)




### 01922: Ride to School

http://cs101.openjudge.cn/practice/01922/



思路：



##### 代码

```python
# 
import math
while True:
    N=int(input())
    if (N==0):
        break
    else :
        t=[]
        for i in range(N):
            vi,ti=list(map(int,input().split()))
            if (ti>=0):
                Ti=ti+4.5/vi*3600
                t.append(math.ceil(Ti))
        if t:
            print(min(t))


```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](01922.png)




## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。==
事实上我暑假学了C++而不是python，当时选课的时候是脑子抽了选了这个导致我0基础，并且我是先做的作业2再做的作业1，一开始感觉超级难...根本不知道怎么入手的那一种。我的室友建议我先看看作业1的前两道题的答案，再慢慢摸索，确实很有效果，至少我会了一点点语言，可以写几行代码了虽然不多。然后刚开始自己写出来的东西总是有错误，而且看了半天都没看出来，最后我求助了助教，他一针见血地指出了我的问题（1和'1'的区别），真的非常感谢他，在实践和错误中我也慢慢涨了知识和经验，感受到计算概论确实是需要大量的练习才能掌握。




