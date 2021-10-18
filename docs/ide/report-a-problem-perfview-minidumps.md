---
description: PerfView 是一个基于 Windows 事件跟踪创建 ETL（事件跟踪日志）文件的工具，可用于排查 Visual Studio 存在的某些类型的问题。
title: 使用 PerfView 收集 ETL 跟踪，以及创建用于所有调用堆栈的小型转储
ms.date: 10/12/2021
ms.topic: how-to
helpviewer_keywords:
- perfview
- ETL Trace
- minidumps for Visual Studio issues"
author: corob-msft
ms.author: corob
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.description: Collect ETL traces using perfview.exe and create minidumps to send to Microsoft, for troubleshooting issues with Visual Studio
ms.openlocfilehash: 45260d0e265f1c1104dad872528a7489994964da
ms.sourcegitcommit: 72f8ce4992cc62c4833e6dcb0f79febb328c44be
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2021
ms.locfileid: "130010647"
---
# <a name="collect-an-etl-trace-with-perfview-and-create-minidumps-with-all-call-stacks"></a>使用 PerfView 收集 ETL 跟踪，以及创建用于所有调用堆栈的小型转储

当你报告 Visual Studio 的问题时，Microsoft 产品团队可能会请求提供 ETL 跟踪或小型转储以收集其他信息进行故障排除。 使用以下步骤收集 ETL 跟踪或创建用于所有调用堆栈的小型转储。

## <a name="collect-an-etl-trace-with-perfview"></a>使用 PerfView 收集 ETL 跟踪

PerfView 是一个基于 [Windows 事件跟踪](/windows/desktop/ETW/event-tracing-portal)创建 ETL（事件跟踪日志）文件的工具，可用于排查 Visual Studio 存在的某些问题类型。 有时，当你报告问题时，产品团队可能会要求你运行 PerfView 以收集其他信息。

### <a name="install-perfview"></a>安装 PerfView

从 [GitHub](https://github.com/Microsoft/perfview/blob/master/documentation/Downloading.md) 下载 PerfView。

### <a name="run-perfview"></a>运行 PerfView

1. 以管理员身份在 Windows 资源管理器中右键单击“PerfView.exe”，然后选择“以管理员身份运行” 。
1. 在“收集”菜单上，选择“收集”。
1. 勾选“压缩”、“合并”和“线程时间”。
1. 将“循环 MB”增加到 1000。
1. 如果要多次收集，请更改“当前目录”以将 ETL 跟踪保存到指定文件夹和数据文件中。
1. 要开始记录数据，请选择“开始收集”按钮。
1. 要停止记录数据，请选择“停止收集”按钮。 PrefView.etl.zip 文件将被保存在指定的目录。

PerfView 只能存储适合其缓冲区的最新数据。 因此，尝试在 Visual Studio 开始冻结或减速后尽快停止收集。 遇到问题后不要收集超过 30 秒。

有关更多信息，请参阅 [Channel9 上的 PerfView 教程](https://channel9.msdn.com/Series/PerfView-Tutorial/PerfView-Tutorial-1-Collecting-data-with-the-Run-command)。

## <a name="create-minidumps-for-a-visual-studio-process-with-all-call-stacks"></a>使用所有调用堆栈为 Visual Studio 进程创建小型转储

在某些情况下，Microsoft 可能会要求提供正在运行的 Visual Studio 进程的小型转储，其中包含所有调用堆栈的信息。 要收集此信息，请执行以下步骤：

### <a name="create-the-minidump-file"></a>创建小型转储文件

1. 启动 Visual Studio 的新实例。
1. 从主菜单中，选择“调试” > “附加到进程”。
1. 勾选相关的“托管”和“本机”复选框，然后按“附加”。

   ![屏幕截图显示“附加到进程”对话框中选中的代码类型。](../ide/media/attach-to-process.png)

1. 从正在运行的进程列表中选择要附加的其他 Visual Studio 实例。
1. 从主菜单中，选择“调试” > “全部中断”。
1. 从主菜单中，选择“调试” > “将转储另存为”。

### <a name="get-the-call-stacks-from-the-minidump"></a>从小型转储中获取调用堆栈

1. 在 Visual Studio 中打开转储文件。
1. 转到“工具” > “选项” > “调试” > “符号”，确保在“符号文件(.pdb) 位置”中勾选“Microsoft 符号服务器”     。
1. 打开“命令”窗口（“视图” > “其他窗口” > “命令窗口”）   。
1. 键入“~*k”。 此窗口会显示所有线程的调用堆栈。
1. 从命令窗口中复制所有文本并保存到文本文件中。
1. 将 txt 文件附加到 bug。
