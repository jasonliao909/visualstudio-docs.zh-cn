---
title: Spy++ 简介 | Microsoft Docs
description: 了解 Spy++ 调试工具。 显示系统对象关系的图形树。 获取所选窗口、线程、进程或消息的属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Spy++
ms.assetid: 733b514b-63a9-402d-89aa-4f0416766655
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 6ab19d666bf02d1c9c9d764ed1c18d097a3f8935
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122138908"
---
# <a name="introducing-spy"></a>Spy++ 简介
可利用 Spy++ 执行以下任务：

- 显示系统对象之间关系的图形树。 这些对象包括 [进程](../debugger/processes-view.md)、 [线程](../debugger/threads-view.md)和 [窗口](../debugger/windows-view.md)。

- 搜索指定 [窗口](../debugger/how-to-search-for-a-window-in-windows-view.md)、 [线程](../debugger/how-to-search-for-a-thread-in-threads-view.md)、 [进程](../debugger/how-to-search-for-a-process-in-processes-view.md)或 [消息](../debugger/how-to-search-for-a-message-in-messages-view.md)。

- 查看所选 [窗口](../debugger/how-to-display-window-properties.md)、 [线程](../debugger/how-to-display-thread-properties.md)、 [进程](../debugger/how-to-display-process-properties.md)或 [消息](../debugger/how-to-display-message-properties.md)的属性。

- 直接从视图中选择窗口、线程、进程或消息。

- 使用 [查找程序工具](../debugger/how-to-use-the-finder-tool.md) ，通过鼠标指针定位选择窗口。

- 使用复杂消息日志选择参数设置[消息选项](../debugger/how-to-open-messages-view-from-find-window.md)。

  Spy++ 拥有工具栏和超链接，可以帮助你更快地工作。 它还提供用于更新活动视图的“刷新”  命令、方便监视的“窗口查找程序工具”  和用于自定义视图窗口的“字体”  对话框。 此外，Spy++ 还可以保存和还原用户首选项。

  在各个 Spy++ 窗口中，可以单击鼠标右键以显示常用命令的快捷菜单。 显示的命令取决于指针所在的位置。 例如，如果在窗口视图中右键单击某个条目，且所选窗口可见，那么单击快捷方式菜单上的“突出显示”  可使所选窗口边框闪烁，以便你能更轻松地找到该窗口。

> [!NOTE]
> 还存在其他两种类似于 Spy++ 的实用工具：用于显示进程和线程详细信息的 PView 和支持监视动态数据交换 (DDE) 消息的 DDESPY.EXE。

## <a name="64-bit-operating-systems"></a>64 位操作系统
 Spy++ 有两个版本。 第一个版本，名为 Spy++ (spyxx.exe)，用于显示发送到在 32 位进程中运行的窗口的消息。 例如，在 32 位进程中运行的 Visual Studio。 因此，可以使用 Spy++ 来显示发送到“解决方案资源管理器” 中的消息。 由于 Visual Studio 中大多数生成的默认配置都是在 32 位进程中运行的，因此如果[已安装所需组件](../debugger/how-to-start-spy-increment.md)，则第一个版本的 Spy++ 就是在 Visual Studio 中的“工具”菜单上可用的那一个。

 第二个版本，名为 Spy++（64 位）(spyxx_amd64.exe)，用于显示发送到在 64 位进程中运行的窗口的消息。 例如，在 64 位操作系统上，记事本在 64 位进程中运行。 因此，可以使用 Spy++（64 位）来显示发送到记事本的消息。 Spy++ （64 位）通常位于

 ..\\*Visual Studio 安装文件夹*\Common7\Tools\spyxx_amd64.exe。

 可以直接从命令行运行任一版本的 Spy++。

> [!NOTE]
> 虽然 Spy++（64 位）文件名包含 "amd"，但它可在任何 x64 Windows 操作系统中运行。

## <a name="see-also"></a>请参阅
- [如何：启动 Spy++](../debugger/how-to-start-spy-increment.md)
- [使用 Spy++](../debugger/using-spy-increment.md)
- [Spy++ 视图](../debugger/spy-increment-views.md)
- [Spy++ 参考](../debugger/spy-increment-reference.md)