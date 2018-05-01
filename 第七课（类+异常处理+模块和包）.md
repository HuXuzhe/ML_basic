<font size = 4>

# 大纲
## 类属性、类方法、静态方法
## 单例类
## 异常处理
## 包和模块
## 项目实践
----

### 1. 类属性（可以理解为类中共享的全局变量）
#### 1.1 实例属性
- 所属于具体的实例对象，不同实例对象之间的实例属性互不影响

![实例对象](https://note.youdao.com/yws/public/resource/6ba936a8828c83c2940f8cb66c8405a1/xmlnote/FAC7449A79C04545971F4C73DBB13260/3240)




#### 1.2 类属性
- 所属于类对象，多个实例对象之间共享同一个类属性
- 获取类属性方法：类名.类属性
- 通过实例对象不能够修改类属性

<font color = red> 实例1：</font>
```
class Person:
    #类属性
    sum_num = 0
    def __init__(self,name):
        #赋值给实例属性
        self.name = name
        #修改类属性值，每创建一个实例对象，类属性值+1
        Person.sum_num += 1
        
p1 = Person('zhangsan')
#通过实例对象访问类属性，通过类名访问类属性
print(p1.sum_num,Person.sum_num)

p2 = Person('lisi')
print(p1.sum_num,p2.sum_num,Person.sum_num)

##为什么没有构造实例对象的实例属性sum_num，还可以获取值？如果没有实例属性就会去类属性。
```
结果：
```
1 1
2 2 2

```
<font color = red> 实例2：</font>
```
class Person:
    #类属性
    sum_num = 0
    def __init__(self,name):
        #赋值给实例属性
        self.name = name
        #修改类属性值，每创建一个实例对象，类属性值+1
        #Person.sum_num += 1
        
p1 = Person('zhangsan')
#通过实例对象访问类属性，通过类名访问类属性
#print(p1.sum_num,Person.sum_num)

p2 = Person('lisi')

##通过实例对象p1，来修改类属性的值
p1.sum_num = 100
print(p1.sum_num,p2.sum_num,Person.sum_num)
```
结果：
```
100 0 0

#由结果可知，通过实例对象不能修改类属性的值，如果修改的属性在实例中不存在，则动态添加实例属性
```

<font color = red>实例3：</font>
```
class Person:
    #类属性
    sum_num = 0
    def __init__(self,new_name,new_num):
        #赋值给实例属性
        self.name = new_name
        #定义一个与类属性同名的实例属性
        self.sum_num = new_num
        #修改类属性值，每创建一个实例对象，类属性值加1
        Person.sum_num += 1
        
p1 = Person('zhangsan',10)
print(p1.sum_num,Person.sum_num)
```
结果：
```
10 1

#由结果可以看出，同时调用同名属性的时候，优先调用对象属性，不是类属性
```

### 2. 类方法、静态方法
#### 2.1 类方法---操作类属性
- 所属于类对象，使用@classmethod修饰的方法
- 定义类方法的第一个参数通常以"cls"参数作为类对象被传入
- 调用方式：类名.类方法 或者 实例对象.类方法（不推荐）

<font color = red >实例3：</font>
```
class Person:
    #类属性
    sum_num = 0
    def __init__(self,new_name):
        #赋值给实例属性
        self.name = new_name
    
    #类方法
    @classmethod
    def add_sum_num(cls): #cls表示类对象
        cls.sum_num += 1
        print(cls.sum_num)
        
        
#类方法调用
#方法1 ：类名.类方法
Person.add_sum_num()
print('============分割线============')
#：方法2：实例对象.类方法(不推荐这样调用类方法)
p = Person('zhangsan')
p.add_sum_num()

#类方法(cls)和实例方法(self),类方法--类属性，实例方法--实例属性（很重要！！！）

```
结果：
```
1
============分割线============
2
```

#### 2.2 静态方法----和类和对象没有太大关系
- 使用@staticmethod修饰的方法，不需要默认传递任何参数
- 调用方式：类名.静态方法 或者实例对象.静态方法

<font color = red >实例4：</font>
```
class Person:
    #类属性
    sum_num = 0
    def __init__(self,new_name):
        #赋值给实例属性
        self.name = new_name
    
    #类方法
    @classmethod
    def add_sum_num(cls): #cls表示类对象
        cls.sum_num += 1
        print(cls.sum_num)
    
    #静态方法，静态方法里面不用传入参数的
    @staticmethod
    def static_test():
        print('----静态方法----')
        Person.sum_num += 1
        print(Person.sum_num)
        
#调用静态方法(尽量少使用静态方法，如果要使用的话，可以在打印提示性的信息时候使用)
Person.static_test()
print('------------')
p = Person('zhangsan')
p.static_test()

#总结：在类方法和静态方法中不能直接调用实例属性
```
结果：

```
----静态方法----
1
------------
----静态方法----
2

```

### 3. 单例类
#### 3.1 __new__(cls)
- 超类object类内置的方法，用户创建对象，返回创建对象的引用
- 必须要提供cls参数，代表类对象
- 必须要有返回值，返回创建对象的引用

<font color = red> 实例5：</font>
```
"""
#过程：解释器先用new方法来创建object对象，然后返回一个引用来给init构造方法，
self就相当于返回对象的一个引用，接收到这个对象后，对对象进行初始化，
打印构造方法后，返回对象的引用给变量db，变量db就指向内存中创建的这个对象。


# cls-->类对象  self-->是传入的对象本身

"""

class DataBaseObj(object):  #object是可以省略的，缺省object  #init方法是无返回值
    def __init__(self,new_name): #对象的初始化
        print('-----init构造方法------')
        self.name = new_name
        print(self.name)
    
    def __new__(cls,name): #object类是所有类的基类，object这个类的new方法是创建对象
        print('cls_id:',id(cls))
        return object.__new__(cls)
        
        
print(id(DataBaseObj)) ##打印的类对象的id
db = DataBaseObj('mysql')
print('----分割线-----')
print(db) 

```

结果：
```
1706654249752
cls_id: 1706654249752
-----init构造方法------
mysql
----分割线-----
<__main__.DataBaseObj object at 0x0000018D5ED1FE10>


```



#### 3.2 单例类
- 在整个程序系统中确保某一个类只有一个实例对象

<font color = red> 实例6：</font>
```
#单例类
class SingleInstance:
	__instance = None
	def __init__(self):
		print("-----init-----")
	def __new__(cls):
		if cls.__instance == None:
			cls.__instance = object.__new__(cls)
		return cls.__instance

s1 = SingleInstance()
print(id(s1))
s2 = SingleInstance()
print(id(s2))
```
结果：

```
-------init-------
1706683752288
-------init-------
1706683752288

```

### 3. 异常处理

链接：[异常处理](http://www.runoob.com/python/python-exceptions.html)

#### 3.1 捕获异常
```
try:
    逻辑代码块
expect ExceptionType as err：
    异常处理方法

```
<font color = red>实例7：</font>
```
try:
    open("test.txt", "r")

except FileNotFoundError as err:
    print('捕获到了异常！文件不存在',err)

print('哈哈哈哈')
```
结果:
```
捕获到了异常！文件不存在 [Errno 2] No such file or directory: 'test.txt'
哈哈哈哈


```

#### 3.2 捕获多个异常
```
try:
    逻辑代码块
except (ExceptionTypl1, ExceptionType2, ···) as err:
    异常处理方法
```

<font color = red >实例8：</font>
```
try:
    print(num)
    print("==============")
    open("test.txt", "r")
except (NameError,FileNotFoundError) as err:  #用元组将所有异常括起来
    print("捕获到了异常!",err)

print("哈哈哈哈哈")
```
结果：
```
捕获到了异常! name 'num' is not defined
哈哈哈哈哈

```
#### 3.3 捕获所有可能发生的异常
```
try:
    逻辑代码块
except (ExceptionType1, ExceptionType2, ···) as err:
    异常处理方法
except ExceptionType as err：
    异常处理方法
```

<font color = red>实例9：</font>
```
try:
    open("test.txt", "r")
except NameError as err1:
    print("捕获到了异常!",err1)
except Exception as err2:
    print("捕获所有可能的异常",err2)

print("哈哈哈哈哈")
```
结果：
```
捕获所有可能的异常 [Errno 2] No such file or directory: 'test.txt'
哈哈哈哈哈
```

#### 3.4 finally
```
try:
    逻辑代码块
exception(ExceptionType1, ExceptionType2, ···) as err:
    异常处理方法
except ExceptionType as err：
    异常处理方法
finally:
    无论是否有异常产生，都会执行这里的代码块
```

<font color = red>实例10：</font>
```
f = None
try:
    f = open("test.txt","r")
    print("打印文件内容")
except FileNotFoundError as error:
    print("捕获到了异常",error)
finally:
    print("关闭文件")
    if f != None:
        print("正在关闭文件")
        f.close()
```
结果：
```
捕获到了异常 [Errno 2] No such file or directory: 'test.txt'
关闭文件
```
#### 3.5 函数嵌套异常传递

<font color = red>实例11：</font>
```
def test1(): #通过打印的方式也可以查询问的所在处
    print("------test1-1--------")
    print(num) #打印一个不存在的变量
    print("------test1-2--------")

def test2():
    try:
        print("------test2-1--------")
        test1()
        print("------test2-2--------")
    except Exception as error:
        print("捕获到异常",error)

    print("------test2-3--------")

test2()
```
结果：
```
------test2-1--------
------test1-1--------
捕获到异常 name 'num' is not defined
------test2-3--------


##总结：异常处理的意义是防止某个业务产生异常而影响到整个程序中的其他业务。

##当Python脚本发生异常时我们需要捕获处理它，否则程序会终止执行。 
```

### 4. 包和模块（包可以类比成文件夹）

链接：[模块和包](http://www.runoob.com/python/python-modules.html)

![包和模块](https://note.youdao.com/yws/public/resource/6ba936a8828c83c2940f8cb66c8405a1/xmlnote/8C2AEDD70E354452861FEDBF87F546F5/3241)

#### 4.1 模块的名字： .py文件的名字

<font color = blue>下面是关于pycharm，能够引用包的设置步骤：若设置成功，则文件夹中间是实心，而非空心。</font>
![image](https://note.youdao.com/yws/public/resource/6ba936a8828c83c2940f8cb66c8405a1/xmlnote/66B0A2D503B44E0DA64B7851886AD880/3444)

<font color = blue>下图是包的形式，以.py的文件名字，包分别是bussiness和tool:</font>

![image](https://note.youdao.com/yws/public/resource/6ba936a8828c83c2940f8cb66c8405a1/xmlnote/F1F35162F68D425A82C3AE829BA5B189/3443)

#### 4.2 包下可以包含子包

#### 4.3 不同包下可以有相同的模块名称，使用‘包名.模块名’的方式区分

<font color = red>实例12：</font>
```
import bussiness.model1,tool.model1
#import tool.model1

bussiness.model1.project_info()
tool.model1.tool_info()
```

#### 4.4 引入模块的方式
- 引入单个模块：import module_name
- 引入多个模块：import module_name1,module_name2,···
- 引入模块中的指定函数：from module_name import func1,func2,···

<font color = red>实例13：</font>
```
from bussiness import * #批量导入
model3.test1()
model3.test2()
model3.test3()
model1.project_info()

```



#### 4.5 包中必须包含一个默认的__init__文件
- 用于标识一个包，而不是普通的文件夹
- 会在包或者该包下的模块被引入时自动调用
- 常用于设置包和模块的一些初始化操作

<font color = red>实例14：</font>
```
#init可以对包进行初始化的设置
print("init文件被自动调用")

#__all__方法，这里指只有model3才能被其他的引用
__all__ = ["model3"]
```

### 5. 项目实践
- 通过包和模块将项目组织结构划分清晰
- 将不同的管理系统按照类别划分到不同的模块
- 重构无人便利店项目

<font color = red>实例15：</font>
```
import datetime
import csv
'''
用户管理系统
仓库管理系统
货架管理系统
升级购物车
推荐系统
'''
from infrastructure.warehouse import WarehouseManageSys
from infrastructure.rack import RackManageSys
from infrastructure.user import UserManageSys,BuyCar
from infrastructure.log import LogMangerSys
from infrastructure.recommend import BaseItemRecommendSys

class UnstaffedStore:
	# 购物大厅
	def shopping_hall(self):
		#仓库管理系统初始化
		warehouse_manage = WarehouseManageSys()
		#货架管理系统初始化
		rack_manage = RackManageSys()
		#用户管理系统初始化
		user_manage = UserManageSys()
		#日志管理系统初始化
		log_manage = LogMangerSys()
		#推荐系统初始化
		recommend_sys = BaseItemRecommendSys()

		# 三个空货架
		pm_rack = []
		zc_rack = []
		xc_rack = []
		# 货架摆放商品数量
		pm_rack_counts = 1
		zc_rack_counts = 1
		xc_rack_counts = 1

		while True:
			print("欢迎光临")
			user_id = ""
			while True:
				user_id = input("请输入手机号作为用户id使用：")
				if user_id != "":
					user_manage.add_new_user(user_id)
					break
				else:
					print("输入的手机号不能为空，请输入正确的手机号！")
			#给用户分配一个购物车
			buy_car = BuyCar(user_id,user_manage)

			while True:
				# 自动检测货架是否需要补货
				rack_manage.check_add_rack(pm_rack, "pm", pm_rack_counts,warehouse_manage)
				rack_manage.check_add_rack(zc_rack, "zc", zc_rack_counts,warehouse_manage)
				rack_manage.check_add_rack(xc_rack, "xc", xc_rack_counts,warehouse_manage)
				item_id = input("==本店售卖商品：1 泡面，2 榨菜，3 香肠。请输入想要购买的商品编号：")
				#向购物车添加商品
				buy_car.add_item_2_car(pm_rack,zc_rack,xc_rack,item_id)
				if_buy = input("请输入y或者n选择是否继续购物：")
				if if_buy == "n":
					#购物车结算
					if len(buy_car.buy_car) > 0:
						total_money = buy_car.account(warehouse_manage)
						print("您的购物车商品如下：", buy_car.buy_car)
						print("$您本次消费金额{}元：".format(total_money))
						# 购物日志管理
						log_manage.buy_log_manage(user_id, total_money, *buy_car.buy_car)
						recommend_item_list = recommend_sys.recommend(user_id,log_manage.buy_logs)
						if recommend_item_list != None:
							print("买了该商品的其他用户，还买了{}".format(recommend_item_list))
						print("欢迎下次光临")
					else:
						print("您没有购买任何商品")
						print("欢迎下次光临")
					break
store = UnstaffedStore()
store.shopping_hall()
```

### 6. 作业

在奶茶馆的顾客反馈中，有的顾客提出输入信息的时候一不小心输入格式错 误就会跳出系统，所以，您决定对输入异常进行处理，使用 try-except 语句，处 理的 points 如下： 
1. 设置顾客输入生日为日期格式，并且对错误格式造成的异常进行处理。 
2. 处理其它输入过程中可能出现的异常。 
3. 系统运行结束之后，设置输入文件名称来读取文件的操作，并且对输入错 误造成的异常进行处理。 
