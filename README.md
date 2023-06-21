# Lua基本要点
参考：
Lua官网：http://www.lua.org/manual/5.3/
ASCII码对照表：http://c.biancheng.net/c/ascii/

## 1.1
* 直接赋值使用，全局变量，关键字` local `可以声明局部变量
* 未声明变量类型为` nil `，值也为` nil `
* 支持多变量赋值` a,b = 1,2 `
* Number类型，同时支持十六进制表示，科学计数法表示 a = 0x11 b = 2e10
* 运算相对不严谨，可直接使用运算符 (a+b)
* Lua5.3支持数值移动语法 1<<3 输出8
### 总结：弱类型脚本语言特性

## 1.2
* 字符串可用""或''
* 支持/n
* [[[文本]]可打印原始值
* 字符串连接符号采用. c = a.b
* 类型转换支持tostring和tonumber 出现error默认nil
* 支持通过#a的形式可直接获取字符的length
### 总结：提供较多简便语法

## 1.3
* funtion f(n)
<br>body……</br> 
<br>end</br> 
* 函数中没传入的值为nil
* return可以同时返回多个值 return a,b
* 支持同时通过函数返回值赋值多个变量 i,j = f(1,2)
### 总结：风格十分自由，但需要习惯

## 1.4
* table类似数组，不同在于不限制存放类型，并且索引从1开始，而非从0开始 a = {1,"abcde",function() end}
* 索引a[1]形式查找，不存在则为nil，同时支持#a得到数组长度
* 提供工具实现table插入，但不确定性能损耗 table.insert(table_A,"abcde")
* 工具类十分强大，table.insert(table_A,2,"abc")可直接在第二项插入abc，此时所有的数据向后移动
* 支持table.remove(a,2)，此时我们移除了索引为2的元素，其他元素向前补，此外，remove方法存在返回值，为对应索引的值，支持b = talbe.remove(a,2)
* 支持索引为字符串，类似字典，或二维数组，也很像json
<br>a = {
<br>a = 1 , 
<br>b = "abc" , 
<br>c = function()
<br>end,
<br>d = 123456
<br>}
<br>查找支持简便写法，a.a表示索引为a的值
* 存在内置_G，类型为table，其中包含所有已定义的全局变量，Lua围绕其运转，_G多维结构构建出类与方法，类似Java中的面对对象，_G["table"]即table类所在，同时，_G["table"]["insert"]即table类的方法table.insert
### 总结：Table是Lua最重要的基础，包含大量工具，结合了链表和数组的特点，应从底层多加理解，通过_G我们就了解了Lua的运作原理，是Lua灵魂所在

## 1.5.1
* < , <=. ==等被支持
* ~=为不等于符号
* 与 - and
* 或 - or
* 非 - not
* 0不代表假，只有nil和false为假
* 返回值中，与，或不返回true和false，而是返回数值，b = 0 , a = nil此时(a and b)为nil，(a or b)为0， (not a)为true， (not b)为false
* 由上一点的特性，可以简化短路求值 (a > 100 and "yes" or "no")，类似三元运算
### 总结：lua中0代表真很重要

## 1.5.2
* if分支判断写法<br>if 1 > 5 then
<br>print("yes,1>5")
<br>else 
<br>print("no,1<5")
<br>end
* 同时支持elseif 1 < 5 then
### 总结：then和end需要特别留意

## 1.5.3
* for循环写法<br>for i=1,10 do

<br>print (i)
<br>end
* 可规定步长<br>for i=1,10,2 do
<br>print (i)
<br>end
<br>此时步长为2
* 在循环中不允许i发生变化，如修改编译器将其自动译为local局部临时变量
* 支持break提前结束循环 if i == 3 then break end 
### 总结：注意for后面的do，注意与C不同之处在于不能修改循环参数

## 1.5.4
* while循环写法 <br>local n = 10
<br>while n > 5 do
<br> n = n - 1
<br>print(n)
<br>end
* 同样支持break语法，语法相同
* 不支持自减自增操作，n++等写法报错
### 总结：注意do，注意自增自减的不兼容

## 1.6
* 提供工具a = string.char(0x36,0x37)，直接转译ASCII码，得到67
* 0x00也被允许存储
* string.byte(a , 2)此方法实现直接获取字符对应位数的字符
### 总结：Lua的string工具类允许我们在其中安全存储大量二进制流，不会受到影响

  



