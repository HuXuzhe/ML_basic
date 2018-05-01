<font color=black size=4>

# 大纲
## 1. 循环语句
## 2. 字符串操作
## 3. 列表
## 4. 项目实践

---
## 1.循环语句（三大执行流程之一，还包括选择执行，顺序执行）
######  * 下面是程序流程图：
![三大执行流程](https://note.youdao.com/yws/public/resource/6ba936a8828c83c2940f8cb66c8405a1/xmlnote/047974EED5E3496E9C96A03E91536B02/144)

### 1.1 while循环
#### <font color=red size=4> 1.1.1 语法格式 </font>
```
while 判断条件：
    条件满足，执行语句
```
#### ==程序样例1：==
```
num = 1
while num <= 10: #打印1-10的数字
    print(num)
    num += 1
```
#### ==结果：==
```
1
2
3
4
5
6
7
8
9
10
```

#### 1.1.2 执行流程
![for循环](https://note.youdao.com/yws/public/resource/6ba936a8828c83c2940f8cb66c8405a1/xmlnote/2956E979C15542AEAF39D899362236FE/175)

#### 1.1.3 应用场景
对于满足某种条件，调用实现相同功能的代码

#### 1.1.4 循环嵌套
<font color=red size=4>语法结构</font>：
```
while 判断条件：
    调价你满足，执行语句
    while 嵌套判断条件：
        条件满足，执行语句
```
#### ==程序2.打印到三角形:==
```
i = 0 #第几行，行号
#  4行的到三角形
while i < 4: 
    print(" "* i,end="")#打印每行开头的空格
    j = 0 #控制*个数
    #进行while的嵌套
    while j < 7-i*2:
        print("*",end="") # end表示循环内不空行
        j +=1
    print("") #实现每一行打印完换行
    i = i+1 #对i进行自加，如果不自加则会进行无限循环

```
#### ==结果：==
```
*******
 *****
  ***
   *
```

#### ==程序3.打印正三角形：==
```
i = 4 #4行的正三角形，定义行数
while i > 0:
    i -= 1
    print(" "*i,end="")#打印开头空格
    j = 0
    while j < 7-i*2:
        print("*",end="")
        j +=1
    print("")
```
#### ==结果:==
```
   *
  ***
 *****
*******
```
#### ==程序4.打印沙漏：==

```
m = 7  #控制总行数
i = 0  #外层循环的次数，行号
h = 0  #空格的个数
middle = m // 2  #中间位置
while i < m:
    if i <= middle:
        h = i #倒正三角形的时候，空格个数等于行号
    else:
        h -= 1
    n = m-h*2
    #打印一行开头的空格和星号
    print(" "*h,end="")#打印开头空格
    j = 0
    while j < n:
        print("*",end="")
        j +=1
    print("")
    i += 1
```
##### ##如果有不明白的地方，可以通过==pycharm==的==debug模式==进行一步步看结果的变化，i，h随时循环的进行，是变化的。
#### ==结果：==
```
*******
 *****
  ***
   *
  ***
 *****
*******
```

#### 1.1.5 while的循环中的break和continue
<font color=red size=4>1.1.5.1 break语法结构</font>：
```
while 条件：
    break #整个循环结束
```
while循环嵌套中使用break：
```
while 条件：
    代码
    while 条件：
        break #只结束内层整个循环
```
#### ==程序5：break跳出循环==
```
#当时i= 10的时候，跳出break循环（并且不能打印10）
i = 1
while i <= 20:
    if i % 2 == 0:
        if i % 10 == 0:
            break
        print(i)
    i += 1
```
#### ==结果：==
```
2
4
6
8
```
<font color=red size=4>1.1.5.2 continue语法结构:</font>
```
while 条件：
    if 条件：
        continue #本次循环结束，后边的代码语句不执行
    代码语句
```

#### ==程序6：continue==
```
#当i=10的时候，不执行print打印，直接继续进入下一个循环循环
i = 1
while i <= 20:
    i += 1
    if i % 2 == 0:
        if i % 10 == 0:
            continue
        print(i)
```

#### ==结果：==
```
2
4
6
8
12
14
16
18
```
### 1.2 for 循环
#### <font color=red size=4>1.2.1 语法结构:</font>
```
for 临时变量 in 序列： #这里的序列是一个迭代器（iterator）
    序列中存在待处理元素则进入循环体执行代码
```

#### 1.2.2 执行流程
for 循环遍历，序列中所有的元素，并执行对应的语句。
![for 循环](https://note.youdao.com/yws/public/resource/6ba936a8828c83c2940f8cb66c8405a1/xmlnote/2B49C362856A4A8E82A8FA40B881B5ED/374)

#### ==程序7：for 循环==


```
for i in range(0,10):
    print(i)
```
#### ==结果：==
```
0
1
2
3
4
5
6
7
8
9
```
#### 1.2.3 for 循环的break和continue
#### <font color=red size=4>break语法结构:</font>
```
for 变量 in 序列：
    break #整个循环结束
```
#### ==程序8：break跳出循环for==
```
#当 i = 4的时候，j能取到3，直接跳出循环，继续外循环
for i in range(1,5):  ##range（起始，结束，步长）
    for j in range(0,i):
        if j == 2:
            break
        print("*",end="")
    print("")
    print(i)
```

#### ==结果：==
```
*
1
**
2
**
3
**
4
```

#### <font color=red size=4>continue语法结构:</font>
```
for 变量 in 序列：
    if 条件：
        continue #本次循环结束，后边的代码语句不执行，但仍然继续循环
```

#### ==程序9：continue继续循环==

```
for i in range(1,5):
    for j in range(0,i):
        if j == 2:
            continue
        print("*",end="")
    print("")
    print(i)
```

#### ==结果：==

```
*
1
**
2
**
3
***
4
```
### 2.1 字符串类型变量定义
```
s = 'hello'
s = "hello"
##如果字符串里面需要有单引号的情况，可以以下情况
s ="'name'"
```

### 2.2 组成字符串的方式
- 使用"+"号将两个字符串连接成一个新的字符串
```
print('hello'+'world')
```
-使用字符串格式化符号
```
#将int类型转换为字符串类型
num = 123
num_str = str(num)
print(type(num))
print(type(num_str))
```
==结果为：==
```
<class 'int'>
<class 'str'>
```

### 2.3 下标
![下标](https://note.youdao.com/yws/public/resource/6ba936a8828c83c2940f8cb66c8405a1/xmlnote/2EAE9E77D1724AB697120CE902634113/478)

通过下标获取指定位置的字符：<font size= 4 color = red>string_name[index]</font>
```
#符号空格都占一个字符
name = 'zhangsan,20'
print(name[0])
#-1是指最后一个位置
print(name[-1])
```
==结果:==
```
z
0
```
### 2.4 切片

语法：<font color =red size = 4>string_name[起始：结束：步长]</font>

==程序10：字符串的切片：==
```
line = "zhangsan,20"
name = line[0:8]
print(name)

age1 = line[9:]  #不写默认到最后一位
age2 = line[9:11]
print(age1)
print(age2)
#2指步长，相隔一个取
s = "abcde"
print(s[0::2])
```
==结果：==
```
zhangsan
20
20
ace
```
### 3.1 列表的定义和基础属性
1. 可以储存相同或者不同类型数据的集合
```
list = [a,'123',456]
```
2. 顺序储存，可通过下标获取内部元素
```
list = [a,'123',456]
print(list[0])
print(list[2])


##结果
a
456
```

3. 内容可变，可通过下标修改元素值
```
list = [a,'123',456]
list[2] = 'zhangsan'

#结果
[a,'123','zhangsan']
```
4. 使用循环遍历列表
```
info_list = ["zhangsan",20,180.5]
#while遍历
while i < len(info_list):
    print(info_list[i])
    i += 1

#for遍历
for i in range(0,len(info_list)):
    print(info_list[i])

#简便方法
for item in info_list:
    print(item)
```
==结果：==
```
zhangsan
20
180.5
zhangsan
20
180.5
```
5. 循环的嵌套
```
infos_list = [["zhangsan",20,180.5],["lisi",21,170],["wangwu",25,190]]
print(infos_list[0][0])
print(infos_list[1][0])
print('\n') #空一行
for lst in infos_list:
    print(lst)
    for item in lst:
        print(item)
```
==结果：==
```
zhangsan
lisi

['zhangsan', 20, 180.5]
zhangsan
20
180.5
['lisi', 21, 170]
lisi
21
170
['wangwu', 25, 190]
wangwu
25
190
```

### 3.2 列表的相关内置函数
1. append()/insert()添加元素
```
#append列表末尾添加元素
infos_list = [["zhangsan",20,180.5],["lisi",21,170],["wangwu",25,190]]
infos_list.append(["xiaobai",30,175])
print(infos_list)
print('\n')

#insert向列表指定位置添加元素
new_info = ["孙悟空",18,160]
new_info.insert(1,50) #1指列表中的1号位置
print(new_info)
```

结果：
```
[['zhangsan', 20, 180.5], ['lisi', 21, 170], ['wangwu', 25, 190], ['xiaobai', 30, 175]]


['孙悟空', 50, 18, 160]
```

2. "+"组合两个列表生成新的列表,append(),extend()
```
#+拼接两个列表
name_list1 = ["zhangsan"]
name_list2 = ["lisi","wangwu"]
name_list3 = name_list1 + name_list2
print(name_list3)

#extend 向一个列表中添加另外一个列表的元素
name_list1.extend(name_list2)
print(name_list1)

name_list1.append(name_list2)
print(name_list1)
```
结果：
```
['zhangsan', 'lisi', 'wangwu']
['zhangsan', 'lisi', 'wangwu']
['zhangsan', 'lisi', 'wangwu', ['lisi', 'wangwu']]
```

3. del()/pop()/remove()删除元素
```
#删除列表元素
group = ["唐僧","悟空","八戒","白龙马"]
del group[1]
group.remove("八戒")
group.pop(0)
print(group)
```
结果：
```
['白龙马']
```

4. 切片（如同上字符串切片语法相同，只不过单个字符变为列表中的元素）
5. in/not in 判断元素在列表中是否存在
```
group = ['白龙马']
if "唐僧" in group:
    print("师傅还在")
else:
    print("师傅没了")
```
结果：
```
师傅没了
```
6. sort()列表内元素重排序
```
#sort()
num_list = [5,2,6,1]
# num_list.sort()#升序
num_list.sort(reverse=True)
print(num_list)
#reverse()将列表内容 倒置
group = [1,3,4,5,6,7,8]
group.reverse()
print(group)
```
结果：
```
[6, 5, 2, 1]
[8, 7, 6, 5, 4, 3, 1]
```
7. count()统计列表内指定元素个数
```
group = [1,2,3,4,5,4,3,2,2,2,3]
print(group.count(4))
```
结果：
```
2
```
8. 附加：条件表达式和列表推导式（能够缩减代码的运行时间）
```
#条件表达式
import math
def get_log(x):
    log_v = math.log(x) if x>0 else float('nan')

    return log_v
print (get_log(5))
print (get_log(-1))
print('======')
#列表推导式
l1 = [i for i in range(1,10) if i%2 ==0]
print(l1)
```
==结果：==
```
1.6094379124341003
nan
======
[2, 4, 6, 8]
```

### 4.项目实践
功能：
1. 售卖商品：泡面、榨菜、香肠，不同商品摆放在不同的货架
2. 最后被放入货架的货品先被取走
3. 顾客输入不同的商品编号，在购物车中添加对应编号的商品
4. 当顾客输错商品编号，则跳出本次购物，再次让用户输入商品编号
5. 当所有的货架的商品都卖完后，提醒顾客，程序退出
6. 顾客在购物过程中可以随时结束购物

```
'''
无人便利店
'''
#三个空货架
pm_rack = []
zc_rack = []
xc_rack = []
#向货架摆货
#泡面
pm_list = ["老坛酸菜","红烧牛肉","酸辣粉","拉面"]
pm_rack_num = 3
while len(pm_rack) < pm_rack_num:
    pm_index = len(pm_rack)%len(pm_list)
    pm_rack.append(pm_list[pm_index])
#榨菜
zc_list = ["老干妈","乌江"]
zc_rack_num = 3
while len(zc_rack) < zc_rack_num:
    zc_index = len(zc_rack)%len(zc_list)
    zc_rack.append(zc_list[zc_index])
# 香肠
xc_list = ["王中王","蒜肠","淀粉肠"]
xc_rack_num = 3
while len(xc_rack) < xc_rack_num:
    xc_index = len(xc_rack)%len(xc_list)
    xc_rack.append(xc_list[xc_index])
buy_car = []
while True:
    if len(pm_rack) == 0 and len(zc_rack) == 0 and len(xc_rack) == 0:
        print("已售罄")
        break

    goods_num = input("==本店售卖商品：1 泡面，2 榨菜，3 香肠。请输入想要购买的商品编号：")
    if int(goods_num) == 1:
        if len(pm_rack) >= 1:
            buy_car.append(pm_rack[len(pm_rack)-1])
            pm_rack.pop()
        else:
            print("亲！非常抱歉，泡面已卖完。")
    elif int(goods_num) == 2:
        if len(zc_rack) >= 1:
            buy_car.append(zc_rack[len(zc_rack)-1])
            zc_rack.pop()
        else:
            print("亲！非常抱歉，榨菜已卖完。")
    elif int(goods_num) == 3:
        if len(xc_rack) >= 1:
            buy_car.append(xc_rack[len(xc_rack)-1])
            xc_rack.pop()
        else:
            print("亲！非常抱歉，香肠已卖完。")
    else:
        print("亲！您输入的商品还在火星，请输入在售的商品编号！")
        continue

    if len(buy_car)>0:
        print("您的购物车商品如下：",buy_car)
    else:
        print("您没有购买任何商品")

    if_buy = input("请输入y或者n选择是否继续购物：")
    if if_buy == "n":
        break

print("欢迎下次光临！拜拜..")
```
==结果：==
```
==本店售卖商品：1 泡面，2 榨菜，3 香肠。请输入想要购买的商品编号：1
您的购物车商品如下： ['酸辣粉']
请输入y或者n选择是否继续购物：y
==本店售卖商品：1 泡面，2 榨菜，3 香肠。请输入想要购买的商品编号：3
您的购物车商品如下： ['酸辣粉', '淀粉肠']
请输入y或者n选择是否继续购物：n
欢迎下次光临！拜拜..
```
======================================
### **作业
要求：
1. 顾客输入会员号，可判断是否为本管会员。新会员直接设置会员号，但第二次购买才可享受会员价。（将会员号记录在列表中，使用in语句判断是否为会员）
2. 使用列表记录每位顾客的消费信息
3. 使用嵌套列表记录每位顾客的消费信息
4. 本店每日只接待20位顾客，并在顾客光临时输出顾客的序号，第二十位顾客购买完毕后输出：‘今日已闭店，欢迎您明天光临’。

<font color = red size = 4>相对于课程的的code，多加了一个判断是否是会员，会更加合理。</font>

==程序：==
```
#设计一款价格结算系统的程序
print('小象奶茶管盛大开业了！小象奶茶馆售卖宇宙无敌奶茶，奶茶虽好，可不要贪杯哦！')
print('每次限尝鲜一种口味：\n 1）原味冰奶茶 3 元 \n 2）香蕉冰奶茶 5 元\n 3) 草莓冰奶茶 5 元\n 4）蒟蒻冰奶茶 7 元\n 5）珍珠冰奶茶 7 元')
print('')
#定义奶茶名称和价格
mt_name = ['原味冰奶茶','香蕉冰奶茶','草莓冰奶茶','蒟蒻冰奶茶','珍珠冰奶茶']
mt_price = [3,5,5,7,7]


# human_num = 0  # 人数初始化
#用于打印选择的口味、数量、总价
human_num = 0    # 人数初始化
#根据是否是会员输出总价，并登记会员号
vip_num_list = [] #会员号的列表
cus_record = []

while True:

    user_choice = input('请输入数字1-5选择您喜欢的口味：')
    user_choice = int(user_choice)
    if user_choice < 6:
        user_num = input('请输入你购买的数量：')
        user_num = int(user_num)
        money = mt_price[user_choice - 1]*user_num
        money = round(money,2)
        print('你购买的奶茶口味是{}，数量为{},总价为{}。'.format(mt_name[user_choice - 1],user_num,money))

        #根据是否是会员输出总价，并登记会员号
        #vip_num_list = [] #会员号的列表
        vip = input('请确认您是否是会员（1是，2不是）：')
        vip = int(vip)
        if vip == 1:
            vip_num = input('请输入您的会员号：')
            vip_num = int(vip_num)
            if vip_num in vip_num_list:
                money = mt_price[user_choice-1]*user_num*0.9
                money = round(money,2)
                print('您是尊贵的会员，可以享受会员价，总价是：{}。'.format(money))
            else:
                vip_num_list.append(vip_num)
                #print(vip_num_list)
                money = mt_price[user_choice-1]*user_num
                print('你是第一次办会员，第二次才可享受会员价，总价为：{}。'.format(money))
    

        elif vip == 2:
            money = mt_price[user_choice-1]*user_num
            vip_num = None
            print('如果你办会员第二次起可以享受9折会员价，这次总价为:{}。'.format(money))
        else:
            print('您输入错误，只能输1或者2两个数字，会自动返回到开始点单页面。')
            continue
        
        #记录今日日来的客人的数量和记录
        single_cus_record = []
        single_cus_record.append(mt_name[user_choice - 1])
        single_cus_record.append(user_num)
        single_cus_record.append(money)
        single_cus_record.append(vip_num)
        cus_record.append(single_cus_record)
        #print(cus_record)
        human_num +=1 #计算人数
        print('本店今日只招待20位客人，您是今天第{}位客人。\n'.format(human_num))
    else:
        print('Woops! 我们只售卖以上五种奶茶哦！新口味敬请期待！')
    

    if human_num > 19:
        print('==========================')
        print('今日已闭店，欢迎您明天光临')
        print('==========================')
        break

```

==部分结果：==
```
奶茶管盛大开业了！小象奶茶馆售卖宇宙无敌奶茶，奶茶虽好，可不要贪杯哦！
每次限尝鲜一种口味：
 1）原味冰奶茶 3 元 
 2）香蕉冰奶茶 5 元
 3) 草莓冰奶茶 5 元
 4）蒟蒻冰奶茶 7 元
 5）珍珠冰奶茶 7 元


请输入数字1-5选择您喜欢的口味：1
请输入你购买的数量：2
你购买的奶茶口味是原味冰奶茶，数量为2,总价为6。
请确认您是否是会员（1是，2不是）：1
请输入您的会员号：123
你是第一次办会员，第二次才可享受会员价，总价为：6。
本店今日只招待20位客人，您是今天第1位客人。


请输入数字1-5选择您喜欢的口味：2
请输入你购买的数量：3
你购买的奶茶口味是香蕉冰奶茶，数量为3,总价为15。
请确认您是否是会员（1是，2不是）：1
请输入您的会员号：123
您是尊贵的会员，可以享受会员价，总价是：13.5。
本店今日只招待20位客人，您是今天第2位客人。


请输入数字1-5选择您喜欢的口味：3
请输入你购买的数量：2
你购买的奶茶口味是草莓冰奶茶，数量为2,总价为10。
请确认您是否是会员（1是，2不是）：2
如果你办会员第二次起可以享受9折会员价，这次总价为:10。
本店今日只招待20位客人，您是今天第3位客人。


请输入数字1-5选择您喜欢的口味：4
请输入你购买的数量：5
你购买的奶茶口味是蒟蒻冰奶茶，数量为5,总价为35。
请确认您是否是会员（1是，2不是）：1
请输入您的会员号：456
你是第一次办会员，第二次才可享受会员价，总价为：35。
本店今日只招待20位客人，您是今天第4位客人。
```