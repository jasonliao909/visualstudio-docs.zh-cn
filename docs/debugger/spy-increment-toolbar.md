---
title: Spy++ 工具栏 | Microsoft Docs
description: 了解菜单栏下显示的 Spy++ 工具栏中的用户界面元素。 若要显示或隐藏工具栏，请在“视图”菜单上单击“工具栏”。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Spy++ toolbar
ms.assetid: 949c18fb-bb25-42ed-9130-c4a47869f24d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 97c03fe68b810cbd7e907b4020b8487ae5c547f2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641622"
---
# <a name="spy-toolbar"></a>Spy++ 工具栏
工具栏出现在 Spy++ 菜单栏下方。 若要显示或隐藏工具栏，请在“视图”菜单上单击“工具栏”。

 工具栏上提供以下控件。

## <a name="uielement-list"></a>UIElement 列表

|Button|效果|
|------------|------------|
|![Spy++“窗口”按钮](../debugger/media/icon_spy--_windows.gif "Icon_Spy++_Windows")|显示系统中窗口和控件的树状视图。 有关详细信息，请参阅[窗口视图](../debugger/windows-view.md)。|
|![Spy++“进程”按钮](../debugger/media/icon_spy--_processes.gif "Icon_Spy++_Processes")|显示系统中进程的树状视图。 有关详细信息，请参阅[进程视图](../debugger/processes-view.md)。|
|![Spy++“线程”按钮](../debugger/media/icon_spy--_threads.gif "Icon_Spy++_Threads")|显示系统中线程的树状视图。 有关详细信息，请参阅[线程视图](../debugger/threads-view.md)。|
|![Spy++“消息”按钮](../debugger/media/icon_spy--_messages.gif "Icon_Spy++_Messages")|创建一个显示窗口消息的窗口并打开“消息选项”对话框，以便你可以选择要显示其消息的窗口，还可以选择其他选项。 有关详细信息，请参阅[消息视图](../debugger/messages-view.md)。|
|![Spy++“启动日志”按钮](../debugger/media/icon_spy--_startlog.gif "Icon_Spy++_StartLog")|启动消息日志记录并显示消息流。 仅当“消息”窗口为活动窗口时，此控件才可用。 有关详细信息，请参阅[如何：开始和停止消息日志显示](../debugger/how-to-start-and-stop-the-message-log-display.md)。|
|![Spy++“停止日志”按钮](../debugger/media/icon_spy--_stoplog.gif "Icon_Spy++_StopLog")|停止消息日志记录和消息流的显示。 仅当“消息”窗口为活动窗口时，此控件才可用。 有关详细信息，请参阅[如何：开始和停止消息日志显示](../debugger/how-to-start-and-stop-the-message-log-display.md)。|
|![Spy++“日志选项”按钮](../debugger/media/icon_spy--_logoptions.gif "Icon_Spy++_LogOptions")|显示[消息选项](../debugger/message-options-dialog-box.md)对话框。 使用此对话框可以选择要查看的窗口和消息类型。 仅当“消息”窗口为活动窗口时，此控件才可用。|
|![Spy++“清除日志”按钮](../debugger/media/spy--_clearlog.gif "Spy++_ClearLog")|清除活动“消息”窗口的内容。 仅当“消息”窗口为活动窗口时，此控件才可用。|
|![Spy++“查找窗口”按钮](../debugger/media/icon_spy--_findwindow.gif "Icon_Spy++_FindWindow")|打开[查找窗口](../debugger/find-window-dialog-box.md)对话框，你可以在其中设置窗口搜索条件并显示属性或消息。 有关详细信息，请参阅[如何：使用查找程序工具](../debugger/how-to-use-the-finder-tool.md)。|
|![Spy++“查找第一个窗口”按钮](../debugger/media/icon_spy--_window.gif "Icon_Spy++_Window")|在当前视图中搜索匹配的窗口、进程、线程或消息。|
|![Spy++“查找下一个窗口”按钮](../debugger/media/icon_spy--_nextwindow.gif "Icon_Spy++_NextWindow")|在当前视图中搜索下一个匹配的窗口、进程、线程或消息。 仅当存在并非唯一的有效搜索结果时，此控件（以及相关的菜单命令）才可用。 例如，当你在窗口树中使用窗口句柄作为搜索条件时，它会生成唯一的结果，因为窗口树中只有一个具有该句柄的窗口；在这种情况下，“查找下一个”不可用。|
|![Spy++“查找上一个窗口”按钮](../debugger/media/icon_spy--_prevwindow.gif "Icon_Spy++_PrevWindow")|在当前视图中搜索上一个匹配的窗口、进程、线程或消息。 仅当存在并非唯一的有效搜索结果时，此控件（以及相关的菜单命令）才可用。 例如，当你在窗口树中使用窗口句柄作为搜索条件时，它会生成唯一的结果，因为窗口树中只有一个具有该句柄的窗口；在这种情况下，“查找上一个”不可用。|
|![Spy++“属性资源管理器”按钮](../debugger/media/icon_spy--_propexp.gif "Icon_Spy++_PropExp")|显示窗口视图中所选窗口的属性。|
|![Spy++“刷新”按钮](../debugger/media/icon_spy--_refresh.gif "Icon_Spy++_Refresh")|刷新系统视图。|

## <a name="see-also"></a>请参阅
- [使用 Spy++](../debugger/using-spy-increment.md)
- [Spy++ 视图](../debugger/spy-increment-views.md)
- [Spy++ 参考](../debugger/spy-increment-reference.md)