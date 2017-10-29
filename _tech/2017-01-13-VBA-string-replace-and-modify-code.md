---
title: VBA中字符处理函数和替换函数的使用 
layout: single
toc: true
---

## 替换函数repalce的用法

### 语法

`Replace(expression, find, replace[, start[, count[, compare]]])`

### 解释

> expression 必需的。字符串表达式，包含要替换的子字符串。 
> find 必需的。要搜索到的子字符串。 
> replace 必需的。用来替换的子字符串。 
> start 可选的。在表达式中子字符串搜索的开始位置。如果忽略，假定从1开始。 
> count 可选的。子字符串进行替换的次数。如果忽略，缺省值是 –1，它表明进行所有可能的替换。 
> compare 可选的。数字值，表示判别子字符串时所用的比较方式。

### 示例

`compStrConv = Sheets("门店地址").Cells(F, compColumn).Text`

`compStrCleanSpace = Replace(compStrConv, " ", "") #替换空格 `

`compStrCleanSpace = Replace("hello world ", " hello ", "")`



处理替换字符是 这个是必须的



## 把字符转化成指定类型strconv

### 语法

`StrConv(string,   conversion,   LCID) `

### 解释

>string   必要参数。要转换的字符串表达式。    
>conversion   必要参数。Integer。其值的和决定转换的类型。    
>LCID   可选的。如果与系统LocaleID不同，则为LocaleID（系统LocaleID为缺省值。）
>
>conversion   参数的设置值为：  
>
>常数   值   说明    
>vbUpperCase   1   将字符串文字转成大写。    
>vbLowerCase   2   将字符串文字转成小写。    
>vbProperCase  3   将字符串中每个字的开头字母转成大写。    
>vbWide        4   将字符串中单字节字符转成双字节字符。    
>vbNarrow      8   将字符串中双字节字符转成单字节字符。*    
>vbKatakana    16  将字符串中平假名字符转成片假名字符。  **  
>
>vbHiragana    32  将字符串中片假名字符转成平假名字符。  **  
>vbUnicode     64  根据系统的缺省码页将字符串转成   Unicode。    
>vbFromUnicode 128 将字符串由   Unicode   转成系统的缺省码页。    
>
>
>
>*应用到远东国别。  
>**仅应用到日本。  
>
>注意   这些常数是由   VBA   指定的。可以在程序中使用它们来替换真正的值。其中大部分是可以组合的，例如   vbUpperCase   +   vbWide，互斥的常数不能组合，例如   vbUnicode   +   vbFromUnicode。当在不适用的国别使用常数   vbWide、vbNarrow、vbKatakana，和   vbHiragana   时，就会导致运行时错误。 
>
>注意   这些常数是由   VBA   指定的。可以在程序中使用它们来替换真正的值。其中大部分是可以组合的，例如   vbUpperCase   +   vbWide，互斥的常数不能组合，例如   vbUnicode   +   vbFromUnicode。当在不适用的国别使用常数   vbWide、vbNarrow、vbKatakana，和   vbHiragana   时，就会导致运行时错误。  
>
>下面是一些一般情况下的有效分界符：Null   (Chr$(0))，水平制表符   (Chr$(9))，换行   (Chr$(10))，垂直制表符   (Chr$(11))，换页   (Chr$(12))   ，回车   (Chr$(13))，空白   (SBCS)   (Chr$(32))。在   DBCS中，空白的实际值会随国家/地区而不同。  
>
>说明  
>
>在把   ANSI   格式的   Byte   数组转换为字符串时，您应该使用   StrConv   函数。当您转换   Unicode   格式的这种数组时，使用赋值语句。

### 示例

`StrConv(Sheets("门店地址").Cells(F, compColumn).Text, vbNarrow)`

参考链接[StrConv Function](https://msdn.microsoft.com/en-us/library/office/gg264628.aspx)

## 查找字符的位置instr

### 语法

`InStr([Start,]string1,string2[,compare])`

### 解释

> 参数Start为可选参数，设置查找的起点，如果省略，则从第一个字符的位置开始查找，当指定了参数Compare时，则要指定此参数。
>
> 参数string1为被查找的字符串，
>
> 参数string2为要查找的字符串，这两个参数都是必需的。
>
> 如果在String1中没有找到String2，返回0；
>
> 如果找到String2，则返回String2第一个出现的首字符位置(即1到String1的长度)；
>
> 如果String2的长度为零，返回Start。



### 示例

> Sub test()
>
> Dim SearchString, SearchChar, MyPos
>
> SearchString = "XXpXXpXXPXXP"   '被搜索的字符串
>
> SearchChar = "P"    '要查找字符串 "P"

  '从第四个字符开始，以文本比较的方式找起，返回值为 6(小写 p)
  '小写 p 和大写 P 在文本比较下是一样的
  MyPos = InStr(4, SearchString, SearchChar, 1)
  Debug.Print MyPos
  '从第一个字符开使，以二进制比较的方式找起，返回值为 9(大写 P)
  '小写 p 和大写 P 在二进制比较下是不一样的
  MyPos = InStr(1, SearchString, SearchChar, 0)
  Debug.Print MyPos
  '缺省的比对方式为二进制比较(最后一个参数可省略)
  MyPos = InStr(SearchString, SearchChar)    '返回 9
  Debug.Print MyPos
  MyPos = InStr(1, SearchString, "W")    '返回 0
  Debug.Print MyPos
End Sub

## mid函数用法

### 语法

`Mid(String,Start[,Len])`

### 解释

> 如果参数String包含Null，则返回Null；
>
> 如果参数Start超过了String的字符数，则返回零长度字符串(“”)；
>
> 如果参数Len省略或超过了文本的字符数，则返回字符串从Start到最后的所有字符。

### 示例

> Str=Mid(“This is a pig.”,6,2)
>
> MyString = "Mid Function Demo"    '建立一个字符串
> FirstWord = Mid(MyString, 1, 3)    '返回 "Mid"
> LastWord = Mid(MyString, 14, 4)    '返回 "Demo"
> MidWords = Mid(MyString, 5)    '返回 "Funcion Demo"
>
> 





参考链接[在VBA中处理字符串常用的函数](http://www.51testing.com/html/19/226119-212209.html)

