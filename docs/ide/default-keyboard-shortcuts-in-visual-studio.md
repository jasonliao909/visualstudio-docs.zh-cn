---
title: 键盘快捷方式
description: 了解 Visual Studio 中的默认键盘快捷方式，以便通过它们访问各种命令和窗口。
ms.custom: SEO-VS-2020
ms.date: 11/15/2021
ms.topic: reference
helpviewer_keywords:
- shortcut keys [Visual Studio], keyboard binding schemes
- keyboard binding schemes [Visual Studio]
- Help [Visual Studio], shortcut keys
- keyboard shortcuts [Visual Studio], keyboard binding schemes
- keyboard shortcuts
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 34848eb9101029a9fe1fc30f088535b7f54e5ce5
ms.sourcegitcommit: 1ed233bb3afc5ae1f52aff8e41f7e650342033ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2022
ms.locfileid: "141274619"
---
# <a name="keyboard-shortcuts-in-visual-studio"></a>Visual Studio 中的键盘快捷方式

通过选择相应的键盘快捷方式，可访问 Visual Studio 中的各种[命令](reference/visual-studio-commands.md)和窗口。 本页列出了常规配置文件的默认命令快捷方式，安装 Visual Studio 时可能已选择该配置文件。 无论选择哪个配置文件，都可以通过打开“选项”对话框，展开“环境”节点，然后选择“键盘”，[认识命令的快捷方式](identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)。 你还可以为任意给定命令分配不同的快捷键，以自定义你的快捷键。

有关常见键盘快捷方式列表和其他工作效率信息，请参阅：

- [键盘提示](../ide/productivity-shortcuts.md)
- [工作效率提示](../ide/productivity-features.md)

有关 Visual Studio 中辅助功能的详细信息，请参阅[辅助功能提示和技巧](../ide/reference/accessibility-tips-and-tricks.md)以及[如何：仅使用键盘进行操作](../ide/reference/how-to-use-the-keyboard-exclusively.md)。

## <a name="printable-shortcut-cheatsheet"></a>可打印快捷方式备忘单

单击可获取[适用于 Visual Studio 的可打印键盘快捷方式备忘单](https://visualstudio.microsoft.com/keyboard-shortcuts.pdf)。

[:::image type="content" source="media/default-keyboard-shortcuts-in-visual-studio/visual-studio-keyboard-shortcut-cheatsheet.png" alt-text="可打印键盘快捷方式备忘单。":::](https://visualstudio.microsoft.com/keyboard-shortcuts.pdf)

<a name="popular"></a>
## <a name="popular-keyboard-shortcuts-for-visual-studio"></a>Visual Studio 的常用键盘快捷方式

本部分中的所有快捷方式都将全局应用（除非另有指定）。 “全局”上下文表示该快捷方式适用于 Visual Studio 中的任何工具窗口。

> [!NOTE]
> 通过打开“选项”对话框，展开“环境”节点，然后选择“键盘”，可以[查找任何命令的快捷方式](identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)  。

- [生成](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_build-popular-shortcuts)
- [调试](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_debug-popular-shortcuts)
- [编辑](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_edit-popular-shortcuts)
- [文件](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_file-popular-shortcuts)
- [项目](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_project-popular-shortcuts)
- [重构](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_refactor-popular-shortcuts)
- [工具](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_tools-popular-shortcuts)
- [视图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_view-popular-shortcuts)
- [窗口](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_window-popular-shortcuts)

#### <a name="build-popular-shortcuts"></a><a name="bkmk_build-popular-shortcuts"></a> 生成：常用快捷方式

|命令|键盘快捷键 |命令 ID|
|-|-|-|
|生成解决方案|**Ctrl+Shift+B** | 生成.生成解决方案 |
|取消|**Ctrl+Break** | 生成.取消 |
|Compile|**Ctrl+F7** | 生成.编译 |
|对解决方案运行代码分析|**Alt+F11**| 生成.对解决方案运行代码分析 |

#### <a name="debug-popular-shortcuts"></a><a name="bkmk_debug-popular-shortcuts"></a> 调试：常用快捷方式

|命令|键盘快捷方式 [特殊上下文]|命令 ID|
|-|-|-|
|遇到函数时断开|**Ctrl+B**| 调试.在函数处中断 |
|全部中断|**Ctrl+Alt+Break**| 调试.全部中断 |
|删除所有断点|**Ctrl+Shift+F9**| 调试.删除所有断点 |
|异常|**Ctrl+Alt+E**| 调试.异常 |
|快速监视|**Ctrl+Alt+Q**<br /><br />或 Shift+F9| 调试.快速监视 |
|重启|**Ctrl+Shift+F5**| 调试.重新启动 |
|运行到光标处|**Ctrl+F10**| 调试.运行到光标处 |
|设置下一语句|**Ctrl+Shift+F10**| 调试.设置下一语句 |
|开始|**F5**| 调试.启动 |
|启动时不调试|**Ctrl+F5**| 调试.开始执行不调试 |
|“单步执行”|**F11**| 调试.逐语句 |
|单步跳出|**Shift+F11**| 调试.跳出 |
|逐过程|**F10**| 调试.逐过程 |
|停止调试|**Shift+F5**| 调试.停止调试 |
|切换断点|**F9**| 调试.切换断点 |

#### <a name="edit-popular-shortcuts"></a><a name="bkmk_edit-popular-shortcuts"></a> 编辑：常用快捷方式

|命令|键盘快捷方式 [特殊上下文]|命令 ID|
|-|-|-|
|断行|**Enter** [文本编辑器、报表设计器、Windows 窗体设计器]<br /><br />或 **Shift+Enter** [文本编辑器]| 编辑.分行 |
|折叠到定义|**Ctrl+M**、**Ctrl+O** [文本编辑器]| Edit.CollapseToDefinitions |
|注释选定内容|**Ctrl+K**、**Ctrl+C** [文本编辑器]| 编辑.注释选定内容 |
|完成单词|**Alt+向右键** [文本编辑器、工作流设计器]<br /><br />或 **Ctrl+空格键** [文本编辑器、工作流设计器]<br /><br />或 **Ctrl+K**、**W** [工作流设计器]<br /><br />或 **Ctrl+K、Ctrl+W** [工作流设计器]| 编辑.完成单词 |
|复制|**Ctrl+C**<br /><br />或 Ctrl+Insert| 编辑.复制 |
|剪切|**Ctrl+X**<br /><br />或 Shift+Delete| 编辑.剪切 |
|删除|删除 [团队资源管理器]<br /><br />或 **Shift+Delete** [序列图、UML 活动图、层关系图]<br /><br />或 **Ctrl+Delete** [类图]| 编辑.删除 |
|查找|**Ctrl+F**| 编辑.查找 |
|查找所有引用|**Shift+F12**| 编辑.查找所有引用 |
|在文件中查找|**Ctrl+Shift+F**| 编辑.在文件中查找 |
|查找下一个|**F3**| 编辑.查找下一个 |
|查找下一个选择|**Ctrl+F3**| 编辑.查找下一个选定项 |
|设置文档格式|**Ctrl+K、Ctrl+D** [文本编辑器]| 编辑.编排文档格式 |
|设置选定内容的格式|**Ctrl+K、Ctrl+F** [文本编辑器]| 编辑.格式化选定内容 |
|转到|**Ctrl+G**| 编辑.转到 |
|转到声明|**Ctrl+F12**| 编辑.转到声明 |
|转到定义|**F12**| 编辑.转到定义 |
|转到查找组合|**Ctrl+D**| 编辑.转到查找组合框 |
|转到下一个位置|**F8**| 编辑.转到下一个位置 |
|插入代码片段|Ctrl+K、Ctrl+X | 编辑.插入代码片段 |
|“插入”选项卡|**Tab** [报表设计器、Windows 窗体设计器、文本编辑器]| 编辑.插入制表符 |
|行 - 剪切|**Ctrl+L** [文本编辑器]| 编辑.剪切行 |
|行 - 向下扩展列|**Shift+Alt+向下箭** [文本编辑器]| 编辑.向下扩展列 |
|行 - 打开上面的内容|**Ctrl+Enter** [文本编辑器]| 编辑.上开新行 |
|列出成员|**Ctrl+J** [文本编辑器、工作流设计器]<br /><br />或 **Ctrl+K、Ctrl+L** [工作流设计器]<br /><br />或 **Ctrl+K、L** [工作流设计器]| 编辑.列出成员 |
|导航到|**Ctrl+,**| Edit.NavigateTo |
|打开文件|**Ctrl+Shift+G**| 编辑.打开文件 |
|改写模式|**Insert** [文本编辑器]| 编辑.改写模式 |
|参数信息|**Ctrl+Shift+空格键** [文本编辑器、工作流设计器]<br /><br />或 **Ctrl+K、Ctrl+P** [工作流设计器]<br /><br />或 **Ctrl+K、P** [工作流设计器]| 编辑.参数信息 |
|粘贴|**Ctrl+V**<br /><br />或 Shift+Insert| 编辑.粘贴 |
|查看定义|**Alt+F12** [文本编辑器]| 编辑.查看定义 |
|重做|**Ctrl+Y**<br /><br />或 Shift+Alt+Backspace<br /><br />或 Ctrl+Shift+Z| 编辑.重做 |
|Replace|**Ctrl+H**| 编辑.替换 |
|全选|**Ctrl+A**| 编辑.全选 |
|选择当前字词|**Ctrl+W** [文本编辑器]| 编辑.选择当前字 |
|取消选择|**Esc** [文本编辑器、报表设计器、设置设计器、Windows 窗体设计器、托管资源编辑器]| 编辑.取消选定 |
|环绕|**Ctrl+K、Ctrl+S** <br>（仅可用于 Visual Studio 2019 及更早版本）| 编辑.外侧代码 |
|选项卡左侧|**Shift+Tab** [文本编辑器、报表设计器、Windows 窗体设计器]| 编辑.左缩进 |
|切换所有大纲显示|**Ctrl+M、Ctrl+L** [文本编辑器]| 编辑.切换所有大纲显示 |
|切换书签|**Ctrl+K、Ctrl+K** [文本编辑器]| 编辑.切换书签 |
|切换完成模式|**Ctrl+Alt+空格键** [文本编辑器]| Edit.ToggleCompletionMode |
|切换大纲显示展开|**Ctrl+M、Ctrl+M** [文本编辑器]| 编辑.切换大纲显示展开 |
|取消注释选定内容|**Ctrl+K、Ctrl+U** [文本编辑器]| 编辑.取消注释选定内容 |
|撤消|**Ctrl+Z**<br /><br />或 Alt+Backspace| 编辑.取消 |
|字词 - 删除至结尾|**Ctrl+Delete** [文本编辑器]| 编辑.字删除直至结尾处 |
|字词 - 删除至开头|**Ctrl+Backspace** [文本编辑器]| 编辑.字删除直至开始处 |

#### <a name="file-popular-shortcuts"></a><a name="bkmk_file-popular-shortcuts"></a> 文件：常用快捷方式

|命令|键盘快捷方式 [特殊上下文]|命令 ID|
|-|-|-|
|退出|**Alt+F4**| 文件.退出 |
|新建文件|**Ctrl+N**| 文件.新建文件 |
|新建项目|**Ctrl+Shift+N**| 文件.新建项目 |
|新建网站|**Shift+Alt+N**| 文件.新建网站 |
|打开文件|**Ctrl+O**| 文件.打开文件 |
|打开项目|**Ctrl+Shift+O**| 文件.打开项目 |
|打开网站|**Shift+Alt+O**| 文件.打开网站 |
|重命名|**F2** [团队资源管理器]| 文件.重命名 |
|全部保存|**Ctrl+Shift+S**| 文件.全部保存 |
|保存选定项|**Ctrl+S**| 文件.保存选定项 |
|在浏览器中查看|**Ctrl+Shift+W**| 文件.在浏览器中查看 |

#### <a name="project-popular-shortcuts"></a><a name="bkmk_project-popular-shortcuts"></a> 项目：常用快捷方式

|命令|键盘快捷方式 [特殊上下文]|命令 ID|
|-|-|-|
|添加现有项|**Shift+Alt+A**| 项目.添加现有项 |
|添加新项|**Ctrl+Shift+A**| 项目.添加新项 |

#### <a name="refactor-popular-shortcuts"></a><a name="bkmk_refactor-popular-shortcuts"></a> 重构：常用快捷方式

|命令|键盘快捷方式 [特殊上下文]|命令 ID|
|-|-|-|
|提取方法|**Ctrl+R、Ctrl+M**| 重构.提取方法 |

#### <a name="tools-popular-shortcuts"></a><a name="bkmk_tools-popular-shortcuts"></a> 工具：常用快捷方式

|命令|键盘快捷方式 [特殊上下文]|命令 ID|
|-|-|-|
|附加到进程|**Ctrl+Alt+P**| 工具.附加到进程 |

#### <a name="view-popular-shortcuts"></a><a name="bkmk_view-popular-shortcuts"></a> 视图：常用快捷方式

|命令|键盘快捷方式 [特殊上下文]|命令 ID|
|-|-|-|
|类视图|**Ctrl+Shift+C**| 视图.类视图 |
|编辑标签|F2| 视图.编辑标签 |
|错误列表|**Ctrl+\\、Ctrl+E**<br /><br />或 Ctrl+\\、E| 视图.错误列表 |
|向后导航|**Ctrl+-**| 视图.向后定位 |
|向前导航|**Ctrl+Shift+-**| 视图.向前定位 |
|对象浏览器|**Ctrl+Alt+J**| 视图.对象浏览器 |
|输出|**Ctrl+Alt+O**| 视图.输出 |
|“属性”窗口|F4| 视图.属性窗口 |
|刷新|**F5** [团队资源管理器]| 视图.刷新 |
|服务器资源管理器|**Ctrl+Alt+S**| 视图.服务器资源管理器 |
|显示智能标记|**Ctrl+.**<br /><br />或 Shift+Alt+F10 [HTML 编辑器设计视图]| 视图.显示智能标记 |
|解决方案资源管理器|**Ctrl+Alt+L**| 视图.解决方案资源管理器 |
|TFS 团队资源管理器|**Ctrl+\\、Ctrl+M**| 视图.Tfs 团队资源管理器 |
|工具箱|**Ctrl+Alt+X**| 视图.工具箱 |
|查看代码|**Enter** [类图]<br /><br />或 **F7** [设置设计器]| 视图.查看代码 |
|视图设计器|**Shift+F7** [HTML 编辑器源视图]| 视图.视图设计器 |

#### <a name="window-popular-shortcuts"></a><a name="bkmk_window-popular-shortcuts"></a> 窗口：常用快捷方式

|命令|键盘快捷方式 [特殊上下文]|命令 ID|
|-|-|-|
|激活文档窗口|**Esc**| 窗口.激活文档窗口 |
|关闭文档窗口|**Ctrl+F4**| 窗口.关闭文档窗口 |
|下一个文档窗口|**Ctrl+F6**| 窗口.下一个文档窗口 |
|下一个文档窗口导航|**Ctrl+Tab**| 窗口.下一个文档窗口导航栏 |
|下一个拆分窗格|**F6**| 窗口.下一个拆分窗格 |


## <a name="global-shortcuts"></a>全局快捷键

这些键盘快捷键为全局快捷键，这意味着你可以在任何 Visual Studio 窗口具有焦点时使用它们。

- [分析](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_analyze-global-shortcuts)
- [体系结构](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_architecture-global-shortcuts)
- [Azure](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_windowsazure-global-shortcuts)
- [生成](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_build-global-shortcuts)
- [类视图上下文菜单](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_classview-global-shortcuts)
- [调试](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_debug-global-shortcuts)
- [调试上下文菜单](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_debugger-global-shortcuts)
- [诊断中心](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_diagnostics-global-shortcuts)
- [编辑](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_edit-global-shortcuts)
- [编辑器上下文菜单](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_editorContext-global-shortcuts)
- [文件](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_file-global-shortcuts)
- [帮助](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_help-global-shortcuts)
- [负载测试](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_loadtest-global-shortcuts)
- [其他上下文菜单](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_otherContext-global-shortcuts)
- [项目](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_project-global-shortcuts)
- [项目和解决方案上下文菜单](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_projectContext-global-shortcuts)
- [重构](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_refactor-global-shortcuts)
- [解决方案资源管理器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_solutionexplorerGLOBAL)
- [团队](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_team-global-shortcuts)
- [Team Foundation 上下文菜单](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_TFcontext-global-shortcuts)
- [测试](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_test-global-shortcuts)
- [测试资源管理器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_testexplorerGLOBAL)
- [工具](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_tools-global-shortcuts)
- [视图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_view-global-shortcuts)
- [窗口](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_window-global-shortcuts)

### <a name="analyze-global-shortcuts"></a><a name="bkmk_analyze-global-shortcuts"></a> 分析：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|向后导航|**Shift+Alt+3**| 分析.向后定位 |
|向前导航|**Shift+Alt+4**| 分析.向前定位 |

### <a name="architecture-global-shortcuts"></a><a name="bkmk_architecture-global-shortcuts"></a> 体系结构：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|新建关系图|**Ctrl+\\、Ctrl+N**| 体系结构.新建关系图 |

### <a name="azure-global-shortcuts"></a><a name="bkmk_windowsazure-global-shortcuts"></a> Azure：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|重试移动服务脚本操作|**Ctrl+Num \*、Ctrl+R**| WindowsAzure.重试移动服务脚本操作 |
|显示移动服务脚本错误详细信息|**Ctrl+Num \*、Ctrl+D**| WindowsAzure.显示移动服务脚本错误详细信息 |

### <a name="build-global-shortcuts"></a><a name="bkmk_build-global-shortcuts"></a> 生成：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|生成选择|**Ctrl+B** (Visual Studio 2019)| Build.BuildSelection |
|生成解决方案|**Ctrl+Shift+B**| 生成.生成解决方案 |
|取消|**Ctrl+Break**| 生成.取消 |
|Compile|**Ctrl+F7**| 生成.编译 |
|对解决方案运行代码分析|**Alt+F11**| 生成.对解决方案运行代码分析 |

### <a name="class-view-context-menus-global-shortcuts"></a><a name="bkmk_classview-global-shortcuts"></a> 类视图上下文菜单：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|属性|**Alt+Enter**| 类视图上下文菜单.类视图多选项目引用项.属性 |

### <a name="debug-global-shortcuts"></a><a name="bkmk_debug-global-shortcuts"></a> 调试：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|应用代码更改|**Alt+F10**| 调试.应用代码更改 |
|附加到进程|**Ctrl+Alt+P**| 调试.附加到进程 |
|自动|**Ctrl+Alt+V、A**| 调试.自动窗口 |
|全部中断|**Ctrl+Alt+Break**| 调试.全部中断 |
|断点|**Ctrl+Alt+B**| 调试.断点 |
|“调用堆栈”|**Ctrl+Alt+C**| 调试.调用堆栈 |
|删除所有断点|**Ctrl+Shift+F9**| 调试.删除所有断点 |
|启动|**Alt+F2**| 调试.诊断中心.启动 |
|反汇编|**Ctrl+Alt+D**| 调试.反汇编 |
|DOM 资源管理器|**Ctrl+Alt+V、D**| 调试.DOM 资源管理器 |
|启用断点|**Ctrl+F9**| 调试.启用断点 |
|异常|**Ctrl+Alt+E**| 调试.异常 |
|函数断点|**Ctrl+K、B** (Visual Studio 2019)<br />**Ctrl**+**B** (Visual Studio 2017)| Debug.FunctionBreakpoint |
|转到上一个调用或 IntelliTrace 事件|**Ctrl+Shift+F11**| 调试.转到上一个调用或 IntelliTrace 事件 |
|开始诊断|**Alt+F5**| 调试.图形.启动诊断 |
|即时|**Ctrl+Alt+I**| 调试.即时 |
|IntelliTrace 调用|**Ctrl+Alt+Y、T**| 调试.IntelliTrace 调用 |
|IntelliTrace 事件|**Ctrl+Alt+Y、F**| 调试.IntelliTrace 事件 |
|JavaScript 控制台|**Ctrl+Alt+V、C**| 调试.JavaScript 控制台 |
|局部变量|**Ctrl+Alt+V、L**| 调试.局部变量 |
|进程组合|**Ctrl+5**| 调试.位置工具栏.进程组合框 |
|堆栈帧组合|**Ctrl+7**| 调试.位置工具栏.堆栈帧组合框 |
|线程组合|**Ctrl+6**| 调试.位置工具栏.线程组合框 |
|切换当前线程标记状态|**Ctrl+8**| 调试.位置工具栏.切换当前线程标志状态 |
|切换已标记的线程|**Ctrl+9**| 调试.位置工具栏.切换标记的线程 |
|内存 1|**Ctrl+Alt+M、1**| 调试.内存1 |
|内存 2|**Ctrl+Alt+M、2**| 调试.内存2 |
|内存 3|**Ctrl+Alt+M、3**| 调试.内存3 |
|内存 4|**Ctrl+Alt+M、4**| 调试.内存4 |
|模块|**Ctrl+Alt+U**| 调试.模块 |
|并行堆栈|**Ctrl+Shift+D、S**| 调试.并行堆栈 |
|并行监视 1|**Ctrl+Shift+D、1**| 调试.并行监视 1 |
|并行监视 2|**Ctrl+Shift+D、2**| 调试.并行监视 2 |
|并行监视 3|**Ctrl+Shift+D、3**| 调试.并行监视 3 |
|并行监视 4|**Ctrl+Shift+D、4**| 调试.并行监视 4 |
|进程|**Ctrl+Alt+Z**| 调试.进程 |
|快速监视|**Shift+F9** 或 **Ctrl+Alt+Q**| 调试.快速监视 |
|重新附加到进程|**Shift+Alt+P**| Debug.ReattachtoProcess |
|刷新 Windows 应用|**Ctrl+Shift+R**| Debug.RefreshWindowsapp |
|寄存器|**Ctrl+Alt+G**| 调试.寄存器 |
|重启|**Ctrl+Shift+F5**| 调试.重新启动 |
|运行到光标处|**Ctrl+F10**| 调试.运行到光标处 |
|设置下一语句|**Ctrl+Shift+F10**| 调试.设置下一语句 |
|在代码图上显示调用堆栈|**Ctrl+Shift+`**| 调试.在代码图上显示调用堆栈 |
|显示下一语句|**Alt+Num** *| 调试.显示下一语句 |
|开始|**F5**| 调试.启动 |
|启动 Windows Phone 应用程序分析|**Alt+F1**| 调试.启动 Windows Phone 应用程序分析 |
|启动时不调试|**Ctrl+F5**| 调试.开始执行不调试 |
|“单步执行”|**F11**| 调试.逐语句 |
|单步执行当前进程|**Ctrl+Alt+F11**| 调试.进入并单步执行当前进程 |
|单步执行特定内容|**Shift+Alt+F11**| 调试.单步执行特定函数 |
|单步跳出|**Shift+F11**| 调试.跳出 |
|跳出当前进程|**Ctrl+Shift+Alt+F11**| 调试.跳出当前进程 |
|逐过程|F10（执行调试时：执行单步跳过操作）| 调试.逐过程 |
|逐过程|F10（未在执行调试时：启动调试，并在第一行用户代码上停止）| 调试.逐过程 |
|单步跳过当前进程|**Ctrl+Alt+F10**| 调试.逐过程执行当前进程 |
|停止调试|**Shift+F5**| 调试.停止调试 |
|停止性能分析|**Shift+Alt+F2**| 调试.停止性能分析 |
|任务|**Ctrl+Shift+D、K**| 调试.任务 |
|线程数|**Ctrl+Alt+H**| 调试.线程 |
|切换断点|**F9**| 调试.切换断点 |
|切换反汇编|**Ctrl+F11**| 调试.切换反汇编 |
|监视 1|**Ctrl+Alt+W、1**| 调试.监视 1 |
|监视 2|**Ctrl+Alt+W、2**| 调试.监视2 |
|监视 3|**Ctrl+Alt+W、3**| 调试.监视3 |
|监视 4|**Ctrl+Alt+W、4**| 调试.监视4 |

### <a name="debugger-context-menus-global-shortcuts"></a><a name="bkmk_debugger-global-shortcuts"></a> 调试器上下文菜单：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|删除|**Alt+F9、D**| 调试器上下文菜单.断点窗口.删除 |
|转到反汇编|**Alt+F9、A**| 调试器上下文菜单.断点窗口.转到反汇编 |
|转到源代码|**Alt+F9、S**| 调试器上下文菜单.断点窗口.转到源代码 |

### <a name="diagnostics-hub-global-shortcuts"></a><a name="bkmk_diagnostics-global-shortcuts"></a> 诊断中心：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|停止收集|**Ctrl+Alt+F2**| 诊断中心.停止收集 |

### <a name="edit-global-shortcuts"></a><a name="bkmk_edit-global-shortcuts"></a> 编辑：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|复制|**Ctrl+C**<br /><br /> or<br /><br /> **Ctrl+Ins**| 编辑.复制 |
|剪切|**Ctrl+X**<br /><br /> or<br /><br /> **Shift+Delete**| 编辑.剪切 |
|循环剪贴板环|**Ctrl+Shift+V**<br /><br /> or<br /><br /> **Ctrl+Shift+Ins**| 编辑.循环应用剪贴板中的复制项 |
|删除|**删除**| 编辑.删除 |
|复制|**Ctrl+D**| Edit.Duplicate |
|查找|**Ctrl+F**| 编辑.查找 |
|查找所有引用|**Shift+F12**| 编辑.查找所有引用 |
|在文件中查找|**Ctrl+Shift+F**| 编辑.在文件中查找 |
|查找下一个|**F3**| 编辑.查找下一个 |
|查找下一个选择|**Ctrl+F3**| 编辑.查找下一个选定项 |
|查找上一个|**Shift+F3**| 编辑.查找上一个 |
|查找上一个选择|**Ctrl+Shift+F3**| 编辑.查找上一个选定项 |
|生成方法|**Ctrl+K、Ctrl+M**| 编辑.生成方法 |
|转到|**Ctrl+G**| 编辑.转到 |
|转到全部|Ctrl+ 或 Ctrl+T| Edit.GoToAll |
|转到声明|**Ctrl+F12**| 编辑.转到声明 |
|转到定义|**F12**| 编辑.转到定义 |
|转到成员|Ctrl+1、Ctrl+M 或 Ctrl+1、M 或 Alt+\\| Edit.GoToMember |
|转到下一个位置|F8（错误列表或输出窗口中的下一个错误）| 编辑.转到下一个位置 |
|转到上一个位置|Shift+F8（错误列表或输出窗口中的上一个错误）| 编辑.转到上一个位置 |
|插入代码片段|**Ctrl+K、Ctrl+X**| 编辑.插入代码片段 |
|向下移动控件|**Ctrl+向下键**| 编辑.下移控件 |
|向下移动控件网格|向下键| 编辑.将控件移动到下侧网格 |
|向左移动控件|**Ctrl+向左键**| 编辑.左移控件 |
|向左移动控件网格|**向左键**| 编辑.将控件移动到左侧网格 |
|向右移动控件|**Ctrl+向右键**| 编辑.右移控件 |
|向右移动控件网格|**向右键**| 编辑.将控件移动到右侧网格 |
|向上移动控件|**Ctrl+向上键**| 编辑.上移控件 |
|向上移动控件网格|向上键| 编辑.将控件移动到上侧网格 |
|下一个书签|**Ctrl+K、Ctrl+N**| 编辑.下一书签 |
|文件夹中的下一个书签|**Ctrl+Shift+K、Ctrl+Shift+N**| 编辑.文件夹中的下一书签 |
|打开文件|Ctrl+Shift+G（打开光标下的文件名称）| 编辑.打开文件 |
|粘贴|**Ctrl+V**<br /><br /> or<br /><br /> **Shift+Ins**| 编辑.粘贴 |
|上一个书签|**Ctrl+K、Ctrl+P**| 编辑.上一书签 |
|文件夹中的上一个书签|**Ctrl+Shift+K、Ctrl+Shift+P**| 编辑.文件夹中的上一书签 |
|快速查找符号|**Shift+Alt+F12**| 编辑.快速查找符号 |
|重做|**Ctrl+Y**<br /><br /> or<br /><br /> **Ctrl+Shift+Z**<br /><br /> or<br /><br /> **Shift+Alt+Backspace**| 编辑.重做 |
|刷新远程引用|**Ctrl+Shift+J**| 编辑.刷新远程引用 |
|Replace|**Ctrl+H**| 编辑.替换 |
|在文件中替换|**Ctrl+Shift+H**| 编辑.在文件中替换 |
|全选|**Ctrl+A**| 编辑.全选 |
|选择下一个控件|Tab| 编辑.选择下一个控件 |
|选择上一个控件|**Shift+Tab**| 编辑.选择上一个控件 |
|显示磁贴网格|Enter| 编辑.显示平铺网格 |
|向下调整控件大小|**Ctrl+Shift+向下键**| 编辑.向下调大控件大小 |
|向下调整控件大小网格|**Shift+向下键**| 编辑.将控件调大到下侧网格 |
|向左调整控件大小|**Ctrl+Shift+向左键**| 编辑.向左调整控件大小 |
|向左调整控件大小网格|**Shift+向左键**| 编辑.将控件调大到左侧网格 |
|向右调整控件大小|**Ctrl+Shift+向右键**| 编辑.向右调整控件大小 |
|向右调整控件大小网格|**Shift+向右键**| 编辑.将控件调大到右侧网格 |
|向上调整控件大小|**Ctrl+Shift+向上键**| 编辑.向上调整控件大小 |
|向上调整控件大小网格|**Shift+向上键**| 编辑.将控件调大到上侧网格 |
|停止搜索|**Alt+F3、S**| 编辑.停止搜索 |
|环绕|**Ctrl+K、Ctrl+S** <br>（仅可用于 Visual Studio 2019 及更早版本）| 编辑.外侧代码 |
|撤消|**Ctrl+Z**<br /><br /> or<br /><br /> **Alt+Backspace**| 编辑.取消 |

### <a name="editor-context-menus-global-shortcuts"></a><a name="bkmk_editorContext-global-shortcuts"></a> 编辑器上下文菜单：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|断点条件|**Alt+F9, C**| EditorContextMenus.CodeWindow.Breakpoint.BreakpointConditions |
|断点编辑标签|**Alt+F9、L**| 编辑器上下文菜单.代码窗口.断点.断点编辑标签 |
|插入临时断点|**Shift+Alt+F9、T**| 编辑器上下文菜单.代码窗口.断点.插入临时断点 |
|显示项|**Ctrl+`**| 编辑器上下文菜单.代码窗口.代码图.显示项 |
|执行|**Ctrl+Alt+F5**| 编辑器上下文菜单.代码窗口.执行 |
|转到视图|**Ctrl+M、Ctrl+G**| 编辑器上下文菜单.代码窗口.转到视图 |
|切换标头代码文件|**Ctrl+K、Ctrl+O**（字母“O”）| 编辑器上下文菜单.代码窗口.切换标头代码文件 |
|查看调用层次结构|**Ctrl+K、Ctrl+T**<br /><br /> or<br /><br /> **Ctrl+K、T**| 编辑器上下文菜单.代码窗口.查看调用层次结构 |

### <a name="file-global-shortcuts"></a><a name="bkmk_file-global-shortcuts"></a> 文件：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|退出|**Alt+F4**| 文件.退出 |
|新建文件|**Ctrl+N**| 文件.新建文件 |
|新建项目|**Ctrl+Shift+N**| 文件.新建项目 |
|新建网站|**Shift+Alt+N**| 文件.新建网站 |
|打开文件|**Ctrl+O**（字母“O”）| 文件.打开文件 |
|打开项目|**Ctrl+Shift+O**（字母“O”）| 文件.打开项目 |
|打开网站|**Shift+Alt+O**（字母“O”）| 文件.打开网站 |
|打印|**Ctrl+P**| 文件.打印 |
|全部保存|**Ctrl+Shift+S**| 文件.全部保存 |
|保存选定项|**Ctrl+S**| 文件.保存选定项 |
|在浏览器中查看|**Ctrl+Shift+W**| 文件.在浏览器中查看 |

### <a name="help-global-shortcuts"></a><a name="bkmk_help-global-shortcuts"></a> 帮助：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|添加和删除帮助内容|**Ctrl+Alt+F1**| 帮助.添加和移除帮助内容 |
|F1 帮助|F1| 帮助.F1 帮助 |
|查看帮助|**Ctrl+F1**| Help.ViewHelp |
|窗口帮助|**Shift+F1**| 帮助.窗口帮助 |

### <a name="load-test-global-shortcuts"></a><a name="bkmk_loadtest-global-shortcuts"></a> 负载测试：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|跳至计数器窗格|**Ctrl+R、Q**| 负载测试.跳至计数器窗格 |

### <a name="other-context-menus-global-shortcuts"></a><a name="bkmk_otherContext-global-shortcuts"></a> 其他上下文菜单：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|添加新关系图|插入| 其他上下文菜单.Microsoft 数据实体设计上下文.添加新关系图 |

### <a name="project-global-shortcuts"></a><a name="bkmk_project-global-shortcuts"></a> 项目：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|添加现有项|**Shift+Alt+A**| 项目.添加现有项 |
|添加新项|**Ctrl+Shift+A**| 项目.添加新项 |
|类向导|**Ctrl+Shift+X**| 项目.类向导 |
|替代|**Ctrl+Alt+Ins**| 项目.重写 |
|预览更改|依次按 Alt+; 和 Alt+C| 项目.预览更改 |
|发布选定的文件|依次按 Alt+; 和 Alt+P| 项目.发布选定文件 |
|替换服务器中的选定文件|依次按 Alt+; 和 Alt+R| 项目.替换服务器上的选定文件 |

### <a name="project-and-solution-context-menus-global-shortcuts"></a><a name="bkmk_projectContext-global-shortcuts"></a> 项目和解决方案上下文菜单：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|下移|**Alt+向下键**| 项目和解决方案上下文菜单.项.下移 |
|上移|**Alt+向上键**| 项目和解决方案上下文菜单.项.上移 |

### <a name="refactor-global-shortcuts"></a><a name="bkmk_refactor-global-shortcuts"></a> 重构：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|封装字段|**Ctrl+R、Ctrl+E**| 重构.封装字段 |
|提取接口|**Ctrl+R、Ctrl+I**| 重构.提取接口 |
|提取方法|**Ctrl+R、Ctrl+M**| 重构.提取方法 |
|移除参数|**Ctrl+R、Ctrl+V**| 重构.移除参数 |
|重命名|**Ctrl+R、Ctrl+R**| 重构.重命名 |
|重新排列参数|**Ctrl+R、Ctrl+O**（字母“O”）| 重构.重新排列参数 |

### <a name="solution-explorer-global-shortcuts"></a><a name="bkmk_solutionexplorerGLOBAL"></a> 解决方案资源管理器：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|开启文件筛选器|**Ctrl+[** 、**O**（字母“O”）<br /><br /> or<br /><br /> **Ctrl+[** 、**Ctrl+O**（字母“O”）| 解决方案资源管理器.打开文件筛选器 |
|挂起的更改筛选器|**Ctrl+[** 、**P**<br /><br /> or<br /><br /> **Ctrl+[** 、**Ctrl+P**| 解决方案资源管理器.挂起更改筛选器 |
|与活动文档同步|**Ctrl+[** 、**S**<br /><br /> or<br /><br /> **Ctrl+[** 、**Ctrl+S**| 解决方案资源管理器.与活动文档同步 |

### <a name="team-global-shortcuts"></a><a name="bkmk_team-global-shortcuts"></a> 团队：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|转到 git 分支|**Ctrl+0**（数字“0”）、**Ctrl+N**<br /><br /> or<br /><br /> **Ctrl+0、N**| 团队.Git.转到 Git 分支 |
|转到 git 更改|**Ctrl+0**（数字“0”）、**Ctrl+G**<br /><br /> or<br /><br /> **Ctrl+0、G**| 团队.Git.转到 Git 更改 |
|转到 git 提交|**Ctrl+0**（数字“0”）、**Ctrl+O**（字母“O”）<br /><br /> or<br /><br /> **Ctrl+0、O**| 团队.Git.转到 Git 提交 |
|团队资源管理器搜索|**Ctrl+'**| 团队.团队资源管理器搜索 |

### <a name="team-foundation-context-menus-global-shortcuts"></a><a name="bkmk_TFcontext-global-shortcuts"></a> Team Foundation 上下文菜单：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|转到生成|**Ctrl+0**（数字“0”）、**Ctrl+B**<br /><br /> or<br /><br /> **Ctrl+0、B**| Team Foundation 上下文菜单.命令.转到生成 |
|转到连接|**Ctrl+0**（数字“0”）、**Ctrl+C**<br /><br /> or<br /><br /> **Ctrl+0、C**| Team Foundation 上下文菜单.命令.转到连接 |
|转到文档|**Ctrl+0**（数字“0”）、**Ctrl+D**<br /><br /> or<br /><br /> **Ctrl+0、D**| Team Foundation 上下文菜单.命令.转到文档 |
|转到主页|**Ctrl+0**（数字“0”）、**Ctrl+H**<br /><br /> or<br /><br /> **Ctrl+0、H**| Team Foundation 上下文菜单.命令.转到主页 |
|转到我的工作|**Ctrl+0**（数字“0”）、**Ctrl+M**<br /><br /> or<br /><br /> **Ctrl+0、M**| Team Foundation 上下文菜单.命令.转到我的工作 |
|转到挂起的更改|**Ctrl+0**（数字“0”）、**Ctrl+P**<br /><br /> or<br /><br /> **Ctrl+0、P**| Team Foundation 上下文菜单.命令.转到挂起的更改 |
|转到报表|**Ctrl+0**（数字“0”）、**Ctrl+R**<br /><br /> or<br /><br /> **Ctrl+0、R**| Team Foundation 上下文菜单.命令.转到报告 |
|转到设置|**Ctrl+0**（数字“0”）、**Ctrl+S**<br /><br /> or<br /><br /> **Ctrl+0、S**| Team Foundation 上下文菜单.命令.转到设置 |
|转到 Web 访问|**Ctrl+0**（数字“0”）、**Ctrl+A**<br /><br /> or<br /><br /> **Ctrl+0、A**| Team Foundation 上下文菜单.命令.转到 Web 访问 |
|转到工作项|**Ctrl+0**（数字“0”）、**Ctrl+W**<br /><br /> or<br /><br /> **Ctrl+0、W**| Team Foundation 上下文菜单.命令.转到工作项 |

### <a name="test-global-shortcuts"></a><a name="bkmk_test-global-shortcuts"></a> 测试：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|使用编码的 UI 测试生成器|**Ctrl+\\、Ctrl+C**| 测试.使用编码的 UI 测试生成器 |
|使用现有的操作录制|**Ctrl+\\、Ctrl+A**| 测试.使用现有的操作录制 |

### <a name="test-explorer-global-shortcuts"></a><a name="bkmk_testexplorerGLOBAL"></a> 测试资源管理器：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|调试所有测试|**Ctrl+R、Ctrl+A**| 测试资源管理器.调试所有测试 |
|调试上下文中的所有测试|**Ctrl+R、Ctrl+T**| 测试资源管理器.调试上下文中的所有测试 |
|调试上次运行|Ctrl+R、D| TestExplorer.DebugLastRun |
|重复上次运行|**Ctrl+R、L**| 测试资源管理器.重复上次运行 |
|运行所有测试|**Ctrl+R、A**| 测试资源管理器.运行所有测试 |
|运行上下文中的所有测试|**Ctrl+R、T**| 测试资源管理器.运行上下文中的所有测试 |
|显示测试资源管理器|Ctrl+E、T| TestExplorer.ShowTestExplorer |
|打开选项卡|Ctrl+E、L| LiveUnitTesting.OpenTab |
|代码覆盖率结果|**Ctrl+E、C**| Test.CodeCoverageResults |

### <a name="tools-global-shortcuts"></a><a name="bkmk_tools-global-shortcuts"></a> 工具：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|附加到进程|**Ctrl+Alt+P**| 工具.附加到进程 |
|代码片段管理器|**Ctrl+K、Ctrl+B**| 工具.代码段管理器 |
|强制 GC|**Ctrl+Shift+Alt+F12、Ctrl+Shift+Alt+F12**| 工具.强制 GC |

### <a name="view-global-shortcuts"></a><a name="bkmk_view-global-shortcuts"></a> 视图：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|所有窗口|**Shift+Alt+M**| 视图.所有窗口 |
|体系结构资源管理器|**Ctrl+\\、Ctrl+R**| 视图.体系结构资源管理器 |
|下移|Alt+向左键（在文本编辑器中，这些功能不同于 View.NavigateBackward）| 视图.向后 |
|书签窗口|**Ctrl+K、Ctrl+W**| 视图.书签窗口 |
|浏览下一个|**Ctrl+Shift+1**| 视图.浏览下一个 |
|浏览上一个|**Ctrl+Shift+2**| 视图.浏览上一个 |
|调用层次结构|**Ctrl+Alt+K**| 视图.调用层次结构 |
|类视图|**Ctrl+Shift+C**| 视图.类视图 |
|类视图转到搜索组合|**Ctrl+K、Ctrl+V**| 视图.类视图转到搜索组合框 |
|代码定义窗口|**Ctrl+\\、D**<br /><br /> or<br /><br /> **Ctrl+\\、Ctrl+D**| 视图.代码定义窗口 |
|“命令”窗口|**Ctrl+Alt+A**| 视图.命令窗口 |
|数据源|**Shift+Alt+D**| View.DataSources |
|文档大纲|**Ctrl+Alt+T**| 视图.文档大纲 |
|编辑标签|F2| 视图.编辑标签 |
|错误列表|**Ctrl+\\、E**<br /><br /> or<br /><br /> **Ctrl+\\、Ctrl+E**| 视图.错误列表 |
|F# 交互|**Ctrl+Alt+F**| 视图.F# Interactive |
|查找符号结果|**Ctrl+Alt+F12**| 视图.查找符号结果 |
|前进|Alt+向右键（在文本编辑器中，这些功能不同于 View.NavigateForward）| 视图.向前 |
|向前浏览上下文|**Ctrl+Shift+7**| 视图.向前浏览上下文 |
|全屏|**Shift+Alt+Enter**| 视图.全屏 |
|向后导航|**Ctrl+-**| 视图.向后定位 |
|向前导航|**Ctrl+Shift+-**| 视图.向前定位 |
|下一个错误|**Ctrl+Shift+F12**| 视图.下一个错误 |
|通知|**Ctrl+W、N**<br /><br /> or<br /><br /> **Ctrl+W、Ctrl+N**| 视图.通知 |
|对象浏览器|**Ctrl+Alt+J**| 视图.对象浏览器 |
|对象浏览器转到搜索组合|**Ctrl+K、Ctrl+R**| 视图.对象浏览器转到搜索组合框 |
|输出|**Ctrl+Alt+O**（字母“O”）| 视图.输出 |
|Pop 浏览上下文|Ctrl+Shift+8（仅限 C++）| View.PopBrowseContext |
|“属性”窗口|F4| 视图.属性窗口 |
|属性页|**Shift+F4**| 视图.属性页 |
|资源视图|**Ctrl+Shift+E**| 视图.资源视图 |
|服务器资源管理器|**Ctrl+Alt+S**| 视图.服务器资源管理器 |
|显示智能标记|**Shift+Alt+F10**<br /><br /> or<br /><br /> **Ctrl+.**| 视图.显示智能标记 |
|解决方案资源管理器|**Ctrl+Alt+L**| 视图.解决方案资源管理器 |
|SQL Server 对象资源管理器|**Ctrl+\\、Ctrl+S**| 视图.SQL Server 对象浏览器 |
|任务列表|**Ctrl+\\、T**<br /><br /> or<br /><br /> **Ctrl+\\、Ctrl+T**| 视图.任务列表 |
|TFS 团队资源管理器|**Ctrl+\\、Ctrl+M**| 视图.Tfs 团队资源管理器 |
|工具箱|**Ctrl+Alt+X**| 视图.工具箱 |
|UML 模型资源管理器|**Ctrl+\\、Ctrl+U**| 视图.UML 模型资源管理器 |
|查看代码|**F7**| 视图.查看代码 |
|视图设计器|**Shift+F7**| 视图.视图设计器 |
|Web 浏览器|**Ctrl+Alt+R**| 视图.Web浏览器 |
|放大|**Ctrl+Shift+.**| 视图.放大 |
|缩小|**Ctrl+Shift+,**| 视图.缩小 |
|显示测试资源管理器|Ctrl+E、T| TestExplorer.ShowTestExplorer |

### <a name="window-global-shortcuts"></a><a name="bkmk_window-global-shortcuts"></a> Windows：全局快捷方式

|命令|键盘快捷键|命令 ID|
|-|-|-|
|激活文档窗口|**Esc**| 窗口.激活文档窗口 |
|将选项卡添加到选定内容|**Ctrl+Shift+Alt+空格键**| 窗口.将选项卡添加到所选内容 |
|关闭文档窗口|**Ctrl+F4**| 窗口.关闭文档窗口 |
|关闭工具窗口|**Shift+Esc**| 窗口.关闭工具窗口 |
|使选项卡保持打开|**Ctrl+Alt+Home**| 窗口.将选项卡保持打开状态 |
|移动到导航栏|**Ctrl+F2**| 窗口.移动到导航栏 |
|下一个文档窗口|**Ctrl+F6**| 窗口.下一个文档窗口 |
|下一个文档窗口导航|**Ctrl+Tab**| 窗口.下一个文档窗口导航栏 |
|下一个窗格|**Alt+F6**| 窗口.下一窗格 |
|下一个拆分窗格|**F6**| 窗口.下一个拆分窗格 |
|下一个选项卡|**Ctrl+Alt+PgDn**<br /><br /> or<br /><br /> **Ctrl+PgDn**| 窗口.下一选项卡 |
|下一个选项卡并添加到选定内容|**Ctrl+Shift+Alt+PgDn**| Window.NextTabandAddtoSelection |
|下一个工具窗口导航|**Alt+F7**| 窗口.下一个工具窗口导航栏 |
|上一个文档窗口|**Ctrl+Shift+F6**| 窗口.上一个文档窗口 |
|上一个文档窗口导航|**Ctrl+Shift+Tab**| 窗口.上一个文档窗口导航栏 |
|上一个窗格|**Shift+Alt+F6**| 窗口.上一窗格 |
|上一个拆分窗格|**Shift+F6**| 窗口.上一个拆分窗格 |
|上一个选项卡|**Ctrl+Alt+PgUp**<br /><br /> or<br /><br /> **Ctrl+PgUp**| 窗口.上一选项卡 |
|上一个选项卡并添加到选定内容|**Ctrl+Shift+Alt+PgUp**| Window.PreviousTabandAddtoSelection |
|上一个工具窗口导航|**Shift+Alt+F7**| 窗口.上一个工具窗口导航栏 |
|快速启动|**Ctrl+Q**| 窗口.快速启动 |
|快速启动上一个类别|**Ctrl+Shift+Q**| 窗口.快速启动以前分类 |
|显示停靠菜单|**Alt+-**| 窗口.显示停靠菜单 |
|显示 Ex MDI 文件列表|**Ctrl+Alt+向下键**| 窗口.显示EzMDI文件列表 |
|解决方案资源管理器搜索|**Ctrl+;**| 窗口.解决方案资源管理器搜索 |
|窗口搜索|**Alt+`**| 窗口.窗口搜索 |

## <a name="context-specific-shortcuts"></a>上下文特定的快捷方式
这些键盘快捷方式是特定于上下文的，这意味着你可以在 Visual Studio 中使用特定于项目类型、编程语言或平台的菜单和项目。

- [ADO.NET 实体数据模型设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_adonet-entity-data-model-designer-context-specific-shortcuts)
- [类图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_class-diagram-context-specific-shortcuts)
- [编码的 UI 测试编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_coded-ui-test-editor-context-specific-shortcuts)
- [数据集编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_dataset-editor-context-specific-shortcuts)
- [差异查看器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_difference-viewer-context-specific-shortcuts)
- [DOM 资源管理器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_dom-explorer-context-specific-shortcuts)
- [F# Interactive](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_f-interactive-context-specific-shortcuts)
- [关系图文档编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_graph-document-editor-context-specific-shortcuts)
- [图形诊断](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_graphics-diagnostics-context-specific-shortcuts)
- [HTML 编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_html-editor-context-specific-shortcuts)
- [HTML 编辑器设计视图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_html-editor-design-view-context-specific-shortcuts)
- [HTML 编辑器源视图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_html-editor-source-view-context-specific-shortcuts)
- [层关系图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_layer-diagram-context-specific-shortcuts)
- [托管资源编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_managed-resources-editor-context-specific-shortcuts)
- [合并编辑器窗口](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_merge-editor-window-context-specific-shortcuts)
- [Microsoft SQL Server Data Tools，架构比较](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_microsoft-sql-server-data-tools-schema-compare-context-specific-shortcuts)
- [Microsoft SQL Server Data Tools，表设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_microsoft-sql-server-data-tools-table-designer-context-specific-shortcuts)
- [Microsoft SQL Server Data Tools，T-SQL 编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_microsoft-sql-server-data-tools-t-sql-editor-context-specific-shortcuts)
- [Microsoft SQL Server Data Tools，T-SQL PDW 编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_microsoft-sql-server-data-tools-t-sql-pdw-editor-context-specific-shortcuts)
- [Page Inspector](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_page-inspector-context-specific-shortcuts)
- [查询设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_query-designer-context-specific-shortcuts)
- [查询结果](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_query-results-context-specific-shortcuts)
- [报表设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_report-designer-context-specific-shortcuts)
- [序列图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_sequence-diagram-context-specific-shortcuts)
- [设置设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_settings-designer-context-specific-shortcuts)
- [解决方案资源管理器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_solution-explorer-context-specific-shortcuts)
- [Team Explorer](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_team-explorer-context-specific-shortcuts)
- [测试资源管理器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_test-explorer-context-specific-shortcuts)
- [文本编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_text-editor-context-specific-shortcuts)
- [UML 活动图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_uml-activity-diagram-context-specific-shortcuts)
- [UML 类图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_uml-class-diagram-context-specific-shortcuts)
- [UML 组件图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_uml-component-diagram-context-specific-shortcuts)
- [UML 用例图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_uml-use-case-diagram-context-specific-shortcuts)
- [VC 快捷键编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_vc-accelerator-editor-context-specific-shortcuts)
- [VC 对话框编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_vc-dialog-editor-context-specific-shortcuts)
- [VC 图像编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_vc-image-editor-context-specific-shortcuts)
- [VC 字符串编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_vc-string-editor-context-specific-shortcuts)
- [视图设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_view-designer-context-specific-shortcuts)
- [Visual Studio](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_visual-studio-context-specific-shortcuts)
- [Windows Forms Designer — Windows 窗体设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_windows-forms-designer-context-specific-shortcuts)
- [工作项编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_work-item-editor-context-specific-shortcuts)
- [工作项查询视图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_work-item-query-view-context-specific-shortcuts)
- [工作项结果视图](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_work-item-results-view-context-specific-shortcuts)
- [工作流设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_workflow-designer-context-specific-shortcuts)
- [XAML 设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_xaml-ui-designer-context-specific-shortcuts)
- [XML（文本）编辑器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_xml-text-editor-context-specific-shortcuts)
- [XML 架构设计器](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_xml-schema-designer-context-specific-shortcuts)

### <a name="adonet-entity-data-model-designer-context-specific-shortcuts"></a><a name="bkmk_adonet-entity-data-model-designer-context-specific-shortcuts"></a> ADO.NET 实体数据模型设计器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：

|命令|键盘快捷键|命令 ID|
|-|-|-|
|向下|**Alt+向下键**| 其他上下文菜单.Microsoft 数据实体设计上下文.移动属性.向下 |
|向下 5|**Alt+PgDn**| 其他上下文菜单.Microsoft 数据实体设计上下文.移动属性.向下 5 |
|到底部|**Alt+End**| 其他上下文菜单.Microsoft 数据实体设计上下文.移动属性.到底部 |
|到顶部|**Alt+Home**| 其他上下文菜单.Microsoft 数据实体设计上下文.移动属性.到顶部 |
|向上|**Alt+向上键**| 其他上下文菜单.Microsoft 数据实体设计上下文.移动属性.向上 |
|向上 5|**Alt+PgUp**| 其他上下文菜单.Microsoft 数据实体设计上下文.移动属性.向上 5 |
|重命名|**Ctrl+R、R**| 其他上下文菜单.Microsoft 数据实体设计上下文.重构.重命名 |
|从关系图中删除|**Shift+Del**| 其他上下文菜单.Microsoft 数据实体设计上下文.从关系图中移除 |
|实体数据模型浏览器|**Ctrl+1**| 视图.实体数据模型资源浏览器 |
|实体数据模型映射详细信息|**Ctrl+2**| 视图.实体数据模型映射详细信息 |

### <a name="class-diagram-context-specific-shortcuts"></a><a name="bkmk_class-diagram-context-specific-shortcuts"></a> 类图：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|折叠|**Num -**| 类图.折叠 |
|展开|**Num +**| 类图.展开 |
|删除|**Ctrl+Del**| 编辑.删除 |
|展开/折叠基类型列表|**Shift+Alt+B**| 编辑.展开折叠基类型列表 |
|定位到棒糖形|**Shift+Alt+L**| 编辑.定位到棒糖形 |
|从关系图中删除|**删除**| 编辑.从关系图中移除 |
|查看代码|Enter| 视图.查看代码 |

### <a name="coded-ui-test-editor-context-specific-shortcuts"></a><a name="bkmk_coded-ui-test-editor-context-specific-shortcuts"></a> 编码的 UI 测试编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|将引用复制到剪贴板|**Ctrl+C**| 其他上下文菜单.UI 测试编辑器上下文菜单.将引用复制到剪贴板 |
|在前面插入延迟|**Ctrl+Alt+D**| 其他上下文菜单.UI 测试编辑器上下文菜单.在前面插入延迟 |
|查找全部|**Shift+Alt+L**| 其他上下文菜单.UI 测试编辑器上下文菜单.查找全部 |
|查找 UI 控件|**Ctrl+Shift+L**| 其他上下文菜单.UI 测试编辑器上下文菜单.查找 UI 控件 |
|移动代码|**Ctrl+Alt+C**| 其他上下文菜单.UI 测试编辑器上下文菜单.移动代码 |
|拆分成新方法|**Ctrl+Shift+T**| 其他上下文菜单.UI 测试编辑器上下文菜单.拆分成新方法 |

### <a name="dataset-editor-context-specific-shortcuts"></a><a name="bkmk_dataset-editor-context-specific-shortcuts"></a> 数据集编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|插入列|插入| OtherContextMenus.ColumnContext.InsertColumn |
|列|**Ctrl+L**| OtherContextMenus.DbTableContext.Add.Column |

### <a name="difference-viewer-context-specific-shortcuts"></a><a name="bkmk_difference-viewer-context-specific-shortcuts"></a> 差异查看器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|忽略修整空白|**Ctrl+\\、Ctrl+空格键**| 差异.忽略修整空白 |
|内联视图|**Ctrl+\\、Ctrl+1**| 差异.内联视图 |
|仅左侧视图|**Ctrl+\\、Ctrl+3**| 差异.仅左视图 |
|下一个差异|**F8**| 差异.下一个差异 |
|上一个差异|**Shift+F8**| 差异.上一个差异 |
|仅右侧视图|**Ctrl+\\、Ctrl+4**| 差异.仅右视图 |
|并排视图|**Ctrl+\\、Ctrl+2**| 差异.并列视图 |
|在左侧和右侧之间切换|**Ctrl+\\、Ctrl+Tab**| 差异.在左视图和右视图之间切换 |
|同步视图切换|**Ctrl+\\、Ctrl+向下键**| 差异.同步视图切换 |
|添加注释|**Ctrl+Shift+K**| 编辑器上下文菜单.代码窗口.添加注释 |
|编辑本地文件|**Ctrl+Shift+P**| 编辑器上下文菜单.代码窗口.编辑本地文件 |

### <a name="dom-explorer-context-specific-shortcuts"></a><a name="bkmk_dom-explorer-context-specific-shortcuts"></a> DOM 资源管理器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|刷新|**F5**| DOM 资源管理器.刷新 |
|选择元素|**Ctrl+B**| DOM 资源管理器.选择元素 |
|显示布局|**Ctrl+Shift+I**| DOM 资源管理器.显示布局 |

### <a name="f-interactive-context-specific-shortcuts"></a><a name="bkmk_f-interactive-context-specific-shortcuts"></a> F# 交互窗口：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|取消交互式评估|**Ctrl+Break**| 其他上下文菜单.FSI 控制台上下文.取消交互评估 |

### <a name="graph-document-editor-context-specific-shortcuts"></a><a name="bkmk_graph-document-editor-context-specific-shortcuts"></a> 关系图文档编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|添加节点|插入| 体系结构上下文菜单.定向关系图上下文菜单.高级.添加.添加节点 |
|两个依赖项|**B**| 体系结构上下文菜单.定向关系图上下文菜单.高级.选择.两个依赖项 |
|传入依赖项|**I**| 体系结构上下文菜单.定向关系图上下文菜单.高级.选择.传入依赖项 |
|传出依赖项|**O**| 体系结构上下文菜单.定向关系图上下文菜单.高级.选择.传出依赖项 |
|新建注释|**Ctrl+Shift+K**<br /><br /> or<br /><br /> **Ctrl+E、C**| 体系结构上下文菜单.定向关系图上下文菜单.新注释 |
|删除|**删除**| 体系结构上下文菜单.定向关系图上下文菜单.删除 |
|重命名|F2| 体系结构上下文菜单.定向关系图上下文菜单.重命名 |

### <a name="graphics-diagnostics-context-specific-shortcuts"></a><a name="bkmk_graphics-diagnostics-context-specific-shortcuts"></a> 图形诊断：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|捕获帧|无| 调试.图形.捕获帧 |
|向下移动像素选择|**Shift+Alt+向下键**| Graphics.MovePixelSelectionDown |
|向左移动像素选择|**Shift+Alt+向左键**| Graphics.MovePixelSelectionLeft |
|向右移动像素选择|**Shift+Alt+向右键**| Graphics.MovePixelSelectionRight |
|向上移动像素选择|**Shift+Alt+向上键**| Graphics.MovePixelSelectionUp |
|缩放到实际大小|**Shift+Alt+0**（数字“0”）| Graphics.ZoomToActualSize |
|缩放以适应窗口|**Shift+Alt+9**| Graphics.ZoomToFitInWindow |
|放大|**Shift+Alt+=**| Graphics.ZoomIn |
|缩小|**Shift+Alt+-**| Graphics.ZoomOut |

### <a name="html-editor-context-specific-shortcuts"></a><a name="bkmk_html-editor-context-specific-shortcuts"></a> HTML 编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|转到控制器|**Ctrl+M、Ctrl+G**| 其他上下文菜单.HTML 上下文.转到控制器 |

### <a name="html-editor-design-view-context-specific-shortcuts"></a><a name="bkmk_html-editor-design-view-context-specific-shortcuts"></a> HTML 编辑器设计视图：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|向下移动控件|**Ctrl+向下键**| 编辑.下移控件 |
|向上移动控件|**Ctrl+向上键**| 编辑.上移控件 |
|Bold|**Ctrl+B**| 格式.粗体 |
|转换为超链接|**Ctrl+L**| 格式.转换为超链接 |
|插入书签|**Ctrl+Shift+L**| 格式.插入书签 |
|斜体|**Ctrl+I**| 格式.斜体 |
|下划线|**Ctrl+U**| 格式.下划线 |
|添加内容页|**Ctrl+M、Ctrl+C**| 项目.添加内容页 |
|左侧的列|**Ctrl+Alt+向左键**| 表.左侧列 |
|右侧的列|**Ctrl+Alt+向右键**| 表.右侧列 |
|上方的行|**Ctrl+Alt+向上键**| 表.上面的行 |
|下方的行|**Ctrl+Alt+向下键**| 表.下面的行 |
|净不可见控件|**Ctrl+Shift+N**| 视图.ASP.NET 非可视控件 |
|编辑主视图|**Ctrl+M、Ctrl+M**| 视图.编辑主表 |
|下一个视图|**Ctrl+PgDn**| 视图.下一个视图 |
|显示智能标记|**Shift+Alt+F10**| 视图.显示智能标记 |
|查看标记|**Shift+F7**| 视图.查看标记 |
|上一个选项卡|**Ctrl+PgUp**| 窗口.上一选项卡 |

### <a name="html-editor-source-view-context-specific-shortcuts"></a><a name="bkmk_html-editor-source-view-context-specific-shortcuts"></a> HTML 编辑器源视图：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|转到控制器|**Ctrl+M、Ctrl+G**| 其他上下文菜单.HTML 上下文.转到控制器 |
|下一个视图|**Ctrl+PgDn**| 视图.下一个视图 |
|同步视图|**Ctrl+Shift+Y**| 视图.同步视图 |
|视图设计器|**Shift+F7**| 视图.视图设计器 |
|上一个选项卡|**Ctrl+PgUp**| 窗口.上一选项卡 |

### <a name="layer-diagram-context-specific-shortcuts"></a><a name="bkmk_layer-diagram-context-specific-shortcuts"></a> 层关系图：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|删除|**Shift+Delete**| 编辑.删除 |

### <a name="managed-resources-editor-context-specific-shortcuts"></a><a name="bkmk_managed-resources-editor-context-specific-shortcuts"></a> 托管资源编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|编辑单元格|F2| 编辑.编辑单元格 |
|删除|**删除**| 编辑.移除 |
|删除行|**Ctrl+Delete**| 编辑.移除行 |
|取消选择|**Esc 键**| 编辑.取消选定 |
|音频|**Ctrl+4**| 资源.音频 |
|文件|**Ctrl+5**| 资源.文件 |
|图标|**Ctrl+3**| 资源.图标 |
|映像|**Ctrl+2**| 资源.图像 |
|其他|**Ctrl+6**| 资源.其他 |
|字符串|**Ctrl+1**| 资源.字符串 |

### <a name="merge-editor-window-context-specific-shortcuts"></a><a name="bkmk_merge-editor-window-context-specific-shortcuts"></a> 合并编辑器窗口：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|在左侧窗口上设置焦点|**Alt+1**| Team Foundation 上下文菜单.合并上下文菜单.在左侧窗口上设置焦点 |
|在结果窗口上设置焦点|**Alt+2**| Team Foundation 上下文菜单.合并上下文菜单.在结果窗口上设置焦点 |
|在右侧窗口上设置焦点|**Alt+3**| Team Foundation 上下文菜单.合并上下文菜单.在右侧窗口上设置焦点 |

### <a name="microsoft-sql-server-data-tools-schema-compare-context-specific-shortcuts"></a><a name="bkmk_microsoft-sql-server-data-tools-schema-compare-context-specific-shortcuts"></a> Microsoft SQL Server Data Tools，架构比较：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|SSDT 架构比较 - 比较|**Shift+Alt+C**| SQL.SSDT 架构比较比较 |
|SSDT 架构比较 - 生成脚本|**Shift+Alt+G**| SQL.SSDT 架构比较生成脚本 |
|SSDT 架构比较 - 下一个更改|**Shift+Alt+.**| SQL.SSDT 架构比较下一个更改 |
|SSDT 架构比较 - 上一个更改|**Shift+Alt+,**| SQL.SSDT 架构比较上一个更改 |
|SSDT 架构比较 - 停止|**Alt+Break**| SQL.SSDT 架构比较停止 |
|SSDT 架构比较 - 写入更新|**Shift+Alt+U**| SQL.SSDT 架构比较写入更新 |

### <a name="microsoft-sql-server-data-tools-table-designer-context-specific-shortcuts"></a><a name="bkmk_microsoft-sql-server-data-tools-table-designer-context-specific-shortcuts"></a> Microsoft SQL Server Data Tools，表设计器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|提交所有编辑|**Shift+Alt+U**|
|扩展通配符|**Ctrl+R、E**<br /><br /> or<br /><br /> **Ctrl+R、Ctrl+E**| SQL.展开通配符 |
|完全限定名|**Ctrl+R、Q**<br /><br /> or<br /><br /> **Ctrl+R、Ctrl+Q**| SQL.完全限定名称 |
|移到架构|**Ctrl+R、M**<br /><br /> or<br /><br /> **Ctrl+R、Ctrl+M**| SQL.移至架构 |
|重命名|F2<br /><br /> or<br /><br /> **Ctrl+R、R**<br /><br /> or<br /><br /> **Ctrl+R、Ctrl+R**| SQL.重命名 |
|在脚本面板中查看文件|**Shift+Alt+PgDn**| |

### <a name="microsoft-sql-server-data-tools-t-sql-editor-context-specific-shortcuts"></a><a name="bkmk_microsoft-sql-server-data-tools-t-sql-editor-context-specific-shortcuts"></a> Microsoft SQL Server Data Tools，T-SQL 编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|提交所有编辑|**Shift+Alt+U**|
|使用调试器执行|**Alt+F5**| SQL.使用调试器执行 |
|扩展通配符|**Ctrl+R、E**<br /><br /> or<br /><br /> **Ctrl+R、Ctrl+E**| SQL.展开通配符 |
|完全限定名|**Ctrl+R、Q**<br /><br /> or<br /><br /> **Ctrl+R、Ctrl+Q**| SQL.完全限定名称 |
|移到架构|**Ctrl+R、M**<br /><br /> or<br /><br /> **Ctrl+R、Ctrl+M**| SQL.移至架构 |
|重命名|F2<br /><br /> or<br /><br /> **Ctrl+R、R**<br /><br /> or<br /><br /> **Ctrl+R、Ctrl+R**| SQL.重命名 |
|T SQL 编辑器 - 取消查询|**Alt+Break**| SQL.TSql 编辑器取消查询 |
|T SQL 编辑器 - 执行查询|**Ctrl+Shift+E**| SQL.TSql 编辑器执行查询 |
|T SQL 编辑器 - 结果保存为文件|**Ctrl+D、F**| SQL.TSql 编辑器结果显示为文件 |
|T SQL 编辑器 - 结果显示为网格|**Ctrl+D、G**| SQL.TSql 编辑器结果显示为网格 |
|T SQL 编辑器 - 结果显示为文本|**Ctrl+D、T**| SQL.TSql 编辑器结果显示为文本 |
|T SQL 编辑器 - 显示预估计划|**Ctrl+D、E**| SQL.TSql 编辑器显示估计计划 |
|T SQL 编辑器 - 切换执行计划|**Ctrl+D、A**| SQL.TSql 编辑器切换执行计划 |
|T SQL 编辑器 - 切换结果窗格|**Ctrl+D、R**| SQL.TSql 编辑器切换结果窗格 |
|T SQL 编辑器 - 克隆查询|**Ctrl+Alt+N**|SQL.TSqlEditorCloneQuery |
|T SQL 编辑器 - 数据库组合|**Shift+Alt+PgDn**|SQL.TSqlEditorDatabaseCombo |

### <a name="microsoft-sql-server-data-tools-t-sql-pdw-editor-context-specific-shortcuts"></a><a name="bkmk_microsoft-sql-server-data-tools-t-sql-pdw-editor-context-specific-shortcuts"></a> Microsoft SQL Server Data Tools，T-SQL PDW 编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|T SQL 编辑器 - 取消查询|**Alt+Break**| SQL.TSql 编辑器取消查询 |
|T SQL 编辑器 - 执行查询|**Ctrl+Shift+E**| SQL.TSql 编辑器执行查询 |
|T SQL 编辑器 - 结果保存为文件|**Ctrl+D、F**| SQL.TSql 编辑器结果显示为文件 |
|T SQL 编辑器 - 结果显示为网格|**Ctrl+D、G**| SQL.TSql 编辑器结果显示为网格 |
|T SQL 编辑器 - 结果显示为文本|**Ctrl+D、T**| SQL.TSql 编辑器结果显示为文本 |
|T SQL 编辑器 - 显示预估计划|**Ctrl+D、E**| SQL.TSql 编辑器显示估计计划 |
|T SQL 编辑器 - 切换执行计划|**Ctrl+D、A**| SQL.TSql 编辑器切换执行计划 |
|T SQL 编辑器 - 切换结果窗格|**Ctrl+D、R**| SQL.TSql 编辑器切换结果窗格 |
|T SQL 编辑器 - 克隆查询|**Ctrl+Alt+N**|SQL.TSqlEditorCloneQuery |
|T SQL 编辑器 - 克隆查询|**Shift+Alt+PgDn**|SQL.TSqlEditorCloneQuery |

### <a name="page-inspector-context-specific-shortcuts"></a><a name="bkmk_page-inspector-context-specific-shortcuts"></a> Page Inspector：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|最小化|**F12**| PageInspector.最小化 |

### <a name="query-designer-context-specific-shortcuts"></a><a name="bkmk_query-designer-context-specific-shortcuts"></a> 查询设计器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|取消检索数据|**Ctrl+T**| 查询设计器.取消检索数据 |
|条件|**Ctrl+2**| 查询设计器.条件 |
|图示|**Ctrl+1**| 查询设计器.关系图 |
|执行 SQL|**Ctrl+R**| 查询设计器.执行SQL |
|转到行|**Ctrl+G**| 查询设计器.转到行 |
|联接模式|**Ctrl+Shift+J**| 查询设计器.联接模式 |
|结果|**Ctrl+4**| 查询设计器.结果 |
|Sql|**Ctrl+3**| 查询设计器.SQL |

### <a name="query-results-context-specific-shortcuts"></a><a name="bkmk_query-results-context-specific-shortcuts"></a> 查询结果：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|查询结果新行|**Alt+End**| SQL.查询结果新行 |
|查询结果刷新|**Shift+Alt+R**| SQL.查询结果刷新 |
|查询结果停止|**Alt+Break**| SQL.查询结果停止 |

### <a name="report-designer-context-specific-shortcuts"></a><a name="bkmk_report-designer-context-specific-shortcuts"></a> 报表设计器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|断行|Enter| 编辑.分行 |
|字符左侧|**向左键**| 编辑.左移字符 |
|字符左侧扩展|**Shift+向左键**| 编辑.向左扩展一个字符 |
|字符右侧|**向右键**| 编辑.右移字符 |
|字符右侧扩展|**Shift+向右键**| 编辑.向右扩展一个字符 |
|“插入”选项卡|Tab| 编辑.插入制表符 |
|向下移动一行|向下键| 编辑.向下移动一行 |
|行 - 向下扩展|**Shift+向下键**| 编辑.向下扩展一行 |
|向上移动一行|向上键| 编辑.向上移动一行 |
|行 - 向上扩展|**Shift+向上键**| 编辑.向上扩展一行 |
|向下移动控件|**Ctrl+向下键**| 编辑.下移控件 |
|向左移动控件|**Ctrl+向左键**| 编辑.左移控件 |
|向右移动控件|**Ctrl+向右键**| 编辑.右移控件 |
|向上移动控件|**Ctrl+向上键**| 编辑.上移控件 |
|取消选择|**Esc**| 编辑.取消选定 |
|向下调整控件大小|**Ctrl+Shift+向下键**| 编辑.向下调大控件大小 |
|向左调整控件大小|**Ctrl+Shift+向左键**| 编辑.向左调整控件大小 |
|向右调整控件大小|**Ctrl+Shift+向右键**| 编辑.向右调整控件大小 |
|向上调整控件大小|**Ctrl+Shift+向上键**| 编辑.向上调整控件大小 |
|选项卡左侧|**Shift+Tab**| 编辑.左缩进 |
|数据源|**Ctrl+Alt+D**| 视图.报告数据 |

### <a name="sequence-diagram-context-specific-shortcuts"></a><a name="bkmk_sequence-diagram-context-specific-shortcuts"></a> 序列图：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|导航到代码|**F12**| 体系结构设计器.序列.导航到代码 |
|删除|**Shift+Del**| 编辑.删除 |

### <a name="settings-designer-context-specific-shortcuts"></a><a name="bkmk_settings-designer-context-specific-shortcuts"></a> 设置设计器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|编辑单元格|F2| 编辑.编辑单元格 |
|删除行|**Ctrl+Delete**| 编辑.移除行 |
|取消选择|**Esc**| 编辑.取消选定 |
|查看代码|**F7**| 视图.查看代码 |

### <a name="solution-explorer-context-specific-shortcuts"></a><a name="bkmk_solution-explorer-context-specific-shortcuts"></a> 解决方案资源管理器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|在页面检查器中查看|**Ctrl+K、Ctrl+G**| 类视图上下文菜单.类视图项目.查看.在 Page Inspector 中查看 |

### <a name="team-explorer-context-specific-shortcuts"></a><a name="bkmk_team-explorer-context-specific-shortcuts"></a> 团队资源管理器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|删除|**删除**| 编辑.删除 |
|重命名|F2| 文件.重命名 |
|转到团队资源管理器导航|**Alt+Home**| Team Foundation 上下文菜单.命令.转到团队资源管理器导航 |
|转到团队资源管理器下一节内容|**Alt+向下键**| Team Foundation 上下文菜单.命令.转到团队资源管理器下一节内容 |
|转到团队资源管理器页内容|**Alt+0**（数字“0”）| Team Foundation 上下文菜单.命令.转到团队资源管理器页面内容 |
|转到团队资源管理器上一节内容|**Alt+向上键**| Team Foundation 上下文菜单.命令.转到团队资源管理器上一节内容 |
|转到团队资源管理器第 1 节内容|**Alt+1**| Team Foundation 上下文菜单.命令.转到团队资源管理器第 1 节内容 |
|转到团队资源管理器第 2 节内容|**Alt+2**| Team Foundation 上下文菜单.命令.转到团队资源管理器第 2 节内容 |
|转到团队资源管理器第 3 节内容|**Alt+3**| Team Foundation 上下文菜单.命令.转到团队资源管理器第 3 节内容 |
|转到团队资源管理器第 4 节内容|**Alt+4**| Team Foundation 上下文菜单.命令.转到团队资源管理器第 4 节内容 |
|转到团队资源管理器第 5 节内容|**Alt+5**| Team Foundation 上下文菜单.命令.转到团队资源管理器第 5 节内容 |
|转到团队资源管理器第 6 节内容|**Alt+6**| Team Foundation 上下文菜单.命令.转到团队资源管理器第 6 节内容 |
|转到团队资源管理器第 7 节内容|**Alt+7**| Team Foundation 上下文菜单.命令.转到团队资源管理器第 7 节内容 |
|转到团队资源管理器第 8 节内容|**Alt+8**| Team Foundation 上下文菜单.命令.转到团队资源管理器第 8 节内容 |
|转到团队资源管理器第 9 节内容|**Alt+9**| Team Foundation 上下文菜单.命令.转到团队资源管理器第 9 节内容 |
|团队资源管理器向后导航|**Alt+向左键**| Team Foundation 上下文菜单.命令.团队资源管理器向后定位 |
|团队资源管理器向前导航|**Alt+向右键**| Team Foundation 上下文菜单.命令.团队资源管理器向前定位 |
|TFS 上下文我的工作页 - 创建副本 wi|**Shift+Alt+C**| Team Foundation 上下文菜单.我的工作页正在进行.Tfs 上下文我的工作页创建副本 WI |
|TFS 上下文我的工作页 - 新建已链接 wi|**Shift+Alt+L**| Team Foundation 上下文菜单.我的工作页正在进行.Tfs 上下文我的工作页新建链接 WI |
|刷新|**F5**| 视图.刷新 |

### <a name="test-explorer-context-specific-shortcuts"></a><a name="bkmk_test-explorer-context-specific-shortcuts"></a> 测试资源管理器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|打开测试|**F12**| 测试资源管理器.打开测试 |

### <a name="text-editor-context-specific-shortcuts"></a><a name="bkmk_text-editor-context-specific-shortcuts"></a> 文本编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


| 命令 | 键盘快捷键 |命令 ID|
|-|-|-|
|断行| Enter<br /><br /> or<br /><br /> **Shift+Enter** | 编辑.分行 |
|字符左侧| **向左键** | 编辑.左移字符 |
|字符左侧扩展| **Shift+向左键** | 编辑.向左扩展一个字符 |
|字符左侧扩展列| **Shift+Alt+向左键** | 编辑.向左扩展一个字符列 |
|字符右侧| **向右键** | 编辑.右移字符 |
|字符右侧扩展| **Shift+向右键** | 编辑.向右扩展一个字符 |
|字符右侧扩展列| **Shift+Alt+向右键** | 编辑.向右扩展一个字符列 |
|清除书签| **Ctrl+K、Ctrl+L** | 编辑.清除书签 |
|折叠所有大纲显示| **Ctrl+M、Ctrl+A** | 编辑.折叠所有大纲显示 |
|折叠当前区域| **Ctrl+M、Ctrl+S** | 编辑.折叠当前区域 |
|折叠标记| **Ctrl+M、Ctrl+T** | 编辑.折叠标记 |
|折叠到定义| **Ctrl+M、Ctrl+O**（字母“O”） | Edit.CollapseToDefinitions |
|合拢选定内容| **Shift+Alt+-** | Edit.ContractSelection |
|注释选定内容| **Ctrl+K、Ctrl+C** | 编辑.注释选定内容 |
|完成单词| **Ctrl+空格键**<br /><br /> or<br /><br /> **Alt+向右键** | 编辑.完成单词 |
|复制参数提示| **Ctrl+Shift+Alt+C** | 编辑.复制参数提示 |
|降低筛选器级别| **Alt+,** | 编辑.减少筛选器级别 |
|向后删除| Backspace<br /><br /> or<br /><br /> **Shift+Bkspce** | 编辑.向后删除 |
|删除水平空白| **Ctrl+K、Ctrl+\\** | 编辑.删除水平空白 |
|文档结尾| **Ctrl+End** | 编辑.文档结尾 |
|文档结尾扩展| **Ctrl+Shift+End** | 编辑.文档结尾扩展 |
|文档开头| **Ctrl+Home** | 编辑.文档开始 |
|文档开头扩展| **Ctrl+Shift+Home** | 编辑.文档开始扩展 |
|展开所有大纲显示| **Ctrl+M、Ctrl+X** | 编辑.展开所有大纲显示 |
|展开当前区域| **Ctrl+M、Ctrl+E** | 编辑.展开当前区域 |
|展开所选内容| **Shift+Alt+=** | Edit.ExpandSelection |
|扩展选定内容至包含块| **Shift+Alt+]** | Edit.ExpandSelectiontoContainingBlock |
|设置文档格式| **Ctrl+K、Ctrl+D** | 编辑.编排文档格式 |
|设置选定内容的格式| **Ctrl+K、Ctrl+F** | 编辑.格式化选定内容 |
|转到全部| **Ctrl+T**<br /><br /> or<br /><br /> **Ctrl+,** | 编辑.转到全部 |
|转到大括号| **Ctrl+]** | 编辑.转到大括号 |
|转到大括号扩展| **Ctrl+Shift+]** | 编辑.扩展转到大括号 |
|转到最近| **Ctrl+T、R** | 编辑.转到当前 |
|转到文件中的下一个问题| **Alt+PgDn** | 编辑.转到文件中的下一个问题 |
|转到文件中的上一个问题| **Alt+PgUp** | Edit.GotoPreviousIssueinFile |
|隐藏选定内容| **Ctrl+M、Ctrl+H** | 编辑.隐藏选定内容 |
|提高筛选器级别| **Alt+.** | 编辑.增加筛选器级别 |
|渐进式搜索| **Ctrl+I** | 编辑.渐进式搜索 |
|在所有匹配位置插入插入点| **Shift+Alt+;** | 编辑.插入所有匹配的 Caretsat |
|插入下一个匹配的插入点| **Shift+Alt+.** | 编辑.插入下一个匹配的 Caret |
|“插入”选项卡| Tab | 编辑.插入制表符 |
|行 - 剪切| **Ctrl+L** | 编辑.剪切行 |
|行 - 删除| **Ctrl+Shift+L** | 编辑.删除行 |
|向下移动一行| 向下键 | 编辑.向下移动一行 |
|行 - 向下扩展| **Shift+向下键** | 编辑.向下扩展一行 |
|行 - 向下扩展列| **Shift+Alt+向下键** | 编辑.向下扩展列 |
|行 - 结尾| **End** | 编辑.行尾 |
|行 - 结尾扩展| **Shift+End** | 编辑.扩展到行尾 |
|行 - 结尾扩展列| **Shift+Alt+End** | 编辑.行尾扩展列 |
|行 - 打开上面的内容| **Ctrl+Enter** | 编辑.上开新行 |
|行 - 打开下面的内容| **Ctrl+Shift+Enter** | 编辑.下开新行 |
|行 - 开头| **Home** | 编辑.行首 |
|行 - 开头扩展| **Shift+Home** | 编辑.扩展到行首 |
|行 - 开头扩展列| **Shift+Alt+Home** | 编辑.行首扩展列 |
|行 - 转置| **Shift+Alt+T** | 编辑.行转置 |
|向上移动一行| 向上键 | 编辑.向上移动一行 |
|行 - 向上扩展| **Shift+向上键** | 编辑.向上扩展一行 |
|行 - 向上扩展列| **Shift+Alt+向上键** | 编辑.向上扩展列 |
|列出成员| **Ctrl+J** | 编辑.列出成员 |
|转换为小写| **Ctrl+U** | 编辑.转换为小写 |
|转换为大写| **Ctrl+Shift+U** | 编辑.转换为大写 |
|将选定行下移| **Alt+向下键** | 编辑.将选定行下移 |
|将选定行上移| **Alt+向上键** | 编辑.将选定行上移 |
|下一个突出显示的引用| **Ctrl+Shift+向下键** | 编辑.下一个突出显示的引用 |
|改写模式| 插入 | 编辑.改写模式 |
|向下翻页| **PgDn** | 编辑.向下翻页 |
|页向下扩展| **Shift+PgDn** | 编辑.向下扩展一页 |
|向上翻页| **PgUp** | 编辑.向上翻页 |
|页向上扩展| **Shift+PgUp** | 编辑.向上扩展一页 |
|参数信息| **Ctrl+Shift+空格键** | 编辑.参数信息 |
|粘贴参数提示| **Ctrl+Shift+Alt+P** | 编辑.粘贴参数提示 |
|向后速览| **Ctrl+Alt+-** | 编辑.向后查看 |
|查看定义| **Alt+F12** | 编辑.查看定义 |
|向前速览| **Ctrl+Alt+=** | 编辑.向前查看 |
|上一个突出显示的引用| **Ctrl+Shift+向上键** | 编辑.上一个突出显示的引用 |
|快速信息| **Ctrl+K、Ctrl+I** | 编辑.快速信息 |
|反向渐进式搜索| **Ctrl+Shift+I** | 编辑.反向渐进式搜索 |
|向下滚动一行| **Ctrl+向下键** | 编辑.向下滚动一行 |
|向上滚动一行| **Ctrl+向上键** | 编辑.向上滚动一行 |
|选择当前字词| **Ctrl+W** | 编辑.选择当前字 |
|取消选择| **Esc 键** | 编辑.取消选定 |
|选择最后返回| **Ctrl+=** | 编辑.选择到最后一个返回 |
|显示代码透镜菜单| **Ctrl+K、Ctrl+\`** | 编辑.显示 CodeLens 菜单 |
|显示导航菜单| **Alt+\`** | 编辑.显示导航菜单 |
|停止隐藏当前内容| **Ctrl+M、Ctrl+U** | 编辑.停止隐藏当前区域 |
|停止大纲显示| **Ctrl+M、Ctrl+P** | 编辑.停止大纲显示 |
|交换定位点| **Ctrl+K、Ctrl+A** | 编辑.交换定位点 |
|选项卡左侧| **Shift+Tab** | 编辑.左缩进 |
|切换所有大纲显示| **Ctrl+M、Ctrl+L** | 编辑.切换所有大纲显示 |
|切换书签| **Ctrl+K、Ctrl+K** | 编辑.切换书签 |
|切换完成模式| **Ctrl+Alt+空格键** | Edit.ToggleCompletionMode |
|切换大纲显示展开| **Ctrl+M、Ctrl+M** | 编辑.切换大纲显示展开 |
|切换任务列表快捷方式| **Ctrl+K、Ctrl+H** | 编辑.切换任务列表快捷方式 |
|切换自动换行| **Ctrl+E、Ctrl+W** | 编辑.切换自动换行 |
|取消注释选定内容| **Ctrl+K、Ctrl+U** | 编辑.取消注释选定内容 |
|查看底部| **Ctrl+PgDn** | 编辑.视图底部 |
|查看底部扩展| **Ctrl+Shift+PgDn** | 编辑.扩展到视图底部 |
|查看顶部| **Ctrl+PgUp** | 编辑.视图顶部 |
|查看顶部扩展| **Ctrl+Shift+PgUp** | 编辑.扩展到视图顶部 |
|查看空白| **Ctrl+R、Ctrl+W** | 编辑.查看空白 |
|字词 - 删除至结尾| **Ctrl+Delete** | 编辑.字删除直至结尾处 |
|字词 - 删除至开头| **Ctrl+Backspace** | 编辑.字删除直至开始处 |
|字词 - 下一个| **Ctrl+向右键** | 编辑.下一字 |
|字词 - 下一个扩展| **Ctrl+Shift+向右键** | 编辑.扩展到下一字 |
|字词 - 下一个扩展列| **Ctrl+Shift+Alt+向右键** | 编辑.向后扩展一个字列 |
|字词 - 上一个| **Ctrl+向左键** | 编辑.上一字 |
|字词 - 上一个扩展| **Ctrl+Shift+向左键** | 编辑.扩展到上一字 |
|字词 - 上一个扩展列| **Ctrl+Shift+Alt+向左键** | 编辑.向前扩展一个字列 |
|字词 - 转置| **Ctrl+Shift+T** | 编辑.字转置 |
|交互执行| **Alt+Enter** | 编辑器上下文菜单.代码窗口.交互执行 |
|交互执行行| **Alt+'** | 编辑器上下文菜单.代码窗口.交互执行行 |
|在页面检查器中查看| **Ctrl+K、Ctrl+G** | 其他上下文菜单.HTML 上下文.在 Page Inspector 中查看 |
|TFS 批注 - 移动下一个区域| **Alt+PgDn** | Team Foundation 上下文菜单.批注.Tfs 批注移动下一个区域 |
|TFS 批注 - 移动上一个区域| **Alt+PgUp** | Team Foundation 上下文菜单.批注.Tfs 批注移动上一个区域 |

### <a name="uml-activity-diagram-context-specific-shortcuts"></a><a name="bkmk_uml-activity-diagram-context-specific-shortcuts"></a> UML 活动图：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|删除|**Shift+Del**| 编辑.删除 |

### <a name="uml-class-diagram-context-specific-shortcuts"></a><a name="bkmk_uml-class-diagram-context-specific-shortcuts"></a> UML 类图：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|从模型中删除|**Shift+Del**| 编辑.从模型中删除 |

### <a name="uml-component-diagram-context-specific-shortcuts"></a><a name="bkmk_uml-component-diagram-context-specific-shortcuts"></a> UML 组件图：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|从模型中删除|**Shift+Del**| 编辑.从模型中删除 |

### <a name="uml-use-case-diagram-context-specific-shortcuts"></a><a name="bkmk_uml-use-case-diagram-context-specific-shortcuts"></a> UML 用例图：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|从模型中删除|**Shift+Del**| 编辑.从模型中删除 |

### <a name="vc-accelerator-editor-context-specific-shortcuts"></a><a name="bkmk_vc-accelerator-editor-context-specific-shortcuts"></a> VC 快捷方式编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|新建加速器|插入| 编辑.新建快捷键 |
|键入的下一个密钥|**Ctrl+W**| 编辑.键入的下一个键 |

### <a name="vc-dialog-editor-context-specific-shortcuts"></a><a name="bkmk_vc-dialog-editor-context-specific-shortcuts"></a> VC 对话框编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|向下移动控件|向下键| 编辑.下移控件 |
|向左移动控件|**向左键**| 编辑.左移控件 |
|向右移动控件|**向右键**| 编辑.右移控件 |
|向上移动控件|向上键| 编辑.上移控件 |
|向左滚动列|**Ctrl+向左键**| 编辑.向左滚动一列 |
|向右滚动列|**Ctrl+向右键**| 编辑.向右滚动一列 |
|向下滚动一行|**Ctrl+向下键**| 编辑.向下滚动一行 |
|向上滚动一行|**Ctrl+向上键**| 编辑.向上滚动一行 |
|向下调整控件大小|**Shift+向下键**| 编辑.向下调大控件大小 |
|向左调整控件大小|**Shift+向左键**| 编辑.向左调整控件大小 |
|向右调整控件大小|**Shift+向右键**| 编辑.向右调整控件大小 |
|向上调整控件大小|**Shift+向上键**| 编辑.向上调整控件大小 |
|底部对齐|**Ctrl+Shift+向下键**| 格式.底部对齐 |
|居中对齐|**Shift+F9**| 格式.居中对齐 |
|左对齐|**Ctrl+Shift+向左键**| 格式.左对齐 |
|中间对齐|**F9**| 格式.中间对齐 |
|右对齐|**Ctrl+Shift+向右键**| 格式.右对齐 |
|顶部对齐|**Ctrl+Shift+向上键**| 格式.顶部对齐 |
|底部按钮|**Ctrl+B**| 格式.按钮下 |
|右侧按钮|**Ctrl+R**| 格式.按钮右 |
|水平居中|**Ctrl+Shift+F9**| 格式.水平居中 |
|垂直居中|**Ctrl+F9**| 格式.垂直居中 |
|检查助记键|**Ctrl+M**| 格式.检查助记键 |
|按内容调整大小|**Shift+F7**| 格式.按内容调整大小 |
|横向间隔|**Alt+向右键**<br /><br /> or<br /><br /> **Alt+向左键**| 格式.横向间隔 |
|纵向间隔|**Alt+向上键**<br /><br /> or<br /><br /> **Alt+向下键**| 格式.纵向间隔 |
|Tab 键顺序|**Ctrl+D**| 格式.Tab 键顺序 |
|测试对话框|**Ctrl+T**| 格式.测试对话框 |
|切换参考线|**Ctrl+G**| 格式.切换辅助线 |

### <a name="vc-image-editor-context-specific-shortcuts"></a><a name="bkmk_vc-image-editor-context-specific-shortcuts"></a> VC 图像编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|喷枪工具|**Ctrl+A**| 图像.喷枪工具 |
|画笔工具|**Ctrl+B**| 图像.画笔工具 |
|复制和边框选择|**Ctrl+Shift+U**| 图像.复制选定内容并绘制其轮廓 |
|不透明处理|**Ctrl+J**| 图像.不透明处理 |
|椭圆工具|**Alt+P**| 图像.椭圆工具 |
|擦除工具|**Ctrl+Shift+I**| 图像.清除工具 |
|实心椭圆工具|**Ctrl+Shift+Alt+P**| 图像.实心椭圆工具 |
|实心矩形工具|**Ctrl+Shift+Alt+R**| 图像.实心矩形工具 |
|实心圆角矩形工具|**Ctrl+Shift+Alt+W**| 图像.实心圆角矩形工具 |
|填充工具|**Ctrl+F**| 图像.填充工具 |
|水平翻转|**Ctrl+H**| 图像.水平翻转 |
|垂直翻转|**Shift+Alt+H**| 图像.垂直翻转 |
|较大画笔|**Ctrl+=**| 图像.较大画笔 |
|画线工具|**Ctrl+L**| 图像.直线工具 |
|放大工具|**Ctrl+M**| 图像.放大工具 |
|放大|**Ctrl+Shift+M**| 图像.放大 |
|新图像类型|插入| 图像.新建图像类型 |
|下一种颜色|**Ctrl+]**<br /><br /> or<br /><br /> **Ctrl+向右键**| 图像.下一种颜色 |
|右侧下一种颜色|**Ctrl+Shift+]**<br /><br /> or<br /><br /> **Ctrl+Shift+向右键**| Image.NextRightColor |
|空心椭圆工具|**Shift+Alt+P**| 图像.空心椭圆工具 |
|空心矩形工具|**Shift+Alt+R**| 图像.空心矩形工具 |
|空心圆角矩形工具|**Shift+Alt+W**| 图像.空心圆角矩形工具 |
|铅笔工具|**Ctrl+I**| 图像.铅笔工具 |
|上一种颜色|**Ctrl+[**<br /><br /> or<br /><br /> **Ctrl+向左键**| 图像.上一种颜色 |
|右侧上一种颜色|**Ctrl+Shift+[**<br /><br /> or<br /><br /> **Ctrl+Shift+向左键**| Image.PreviousRightColor |
|矩形选择工具|**Shift+Alt+S**| 图像.矩形选择工具 |
|矩形工具|**Alt+R**| 图像.矩形工具 |
|旋转 90 度|**Ctrl+Shift+H**| 图像.旋转 90 度 |
|圆角矩形工具|**Alt+W**| 图像.圆角矩形工具 |
|显示网格|**Ctrl+Alt+S**| 图像.网格 |
|显示磁贴网格|**Ctrl+Shift+Alt+S**| 图像.显示平铺网格 |
|小画笔|**Ctrl+.**| 图像.小画笔 |
|较小画笔|**Ctrl+-**| 图像.较小画笔 |
|文本工具|**Ctrl+T**| 图像.文本工具 |
|使用选定内容作为画笔|**Ctrl+U**| 图像.将所选内容用作画笔 |
|放大|**Ctrl+Shift+.**<br /><br /> or<br /><br /> **Ctrl+向上键**| 图像.放大 |
|缩小|**Ctrl+Shift+,**<br /><br /> or<br /><br /> **Ctrl+向下键**| 图像.缩小 |

### <a name="vc-string-editor-context-specific-shortcuts"></a><a name="bkmk_vc-string-editor-context-specific-shortcuts"></a> VC 字符串编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|新字符串|插入| 编辑.新建字符串 |

### <a name="view-designer-context-specific-shortcuts"></a><a name="bkmk_view-designer-context-specific-shortcuts"></a> 视图设计器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|取消检索数据|**Ctrl+T**| 查询设计器.取消检索数据 |
|条件|**Ctrl+2**| 查询设计器.条件 |
|图示|**Ctrl+1**| 查询设计器.关系图 |
|执行 SQL|**Ctrl+R**| 查询设计器.执行SQL |
|转到行|**Ctrl+G**| 查询设计器.转到行 |
|联接模式|**Ctrl+Shift+J**| 查询设计器.联接模式 |
|结果|**Ctrl+4**| 查询设计器.结果 |
|Sql|**Ctrl+3**| 查询设计器.SQL |

### <a name="visual-studio-context-specific-shortcuts"></a><a name="bkmk_visual-studio-context-specific-shortcuts"></a> Visual Studio：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|隐藏方法窗格|**Ctrl+1**| 其他上下文菜单.或设计器上下文.隐藏方法窗格 |

### <a name="windows-forms-designer-context-specific-shortcuts"></a><a name="bkmk_windows-forms-designer-context-specific-shortcuts"></a> Windows 窗体设计器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|断行|Enter| 编辑.分行 |
|字符左侧|**向左键**| 编辑.左移字符 |
|字符左侧扩展|**Shift+向左键**| 编辑.向左扩展一个字符 |
|字符右侧|**向右键**| 编辑.右移字符 |
|字符右侧扩展|**Shift+向右键**| 编辑.向右扩展一个字符 |
|文档结尾|**End**| 编辑.文档结尾 |
|文档结尾扩展|**Shift+End**| 编辑.文档结尾扩展 |
|文档开头|**Home**| 编辑.文档开始 |
|文档开头扩展|**Shift+Home**| 编辑.文档开始扩展 |
|“插入”选项卡|Tab| 编辑.插入制表符 |
|向下移动一行|向下键| 编辑.向下移动一行 |
|行 - 向下扩展|**Shift+向上键**| 编辑.向下扩展一行 |
|向上移动一行|向上键| 编辑.向上移动一行 |
|行 - 向上扩展|**Shift+向下键**| 编辑.向上扩展一行 |
|向下移动控件|**Ctrl+向下键**| 编辑.下移控件 |
|向左移动控件|**Ctrl+向左键**| 编辑.左移控件 |
|向右移动控件|**Ctrl+向右键**| 编辑.右移控件 |
|向上移动控件|**Ctrl+向上键**| 编辑.上移控件 |
|取消选择|**Esc 键**| 编辑.取消选定 |
|向下调整控件大小|**Ctrl+Shift+向下键**| 编辑.向下调大控件大小 |
|向左调整控件大小|**Ctrl+Shift+向左键**| 编辑.向左调整控件大小 |
|向右调整控件大小|**Ctrl+Shift+向右键**| 编辑.向右调整控件大小 |
|向上调整控件大小|**Ctrl+Shift+向上键**| 编辑.向上调整控件大小 |
|选项卡左侧|**Shift+Tab**| 编辑.左缩进 |

### <a name="work-item-editor-context-specific-shortcuts"></a><a name="bkmk_work-item-editor-context-specific-shortcuts"></a> 工作项编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|创建工作项的副本|**Shift+Alt+C**| 编辑.创建工作项的副本 |
|刷新工作项|**F5**| 编辑.刷新工作项 |
|新链接的工作项|**Shift+Alt+L**| 团队.新建链接工作项 |

### <a name="work-item-query-view-context-specific-shortcuts"></a><a name="bkmk_work-item-query-view-context-specific-shortcuts"></a> 工作项查询视图：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|创建工作项的副本|**Shift+Alt+C**| 编辑.创建工作项的副本 |
|缩进|**Shift+Alt+向右键**| 编辑.缩进 |
|升级|**Shift+Alt+向左键**| 编辑.升级 |
|新链接的工作项|**Shift+Alt+L**| 团队.新建链接工作项 |
|刷新|**F5**| 团队.刷新 |
|切换|**Shift+Alt+V**| 窗口.切换 |

### <a name="work-item-results-view-context-specific-shortcuts"></a><a name="bkmk_work-item-results-view-context-specific-shortcuts"></a> 工作项结果视图：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|创建工作项的副本|**Shift+Alt+C**| 编辑.创建工作项的副本 |
|缩进|**Shift+Alt+向右键**| 编辑.缩进 |
|升级|**Shift+Alt+向左键**| 编辑.升级 |
|转到下一个工作项|**Shift+Alt+N**| 团队.转到下一个工作项 |
|转到上一个工作项|**Shift+Alt+P**| 团队.转到上一个工作项 |
|新链接的工作项|**Shift+Alt+L**| 团队.新建链接工作项 |
|刷新|**F5**| 团队.刷新 |
|切换|**Shift+Alt+V**| 窗口.切换 |

### <a name="workflow-designer-context-specific-shortcuts"></a><a name="bkmk_workflow-designer-context-specific-shortcuts"></a> 工作流设计器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|完成单词|**Ctrl+K、W**<br /><br /> or<br /><br /> **Ctrl+K、Ctrl+W**<br /><br /> or<br /><br /> **Ctrl+空格键**<br /><br /> or<br /><br /> **Alt+向右键**| 编辑.完成单词 |
|降低筛选器级别|**Alt+,**| 编辑.减少筛选器级别 |
|提高筛选器级别|**Alt+.**| 编辑.增加筛选器级别 |
|列出成员|**Ctrl+K、L**<br /><br /> or<br /><br /> **Ctrl+K、Ctrl+L**<br /><br /> or<br /><br /> **Ctrl+J**| 编辑.列出成员 |
|参数信息|**Ctrl+K、P**<br /><br /> or<br /><br /> **Ctrl+K、Ctrl+P**<br /><br /> or<br /><br /> **Ctrl+Shift+空格键**| 编辑.参数信息 |
|快速信息|**Ctrl+K、I**<br /><br /> or<br /><br /> **Ctrl+K、Ctrl+I**| 编辑.快速信息 |
|折叠|**Ctrl+E、Ctrl+C**<br /><br /> or<br /><br /> **Ctrl+E、C**| 工作流设计器.折叠 |
|全部折叠|或| 工作流设计器.全部折叠 |
|连接节点|**Ctrl+E、Ctrl+F**<br /><br /> or<br /><br /> **Ctrl+E、F**| 工作流设计器.连接节点 |
|创建变量|**Ctrl+E、Ctrl+N**<br /><br /> or<br /><br /> **Ctrl+E、N**| 工作流设计器.创建变量 |
|全部展开|**Ctrl+E、Ctrl+X**<br /><br /> or<br /><br /> **Ctrl+E、X**| 工作流设计器.全部展开 |
|就地展开|**Ctrl+E、Ctrl+E**<br /><br /> or<br /><br /> **Ctrl+E、E**| 工作流设计器.就地展开 |
|转到父级|**Ctrl+E、Ctrl+P**<br /><br /> or<br /><br /> **Ctrl+E、P**| 工作流设计器.转到父级 |
|移动焦点|**Ctrl+E、Ctrl+M**<br /><br /> or<br /><br /> **Ctrl+E、M**| 工作流设计器.移动焦点 |
|在设计器中导航|**Ctrl+Alt+F6**| 工作流设计器.在设计器中导航 |
|还原|**Ctrl+E、Ctrl+R**<br /><br /> or<br /><br /> **Ctrl+E、R**| 工作流设计器.还原 |
|显示/隐藏参数设计器|**Ctrl+E、Ctrl+A**<br /><br /> or<br /><br /> **Ctrl+E、A**| 工作流设计器.显示隐藏参数设计器 |
|显示/隐藏导入设计器|**Ctrl+E、Ctrl+I**<br /><br /> or<br /><br /> **Ctrl+E、I**| 工作流设计器.显示隐藏导入设计器 |
|显示/隐藏摘要图|**Ctrl+E、Ctrl+O**（字母“O”）<br /><br /> or<br /><br /> **Ctrl+E、O**| 工作流设计器.显示隐藏摘要图 |
|显示/隐藏变量设计器|**Ctrl+E、Ctrl+V**<br /><br /> or<br /><br /> **Ctrl+E、V**| 工作流设计器.显示隐藏变量设计器 |
|切换选定内容|**Ctrl+E、Ctrl+S**<br /><br /> or<br /><br /> **Ctrl+E、S**| 工作流设计器.切换选择 |
|放大|**Ctrl+Num +**| 工作流设计器.放大 |
|缩小|**Ctrl+Num -**| 工作流设计器.缩小 |

### <a name="xaml-ui-designer-context-specific-shortcuts"></a><a name="bkmk_xaml-ui-designer-context-specific-shortcuts"></a> XAML UI 设计器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|适应全部|**Ctrl+0**（数字“0”）| 设计.适应全部 |
|显示句柄|**F9**| 设计.显示手柄 |
|放大|**Ctrl+Alt+=**| 设计.放大 |
|缩小|**Ctrl+Alt+-**| 设计.缩小 |
|设计器选项|**Ctrl+Shift+;**|
|编辑文本|F2| 格式.编辑文本 |
|全部|**Ctrl+Shift+R**| 格式.重置布局.全部 |
|运行项目代码|**Ctrl+F9**|
|隐藏（仅限 Blend）|**Ctrl+H**| Timeline.Hide（仅限 Blend） |
|锁定（仅限 Blend）|**Ctrl+L**| Timeline.Lock（仅限 Blend） |
|显示（仅限 Blend）|**Ctrl+Shift+H**| Timeline.Show（仅限 Blend） |
|解除锁定（仅限 Blend）|**Ctrl+Shift+L**| Timeline.Unlock（仅限 Blend） |
|左侧边缘左移|**Ctrl+Shift+,**| 视图.向左移动左边缘 |
|左侧边缘右移|**Ctrl+Shift+.**| 视图.向右移动左边缘 |
|右侧边缘左移|**Ctrl+Shift+Alt+,**| 视图.向左移动右边缘 |
|右侧边缘右移|**Ctrl+Shift+Alt+.**| 视图.向右移动右边缘 |
|显示属性标记菜单|**Ctrl+空格键**| View.ShowPropertyMarkerMenu |

### <a name="xml-text-editor-context-specific-shortcuts"></a><a name="bkmk_xml-text-editor-context-specific-shortcuts"></a> XML（文本）编辑器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|启动 XSLT（调试）|**Alt+F5**| XML.启动 XSLT (调试) |
|启动 XSLT（不调试）|**Ctrl+Alt+F5**| XML.启动 XSLT (不调试) |

### <a name="xml-schema-designer-context-specific-shortcuts"></a><a name="bkmk_xml-schema-designer-context-specific-shortcuts"></a> XML 架构设计器：特定于上下文的快捷方式

特定于此上下文的快捷方式如下：


|命令|键盘快捷键|命令 ID|
|-|-|-|
|从下到上|**Alt+向上键**| 关系图视图.从下到上 |
|从左到右|**Alt+向右键**| 关系图视图.从左到右 |
|从右到左|**Alt+向左键**| 关系图视图.从右到左 |
|从上到下|**Alt+向下键**| 关系图视图.从上到下 |
|从工作区中删除|**删除**| 其他上下文菜单.图形视图.从工作区中删除 |
|显示内容模型视图|**Ctrl+2**| Xsd 设计器.显示内容模型视图 |
|显示图形视图|**Ctrl+3**| Xsd 设计器.显示图形视图 |
|显示起始视图|**Ctrl+1**| Xsd 设计器.显示起始视图 |

