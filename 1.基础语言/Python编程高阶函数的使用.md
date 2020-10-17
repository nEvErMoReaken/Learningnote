
### lambda表达式

又被称之为匿名函数

格式lambda参数列表:函数体


```python
def add(x,y):
    return x+y
print(add(3,4))
```

    7
    


```python
add_lambda=lambda x,y:x + y
add_lambda(3,4)
```




    7



### 三元运算符


```python
condition = True
print(1 if condition else 2)
```

    1
    


```python
condition = False
print(1 if condition else 2)
```

    2
    

### map函数的应用


```python
#单个参数
list1 = [1,2,3,4,5]
r = map(lambda x:x + x,list1)
print(list(r))
```

    [2, 4, 6, 8, 10]
    


```python
m1 = map(lambda x,y : x * x + y , [1,2,3,4,5],[1,2,3,4,5])
print(list(m1))
```

    [2, 6, 12, 20, 30]
    

### filter 过滤器


```python
def is_not_none(s):
    return s and len(s.strip()) > 0
list2 = [' ','','hello','greedy',None,'ai']
result = filter(is_not_none,list2)
print(list(result))
```

    ['hello', 'greedy', 'ai']
    

### reduce 函数


```python
from functools import reduce
f = lambda x,y : x+y
r = reduce(f,[1,2,3,4,5],10)
print(r)
```

    25
    

## python中的三大推导式

### 列表推导式
根据已有的列表推导出新的列表


```python
list1 = [1,2,3,4,5,6]
f = map(lambda x:x+x,list1)
print(list(f)) # map需要加一个强转

list2 = [i + i for i in list1]
print(list2)

list3=[i**3 for i in list1]
print(list3)

#有选择性的筛选
list4 = [i*i for i in list1 if i>3]
print(list4)
```

    [2, 4, 6, 8, 10, 12]
    [2, 4, 6, 8, 10, 12]
    [1, 8, 27, 64, 125, 216]
    [16, 25, 36]
    

### 集合推导式 


```python
list1 = {1,2,3,4,5,6}
f = map(lambda x:x+x,list1)
print(list(f)) # map需要加一个强转

list2 = {i + i for i in list1}
print(list2)

list3={i**3 for i in list1}
print(list3)

#有选择性的筛选
list4 = {i*i for i in list1 if i>3}
print(list4)
```

    [2, 4, 6, 8, 10, 12]
    {2, 4, 6, 8, 10, 12}
    {64, 1, 8, 216, 27, 125}
    {16, 25, 36}
    

### 字典推导式


```python
s = {
    'zhangsan':20,
    'lisi':15,
    'wangwu':31
}

# 拿出所有的key，并变成列表
s_key = [key +"aaa" for key,value in s.items()]
print(s_key)
```

    ['zhangsanaaa', 'lisiaaa', 'wangwuaaa']
    


```python
# key 和 value颠倒
s1 = {value: key  for key,value in s.items()}
print(s1)
```

    {20: 'zhangsan', 15: 'lisi', 31: 'wangwu'}
    


```python
# 只拿出符合条件的值
s2 = {key:value for key,value in s.items() if key =='lisi'}
print(s2)
```

    {'lisi': 15}
    

### 闭包：一个返回值是函数的函数


```python
# 调用后打印当前的时间
import time
def runtime():
    def now_time():
        print(time.time())
    return now_time
f = runtime()
f()
```

    1587123636.563505
    


```python
%pycat 123.csv
```


```python
# 读出一个文件中带有某个关键字的行
def make_filter(keep): # keep=8
    def the_filter(file_name):#file_name =123.csv 这个文件
        file = open(file_name)#打开文件
        lines = file.readlines() #读取出来所有文件内容
        file.close() #关闭文件
        filter_doc = [i for i in lines if keep in i] #过滤文件内容
        return filter_doc
    return the_filter

filter1 = make_filter('8')#这一行调用了make_filter函数，接收了the_filter函数作为返回值
#也就是说这里的filter1 就等于函数the_filter

filter_result= filter1('123.csv')
print(filter_result)
```

    ['6,7,8,9,10']
    

## 装饰器、语法糖、注解


```python
# 获取函数运行时间

import time

def runtime(func):
    def get_time():
        print(time.time())
        func()  
    return get_time
    
@runtime
def student_run():
    print("学生跑")
    
student_run()

#如果有参数怎么解决
#有参数的装饰器
```

    1587125886.9863691
    学生跑
    


```python
def runtime(func):
    def get_time(*args):#约定写法 
        print(time.time())
        func(*args)  
    return get_time
    
@runtime
def student_run(i):
    print("1学生跑")
@runtime
def student_run1(i,j):
    print("2学生跑")
        
student_run(1)
student_run1(1,3)

# 关键字参数 key =value
```

    1587126549.071482
    1学生跑
    1587126549.071482
    2学生跑
    


```python
#关键字参数
def runtime(func):
    def get_time(*args,**kwargs):#约定写法 
        print(time.time())
        func(*args,**kwargs)  
    return get_time
    
@runtime
def student_run(i,j):
    print("1学生跑")
@runtime
def student_run1(*args,**kwargs):
    print("2学生跑")
@runtime    
def student_run2():
    print("3学生跑")
student_run(1,3)
student_run1(1,i=5,j=2)
student_run2()
```

    1587127012.0559103
    1学生跑
    1587127012.0559103
    2学生跑
    1587127012.0559103
    3学生跑
    


```python
#开发一个语法糖，实现参数的准确性
def judge(func):
    def normalstuff(*args,**kwargs):#约定写法 
        if type(*args,**kwargs)== int:
            func(*args,**kwargs)  
        else: 
            print('Error')
    return normalstuff

@judge
def rush(*args,**kwargs):
    print('我运行了！')
    
rush('asfd')
rush(123)
```

    Error
    我运行了！
    
