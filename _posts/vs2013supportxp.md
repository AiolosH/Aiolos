---
title: vs2013编写的程序可以运行在xp系统中
description: 转载の
date: 2016-11-01 13:22:51 +08:00
tags: 转载の
category: 转载の
---
<b>[转载]</b> [大传送门](http://blog.csdn.net/asanscape/article/details/38752655)   

微软为了推销自家平台，默认配置下VS2012和VS2013编写的应用程序只能在Vista/Win7/Win8上运行。但幸好还保留了生成XP程序的设置项。XP和Win2003的用户还是大量存在的，我们程序软件的发布不能不考虑他们。


　　1. 项目菜单->项目属性->配置属性->常规->平台工具集，选择“VS2013WindowsXP(v120_xp)”;

　　2. 项目菜单->项目属性->配置属性->常规->MFC的使用，选择在静态库中使用MFC;

　　3. 项目菜单->项目属性->链接器->系统->子系统->控制台或窗口windows（根据你的项目类型选择），第二项版本号设成5.01。

　　4. C/C++->代码生成->运行库，选择“多线程调试(/MTd)";

　　5. 还需要至少带有Update3(或4），这一点我没有验证，因为我直接安装的就是带有Update3的VS2013。

　　以上就OK了。缺点仍然有，例如静态编译的EXE比正常动态要大不少，目前我尚未试出动态编译后在XP中能运行的方法，--不过这个不要紧，因为VS2013版本如此之高，客户的电脑上很难自带配有它的运行库，你即使动态编译，发布软件时也还是要带上运行库的，只不过在多个程序时只需带一份运行库罢了。

　　另外，我在实际大项目中用上述方法，仍有出错现象发生。以后再研究吧。一般情况下上述方法就可以了。

　　在网上另外发现了这个贴子，说得很详细，包括非IDE的命令行编译，一起贴到下面：

　　问题一：编译出来的exe在xp上面运行提示“不是有效的win32应用程序”

　　在vs2012/2013版本里面，其自带的c编译器cl.exe，若直接使用cl a.c编译，那么生成出来的exe放在vista及以上版本直接运行没有问题，但是在xp上则会出来“不是有效的win32应用程序”的出错提示。这是因为vs2012/2013自带的c编译器默认情况下生成的exe会默认只支持vista及以上版本的windows系统。

　　解决方法：

　　对于使用命令行cl.exe直接编译的方式：
先用cl a.c编译一遍，此时会生成a.exe和a.obj两个文件，此时，再执行 link b.obj /subsystem:console,5.01，它会链接一个新的a.exe出来，此时的exe就可以在xp上运行了。相比vs2010以及以前版本的编译器编译，会多第二步的link过程，后面的参数也很容易理解，subsystem,5.01，此处的5.01是指的windows内核版本号，5.01表示windows 2000 with sp1，即此exe可以在win2000 sp1及以上的windows中执行。

　　当然，这个地方的/subsystem后面有很多参数，上面给的console,5.01是指命令行程序，如果是有GUI即有窗口的程序，改成windows,5.01即可。！！注意！！此处的5.01一定不要想当然改成5.0就变成windows 2000 不带sp1的版本，实际上，5.0并不被vs2013的编译所承认，会报警告不认5.0，就会按照默认的不带5.01的方式编译，这样就无法在vista以下的系统中运行生成的exe了。

　　对于在vs2013里面使用新建项目的方式：
右击相应的项目，选择“属性”，在项目属性页中的“配置属性”下面的“常规”里面，把“平台工具集”，由“Visual Studio 2013 (v120)”改成“Visual Studio 2013 - Windows XP (v120_xp)”，确定之后，重新生成项目即可。当然这里按这样修改的话，就只能在winxp及以上的版本系统里面运行了。

　　问题二：用vs2010/2012/2013编译出来的exe在未安装vc++运行库的机器上运行时提示”未找到MSVCR120D.DLL“从而无法运行

　　这是个老问题了，无非就是运行库动态编译和静态编译的问题了。dll动态加载的话有个好处，它可以减少生成的exe文件的体积，但是缺点就是如果对应的系统环境变量或者exe所在的目录里面找不到其所需要的dll文件的话，程序就会拒绝执行。而静态编译就是把所有需要的库都静态编译到exe文件里面，这样就可以在所有的系统平台上都能运行，但它也有一个缺点，就是生成的exe文件因为已经带了部分库的代码，所以体积会相对动态编译出来的exe大（具体大多少要根据库的内容才能确定）。

　　解决方法：

　　对于直接使用cl.exe和link.exe编译连接的方式：
直接在cl.exe编译的时候或者在makefile里面把编译参数加上/MT即可。


　　对于在vs2013里面使用新建项目的方式：
右击相应的项目，选择“属性”，在项目属性页中的“配置属性”下面的“C/C++”下面的“代码生成”一项，由默认的“多线程调试DLL (/MDd)”，改成“多线程 (/MT)”，确定之后，重新生成项目即可。这样所得的exe文件就是静态编译了。