# First_post


# Python项目通用的目录结构总结

**引用链接：**

[Python项目通用的目录结构总结_阿丹的彩蛋-CSDN博客_python项目结构](https://blog.csdn.net/mist99/article/details/80707290?ops_request_misc=%7B%22request%5Fid%22%3A%22163962160816780265426825%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=163962160816780265426825&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~baidu_landing_v2~default-4-80707290.pc_search_mgc_flag&utm_term=python项目结构&spm=1018.2226.3001.4187)

[python开源项目目录结构参考和django最佳实践：项目布局_weixin_30527143的博客-CSDN博客](https://blog.csdn.net/weixin_30527143/article/details/96889789)

[Python 项目布局_边缘迷丛-CSDN博客_python 布局](https://blog.csdn.net/yezhenquan123/article/details/79394939)

一个好的项目结构会让我们在开发中更加得心应手。

## 常用项

[python项目结构 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/133991628)

### 常用目录

**log** 日志目录

**conf** 配置目录 .xml 文件

**src** 核心代码

**lib** 第三方库

**docs** 文档库：应该包括 reStructuredText 格式的文档，以便能够被 Sphinx 处理。

**bin** 启动入口,存放可执行文件 .sh，用来存放将被setup.py安装的二进制脚本

**tests** 存放测试代码

**bin binary**是二进制执行文件目录

**etc** 用来存放配置文件的样例

**tools** 用来存放与工具有关的shell脚本

**data** 用来存放其他类型的文件，如媒体文件



**setup.cfg**： 包含 setup.py 默认命令选项的 ini 文件

**MANIFEST.in**：当需要打包源码中不自动包含的附加文件时使用

**LICENSE.txt**： 发行许可文件

**main.py**

[**setup.py**](https://link.zhihu.com/?target=http%3A//setup.py)：运行环境配置，在安装时，它会通过Python分发工具（**distutils**）进行包的安装。

**requirements.txt**：python版本等，应该包含Python包所需要的依赖包，也就是说，所有这些包都会预先通过pip这样的工具进行安装，以保证你的包能正常工作。还可以包含 **test-requirements.txt**，它只列出运行测试套件所需要的依赖包。

[**README.md**](https://link.zhihu.com/?target=http%3A//README.md)：帮助文档

包中还经常需要包含一些额外的数据，如图片、shell脚本等。不过，关于这类文件如何保存并没有一个统一的标准。因此放到任何觉得合适的地方都可以。

### README说明文档结构

- [x] 1.软件定位，软件的基本功能
- [x] 2.运行代码方法：安装环境、启动命令等
- [x] 3.简要使用说明
- [x] 4.代码目录结构说明
- [x] 5.常见问题说明

## 结构总结

项目结构应该保持简单，审慎地使用包和层次结构：过深的层次结构在目录导航时将如同梦魇，但过平的层次结构则会让项目变得臃肿。

一个常犯的错误是将单元测试放在包目录的外面。这些测试实际上应该被包含在软件的子包中，以便：

- 不会偶尔被 **setuptools**（或者其他打包库）作为 tests 顶层模块自动安装；
- 能够被安装，且被其他包用于构建自己的单元测试。

一个常见的设计问题是根据将要存储的代码的类型来创建文件或模块。使用 **functions.py** 或者 **exceptions.py** 这样的文件是很糟糕的方式。这种方式对代码的组织毫无帮助，只能让读代码的人在多个文件之间毫无理由地来回切换。

此外，应该避免创建那种只有一个 **__init__.py** 文件的目录，例如，如果 **hooks.py** 够用的话就不要创建 **hooks/__init__.py**。如果创建目录，那么其中就应该包含属于这一分类/模块的多个Python文件。



**快速生成项目结构：**这里介绍两款工具： hatch、cookiecutter（具体内容请见第三篇引用链接）

**常用框架：**

- 对于Web项目，我们通常采用Flask或Django等框架，会有一套适合这种项目的工程目录。

- 对于爬虫项目，通常有Scrapy等开源框架，也会提供一套适合这种项目的工程目录。



## Python通用目录结构

### 目录1

ProjectName
│ readme 项目说明文档
│ requirements.txt 存放依赖的外部Python包列表
│ setup.py 安装、部署、打包的脚本
├─ bin 存放脚本，执行文件等
│ └─ projectname
├─ docs 文档和配置
│ └─ abc.rst
│ └─ conf.py 配置文件
└─ projectname 工程源码（包括源码、测试代码等）
│ main.py 程序入口
│ init.py
└─ tests 测试代码
└─ test_main.py
└─ init.py

对于开源的Python项目，一般还会涉及版权方面的信息，可以参考一下文章：
https://www.cnblogs.com/holbrook/archive/2012/02/24/2366386.html

### 目录2*

下面列出python开源项目的通常目录结构及说明：

```shell
.tx/            如果你使用Transifex进行国际化的翻译工作，创建此目录
    config      Transifex的配置文件
$PROJ_NAME/     按照你实际的项目名称创建目录。如果有多个子项目，就创建多个目录
docs/           项目文档
wiki/           如果有wiki，可以创建此目录
scripts/        项目用到的各种脚本
tests/          测试代码
extras/         扩展，不属于项目必需的部分，但是与项目相关的sample、poc等，下面给出4个例子：
    dev_example/
    production_example/
    test1_poc/
    test2_poc/
.gitignore      版本控制文件，现在git比较流行
AUTHORS         作者清单
INSTALL         安装说明
LICENSE         版权声明
MANIFEST.in     装箱清单文件
MAKEFILE        编译脚本
README          项目说明文件，其他需要的目录下也可以放一个README文件，说明该目录的内容
setup.py        python模块的安装脚本1234567891011121314151617181920
```

![example](https://github.com/zuimrs/myBlogFile/raw/master/B010/15fdb6f41b3711aa.png)

![img](https://pic1.zhimg.com/80/v2-c01a0b58990f6cba19f2df7cd2805d14_720w.jpg)

这个目录结构是针对python项目的， 各种语言习惯的目录结构可能不同，但一些基本的要素还是共同的，可以举一反三。

### 目录3

![这里写图片描述](https://img-blog.csdn.net/20180228040557372?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQveWV6aGVucXVhbjEyMw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

在[python开源项目目录结构](http://www.cnblogs.com/holbrook/archive/2012/02/24/2366386.html)的基础上，进一步定义[django](https://so.csdn.net/so/search?from=pc_blog_highlight&q=django)的目录结构。根据django的特性，分成两部分：**project**结构和**app**结构。

## project结构

这里定义的是[python开源项目目录结构](http://www.cnblogs.com/holbrook/archive/2012/02/24/2366386.html)中的$PROJ_NAME目录内的内容，需要与[python开源项目目录结构](http://www.cnblogs.com/holbrook/archive/2012/02/24/2366386.html)结合起来。

> PROJ_NAME/
> __init__.py   这几个文件是django创建project所必须的，不做过多说明
> manage.py
> settings.py
> urls.py  
> apps/        即使是“小”工程，也建议分成多个app，每个app足够简单，只解决某一个方面的问题 （注1）
>   myapp1/
>   myapp2/
> extra_apps/   引用的其他app。
> libs/        加载第三方模块，可以避免版本冲突，按照标准的site-packages管理（注2）
>    [python](https://so.csdn.net/so/search?from=pc_blog_highlight&q=python)*.*/　　指定python版本号
>      site-packages/  
>      requirements.pip  #pip的依赖说明文件
> tests/     project级别的测试，对于每个app，还要有自己的测试代码
> static/     静态内容
>    css/
>    js/
>    images/
> uploads/    上传文件所在目录
> templates/  模板目录，覆盖app的模板
>    flatpages/
>    comments/
>    example/
>    app1/
>    app2/
> templatetags/  tag目录

注1：指定app加载，在settings.py中设置：

```
sys.path.insert(0, os.path.join(PROJECT_ROOT, 'apps'))
sys.path.insert(0, os.path.join(PROJECT_ROOT, 'extras'))
sys.path.insert(0, os.path.join(PROJECT_ROOT, 'libs'))  
```

注2：自定义libs的加载，在settings.py中设置：

```
sys.path.insert(0, '/{{MY_LIB)}/site-packages/*****.egg')
sys.path.insert(0, '/{{MY_LIB}} /site-packages/')  
```

## app目录结构

> $APP_NAME/
>
> tests/          app级别的测试代码
>
> models/         注1
>
> __init__.py
>
> Amodels.py
>
> Bmodels.py
>
> templates/       注2
>
> templatetags/    tag目录

注1：如果很好的控制app的规模，Model类数量少，可以使用惯用的models.py文件中, 否则将models做成一个package
接下来可以有两种做法：

\1. 在__init__.py中import所有的Model类
\2. 指定Model的元类（Meta）的app_label, 参考[这里](http://www.cnblogs.com/holbrook/archive/2012/02/13/2357339.html)

注2：如果extend 工程下的base.html， 使用 !base.html

转载于:https://www.cnblogs.com/Amagasaki/articles/3555509.html

## 详细文件结构

### **Python脚本**

今天来讲讲Python的结构，我们知道Python可为各种不同类型的任务构建小型辅助工具，这些小工具通常可以表示为单个文件Python脚本。

来看一个Python脚本的示例结构：

```text
# the content of my_script.py

# imports
import logging

# constants
LOGGER = logging.getLogger()


def magical_function():
    LOGGER.warning('We are about to do some magical stuff')


def main():
    # The actual logic of the script
    magical_function()


if __name__ == '__main__':
    main()
```

### **Python Package**

python项目的示例结构：

```text
my_project/
    README.md
    requirements.txt
    setup.py

    src/
        my_project/
            __init__.py
            my_module.py
            other_module.py

            my_pkg1/
                __init__.py
                my_third_module.py

    tests/
        conftest.py
        test_module.py
        test_other_module.py

        my_pkg1/
            test_my_third_module.py
```

[requirements.txt](https://link.zhihu.com/?target=https%3A//pip.pypa.io/en/latest/user_guide/%23requirements-files)列出了my_project所依赖的Python包。

这些可以通过运行以下命令来安装

```text
pip install -r requirements 
```

[setup.py](https://link.zhihu.com/?target=https%3A//packaging.python.org/tutorials/distributing-packages/%23setup-py)是一个文件，包含有关项目的信息，这个文件也可用于打包项目。

来看看setup.py的最小示例：

```text
'''Minimal setup.py file'''

from setuptools import setup, find_packages

setup(
    name='my_project',
    version='0.1',
    packages=find_packages(where="src"),
    package_dir={"": "src"})
```

一旦安装了setup.py文件，就可以在项目的根目录下运行可编辑模式，通过pip install -e .安装项目。

在可编辑模式下，当你一更改源代码文件，就自动更新安装的版本。



# [python](https://so.csdn.net/so/search?from=pc_blog_highlight&q=python)项目的结构和包的创建

**原文链接：**[ 第三章：python项目的结构和包的创建](https://blog.csdn.net/the_little_fairy___/article/details/79291654?ops_request_misc=&request_id=&biz_id=102&utm_term=python项目结构&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-7-79291654.nonecase&spm=1018.2226.3001.4187)

在python的圈子里，有许多人无偿得公开自己开发的程序库，使用者可以通过pip 命令来安装这些库，我们在发布时需要将其创建成一种特殊的文件，这种文件就是程序包，我们将会在本节学到程序包的制作流程：

- **python项目目录结构以及文件结构**
- **对第二章学习的留言板应用进行整理，封装成包**
- **最后学习如何将我们开发的项目发布在PyPI上，与全世界的人分享**

------

## 3.1 Python项目

使用python开发的应用程序达到一定的规模之后，必然会出现多个模块或者程序包目录，同时除了源码之外，说明性质的文本文件，管理相关程序库的元信息等都会越来越多，这些为同一个目的服务的文件，目录以及元信息，就是我们所说的项目。

一个完整的结构需要满足以下的条件：

- **拥有一个在版本管理之下的源码目录**
- **程序信息在setup.py中定义**
- **在一个virtualenv环境中运行**

如果项目符合标准，那么它与工具之间就会有很强的亲和力，而且便于今后自己或者其他的开发者进一步开发，另外，本章所介绍的结构记录流程不但适合于个人的开发环境，也适用于团队的开发环境。

## 3.2 环境与工具

### 3.2.1 使用virtualenv搭建独立的环境

使用virtualenv为每一个项目搭建独立的环境，具有以下的优点：

- **添加撤那个续保以及变更版本时，能将影响控制在当前的环境**

- **便于判断已经安装的程序包是否可以删除**

- **不再需要改环境时，可以直接删除整个环境**

- 一旦出现了问题，那么问题必然出现在该环境的项目上，有助于找到问题的所在

  > 使用pip安装外部程序库时，库会被安装到python的安装目录下，不同目的的程序库会被安装到同一目录下，不但容易导致版本冲突，而且很难分辨出来哪些程序库已经没有用了。

### 3.2.2 virtualenv的主要特征体现在下列的功能上

- **在virtualenv 环境中可以自由安装python ，不需要提供操作系统管理员权限**
- **在virtualev 环境下，可以根据目的不同安装程序库**
- **可以随时关闭或者打开virtualenv 环境**

### 3.3.3 virtualenv 环境搭建的数量没有上限

- **不同的环境里面的库没有关系，相互之间没有任何关系**
- **创建virtualenv环境**

```
virtualenv venv11
```

- **激活环境**

```
source venv/bin/activate1
```

- **查找对应的目录**

```
$python
>>>import sys
>>>sys.executable123
```

- **关闭环境**

```
这里写代码片(venv)$deactivate1
```

- **删除环境(首先需要关闭环境）**

```
rm -R venv1
```

## 3.3 文件结构与发布程序包

在这一部分，我们会尝试吧第二章中卡发的留言板应用放到P有PI上面进行公开，在这个过程中学习一下setup.py 的写法以及如何向PyPI上面上传程序包。

### 3.3.1 编写setup.py

setup.py 的功能，python的封装离不开setup.py，封装可以便于编写的长须供其他用户或者项目使用，封装的大部分时间都要小号在白那些setup.py上面。这个名字实在python中定好的，不可以随便更改，我们会在这个文件中定义程序包的名称，包以及依赖包的信息等元数据。另外，将程序包注册到PyPI的操作也需要通过setup.py来进行。

### setup.py的命令

首先，先制作一个可以运行的setup.py的空壳
**setup.py**

```
from setuptools import setup
setup(name='guestbook')12
```

**setup.py的指令一览如下图：**
![这里写图片描述](https://img-blog.csdn.net/20180207142758730?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdGhlX2xpdHRsZV9mYWlyeV9fXw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

下面我们来创建最基本的源码包，源码包需要通过python setup.py sdist命令来创建，如下图所示：
![这里写图片描述](https://img-blog.csdn.net/20180207143127933?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdGhlX2xpdHRsZV9mYWlyeV9fXw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

查看目录如下所示：
![查看目录](https://img-blog.csdn.net/20180207143300832?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdGhlX2xpdHRsZV9mYWlyeV9fXw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
现在，dist目录下面已经生成了guestbook-0.0.0.tar.gz文件，这个文件目前只包含setup.py。

> **注意！！**在执行过程中我们看到了一些warning，这些waring 指出的项目最好都设置一下，我们将会在后面学会如何进行设置。

### 3.3.2 留言板的项目结构

首先，我们先来了解一下python项目一般的目录结构。当封装对象只有一个”.py “文件时，其结构如下所示：

```
/home/chengyiming/project_name
    +--MANIFEST.in
    +--README.rst
    +--packagename.py
    +--setup.py12345
```

如果封装目录下包含多个”.py “文件时，其结构如下所示：

```
/home/chengyiming/project_name
    +--MANIFEST.in
    +--README.rst
    +--packagename/
    |    +--__init__.py
    |    +--module.py
    |    +--templates/
    |       +--index.html
    +--setup.py
12345678910
```

我们的留言板应用有下述文件组成：

| 文件路径             | 说明                                            |
| -------------------- | ----------------------------------------------- |
| guestbooki.py        | 服务器程序                                      |
| guestbook.dat        | 提交数据文件                                    |
| static/main.css      | CSS文件                                         |
| templates/index.html | 输出的HTML的模板，用于显示“提交/留言列表”的页面 |

虽然“.py”文件只有一个，但是static和templates目录下都包含文件，由于我们之前介绍的项目目录无法安装模板等文件，因此这里需要使用最后一种项目文件。最终文件安排如下表所示：

```
？home/chengyiming/guestbook/
    +--LICENSE.txt
    +--MANIFEST.in
    +--README.rst
    |    +--__init__.py
    |    +--static/main.css
    |    +--templates/index.html
    +--setup.py
123456789
```

现在我们来创建guestbook目录，将guestbook.py文件一发动到该目录下并命名为**init**.py。templates和static目录也要移动到guestbook目录下，guestbook.dat 不是我们要发布的东西，所以这里不需要它。
接下来，我们来实际用用这个封装用的结构

### 3.3.3 setup.py 与MANIFEST.in——设置程序包信息与捆绑的文件

接下来，我们将在setup.py中设置程序包的信息，然后子啊MANIFEST.in 中制定捆绑的文件，接下来依次了解一下。
**setup.py**
首先，我们描述一下guestbook项目的setup.py

```
from setuptools import setup,find_packages

setup(
    name='guestbook',
    version='1.0.0',
    packages=find_packages(),
    include_package_data=True,
    install_requires=['Flask',],
)123456789
```

如果一个环境能够使用pip，那么这个环境一定安装了setuptools库。一般情况下，我们习惯使用setuptools提供的含有拓展功能的setup函数，下面来了解一下各个函数的意义：

- name
  程序包的名称，一般情况下，包名与程序名一致，但是一般情况下程序包的名字需要非常独特才好，所以一般会在前面加上发布的组织的名字，chengyiming.guestbook

- version

  ##### 代表版本号的字符串

- packages
  指定所有捆绑的python程序包（可以用python命令import 的目录名），例如，如果一个项目包含多级目录，那么我们需要使用下例所示的方法，列表指定所有的程序包。

```
packages=['guestbook','guestbook.server','guestbooki.server.dir','guestbook.storage',......]1
```

find_packages()还可以自动搜索当前目录下的所有python程序包并返回程序包的名称，有了这个，我们便可以省去一个个列举的麻烦。

- include_package_data
  在packages指定的python包（目录）中，除了“.py”之外的文件都称为程序包资源，这个设置用来指定是否安装了python包中所含的程序包资源。
  这里我们需要安装templates和static这两个程序包资源，所以将它们指定为True。
  这一设置并不能将程序包资源与我们要发布的程序包捆绑在一起，捆绑的方法将在MANIFEST.in中学习
- install_requires
  列表指定依赖包，留言板应用要依赖Flask，所以在这里我们指定Flask，与requirements.txt不同，这里我们一般不指定版本。

**MANIFEST.in**
为了将HTML文件，CSS文件等程序包资源与程序包捆绑刚在一起，我们需要使用MANIFEST.in来制定封装对象文件。
这里我们在setup.py所在的目录下创建MANIFEST.in文件，制定封装对象文件的范围。
**MANIFEST.in**

```
recursive-include guestbook *.html,*.css1
```

recursive-include白哦是捆绑指定目录下所有与制定类型一致的文件，在上面的代码中，我们捆绑了guestbook目录下所有与*.html和*.css一致的文件。
现在我们希望使用这个程序包的环境能够安装这些捆绑好的程序包资源，所以需要把钱买你提到的install_package_data指定为True，不能忘记奥~
MANIFEST.in还可以捆绑vguestbook应用不适用的非程序包资源文件，比如LICENSE.txt，在发布、程序包时最好把许可文件也捆绑进去。
假设我们使用了BSD许可，并在LICENSE.txt文件中描述了许可条款，接下来，我们需要在MANIFEST.in里面添加对他的捆绑指定。
**MANIFEST.in**

```
recursive-include guestbook *.html *.css
include LICENSE.txt12
```

include会捆绑所有于指定类型一致的文件，所以再添加了上面的指定语句之后，LICENSES.txt就和程序包捆绑在了一起。
**确定运行环境**

1. 搭建virtualenv环境及安装

```
cd ..
virtualenv .venv12
```

2.如图所示安装的包
![安装包](https://img-blog.csdn.net/20180207165248922?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdGhlX2xpdHRsZV9mYWlyeV9fXw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
guestbook-1.0.0已经被安装到了虚拟环境中，我们可以看到，记录程序包原数据位置饿的guestbook.egg-link文件被安装到了virtualenv 环境中，easy-install.path文件中添加了guestbook的源码位置。/
这样的话，我们在其他PC或服务器上面构建环境是，就不必再一个个安装依赖包，如果今后需要添加或者更改依赖库，只需要按照i前面的流程更新setup.py,然后再执行一次pip install即可。

#### setup.py——创建执行命令

第二章的留言板项目是一个直接从python启动的脚本，要想让下载他的人用起来更加方便，最好生成一些用户命令，这里外婆们通过设置setup.py，让其自动生成guestbook命令。
我们在setup.py中添加了entry_points。这样在安装程序包时会自动生成guestbook命令。用户执行guestbook命令是将会调用guestbook模块的main函数。
但是guestbook/**init**.py中还没有main函数，所以我们需要添加这个函数，代码如下：

```
略
def main():
    application.run('127.0.0.1',8000)


if __name__=='__main__':
    application.run('127.0.0.1',8000,debug=True)1234567
```

创建用于的发布的程序包时，执行python setup.py sdist命令
![这里写图片描述](https://img-blog.csdn.net/20180207222735987?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdGhlX2xpdHRsZV9mYWlyeV9fXw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

在dist目录下生成了guestbook-1.0.0.tar.gz。这个tar.gz文件中包含了guestbook/**init**.py,setup.py,LICENSE.txt，HTML，CSS等文件，只需要把这个文件安装到我们先安装应用的环境中，就可以运行pip install guestbook-1.0.0.tar.gz，直接从文件进行安装。

#### 3.3.6 提交至版本库

我们先将之前的内容提交到版本库，关于hg 的命令操作，在第一章和第六章有详细的介绍，目前的目录介绍如下所示：

```
/home/chengyiming/guestbook/
    +--.venv/
    +--LICENSE.txt
    +--MANIFEST.in
    +--guestbook
    |    +--__init__.py
    |    +--static/main.css
    |    +--templates/index.html
    +--guestbook.dat
    +--guestbook.egg-info/
    +--setup.py1234567891011
```

在开发python项目时，我们习惯将setup.py放在版本库最初级目录（根目录）下。这样我们就能使用pip直接从版本库进行安装。
另外，有些文件和目录是不用保存到版本库中，guestbook.dat文件的作用时记录留言板接收到的数据，这些数据没必要记录到版本库中。
guestbook.egg-info目录的作用是记录程序包的元数据，.venv可以重新生成，没必要保存在版本库
接下来，我们将除了以上三者的文件提交给版本库

```
cd ~/guestbook
hg init 
hg add LICENSE.txt MANIFEST.in guestbook setup.py
hg ci -m "initial"1234
```

### 3.3.7 README.rst——开发环境设置流程

以下介绍设置流程说明书，总结该留言板应用开发环境的搭建流程，如下：

1. clone项目的版本库

2. 搭建项目专用的virtualenv环境

3. 在virtualenv环境内执行pip install (如果用于开发，执行pip install -e )

   设置流程：

```
hg clone https://bitbucket.org/chengyiming/guestbook
cd guestbook
virtualenv .venv
source .venv/bin/activate
(.venv)$pip install .
(.venv)$guestbook
*Running on http://127.0.0.1:5000/
12345678
```

我们将上图的流程写入README.rst文件即可。
**README.rst**

```
==================
留言板应用
==================

目的
=====
练习开发通过web浏览器提交留言的web应用程序

工具版本
==============
：python：2.7.8
:pip:     1.5.6
:virtualenv:1.11.6


安装与启动方法
==================
从版本库获取代码，然后在该目录下搭建virtualenv环境：
$hg clone https://bitbucket.org/chengyiming/guestbook
$cd guestbook
$virtualenv .venv
$source .venv/bin/activate
(.venv)$pip install .
(.venv)$guestbook


开发流程
===========

用于开发的安装
-----------------
1.检测
2按照以下流程安装
(.venv)$pip install -e .12345678910111213141516171819202122232425262728293031323334
```

写完之后记得将README.rst文件提交到版本库

### 3.3.8 变更依赖包

留言板的依赖包是Flask，但是，我们在开发初期很难确定好一款应用所有的依赖包，有时候还会放弃当前的包而改用其他的，特别是周期段，发布频繁的项目，通常每发布一次，就会变更一次依赖包。

使用pip 更换了程序包，这一步如何告知他人

```
(.venv)$pip install flask
(.venv)$pip install bottle
123
```

留言板的setup.py里面记录着依赖包的信息，我们只需要更改setup.py的设置即可。如果更改了setup.py的install _requires行，需要再次执行pip install -e
即使我们从fsetup.py中删除了flask，之前安装到环境中的flask 以及其关联的程序包也不会被卸载，若想删除没有用的程序包，需要通过virtualenv –clear 。等方法重建环境。
重建环境如下所示：
(.venv)virtualenv –clear .venv  #删除.venv环境内的全部依赖库 
(.venv)virtualenv –clear .venv  #删除.venv环境内的全部依赖库 (.venv)pip install -e #根据./setup.py安装依赖库

#### 3.3.9 通过requirements.txt固定开发版本

我们不仅可以通过setup.py管理依赖包，还可以通过requirements.txt来管理依赖库。
创建requiments.txt:
(.venv)$pip freeze >requirements.txt
其中记录了当前环境已经安装的所有程序包以及其明确的版本号

使用setiup.py管理依赖包时，没有指定版本，这是两者管理的一大区别
要想在其它环境中安装同样的程序包们，我们需要将这个文件防盗盖环境下，在安装
(.venv)$pip install -r requirements.txt
这样，环境中就安装了同样版本的程序包

#### 3.3.10 Python setup.py bdist_wheel_制作用于wheel发布的程序包

制作wheel程序包之前，我们先来安装wheel
pipinstallwheel接下来，生成wheel程序包pipinstallwheel接下来，生成wheel程序包python setup.py bdist_wheel
ls dist/

#### 上传到PyPI进行公开

我们之所以可以通过pip命令安装指定的程序包，是因为这些程序包都被注册到了PyPI上面，PyPI时python的官方网站，所有人都能随意上传以及下载python程序包，如果各位不介意公开自己开发的程序包，不妨将其注册在PyPI上。


