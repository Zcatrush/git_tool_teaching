# 1. 认识界面

对应分支 - start

为获得更好的阅读体验，可以前往飞书知识库

## 熟悉工作环境

在开始之前，得先告诉你们如何优雅地使用VSCode及其提供的git支持

现在，先用VSCode打开本地仓库所在文件夹

> 在对应目录下打开终端：
>
> - 对于Linux系统，你可以右键-Open in Terminal
> - 对于Windows系统，你需要摁住 shift+右键-在此处打开命令窗口（或者Powershell窗口）
>
> 在弹出的终端内，输入
>
> ```bash
> code .
> ```
>
> 这样你就成功使用 VSCode 打开当前目录了

### VSCode界面

![VSCode_interface](.\static\VSCode_interface.png)

在该教程中，你仅需要认识几个基础界面：

- **编辑区** 在该区域进行主要操作，比如修改文件

- **面板** 集成了你可能需要的输出信息，你也可以使用**终端**（快捷键 **ctrl+alt+`** ）快速地执行某些命令（终端默认路径为当前文件夹路径）

- **左侧主侧边栏**

  - **资源管理器** 浏览文件夹内的所有文件，它自带的时间线功能可以记录该文件上几次的修改
  - **Git工具** 可以查看本地git仓库的情况（后文会补充介绍)

- **底部状态栏**
- **当前分支** 这里显示的是当前git仓库所在的分支名
  
- **GitGraph拓展** 这是`Git Graph插件`生成的，点击它可以弹出Git仓库目前的状态（以图表形式，后文会补充介绍） 

#### Git工具

​	现在，在VSCode内切换到**Git工具**页内，你会看到如下页面

![image-20241211201355045](D:\Documents\github\git_tool_teaching\static\git_interface.png)

开启终端(ctrl+alt+`)，执行

```bash
git log
# 这个指令可以让你查看提交历史
```

你会发现，**源代码管理图**中的列表项标题和提交记录的注释相同

```bash
commit cec678527a32a47de87638acfb03c1aaea360a8c (HEAD -> start)
Author: Smoaflie <handsome_shit@outlook.com>
Date:   Wed Dec 11 20:13:37 2024 +0800

    Change file for branch `start` # 提交记录的注释指的是这东西
```

且当前分支`start`所处的位置也被标注了出来

尝试点击任一提交记录

![image-20241211202208140](D:\Documents\github\git_tool_teaching\static\git_interface_1.png) 

你可以发现编辑区内打开了一份**差异比较页面**，左侧是旧文件，右侧是新文件

红色的部分是删除部分绿色的部分是新增部分

你可以通过文件左侧的小箭头折叠不想查看差异的文件

> 这时候你该想到一个命令
>
> ```bash
> git diff
> ```
>
> 尝试使用它比较此分支与上一个分支的差异，这里我们以HEAD分支为例
>
> ```bash
> git diff HEAD HEAD~1
> ```
>
> 对比输出的内容，你可以知道差异比较页面只是将diff命令输出的内容可视化了

---

根据diff信息，你可以知道在最新的提交中，我进行了如下操作：

> - 新建 `new_file` 文件，并输入了一段话
> - 删除 `./static/` 目录下的几张图片
> - 新增 `./static/` 目录下的几张图片
> - 修改 `README.md` 文件

现在，再输入以下命令

```bash
git reset --soft HEAD~1
# 如果你看过基础课程，你应该知道 工作区 - 暂存区 - 本地仓库 的概念
# git reset 可以让你回退到某一版本，HEAD是当前版本，HEAD~1则是回退到当前版本的上一个版本，即上一个提交记录的状态
# --soft 参数的意思是，在回退版本的同时，保留当前工作区的内容
```

---

##### 回顾知识点-git的三个区

![git_area](.\static\git_area.png)

> 简单来说，
>
> - **工作区**是你平时直接修改代码的地方。
> - **暂存区**是一个中转站，当你觉得某些改动可以提交时，先把它们放到暂存区。
> - **本地仓库**是用来保存所有版本记录的地方，你提交代码时，它们就会从暂存区进入本地仓库。

---

你会发现左侧**源代码管理**列表内多了些东西，随便点开一个文件（这里以`new_file`为例），你会观察到如下界面

![git_interface](.\static\git_interface_2.png)

注意几个点（实际情况与图片存在细微不同，请不要在意）：

> - new_file 右侧有字样 `A` ，代表ADD，指代该文件是被新添加进仓库的
> - README.md 右侧有字样 `M`，代表MODIFY，指代该文件遭受到修改
> - xx.png 右侧有字样 `D`，代表DELETE，指代该文件被删除

如果你还保留着对暂存区的理解，你或许能自己领悟 `暂存的更改` 和 `更改` 两个栏目的区别

> 暂存的更改 指的是暂存区内容
>
> 更改 指的是工作区内与本地仓库（当前分支）有出入的文件

因此，你可以尝试把暂存区的内容移出来，看看会发生什么

```bash
git reset new_file #文件从暂存区移出，回到工作区。
```

![git_interface_3](.\static\git_interface_3.png)

> - new_file 右侧的字样变为 `U` ,代表UNSTAGED，指代该文件是未声明的，.git不会追踪该文件的变化
>

你可以重新将文件添入暂存区

```bash
git add new_file
```

理论上，你现在要将暂存区内的文件添加到仓库内，新建一个提交记录:

```bash
git commit -m 'Change file for branch `start`'
```

但你不妨试试使用那个蓝色的`提交`按钮

![git_interface_4](.\static\git_interface_4.png)

再使用git log看看效果，你会发现这俩操作是等价的

---

#### Git Graph插件

接下来我们看看Git Graph插件，点击底部的`Git Graph`字样

![gitgraph_interface](.\static\gitgraph_interface.png)

这比VSCode自带的git工具更加美观，还具有更多的功能，但每个人的需求不同，怎么使用它就留给你自己探索了
