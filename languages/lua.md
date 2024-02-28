**title**: Programming in Lua (fourth edition)  
**author**: Roberto lerusalimschy  
Lua程序设计（第四版） 梅隆魁 译  
ISBN：978-7-121-33804-5
#### 1-0
hello world
~~~lua
-- print Hello world
print("Hello world")
~~~
计算阶乘（修改前）
~~~lua
-- calculate factorial
-- 定义一个计算阶乘的函数
function fact (n)
	if n == 0 then
		return 1
	else
		return n * fact(n - 1)
	end
end

print("enter a number:")

a = io.read("*n")  -- 读取一个数字

print(fact(a))
~~~
#### 1-1 程序段
可以直接在交互模式下运行独立解释器  
不带参数直接调用时
~~~lua
[username@localhost ~]$ lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
>
~~~
输入EOF控制字符（POSIX下为Ctrl-D，windows下为Ctrl-Z），或调用exit函数（ os.exit() ）可以退出  
在交互模式下可以直接输入表达式
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> math.pi / 4
0.78539816339745
> a = 15
> a^2
225.0
> a + 2
17
~~~
用 -i 参数可以在执行完程序段后直接进入交互模式
~~~bash
[username@localhost ~]$ lua -i somefile
~~~
可以用dofile调用文件  
如果已经拥有一个名为**lib1.lua**的文件
~~~lua
-- as a lib, there is no output.
function norm (x, y)
	return math.sqrt(x^2 + y^2)
end

function twice (x)
	return 2.0 * x
end
~~~
则在交互模式下可以直接调用
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> dofile("1_1.lua") --加载文件
> n = norm(3.4, 1.0)
> n
3.5440090293339
> twice(n)
7.0880180586677
~~~
#### 1-2 语法规范
##### 1.名称可以由字母、数字和下划线组成（但是不能以数字开头），例：  
**i** &emsp; **j** &emsp; **i10**   
**\_ij** &emsp; **aSomewhatLongName** &emsp; **\_INPUT**  
##### 2.“\_ \+ 大写字母”（例如 \_VERSION)，会被用为特殊用途，应当避免  
##### 3.保留字不能使用  
**and** &emsp; **break** &emsp; **do** &emsp; **else** &emsp; **elseif**  
**end** &emsp; **false** &emsp; **goto** &emsp; **for** &emsp; **function**  
**if** &emsp; **in** &emsp; **local** &emsp; **nil** &emsp; **not**  
**or** &emsp; **repeat** &emsp; **return** &emsp; **then** &emsp; **ture**  
**until** &emsp; **while**  
##### 4.大小写敏感  
and =~ AND =~ And
##### 5.注释
- 单行注释
~~~lua
-- here is a short comment (1 line)
~~~
- 多行注释  
~~~lua
--[[ 
here is multiline comment
sometext
]]
~~~
- 注释掉代码
~~~lua
-- by adding a "-" in "--[[" , the code can be re-enabled

--[[ 
print(1)
--]]                    -- "--]]" is important.

---[[ 
print(1)
--]]
~~~
##### 5.";"不敏感
~~~lua
-- except for table, ";" is not needed, the following 4 segments are equivalent.

a = 1
b = a * 2
-----
a = 1;
b = a * 2;
-----
a = 1 ; b = a * 2 ;
-----
a = 1  b = a * 2 -- do NOT use this in real projects.
~~~
#### 1-3 全局变量
nil赋值给全局变量时，lua会回收该全局变量
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> b = 10
> b
10
> b = nil
> b
nil
~~~
#### 1-4 类型和值
lua有8种基本类型：**nil** **boolean** **number** **string** **userdate** **function** **thread** **table**
#### 1-5 练习
##### 1.运行阶乘函数并观察，如果输入复数会出现什么问题？尝试修改代码  
"lua:6: stack overflow"  
修改后：
~~~lua
-- calculate factorial
function fact (n)
	if n == 0 then
		return 1
	elseif n < 0 then
		return "math error"
	else
		return n * fact(n - 1)
	end
end

print("enter a number:")

a = io.read("*n")

print(fact(a))
~~~
##### 2.分别使用-l参数和dofile运行twice示例,并感受你喜欢那种方式
lua -l
~~~lua
$ lua -l 1_1    --加载文件并进入交互模式
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> n = norm(3.4, 1.0)
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> n = norm(3.4, 1.0)
> n
3.5440090293339
> twice(n)
7.0880180586677
~~~
dofile
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> dofile("1_1.lua") --加载文件
> n = norm(3.4, 1.0)
> n
3.5440090293339
> twice(n)
7.0880180586677
~~~
##### 3.列举出其他使用“\-\-”的语言
SQL Ada Haskell
##### 4.以下字符串中哪些是有效的标识符
**\_\_\_** &emsp; **\_end** &emsp; **End** &emsp; **end** &emsp; **until?** &emsp; **nil** &emsp; **NULL** &emsp; **one-step**  
有效：\_\_\_ &emsp; _end &emsp; End &emsp; NULL  
无效：end &emsp; until? &emsp; nil &emsp; one-step  
##### 5.表达式`type(nill) ==nil`的值是什么？
false，`type`函数输出的值类型为`string`，`type(nill)`输出"nil"(类型为string)，"nil" =~ nil 
##### 6.除了type外，如何验证一个值为Boolean类
~~~lua
local function verify_bloen(value)
	if value == true or value == false then
		print("Boolean")
	else
		print("Not boolean")
	end
end
~~~
##### 7.考虑表达式`(x and y and (not z)) or ((not y) and x)`，括号是否是必须的
不是必须的，但是推荐使用
##### 8.在不知道自身名字的情况下，编写一个可以打印自身名称的脚本
~~~lua
print(arg[0])
~~~
#### 2-1 八皇后问题
示例
~~~lua
local N = io.read("*n") -- 棋盘大小

-- 检查(n,c)是否不会被攻击
local function isplaceok (a, n, c)
	for i = 1, n - 1 do     -- 对于每一个已经被放置的皇后
		if (a[i] == c ) or (a[i] - i == c - n) or (a[i] + i == c + n) then  -- 同一列 同一对角线 
			return false    -- 位置会被攻击
		end
	end
	return true     -- 不会被攻击；位置有效
end

local function printsolution(a)
	for i = 1, N do     -- 对于每一行
		for j = 1, N do     -- 对于每一列
        -- 输出“X”或“-”，外加一个空格
			io.write(a[i] == j and "X" or "-", " ")
		end
		io.write("\n")
	end
	io.write("\n")
end

-- 把‘n’到‘N’的所有皇后放在棋盘‘a’上
local function addqueen(a, n)
	if n > N then   -- 检查是否所有皇后都放好了
		printsolution(a)
	else    -- 放置第n个皇后
		for c = 1, N do
			if isplaceok(a, n, c) then
			 	a[n] = c    -- 把第n个皇后放在c
				addqueen(a, n + 1)
			end
		end
	end
end

-- 运行
addqueen({}, 1)
~~~
#### 3-1 数值常量
书写常量
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> 4
4
> 0.4
0.4
> 4.57e-3
0.00457
> 0.3e12
300000000000.0
> 0.3e+12
300000000000.0
> 5E+20
5e+20
> 5E20
5e+20
~~~
整型值和浮点值都是“number”
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> type(3)
number
> type(3.5)
number
> type(3.0)
number
~~~
整型值和浮点值可以互相转换，且具有相同算数值的整型值和浮点值是相等的
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> 1 == 1.0
true
> -3 == -3.0
true
> 0.2e3 == 200
true
~~~
需要区分整型值和浮点值时，可以用`math.type`函数
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> math.type(3)
integer
> math.type(3.0)
float
~~~
十六进制
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> 0xff
255
> 0x1A3
419
> 0x0.2
0.125
~~~
十六进制浮点用p表示
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> 0x1p-1
0.5
> 0xa.bp2
42.75
~~~
用`%a`和`string.format`进行格式化输出
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> string.format("%a", 419)
0x1.a3p+8
> string.format("%a", 0.1)
0x1.999999999999ap-4
~~~
#### 3-2 算数运算
##### 加、减、乘、除、取负数
两个整型（浮点）进行加、减、乘、取负数，结果还是两个整型（浮点）  
一个整型和一个浮点进行加、减、乘、取负数时，算数前会将整型转换为浮点
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> 13 + 15
28
> 13.0 + 15.0
28.0
> 13.0 + 25
38.0
> -(3 * 6.0)
-18.0
~~~
除法永远是浮点
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> 3 / 2
1.5
> 3.0 / 2.0
1.5
> 3 / 1
3.0
~~~
##### floor //
对得到的商向负无穷取整
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> 3 // 2
1
> 3.0 // 2
1.0
> 6 // 2
3
> 6.0 // 2.0
3.0
> 9 // 5
1
> 9.0 // 5.0
1.0
> -9 // 2
-5
> 1.5 // 0.5
3.0
~~~
##### 取模
`a % b == a - ((a // b) * b)`  
`x-x%0.01`保留两位小数 `x-x%0.001`保留三位小数
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> x = math.pi
> x - x%0.01
3.14
> x - x%0.001
3.141
~~~
#### 3-2 关系运算
**\< &emsp; \> &emsp; \<= &emsp; \> &emsp; == &emsp; ~=（不等）**  
结果为Boolean
#### 3-4 数学库
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> math.pi
3.1415926535898
> math.sin( math.pi / 6 )
0.5
> math.cos( math.pi / 3 )
0.5
> math.huge
inf
~~~
##### 3-4-1 随机数发生器
`math.random(a)`返回1~a范围内的伪随机数
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> math.random(6)
3
~~~
##### 3-4-2 取整函数
floor向负无穷取整，ceil向正无穷取整，modf向零取整和返回小数部分
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> math.floor(3.3)
3
> math.floor(-3.3)
-4
> math.ceil(3.3)
4
> math.ceil(-3.3)
-3
> math.modf(3.3)
3   0.3
> math.modf(-3.3)
-3  -0.3
> math.floor(2^70)
1.1805916207174e+21
~~~
#### 3-5 范围
超过范围会发生回环
~~~lua
Lua 5.4.6  Copyright (C) 1994-2023 Lua.org, PUC-Rio
> math.maxinteger
9223372036854775807
> math.mininteger
-9223372036854775808
> math.maxinteger + 1 == math.mininteger
true
> math.mininteger - 1 == math.maxinteger
true
> -math.mininteger == math.mininteger
true
> math.mininteger // 1 == math.mininteger
true
~~~

