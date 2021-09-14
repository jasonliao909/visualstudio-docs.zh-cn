---
title: 诊断扩展 UI 在Visual Studio|Microsoft Docs
description: Visual Studio扩展可能导致 UI 延迟时通知你。 了解如何诊断扩展代码中导致 UI 延迟的原因。
ms.custom: SEO-VS-2020
ms.date: 01/26/2018
ms.topic: conceptual
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload: multiple
ms.openlocfilehash: 8ddb58405125b53c955324be55ccb5eec93000e4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600773"
---
# <a name="how-to-diagnose-ui-delays-caused-by-extensions"></a>如何：诊断由扩展引起的 UI 延迟

当 UI 无响应时，Visual Studio检查 UI 线程的调用堆栈，从叶开始，向基线程工作。 如果Visual Studio确定调用堆栈帧属于已安装和已启用扩展的一部分的模块，则会显示通知。

![UI 延迟 (无响应) 通知](media/ui-delay-notification-in-vs.png)

通知通知用户 UI 延迟 (，即 UI) 中的无响应可能是来自扩展的代码的结果。 它还为用户提供了禁用该扩展的扩展或未来通知的选项。

本文档介绍如何诊断扩展代码中导致 UI 延迟通知的内容。

> [!NOTE]
> 请勿使用Visual Studio实例来诊断 UI 延迟。 使用实验实例时，UI 延迟通知所需的调用堆栈分析的某些部分会关闭，这意味着可能不会显示 UI 延迟通知。

诊断过程的概述如下：
1. 确定触发器方案。
2. 重启 VS 并启用活动日志记录。
3. 启动 ETW 跟踪。
4. 触发通知以再次显示。
5. 停止 ETW 跟踪。
6. 检查活动日志，获取延迟 ID。
7. 使用步骤 6 中的延迟 ID 分析 ETW 跟踪。

在下列部分中，我们将更详细地介绍这些步骤。

## <a name="identify-the-trigger-scenario"></a>确定触发器方案

若要诊断 UI 延迟，首先需要确定 (哪些操作) 导致Visual Studio通知。 这样，你以后就可以在启用日志记录时触发通知。

## <a name="restart-vs-with-activity-logging-on"></a>使用活动日志记录重启 VS

Visual Studio生成"活动日志"，该日志提供调试问题时有用的信息。 若要在命令行中Visual Studio日志记录，Visual Studio命令行选项 `/log` 打开活动日志记录。 启动Visual Studio后，活动日志将存储在以下位置：

```DOS
%APPDATA%\Microsoft\VisualStudio\<vs_instance_id>\ActivityLog.xml
```

若要详细了解如何查找 VS 实例 ID，请参阅用于检测[和管理实例Visual Studio工具](../install/tools-for-managing-visual-studio-instances.md)。 稍后我们将使用此活动日志来了解有关 UI 延迟和相关通知的信息。

## <a name="starting-etw-tracing"></a>启动 ETW 跟踪

可以使用 [PerfView](https://github.com/Microsoft/perfview/) 收集 ETW 跟踪。 PerfView 提供了一个易于使用的接口，用于收集 ETW 跟踪和分析它。 使用以下命令收集跟踪：

```DOS
Perfview.exe collect C:\trace.etl /BufferSizeMB=1024 -CircularMB:2048 -Merge:true -Providers:*Microsoft-VisualStudio:@StacksEnabled=true -NoV2Rundown /kernelEvents=default+FileIOInit+ContextSwitch+Dispatcher
```

这将启用"Microsoft-VisualStudio"提供程序，该提供程序Visual Studio UI 延迟通知相关事件的提供程序。 它还为 PerfView 可用于生成线程时间堆栈视图的内核提供程序 **指定** 关键字。

## <a name="trigger-the-notification-to-appear-again"></a>触发通知再次显示

PerfView 开始跟踪收集后，可以使用步骤 1 (中的触发器操作序列) 通知再次显示。 显示通知后，可以停止对 PerfView 的跟踪收集，以处理和生成输出跟踪文件。

## <a name="stop-etw-tracing"></a>停止 ETW 跟踪

若要停止跟踪收集，只需使用 PerfView **窗口中的"** 停止收集"按钮。 停止跟踪收集后，PerfView 将自动处理 ETW 事件并生成输出跟踪文件。

## <a name="examine-the-activity-log-to-get-the-delay-id"></a>检查活动日志，获取延迟 ID

如前所述，可以在 *%APPDATA%\Microsoft\VisualStudio \<vs_instance_id>* \ActivityLog.xml。 每次Visual Studio检测到扩展 UI 延迟时，它会将节点写入活动日志，并 `UIDelayNotifications` 作为源。 此节点包含有关 UI 延迟的四条信息：

- UI 延迟 ID，一个顺序编号，用于唯一标识 VS 会话中的 UI 延迟
- 会话 ID，用于唯一标识Visual Studio从开始到关闭的会话
- 是否显示 UI 延迟的通知
- 可能导致 UI 延迟的扩展

```xml
<entry>
  <record>271</record>
  <time>2018/02/03 12:02:52.867</time>
  <type>Information</type>
  <source>UIDelayNotifications</source>
  <description>A UI delay (Delay ID = 0) has been detected. (Session ID=16e49d4b-26c2-4247-ad1c-488edeb185e0; Blamed extension="UIDelayR2"; Notification shown? Yes.)</description>
</entry>
```

> [!NOTE]
> 并非所有 UI 延迟都会导致通知。 因此，应始终检查"显示 **的通知** ？"值，以正确标识正确的 UI 延迟。

在活动日志中找到正确的 UI 延迟后，请记下节点中指定的 UI 延迟 ID。 你将使用 ID 在下一步中查找相应的 ETW 事件。

## <a name="analyze-the-etw-trace"></a>分析 ETW 跟踪

接下来，打开跟踪文件。 为此，可以使用相同的 PerfView 实例，也可以启动新实例，将窗口左上方的当前文件夹路径设置为跟踪文件的位置。

![在 Perfview 中设置文件夹路径](media/perfview-set-path.png)

然后，在左窗格中选择跟踪文件，然后从右键单击或上下文菜单中选择"打开"将其打开。

> [!NOTE]
> 默认情况下，PerfView 输出 Zip 存档。 打开 *trace.zip，* 它会自动解压缩存档并打开跟踪。 可以通过在跟踪收集过程中取消选中 **"Zip"** 框来跳过此操作。 但是，如果计划在不同计算机上传输和使用跟踪，强烈建议不要取消选中 **"Zip"** 框。 如果没有此选项，Ngen 程序集所需的 PDB 将不会随跟踪一起，因此，目标计算机上将不会解析来自 Ngen 程序集的符号。  (请参阅 [此博客文章](https://devblogs.microsoft.com/devops/creating-ngen-pdbs-for-profiling-reports/) ，详细了解 Ngen 程序集的 PDB。) 

PerfView 可能需要几分钟才能处理并打开跟踪。 打开跟踪后，其下会显示各种"视图"的列表。

![PerfView 跟踪摘要视图](media/perfview-summary-view-events-selected.png)

我们将首先使用 **"事件"** 视图来获取 UI 延迟的时间范围：

1. 通过选择 **跟踪下的** 节点，然后从右键单击或上下文菜单中选择"打开"， `Events` 打开"事件"视图。 
2. 在左 `Microsoft-VisualStudio/ExtensionUIUnresponsiveness` 窗格中选择""。
3. 按 Enter

将应用所选内容， `ExtensionUIUnresponsiveness` 并且所有事件都显示在右窗格中。

![在"事件"视图中选择事件](media/perfview-event-selection.png)

右窗格中的每一行对应于 UI 延迟。 该事件包含"延迟 ID"值，该值应匹配步骤 6 中活动日志中的延迟 ID。 由于 在 UI 延迟结束时触发，因此事件 (时间戳) UI 延迟 `ExtensionUIUnresponsiveness` 的结束时间。 事件还包含延迟的持续时间。 我们可以从结束时间戳中减去持续时间，以获取 UI 延迟开始的时间的时间戳。

![计算 UI 延迟时间范围](media/ui-delay-time-range.png)

例如，在上一个屏幕截图中，事件的时间戳为 12，125.679，延迟持续时间为 6，143.085 (毫秒) 。 因此，
* 延迟开始时间为 12，125.679 - 6，143.085 = 5，982.594。
* UI 延迟时间范围为 5，982.594 到 12，125.679。

有了时间范围后，我们可以关闭"事件"视图，然后打开"线程时间"视图 **("** 启动活动) 堆栈"视图。 此视图特别方便，因为阻止 UI 线程的扩展通常只是等待其他线程或 I/O 绑定操作。 因此， **在大多数情况下，CPU** 堆栈视图（即"转到"选项）可能无法捕获线程阻塞的时间，因为它在此期间没有使用 CPU。 线程 **时间堆栈** 通过正确显示阻塞时间来解决此问题。

![PerfView (视图中的 StartStop 活动) 堆栈节点的线程时间](media/perfview-thread-time-with-startstop-activities-stacks.png)

打开" **线程时间堆栈"** 视图时，选择 **devenv** 进程以开始分析。

![UI 延迟分析的线程时间堆栈视图](media/ui-delay-thread-time-stacks.png)

在"线程时间堆栈"视图中，在页面的左上方，可以将时间范围设置为我们在上一步中计算的值，然后按 **Enter，** 以便根据该时间范围调整堆栈。

> [!NOTE]
> 如果跟踪收集是在打开 (后) 启动的，则确定哪个线程是启动Visual Studio线程的 UI。 但是，UI (启动) 线程堆栈上的第一个元素很可能始终是操作系统 DLL (*ntdll.dll* *kernel32.dll*) 后跟 `devenv!?` 和 `msenv!?` 。 此序列可帮助识别 UI 线程。

 ![标识启动线程](media/ui-delay-startup-thread.png)

还可以进一步筛选此视图，只需包含包含包中的模块的堆栈。

* 将 **GroupPats** 设置为空文本，以删除默认情况下添加的任何分组。
* 将 **IncPats** 设置为除现有进程筛选器外，还包括程序集名称的一部分。 在这种情况下，它应为 **devenv;UIDelayR2**。

![在线程时间堆栈视图中设置 GroupPath 和 IncPath](media/perfview-tts-group-path-inc-path.png)

PerfView 在"帮助"菜单下提供了详细的指导，可用于识别代码中的性能瓶颈。 此外，以下链接提供有关如何利用线程Visual Studio API 优化代码的更多信息：

* [https://github.com/Microsoft/vs-threading/blob/master/doc/index.md](https://github.com/Microsoft/vs-threading/blob/master/doc/index.md)
* [https://github.com/Microsoft/vs-threading/blob/master/doc/cookbook_vs.md](https://github.com/Microsoft/vs-threading/blob/master/doc/cookbook_vs.md)

还可以在此处使用新的 Visual Studio 静态分析器 (NuGet包，) 提供有关如何编写高效扩展的最佳实践[](https://www.nuget.org/packages/microsoft.visualstudio.sdk.analyzers)的指导。 请参阅 VS [SDK 分析器和](https://github.com/Microsoft/VSSDK-Analyzers/blob/master/doc/index.md)[线程分析器的列表](https://github.com/Microsoft/vs-threading/blob/master/doc/analyzers/index.md)。

> [!NOTE]
> 如果由于依赖关系而无法解决无响应问题 (例如，如果扩展必须调用 UI 线程) 上的同步 VS 服务，我们希望了解这一点。 如果你是我们的合作伙伴计划Visual Studio，可以通过提交开发人员支持请求联系我们。 否则，请使用"报告问题"工具提交反馈，并 `"Extension UI Delay Notifications"` 包括到标题中。 此外，请包含分析的详细说明。
