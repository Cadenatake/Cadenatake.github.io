---
title: "md5sum(Linux)の出力をGet-FileHash(Powershell)で実現！"
date: 2022-06-25T23:31:23+09:00
draft: false
---

### お題：Get-FileHash(Powershell)コマンドの出力を、md5sumコマンドのフォーマットに合わせてパースする。

使いどころ：  
LinuxマシンからWindowsマシンにコピーしたファイルをハッシュ値突合したい場合。

```sh
PS C:\Users\test> # 1ファイルのみ抽出  
PS C:\Users\test> Get-FileHash -a md5 test1 | % { $_.Hash.ToLower() + "  " + (Split-Path $_.Path -Leaf) }   
b990bc6bb668d0e7d72c687da363eae3  test1  
PS C:\Users\test>   
PS C:\Users\test> # カレント全ファイル  
PS C:\Users\test> ls .\ | % { (Get-FileHash -a md5 $_.FullName) } | % { $_.Hash.ToLower() + "  " + (Split-Path $_.Path -Leaf) }  
b990bc6bb668d0e7d72c687da363eae3  test1  
09bv1b5dadf53efa78278a486604a3aa  test2  
PS C:\Users\test>   
```

以上！