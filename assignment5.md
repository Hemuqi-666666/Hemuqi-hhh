# Assignment #5: Greedy穷举Implementation

Updated 1939 GMT+8 Oct 21, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 04148: 生理周期

brute force, http://cs101.openjudge.cn/practice/04148

思路：



代码：

```python
groups=[]
while True:
    group=list(map(int,input().split()))
    if group!=[-1,-1,-1,-1]:
        groups.append(group)
    else:
        break
for group in groups:
    j=groups.index(group)
    h=[100000]
    for i in range(1,21253):
        if (i-group[0])%23==0 and (i-group[1])%28==0 and (i-group[2])%33==0:
            h.append(i)
    if min(h)-group[3]<0:
        print(f"Case {j+1}: the next triple peak occurs in {min(h)-group[3]+21252} days.")
    else:
        print(f"Case {j+1}: the next triple peak occurs in {min(h)-group[3]} days.")
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![alt text](image-9.png)



### 18211: 军备竞赛

greedy, two pointers, http://cs101.openjudge.cn/practice/18211

思路：



代码：

```python
p=int(input())
l=list(map(int,input().split()))
l.sort()
m1=m2=0
delt=m1-m2
delts=[]
while len(l)>0 and delt>=0:
    if p>=l[0]:
        p-=l[0]
        del l[0]
        m1+=1
        delt=m1-m2
        delts.append(delt)
    else:
        p+=l[-1]
        del l[-1]
        m2+=1
        delt=m1-m2
        delts.append(delt)
print(max(max(delts),0))

```



代码运行截图 ==（至少包含有"Accepted"）==

![alt text](8dfa4bbd85f58f323a717ae9c5ffc6f.png)


### 21554: 排队做实验

greedy, http://cs101.openjudge.cn/practice/21554

思路：



代码：

```python
n=int(input())
time=list(map(int,input().split()))
time_with_indexes=[]
for i in range(n):
    time_with_index=(time[i],i+1)
    time_with_indexes.append(time_with_index)
time_with_indexes.sort(key=lambda x: (x[0],x[1]))
a=[]
total=0
for j in range(n):
    a.append(time_with_indexes[j][1])
    total+=time_with_indexes[j][0]*(n-j-1)
print(*a)
print("%.2f"%(total/n))



```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-10-3.png)




### 01008: Maya Calendar

implementation, http://cs101.openjudge.cn/practice/01008/

思路：



代码：

```python
Haab_months=['pop','no','zip','zotz','tzec','xul','yoxkin','mol','chen','yax','zac','ceh','mac','kankin','muan','pax','koyab','cumhu','uayet']
Tzolkin_names=['imix','ik','akbal','kan','chicchan','cimi','manik','lamat','muluk','ok','chuen','eb','ben','ix','mem','cib','caban','eznab','canac','ahau']

n=int(input())
Haab_dates=[]
for i in range(n):
    input_str=input()
    day,month,year=input_str.replace('.',' ').split()
    Haab_dates.append((int(day),Haab_months.index(month),int(year)))
def convert(Haab_date):
    day,month_index,year=Haab_date
    Haab_count=365*int(year)+month_index*20+day+1
    Tzolkin_year=(Haab_count//260 if Haab_count%260!=0 else Haab_count//260-1)
    Tzolkin_number=(Haab_count%260%13 if Haab_count%260%13!=0 else 13)
    Tzolkin_name=Tzolkin_names[Haab_count%260%20-1]
    return f"{Tzolkin_number} {Tzolkin_name} {Tzolkin_year}"

print(n)
for i in range(n):
    print(convert(Haab_dates[i]))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![alt text](image-12.png)



### 545C. Woodcutters

dp, greedy, 1500, https://codeforces.com/problemset/problem/545/C

思路：



代码：

```python
n=int(input())
a=[]
for _ in range(n):
    t=list(map(int,input().split()))
    a.append(t)
a.sort()
s=0
if n==1 or n==2:
    print(n)
else:
    for i in range(1,n-1):
        if a[i][1]<a[i][0]-a[i-1][0]:
            s+=1
        elif i<n-1 and a[i][1]<a[i+1][0]-a[i][0]:
            s+=1
            a[i][0]=a[i][0]+a[i][1]
        else:
            continue
    print(s+2)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![alt text](image-13.png)



### 01328: Radar Installation

greedy, http://cs101.openjudge.cn/practice/01328/

思路：



代码：

```python
import math
def solve(n,d,samples):
    lst=[]
    res=0
    ri=-float('inf')
    for x,y in samples:
        if y>d:
            return -1
        r=(d**2-y**2)**0.5
        lst.append((x-r,x+r))
        lst.sort()
    for i in lst:
        ri=min(ri,i[1])
        if i[0]>ri:
            res+=1
    return res

case_number=0
while True:
    n,d=map(int,input().split())
    if n==0 and d==0:
        break
    case_number+=1
    samples=[]
    for _ in range(n):
        samples.append(list(map(int,input().split())))
    result=solve(n,d,samples)
    print(f'Case {case_number}: {result}')
    input()

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>
![alt text](image-14.png)




## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>
做了这次作业感觉写代码已经快了很多，但是总是想不到好的思路，debug也要弄很久。特别是最后一题，我至今都没弄明白我原来的思路到底有什么问题，拼尽全力无法战胜，最后妥协了，充满了悲剧色彩的英雄主义。
还是把原来的代码paste在这里，作为今天整个下午的纪念。
import math
def solve(n,d,samples):
    samples.sort(key=lambda x:x[1])
    if samples[0][1]>d:
        return -1
    else:
        samples.sort(key=lambda x:x[0])
        intervals=[]
        events=[]
        for i in range(n):
            interval_left=samples[i][0]-math.sqrt(d**2-samples[i][1]**2)
            interval_right=samples[i][0]+math.sqrt(d**2-samples[i][1]**2)
            intervals.append((interval_left,interval_right))
        for interval in intervals:
            events.append((interval[0],1))
            events.append((interval[1],-1))
        current_overlap=0
        overlap_count=0
        events.sort(key=lambda x: (x[0], -x[1]))
        for point,flag in events:
            current_overlap+=flag
            if current_overlap>1:
                overlap_count+=1
        return n-overlap_count
case_number=0
while True:
    n,d=map(int,input().split())
    if n==0 and d==0:
        break
    case_number+=1
    samples=[]
    for _ in range(n):
        samples.append(list(map(int,input().split())))
    result=solve(n,d,samples)
    print(f'Case {case_number}: {result}')
    input()




