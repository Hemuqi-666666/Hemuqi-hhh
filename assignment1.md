# Assignment #1: 自主学习

Updated 0110 GMT+8 Sep 10, 2024

2024 fall, Complied by ==同学的姓名、院系==



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 02733: 判断闰年

http://cs101.openjudge.cn/practice/02733/



思路：



##### 代码

```python
# 
year=int(input())
if (year%4!=0 or (year%100==0 and year%400!=0)or year%3200==0):
    print("N")
else :
    print("Y")
```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](02733.png)




### 02750: 鸡兔同笼

http://cs101.openjudge.cn/practice/02750/



思路：



##### 代码

```python
# 
num_feet=int(input())
if (num_feet%2!=0):
    print("{} {}".format(0,0))
elif (num_feet%4==0):
    print("{} {}".format(int(num_feet/4),int(num_feet/2)))
else :
    print("{} {}".format(num_feet//4+1,int(num_feet/2)))

```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](02750.png)




### 50A. Domino piling

greedy, math, 800, http://codeforces.com/problemset/problem/50/A



思路：



##### 代码

```python
# 
M,N=list(map(int,input().split()))
if (M*N%2==0):
    print(M*N//2)
else :
    print(M*N//2)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](50A.png)




### 1A. Theatre Square

math, 1000, https://codeforces.com/problemset/problem/1/A



思路：



##### 代码

```python
# 
m,n,a=list(map(int,input().split()))
if (m%a==0):
    x=m//a
else:
    x=m//a+1
if (n%a==0):
    y=n//a
else:
    y=n//a+1
print(x*y)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](1A.png)




### 112A. Petya and Strings

implementation, strings, 1000, http://codeforces.com/problemset/problem/112/A



思路：



##### 代码

```python
# 
string1=input().lower()
string2=input().lower()
l=len(string1)
for i in range(l):
    if (string1[i]>string2[i]):
        print('1')
        break
    elif (string1[i]<string2[i]):
        print('-1')
        break
    else :
        if (string1[i]==string2[i] and string1==string2):
            print('0')
            break

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](112A.png)




### 231A. Team

bruteforce, greedy, 800, http://codeforces.com/problemset/problem/231/A



思路：



##### 代码

```python
# 
n=int(input())
b=0
for i in range(n):
    a=list(map(int,input().split()))
    if (sum(a)>=2):
        b+=1
print(b)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](231A.png)




## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。==
事实上我暑假学了C++而不是python，当时选课的时候是脑子抽了选了这个导致我0基础，并且我是先做的作业2再做的作业1，一开始感觉超级难...根本不知道怎么入手的那一种。我的室友建议我先看看作业1的前两道题的答案，再慢慢摸索，确实很有效果，至少我会了一点点语言，可以写几行代码了虽然不多。然后刚开始自己写出来的东西总是有错误，而且看了半天都没看出来，最后我求助了助教，他一针见血地指出了我的问题（1和'1'的区别），真的非常感谢他，在实践和错误中我也慢慢涨了知识和经验，感受到计算概论确实是需要大量的练习才能掌握。
