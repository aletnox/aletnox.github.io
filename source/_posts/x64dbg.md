---
title: x64dbg
---

x64dbg下载官网
[https://x64dbg.com/](https://x64dbg.com/)
反反调试插件
[https://github.com/x64dbg/ScyllaHide/releases](https://github.com/x64dbg/ScyllaHide/releases)
确保下面反反调试选项
将ScyllaHide中32和64对应的插件都放到x64dbg的对应位置的plugins目录下面，重新启动就可以看到
![image.png](https://aletnox.github.io/images/x64dbg/1648087364054-0335c8c5-3e61-4e38-839a-c213d9207892.png)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/1723622/1648020881544-3b277a27-d9ed-4f79-89e6-1b9f0a1654e2.png#clientId=u1ffcc760-c4cd-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=507&id=u0ca99c70&margin=%5Bobject%20Object%5D&name=image.png&originHeight=507&originWidth=557&originalType=binary&ratio=1&rotation=0&showTitle=false&size=42708&status=done&style=none&taskId=u2b07d89b-0c5a-4e1e-85c0-7735af3a716&title=&width=557)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/1723622/1648020939236-c96c79ee-1de0-479e-8e81-94e1d28c5822.png#clientId=u1ffcc760-c4cd-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=228&id=ucc855f67&margin=%5Bobject%20Object%5D&name=image.png&originHeight=228&originWidth=560&originalType=binary&ratio=1&rotation=0&showTitle=false&size=20758&status=done&style=none&taskId=u785bfddd-f604-49f4-b182-48f14f872ad&title=&width=560)
<!-- more -->
# 调试dll
因为dll无法自己启动运行，所以需要一个加载dll的程序，一般windows都是用rundll32.exe进行加载
1、首先用x64dbg打开rundll32.exe文件，如果加载的dll，需要设置调试器，如下配置
![image.png](https://cdn.nlark.com/yuque/0/2022/png/1723622/1648093151004-865b6dc3-a57b-454b-8f67-73ef991068d9.png#clientId=u9dc2b3ae-5a8b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=895&id=uc650860c&margin=%5Bobject%20Object%5D&name=image.png&originHeight=895&originWidth=647&originalType=binary&ratio=1&rotation=0&showTitle=false&size=59752&status=done&style=none&taskId=u849c3a99-17fd-4fde-b7c3-92febf9b04c&title=&width=647)
这里需要做两个设置：

- 文件->改变命令行(change command line)
- 将要调试的dll和dll要使用的参数配置并启动，在启动参数的后面配置常规的rundll32.exe dllname,exportName argumetns的格式即可
- 然后想要查看dll的导出函数有哪些的话可以使用PEview或者IDA均可查看

![image.png](https://cdn.nlark.com/yuque/0/2022/png/1723622/1648092972534-a8c2232b-15c5-4208-80f8-69ad39808e0a.png#clientId=u9dc2b3ae-5a8b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=99&id=u097edfa2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=99&originWidth=412&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4788&status=done&style=none&taskId=u5b600b3c-d7a7-49ee-9728-3698fe6429e&title=&width=412)

- 在断点出，右键添加需要调试的dll文件。如下（krpt.dll）

![image.png](https://cdn.nlark.com/yuque/0/2022/png/1723622/1648093050706-42185cb1-58b1-4f20-96e9-58d5e21d46c2.png#clientId=u9dc2b3ae-5a8b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=200&id=u8ede4f23&margin=%5Bobject%20Object%5D&name=image.png&originHeight=200&originWidth=891&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36198&status=done&style=none&taskId=u01882bb7-ecdb-4833-b812-4f1e9004e4a&title=&width=891)
设置好之后就可以进行调试了，按F9 逐个加载dll，当被调试到dll执行入口点处表示程序已经启动。

- 这里我在调试的时候出现了问题，我使用x64位打开的程序，但是本质上被调试的dll是32位的，所以加x64加载的时候会发现直接就载入载出了，无法调试，我换到x32就好了。

综上所述就是需要的准备条件。

## dll分析
在分析的时候结合IDA可以快速定位到想要调试的函数，或者想要调试到的内存地址（位置）

- Ctrl+G 可以跳转到执行的地址，然后打断点，F9

动态调试的话最好是有目的的去查看，某个函数的参数，或者函数的功能时候去静态和动态结合一起看。

如果是要查看具体的行为的话，最好是使用process monitor 监控注册表和文件的变化，但是使用起来有点大海捞针的感觉，但是一般明显的行为还是可以看到的。

目前总结来说就这些，后续根据情况和看书总结进行补充。






















