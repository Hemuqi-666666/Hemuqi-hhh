# Assignment #7: Nov Mock Exam立冬

Updated 1646 GMT+8 Nov 7, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）⽉考： AC6<mark>（请改为同学的通过数）</mark> 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E07618: 病人排队

sorttings, http://cs101.openjudge.cn/practice/07618/

思路：



代码：

```python
n=int(input())
details=[]
details_sort=[]
the_old=[]
the_young=[]
for i in range (n):
    detail_ori=input()
    ID,age=list(detail_ori.split())
    age=int(age)
    details.append((ID,age))
for detail in details:
    if int(detail[1])>=60:
        the_old.append(detail)
    else:
        the_young.append(detail)
sorted_the_old=sorted(the_old,key=lambda x:x[1],reverse=True)
details_sort=sorted_the_old+the_young
for i in range(n):
    print(details_sort[i][0],end='\n')

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image.png)




### E23555: 节省存储的矩阵乘法

implementation, matrices, http://cs101.openjudge.cn/practice/23555/

思路：



代码：

```python
n,m1,m2=map(int,input().split())
m1_matrix=[[0]*n for i in range(n)]
m2_matrix=[[0]*n for i in range(n)]
new_matrix=[[0]*n for i in range(n)]
for i in range(m1):
    x,y,v=map(int,input().split())
    m1_matrix[x][y]=v
for i in range(m2):
    x,y,v=map(int,input().split())
    m2_matrix[x][y]=v
for i in range(n):
    for j in range(n):
        for k in range(n):
            new_matrix[i][j]+=m1_matrix[i][k]*m2_matrix[k][j]
results=[]
for i in range(n):
    for j in range(n):
        if new_matrix[i][j]!=0:
            results.append(f'{i} {j} {new_matrix[i][j]}')
print(*results,sep='\n')


```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](image-1.png)




### M18182: 打怪兽 

implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/

思路：



代码：

```python
nCase=int(input())
results=[]
for j in range(nCase):
    n,m,b=map(int,input().split())
    events=[]
    for i in range(n):
        ti,xi=map(int,input().split())
        events.append((ti,xi))
    events.sort(key=lambda x: x[0])
    current_time=0
    for ti,xi in events:
        if ti>current_time:
            current_time=ti
            x_under_ti=[x for t,x in events if t==current_time]
            if m>=len(x_under_ti):
                b=b-sum(x_under_ti)
            else:
                b=b-sum(sorted(x_under_ti,reverse=True)[:m])
        if b<=0:
            result=current_time
            break
    if b>0:
        result='alive'
    results.append(result)
print(*results,sep='\n')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-2.png)




### M28780: 零钱兑换3

dp, http://cs101.openjudge.cn/practice/28780/

思路：



代码：

```python
n,m=map(int,input().split())
coins=list(map(int,input().split()))
dp=[float('inf')]*(m+1)
for i in range(1,m+1):
    if i in coins:
        dp[i]=1
    else:
        for coin in coins:
            if i-coin>=0:
                dp[i]=min(dp[i],dp[i-coin]+1)
if dp[-1]==float('inf'):
    res=-1
else:
    res=dp[-1]
print(res)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-3.png)




### T12757: 阿尔法星人翻译官

implementation, http://cs101.openjudge.cn/practice/12757

思路：



代码：

```python
sample=[str(i) for i in input().split()]
dic= {'zero':0, 'one':1, 'two':2, 'three':3, 'four':4,'five':5,
      'six':6, 'seven':7, 'eight':8, 'nine':9, 'ten':10,
      'eleven':11, 'twelve':12, 'thirteen':13, 'fourteen':14, 'fifteen':15,
      'sixteen':16, 'seventeen':17, 'eighteen':18, 'nineteen':19, 'twenty':20,
      'thirty':30, 'forty':40, 'fifty':50, 'sixty':60, 'seventy':70, 'eighty':80, 'ninety':90,
      'hundred':100, 'thousand':1000, 'million':1000000}
sign=1
if sample[0]=='negative':
    sign=-1
    del sample[0]
number=0
a=0
for i in sample:
      if i in ('million','thousand'):
            number+=a*dic[i]
            a=0
            continue
      if i=='hundred':
            a*=dic[i]
      else:
            a+=dic[i]
print(sign*(number+a))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-4.png)




### T16528: 充实的寒假生活

greedy/dp, cs10117 Final Exam, http://cs101.openjudge.cn/practice/16528/

思路：



代码：

```python
n=int(input())
activities=[]
for i in range(n):
    begin_date,end_date=map(int,input().split())
    activities.append((begin_date,end_date))
activities.sort(key=lambda x:x[0])
dp=[0]*100
for i in range(n):
    for j in range(activities[i][1],61):
        dp[j]=max(dp[j],dp[activities[i][0]-1]+1)
print(dp[60])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-5.png)




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
前四道题和assignment6比起来简单多了，一下子就做完了。。。特别是第四题和剪彩那道其实是一样的，应该算是dp里面最简单的类型了。不过还是学到了很多可以简化写法的方法，收获颇丰。
翻译官这道题有点难，我是看了答案才理解，自己根本没思路，回顾了一下字典的用法，顺便认识了一下continue的重要作用（BTW我感觉对break，return这类词的掌握还不够）
最后一题思路比较清楚，但是纠结的点是dp数组初始化的时候为什么乘61是错的但是乘65这种比较的的数是对的，老师给的解释是避免数组越界，确实是这样，经过我的尝试大于等于62就可以了，但是我还没搞懂为什么61不行。。。
以后做题初始化就稍微大一点点就可以了。。。吧。。。（小声）




