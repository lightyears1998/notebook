# Visual Basic编程笔记

## 基础

### 基本数据类型

Integer, Boolean

- VB中的不等运算符是`<>`；不能使用`!=`。
- VB中取反是`Not`

## 语句

### 顺序语句

- 注释 `' 在行中以单引号开头的内容为单行注释，没有多行注释。`
- 严格模式 `Option Explicit`
- 声明语句 `Dim PeopleCount As Integer`
- 赋值语句 `PeopleCount = 0`

### 分支语句

```vb
If Len(PeopleNumberTextbox.Text) = 0 Then
    PeopleCount = 0
ElseIf IsNumeric(PeopleNumberTextbox.Text) Then
    PeopleCount = CInt(PeopleNumberTextbox.Text)
Else
    PeopleNumberTextbox.Text = PeopleCount
End If
```

### 循环语句

```vb
While DrawingHasBegin
    DrawLabel.Caption = Int(Rnd() * PeopleCount)

    ' 修改下面的过程可以修改滚动的速度
    Dim Savetime As Single
    Savetime = Timer
    While Timer < Savetime + 0.05  ' 数值越小，滚动速度越快
        DoEvents
    Wend
Wend
```

## 模块

### 函数

```vb
Sub MyFunction()
    If 1 + 1 <> 2 THEN EXIT SUB
End Sub

Call MyFunction
```
