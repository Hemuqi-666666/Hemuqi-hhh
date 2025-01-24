# Assign #3: Oct Mock Exam暨选做题目满百

Updated 1537 GMT+8 Oct 10, 2024

2024 fall, Complied by Hongfei Yan==（请改为同学的姓名、院系）==



**说明：**

1）Oct⽉考： AC6==（请改为同学的通过数）== 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++/C（已经在Codeforces/Openjudge上AC），截图（包含Accepted, 学号），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、作业评论有md或者doc。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E28674:《黑神话：悟空》之加密

http://cs101.openjudge.cn/practice/28674/



思路：



代码

```python
k=int(input())
string=input()
for i in range(len(string)):
    t=ord(string[i])
    s=t-k
    if (65<=t<=90):
        while (s<65):
            s=s+26
    if (97<=t<=122):
        while (s<97):
            s=s+26
    print(chr(s),end='')

```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](image.png)




### E28691: 字符串中的整数求和

http://cs101.openjudge.cn/practice/28691/



思路：



代码

```python
string1,string2=input().split()
n=10*(int(string1[0])+int(string2[0]))+int(string1[1])+int(string2[1])
print(n)

```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](image-2.png)




### M28664: 验证身份证号

http://cs101.openjudge.cn/practice/28664/



思路：



代码

```python
n=int(input())
results=[]
for i in range(n):
    string=list(map(str,input()))
    co=[7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2]
    s=0
    for j in range(0,17):
        s=s+co[j]*int(string[j])
    t=(12-s%11)%11
    if (t==10 and string[17].upper()=='X')or(t==int(string[17]) and t!=10):
        results.append('YES')
    else :
        results.append('NO')
for result in results:
    print(result)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](image-3.png)




### M28678: 角谷猜想

http://cs101.openjudge.cn/practice/28678/



思路：



代码

```python
n=int(input())
while (n!=1):
    if (n%2==0):
        print(int(n),"/2=",int(n/2),sep = '')
        n=n/2
    else :
        print(int(n),"*3+1=",int(n*3+1),sep = '')
        n=n*3+1
print('End')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](image-1.png)




### M28700: 罗马数字与整数的转换

http://cs101.openjudge.cn/practice/28700/



思路：



##### 代码

```python
def r_to_num(s:str)->int:
    r_map={'I':1,'V':5,'X':10,'L':50,'C':100,'D':500,'M':1000}
    total=0
    pre_value=0
    for i in range(len(s)-1,-1,-1):
        value=r_map.get(s[i])
        if(value>=pre_value):
            total+=value
            pre_value=value
        else:
            total-=value
            pre_value=value
    return total
def num_to_r(num:int)->str:
    val = [
        1000, 900, 500, 400,
        100, 90, 50, 40,
        10, 9, 5, 4,
        1
    ]
    syms = [
        "M", "CM", "D", "CD",
        "C", "XC", "L", "XL",
        "X", "IX", "V", "IV",
        "I"
    ]
    r=''
    i=0
    while num>0:
        for _ in range(num//val[i]):
            r+=syms[i]
            num-=val[i]
        i+=1
    return r
def trans(user_input:str)->str:
    if (user_input.isdigit()):
        return num_to_r(int(user_input))
    else:
        return r_to_num(user_input)
user_input=input()
print(trans(user_input))


```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](image-4.png)




### *T25353: 排队 （选做）

http://cs101.openjudge.cn/practice/25353/



思路：



代码

```python


```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。==

python对于我来说真的很难。。。这次的月考题我在机房里只ac了3道，储备知识确实还是太少了，打字速度也够慢的，对机房电脑的熟悉还不够，也总是在很基础但不显眼的地方出一些小毛病，然后又debug很久。。。加油吧









