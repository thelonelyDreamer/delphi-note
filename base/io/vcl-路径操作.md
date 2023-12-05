## 一  windows平台

### 1. 获取启动路径

#### 1.1  vcl 程序

```pascal
 ExtractFilePath(Application.ExeName) // 输出D:\debug\
```

### 2.  绝对路径，相对路径

#### 1. 绝对路径+相对路径=绝对路径

```pascal
RelativePath := 'MyFolder\MyFile.txt'; // 相对路径
AbsolutePath := ExpandFileName(RelativePath); // 将相对路径转换为绝对路径
WriteLn(AbsolutePath); // 输出绝对路径
```



#### 2. 绝对路径-绝对路径=相对路径


## resource
https://www.cnblogs.com/txgh/p/17837089.html