## 如何在mac上编写c++程序

有一部分同学买的电脑是mac，也有很多同学问怎么在mac上写c++代码。现在统一解答一下。

### 方案一：使用Clion

#### 下载

[下载网址](https://www.jetbrains.com/clion/download/#section=mac)

如果你的苹果电脑是M1/M2芯片，那么请选择Apple Sillcon，否则选Intel

![image-20220927201026604](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927201026604.png)

然后打开dmg文件将其拖到applcation文件夹即可。

#### 激活

Clion并不是一个免费的软件。但是作为学生，可以向其申请免费使用。点击[这里](https://www.jetbrains.com/zh-cn/community/education/#students)进入申请页面。正常情况下用你的学生邮箱就可以申请。申请之后会自动跳转到Clion，激活成功。

#### 创建第一个项目

点击“新建项目”，选择默认的c++ excutable

![image-20220927203943145](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927203943145.png)

在location处可以改变项目路径和名称。

如果之前你没写过代码，可能会提示

![image-20220927204027175](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927204027175.png)

安装即可。可能需要等待亿些时间。（类似于visual studio的工具链，可能会捆绑一些你可能其实用不到的东西）

然后安装完确认一下

<img src="/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927211547461.png" alt="image-20220927211547461" style="zoom:50%;" />

项目配置没有报错

![image-20220927211608280](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927211608280.png)

然后选中CMakeLists，点击2处的刷新符号，重新构建

![image-20220927211726878](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927211726878.png)

你应当发现此处的项目配置发生了改变。

![image-20220927211737021](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927211737021.png)

此时点击运行，运行helloworld程序，成功

![image-20220927211838631](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927211838631.png)

#### 简单了解Cmake

如果你想要在这个项目下运行多个cpp文件，你有必要了解一下cmake。

![image-20220927212015622](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927212015622.png)

你会发现cmakelist变成了这样。

![image-20220927212042215](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927212042215.png)

然后你顺理成章的点击了main函数旁边的运行

![image-20220927212255496](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927212255496.png)

报错了！查看倒数第三行的报错信息，你会发现出现了重复（duplicate）的符号。

你想到课上使用vs时讲的，一个项目只能使用一个main函数。你把另外一个main改成了main2。学着这样修改。你发现确实可以正常运行。

<font color='Apricot'>但有没有更优雅的解决方案呢？</font>

![image-20220927212700579](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927212700579.png)

你注意到了cmake中最后一行是add_executable，刚刚发生了变化。从含义可以推测出一定是它控制了程序的执行。

让它们各自生成各自的程序一定可以！

![image-20220927212920160](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927212920160.png)

点击Reload changes。你会发现项目构建出现了两个程序。

![image-20220927213032997](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927213032997.png)

然后你高兴的发现点击哪个程序运行，你就可以运行哪一个cpp文件！

事实上，你点击cmake_build_debug，你会发现add_excutable第一个参数正是生成程序的名称！

![image-20220927213245467](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927213245467.png)



在访达打开![image-20220927213323515](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927213323515.png)



双击---helloworld出现了！它正是你刚刚编写的程序！

![image-20220927213343594](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927213343594.png)

Cmake在大型项目管理中有着重要的用途，其本身也是十分复杂的。但在课程中只需要了解这些即可。

同时Clion在windows下也可以使用。

#### 方案二：使用xcode

xcode是专为mac平台打造的全功能IDE（当然你要问我能不能写exe，只能说emmm）

xcode比较大，下载需要耐心等待。

##### 项目搭建

点击新建项目

![image-20220927213913046](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927213913046.png)

选择macOS控制台应用

![image-20220927213932265](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927213932265.png)

项目选项

![image-20220927214102217](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927214102217.png)

注意组织名称写com，别的其实也行，但此处不作介绍。

语言选择c++。

选择项目位置后就可以愉快开发了！

![image-20220927214344955](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927214344955.png)

控制台在屏幕下方。

![image-20220927214423776](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927214423776.png)

##### 运行多个cpp

这个时候已经创建了一个cpp-project的项目，里面包含了一个main.cpp文件
如果这个时候想要在同一个工程里面创建第二个带main函数的c++文件并运行，就需要通过创建Target来实现

Project是一个工程项目，一个Project可以包含多个Target
Target之间互相没有关系，Target于Project的关系是：Target的Setting一部分继承自Project的Setting

![image-20220927214845054](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927214845054.png)

新建target，同样选择commandline tool，填写一个的名称

![image-20220927215021382](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927215021382.png)

在上方，想运行哪一个target，选择对应的即可。

<img src="/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927215233319.png" alt="image-20220927215233319" style="zoom:50%;" />

### 方案三：命令行方式

安装homebrew（如果已经下载过xcode可以跳过，不过既然如此为什么不用xcode呢？）

在你的终端输入这行指令：

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

如果下载很慢一般是网络问题，请自行解决。

安装完成后

```
brew install g++
```

任意位置新建cpp文件。

cpp文件可以用你喜欢的方式打开编辑。

按⌘（command）+ ⌥（option）+c复制当前文件夹路径

终端输入

```
cd 刚才的路径
```

然后

```
g++ yourprogram.cpp -o target
```

target 是生成的可执行文件的名字。

然后会发现生成了可执行文件，点击即可运行。

![image-20220927220347236](/Users/tianjiaye/Library/Application Support/typora-user-images//image-20220927220347236.png)



