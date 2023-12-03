# Delphi 自学笔记

## 一  基础知识

### 1. 内置数据类型

#### 1.1 基本数据类型

##### (1) 布尔型(Boolean)

```pascal
// 声明变量
var
  value:Boolean;
// 初始化变量
value:=False;

// 在一行中声明并初始化变量,本地变量不支持这种方式
var
  value:Boolean=True;
```



##### (2) 字符型(Char)

```pascal
{
  1. Char 
 	在2010年以前的版本中，占用的字节是1个字节。
 	在2010年以后的版本中，Char类型的变量默认是WideChar，占用2个字节.
}
var
  value:Char='中'
{
  2. WideChar
  	2或4个字节
}
  value:WideChar='中'
{
  3. AnsiChar
    这是 AnsiString 类型的一部分，可以存储一个单字节的字符。好像是旧版的
}

{
  4. UTF8Char
    这种类型用于存储 UTF-8 编码的字符。在 Delphi 的现代版本中，UTF-8 编码是默认的字符串编码。
}
```

```pascal
// 转义字符
// 回车符 #13
// 换行符 #10
```



##### (3) 整数型

Integer：这是最常用的整数类型，用于表示 -2,147,483,648 到 2,147,483,647 的整数。
Word：该类型用于表示 0 到 65,535 的无符号整数。
Byte：该类型用于表示 0 到 255 的无符号整数。
Cardinal：该类型是 32 位无符号整数，用于表示 0 到 4,294,967,295 的整数。
Int64：该类型是 64 位有符号整数，用于表示 -9,223,372,036,854,775,808 到 9,223,372,036,854,775,807 的整数。
UInt64：该类型是 64 位无符号整数，用于表示 0 到 18,446,744,073,709,551,615 的整数。

##### (4) 浮点数

Single：单精度浮点数，占用4字节2；
Double：双精度浮点数，占用8字节2；
Extended：扩展精度浮点数，占用10字节2。

##### (5) 字节型

```pascal
Buffer=array of Byte //  字节数组
```

#### 1.2 复杂数据类型 

##### (1) 枚举类型

```pascal
// 定义枚举类型
TMyEnum = (zero,one,two);

// 初始化以及使用
myEnum:=zero;
case myEnum of
  one:
    WriteLn((Ord(one)));
  two:
    WriteLn(Ord(two));
  else
    WriteLn(Ord(zero));
end;
```

##### (2) 记录类型

类似C语言结构体

```pascal
// 定义record类型
TStudent = record
  Name: string;
  Age: Integer;
end;
// 初始化以及使用
student: TStudent;
student.Name:='Shine';
student.Age:=18;

// 也可以有方法
TMyStruct = record
    X, Y: Integer;
    private
    procedure SetX(value: Integer);
    procedure SetY(value: Integer);
end;
procedure TMyStruct.SetX(value: Integer);
begin
  X := value;
end;
procedure TMyStruct.SetY(value: Integer);
begin
  Y := value;
end;
```

##### (3) 字符串类型

字符串下表从1开始

这个也属于基本类型，没有方法。通过特定结构才具有方法（待研究原理）

字符串是一种特殊的存储结构，它用于存储文本数据。字符串在内存中以UTF-16编码格式存储，可以包含字母、数字、符号和特殊字符。

```pascal
//声明
var
  strValue:string;
// 初始化
strValue:='sdf';
```

常用方法

有系统提供的函数，也有通过record helper for string定义的例程

```pascal
{ Copy方法}
var
  templateStr:string;
  subString:string;
begin
  templateStr:='Hello World!';
  subString:=Copy(templateStr,2); //'ello World!';
  WriteLn(subString);
  subString:=Copy(templateStr,2,3);//'llo'
  WriteLn(subString);
 end
 {Pos 函数 }
 index := Pos('fox', 'mmmfox');//返回'fox'在'mmmfox'的下标
 {Constains 函数}
 WriteLn(text.Contains('fox'));//返回是否包含'fox'
 //未完
```

##### (4) 数组类型

定长数组

```pascal
var
  arr: array[0..99] of Integer;
  i, sum: Integer;
begin
  for i := 0 to 99 do
  begin
    arr[i] := i + 1;
  end;
  sum := 0;
  for i := 0 to 99 do
  begin
    sum := sum + arr[i];
  end;
  WriteLn('The sum of numbers from 1 to 100 is: ', sum);
  ReadLn;
end;
```

不定长数组

```pascal
  arr: array of Integer;
  i: Integer;
begin
  // 分配数组内存
  SetLength(arr, 3); 
  // 添加元素到数组
  arr[0] := 10;
  arr[1] := 20;
  arr[2] := 30;
//  arr[4] :=20;

  // 输出数组元素
  for i := 0 to Length(arr) - 1 do
  begin
    Write(arr[i]);
    Write(' ');
  end;
  WriteLn(Length(arr));
  ReadLn;
end;
```

##### (5) 指针类型

```pascal
var
  address: uTypes.RAddress;
  addressPtr: ^uTypes.RAddress;
begin
  address.FProvince:='北京';
  address.FCity:='北京';
  address.FDistinct:='朝阳区';
  addressPtr:=@address;
  WriteLn(addressPtr.FProvince);
end;
```

(5.1) 类型指针

(5.2) 零指针

(5.3) 函数指针

(5.4) 过程指针

(5.5) 记录指针

(5.6) 对象指针

(5.7) 字符串指针

(5.8) 指针数组

(5.9) 引用计数指针

##### (6) 子界类型 

```pascal
type
  Range=0..10;
var
  myArray: array[Range] of Integer;
  x: Integer;
begin
  x := myArray[11]; // 这里使用数组索引越界错误来演示错误情况
  WriteLn(IntToStr(x));
end;
```



### 2. 常量与变量

#### 2.1 常量

```pascal
{	1. 布尔常量
	True,False
}
{
	2. 整数常量
	MaxInt,MinInt
}

{
	3. todo
}
```

#### 2.2 变量

本地变量声明初始化不能放在同一行

大小写不敏感

工程命名见工程命名规范，

```
//略
```



### 3. 代码注释

```pascal
// 单行注释
{
	多行注释
}
{*******************************************************}
{                                                       }
{           CodeGear Delphi Runtime Library             }
{                                                       }
{ Copyright(c) 1995-2022 Embarcadero Technologies, Inc. }
{              All rights reserved                      }
{                                                       }
{   Copyright and license exceptions noted in source    }
{                                                       }
{*******************************************************}
{*******************************************************}
{               System Utilities Unit                   }
{*******************************************************}

```

### 4.  运算符

#### 4.1 算数运算符

#### 4.2 逻辑运算符

#### 4.3 位运算符

#### 4.4 集合运算符



### 5.  程序三大结构

#### 5.1 顺序结构

```pascal
// 从上到下执行
```

#### 5.2 分支结构

##### (1) if分支

```pascal
var
  i: Integer;
begin
  Randomize;
  i := Random(10);
  if (i < 3) and (i >= 0) then
    WriteLn(IntToStr(i) + '<3')
  else if (i >= 3) and (i < 6) then
    WriteLn('3<=' + IntToStr(i) + '<6')
  else if (i < 10) then
    WriteLn('6<=' + IntToStr(i) + '<10')
  else
  begin
    WriteLn('出现未知情况');
  end;
end;
```

##### (2) case 分支

```pascal
var
  num: Integer;
begin
  Write('Enter an integer: ');
  ReadLn(num);

  if num mod 2 = 0 then
    Write('You entered an even number.')
  else
    Write('You entered an odd number.');

  WriteLn;

  case num of
    1: WriteLn('You entered 1.');
    2: WriteLn('You entered 2.');
    3: WriteLn('You entered 3.');
    else WriteLn('You entered a number other than 1, 2, or 3.');
  end;
end;
```



#### 5.3 循环结构

包括continue和break俩个关键字

##### (1) for循环

```pascal
var
  i:Integer;
begin
  for i := 1 to 5 do
  begin
    // 执行代码块
    if i=2 then
    begin
      continue; // 跳出本轮
    end;
    if i=4 then
    begin
      break; // 跳出本次
    end;
  end;
  WriteLn(i); //4
end;
```

##### (2) while循环

```pascal
var
  i: Integer;
begin
  i := 1;
  while i <= 5 do
  begin
    i := i + 1;
    if i = 2 then
    begin
      continue;  // 跳出本轮
    end;
    if i = 4 then
    begin
      break;  // 跳出本次
    end;

  end;
  WriteLn(i);  //4
end;
```

##### (3) repeat循环

```pascal
var
  i: Integer;
begin
  i := 1;
  repeat
    i := i + 1;
    if i = 3 then
    begin
      continue;
    end;
    if i = 4 then
    begin
      break;
    end;
  until i > 10;
  WriteLn(i); // 4
end;
```

##### (4) goto 语句（一般不使用）

```pascal
var
  i: Integer;
  label EndLoop;
begin
  for i := 1 to 10 do
  begin
    if i = 5 then
      goto EndLoop;
    WriteLn(i);
  end;
EndLoop:
  WriteLn('Loop ended');
end;
```

### 6. 例程(routine)

过程与函数的区别



#### 6.1 过程(procedure)

```

```

#### 6.2 函数(function)

```

```



### 7. 面向对象

### 8.  泛型



## 二 多线程编程

## 三 工程结构与代码规范

### 1. 命名规范

### 2. 源文件格式

#### 2.1 DPR文件

DelphiProject文件，包含了Pascal代码，是应用系统的工程文件。

#### 2.2 PAS文件

Pascal文件，Pascal单元的源代码，可以是与窗体有关的单元或是独立的单元。

```pascal
unit 单元名字
interface //对外暴露的接口
implementation //实现部分
initialization //程序运行前执行
finalization //程序运行后执行
```

