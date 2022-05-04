# 项目介绍

https://github.com/schmurtzm/Gamelist-Translator

这个项目可以利用一个powershell脚本，结合Google翻译对gamelist做翻译。到本文写作时间为止，只翻译介绍的部分。

# 设置powershell

很尴尬的是，这个脚本要在powershell运行，还需要修改权限。

https://blog.csdn.net/m0_47696151/article/details/119803877

简单一点说就是你可以偷懒地在PS上打下面命令

Set-ExecutionPolicy -ExecutionPolicy Bypass -Scope CurrentUser

为安全起见，记得用完关闭权限

Set-ExecutionPolicy -ExecutionPolicy Undefined -Scope CurrentUser

# 翻译

Gamelist-Translator.ps1 "c:\RetroBat\roms\ports\gamelist.xml"