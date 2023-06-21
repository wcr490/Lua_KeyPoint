# Lua基本要点
参考：
* [Lua官网](http://www.lua.org/manual/5.3/)
* [ASCII码对照表](http://c.biancheng.net/c/ascii/)


## 1.1
* 直接赋值使用，全局变量，关键字` local `可以声明局部变量
* 未声明变量类型为` nil `，值也为` nil `
* 支持多变量赋值` a,b = 1,2 `
* Number类型，同时支持十六进制表示，科学计数法表示 ` a = 0x11 b = 2e10 `
* 运算相对不严谨，可直接使用运算符 ` (a+b) `
* Lua5.3支持数值移动语法 ` 1<<3 ` 输出` 8 `
### 总结：弱类型脚本语言特性

## 1.2
* 字符串可用` "" `或` '' `
* 支持` /n `
* ` [[[文本]] `可打印原始值
* 字符串连接符号采用. ` c = a.b `
* 类型转换支持` tostring `和` tonumber ` 出现` error `默认值为` nil `
* 支持通过` #a `的形式可直接获取字符的length
### 总结：提供较多简便语法

## 1.3
*定义写法
```
funtion f(n)
body
end
```
* 函数中没传入的值为` nil `
* return可以同时返回多个值 ` return a,b `
* 支持同时通过函数返回值赋值多个变量 ` i,j = f(1,2) `
### 总结：风格十分自由，但需要习惯

## 1.4
* table类似数组，不同在于不限制存放类型，并且索引从1开始，而非从0开始
```
a = {
1,
"abcde",
function()
body
end
}
```
* 索引` a[1] `形式查找，不存在则为` nil `，同时支持` #a `得到数组长度
* 提供工具实现table插入，但不确定性能损耗 ` table.insert(table_A,"abcde") `
* 工具类十分强大，` table.insert(table_A,2,"abc") `可直接在第二项插入` abc `，此时所有的数据向后移动
* 支持` table.remove(a,2) `，此时我们移除了索引为2的元素，其他元素向前补，此外，remove方法存在返回值，为对应索引的值，支持` b = talbe.remove(a,2) `
* 支持索引为字符串，类似字典，或二维数组，也很像json
```
a = {
a = 1 , 
b = "abc" , 
c = function()
end,
d = 123456
}
```
查找支持简便写法，a.a表示索引为a的值
* 存在内置` _G `，类型为table，其中包含所有已定义的全局变量，Lua围绕其运转，` _G `多维结构构建出类与方法，类似Java中的面对对象，` _G["table"] `即table类所在，同时，` _G["table"]["insert"] `即table类的方法` table.insert `
### 总结：Table是Lua最重要的基础，包含大量工具，结合了链表和数组的特点，应从底层多加理解，通过_G我们就了解了Lua的运作原理，是Lua灵魂所在

## 1.5.1
* ` < , <=. == `等被支持
* ` ~= `为不等于符号
* 与 - ` and `
* 或 - ` or `
* 非 - ` not `
* ` 0 `不代表假，只有` nil `和` false `为假
* 返回值中，与，或不返回` true `和` false `，而是返回数值，` b = 0 , a = nil ` 此时` (a and b) `为` nil `，` (a or b) `为` 0 `， ` (not a) `为` true `， ` (not b) `为` false `
* 由上一点的特性，可以简化短路求值 ` (a > 100 and "yes" or "no") ` ，类似三元运算
### 总结：lua中` 0 `代表真很重要

## 1.5.2
* if分支判断写法
```
if 1 > 5 then
print("yes,1>5")
else 
print("no,1<5")
end
```
* 同时支持` elseif 1 < 5 then `
### 总结：` then `和` end `需要特别留意

## 1.5.3
* for循环写法
```
for i=1,10 do
print (i)
end
```
* 可规定步长
```
for i=1,10,2 do
print (i)
end
```
此时步长为` 2 `
* 在循环中不允许i发生变化，如修改编译器将其自动译为local局部临时变量
* 支持break提前结束循环 ` if i == 3 then break end  `
### 总结：注意` for `后面的` do `，注意与C不同之处在于不能修改循环参数

## 1.5.4
* while循环写法
```
local n = 10
while n > 5 do
n = n - 1
print(n)
end
```
* 同样支持break语法，语法相同
* 不支持自减自增操作，` n++ `等写法报错
### 总结：注意` do `，注意自增自减的不兼容

## 1.6
* 提供工具` a = string.char(0x36,0x37) `，直接转译ASCII码，得到` 67 `
* ` 0x00 `也被允许存储
* ` string.byte(a , 2) `此方法实现直接获取字符对应位数的字符
### 总结：Lua的` string `工具类允许我们在其中安全存储大量二进制流，不会受到影响

  



