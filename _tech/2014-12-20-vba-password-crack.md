---
title: 破解VBA密码
layout: default
---

最近工作需要转换华为TD的MML原始数据，自己原来有的一个版本相对较老了，在[mscbsc](www.mscbsc.com)下载了一个，奈何这个工具是一个exe格式的，我用7z解压后发现其实里面只是一个excel和一个license文件，license还只能够放在C盘，并且还过期了。

在没有办法的情况下，只有自己hack了，发现可以通过更改日期继续使用，但毕竟这样使用不怎么方便。由于该程序是由VBA编写而成的，必须打开excel才能够使用，遂向通过打开VBA工程，查看license的方法，但是VBA工程存在密码，这样的情况下，只能先破解VBA密码解决了。

尝试了网上的集中办法之后，发现最好用的一种办法，记录如下：

1.使用16进制编辑器 [XVI32](http://www.chmaas.handshake.de/delphi/freeware/xvi32/xvi32.htm) 打开需要破解的excel文件

2.找到“CMG”，和"[Host"字符

3.从“CMG”字符开始到“[Host”前的字符全部替换为“”（16进制空格），其中替换的字符包括“CMG”，但不包括“[Host"

4.保存后，重新打开excel文件，按ALT + F11 就可以直接查看VBA的源代码了

注意如果双击excel打开的是界面而不是excel表格，可能是在VBA里禁用了workbook的显示功能，需要先打开一个excel，按ALT+F11打开VBA编辑器，然后再打开之前破解的excel文件，应该就可以看到VBA工程的代码了。

上面的过程也可以使用如下的VBA宏来搞定,代码如下：


	Private Sub VBAPassword()
    '你要解保护的Excel文件路径
	Filename = Application.GetOpenFilename("Excel文件（*.xls & *.xla & *.xlt）,*.xls;*.xla;*.xlt", , "VBA破解")

    If Dir(Filename) = "" Then
        MsgBox "没找到相关文件,清重新设置。"
    Exit Sub
    Else
       FileCopy Filename, Filename & ".bak" '备份文件。
    End If

    Dim GetData As String * 5
    Open Filename For Binary As #1
    Dim CMGs As Long
    Dim DPBo As Long
    For i = 1 To LOF(1)
        Get #1, i, GetData
        If GetData = "CMG=""" Then CMGs = i
        If GetData = "[Host" Then DPBo = i - 2: Exit For
    Next
     
    If CMGs = 0 Then
       MsgBox "请先对VBA编码设置一个保护密码...", 32, "提示"
       Exit Sub
    End If
     
    If Protect = False Then
       Dim St As String * 2
       Dim s20 As String * 1
        
       '取得一个0D0A十六进制字串
       Get #1, CMGs - 2, St
     
       '取得一个20十六制字串
       Get #1, DPBo + 16, s20
     
       '替换加密部份机码
       For i = CMGs To DPBo Step 2
           Put #1, i, St
       Next
        
       '加入不配对符号
       If (DPBo - CMGs) Mod 2 <> 0 Then
          Put #1, DPBo + 1, s20
       End If
       MsgBox "文件解密成功......", 32, "提示"
      End If
    Close #1
	End Sub