---
title: 有关提高性能的提示
description: 了解如何优化某些可能没有使用的 Visual Studio 功能，从而帮助提高性能。
ms.custom: SEO-VS-2020
ms.date: 10/01/2021
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: fd712091bc494d651cb4cd334325c83378048ae1
ms.sourcegitcommit: 541871db9065c4fb1b21c24f980c563991b183c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2021
ms.locfileid: "129431336"
---
# <a name="visual-studio-performance-tips-and-tricks"></a>Visual Studio 性能提示和技巧

Visual Studio 性能建议适用于内存不足的情况，这种情况极少出现。 出现这种情况时，可优化某些未使用的 Visual Studio 功能。 以下提示不作为一般性建议。

> [!NOTE]
> 如果因为内存问题而在使用产品时遇到困难，请通过[反馈工具](../ide/how-to-report-a-problem-with-visual-studio.md)告知我们。

## <a name="use-a-64-bit-os"></a>使用 64 位操作系统

如果将系统从 Windows 32 位版本升级到 64 位版本，那么 Visual Studio 的可用虚拟内存量会从 2 GB 扩展到 4 GB。 这样，即使 Visual Studio 是 32 位进程，也可以处理更大的工作负荷。

有关详细信息，请参阅[内存限制](/windows/desktop/Memory/memory-limits-for-windows-releases)和[在 64 位 Windows 上使用 /LARGEADDRESSAWARE](https://blogs.msdn.microsoft.com/oldnewthing/20050601-24/?p=35483/)。

> [!TIP]
> Windows 上的 Visual Studio 2022 现在是 64 位应用程序。 这意味着，可以在不耗尽内存的情况下打开、编辑、运行和调试最大且最复杂的解决方案。 若要了解详细信息，请参阅 [Visual Studio 2022 愿景](https://devblogs.microsoft.com/visualstudio/visual-studio-2022/)和 [Visual Studio 2022 Preview 1](https://devblogs.microsoft.com/visualstudio/visual-studio-2022-preview-1-now-available/) 博客文章。

## <a name="disable-automatic-file-restore"></a>禁用自动文件还原

Visual Studio 会自动重新打开上一个会话中处于打开状态的文档。 这可将加载解决方案所需的时间延长 30% 或更多，具体取决于项目类型和打开的文档。 Windows 窗体和 XAML 等设计器以及一些 JavaScript 和 typescript 文件的打开速度较慢。

当自动文档还原导致解决方案加载速度明显变慢时，Visual Studio 会以黄色显示栏通知。 可按照以下步骤禁用自动文件重新打开：

1. 选择“工具” > “选项”，打开“选项”对话框。

1. 在“项目和解决方案” > “常规”页面上，取消选中“重新打开解决方案加载文档”。

如果禁止自动还原文件，可使用任一[转到](../ide/go-to.md)命令快速导航到要打开的文件：

- 对于常规“转到”功能，请选择“编辑” > 转到” > 转到所有”（或按 Ctrl+T）。

- 可使用“编辑” > “转到” > “转到上次编辑的位置”（或按“Ctrl”+“Shift”+“Backspace”）跳转到解决方案中上次编辑的位置。

- 使用“转到最近使用的文件”，查看解决方案中最近访问的文件的列表  。 选择“编辑” > “转到” > “转到最近使用的文件”（或按 Ctrl+1、Ctrl +R）。

## <a name="configure-debugging-options"></a>配置调试选项

如果经常在调试会话期间遇到内存不足的情况，可以通过更改一项或多项配置来优化性能。

- **启用“仅我的代码”**

    最简单的优化是启用“仅我的代码”  功能，启用此功能后只会加载你项目的符号。 启用此功能后，调试托管的应用程序 (.NET) 时可节省大量内存。 对于某些项目类型，此选项默认为启用状态。

    要启用“仅我的代码”  ，请选择“工具”   > “选项”   > “调试”   > “常规”  ，然后选择“启用仅我的代码”  。

- **指定要加载的符号**

    对于本机调试，加载符号文件 (.pdb)  会占用很多内存资源。 可通过配置调试程序符号设置来节省内存。 通常情况下，将解决方案配置为仅加载你项目中的模块。

    要指定符号加载，请选择“工具”   > “选项”   > “调试”   > “符号”  。

    将选项设置为“仅指定模块”  ，而不是“所有模块”  ，然后指定要加载的负载。 调试时，还可以在“模块”  窗口中右键单击特定模块，将其显示包含在系统加载中。 （要在调试时打开窗口，请选择“调试”   > “窗口”   > “模块”  。）

    有关详细信息，请参阅[了解符号文件](?view=vs-2019&preserve-view=true)。

- **禁用诊断工具**

    建议在使用 CPU 分析后将其禁用。 此功能可能会占用大量资源。 CPU 分析处于启用状态后，后续调试会话中会一直保持启用状态，因此可在其完成时将其显示关闭。 如果不需要提供的功能，可以通过在调试时禁用诊断工具节省一些资源。

    若要禁用“诊断工具”，请启动调试会话，选择“工具” > “选项” > “调试” > “常规”，然后取消选中“调试时启用诊断工具”选项。

    有关详细信息，请参阅[分析工具](../profiling/profiling-feature-tour.md)。

## <a name="disable-tools-and-extensions"></a>禁用工具和扩展

某些工具或扩展会关闭以提高性能。

> [!TIP]
> 通常可以通过一次关闭一个扩展并重新检查性能来隔离性能问题。

### <a name="managed-language-service-roslyn"></a>托管的语言服务 (Roslyn)

有关 .NET Compiler Platform（“Roslyn”）性能注意事项的详细信息，请参阅 [Performance considerations for large solutions](https://github.com/dotnet/roslyn/blob/master/docs/wiki/Performance-considerations-for-large-solutions.md)（大型解决方案的性能注意事项）。

- **禁用完整解决方案分析**

    Visual Studio 对整个解决方案执行分析，以在调用生成前提供关于错误的丰富体验。 此功能可用于尽快速识别错误。 但是，对于大型解决方案，这一功能可能会占用大量内存资源。 如果遇到内存不足或类似问题，可以禁用此体验并释放这些资源。 默认情况下，Visual Basic 启用此选项，而 C# 禁用此选项。

    若要禁用“完整解决方案分析”，请选择“工具” > “选项” > “文本编辑器”，替换选择“Visual Basic”或“C#”。 选择“高级”，并取消选中“启用完整解决方案分析”   。

- **禁用 CodeLens**

    Visual Studio 对显示的每个方法执行“查找所有引用”  任务。 CodeLens 提供内联显示引用数目等功能。 工作在单独的进程（例如 ServiceHub.RoslynCodeAnalysisService32）中执行  。 在大型解决方案或资源受限的系统中，此功能对性能有显著影响。 例如，如果在 4 GB 计算机上加载大型解决方案时遇到内存问题，或进程的 CPU 使用率过高，可禁用 CodeLens 以释放资源。

    要禁用 CodeLens  ，请选择“工具”   > “选项”   > “文本编辑器”   > “所有语言”   > “CodeLens”  ，然后取消选择该功能。

    > [!NOTE]
    > CodeLens 在 Visual Studio Professional 和 Enterprise 版本中提供。

### <a name="other-tools-and-extensions"></a>其他工具和扩展

- **禁用扩展**

    扩展是添加到 Visual Studio 的附加软件组件，用于提供新功能或扩展现有功能。 扩展通常可能导致内存资源问题。 如果遇到内存资源问题，请尝试一次禁用一个扩展，并查看这将如何影响方案或工作流。

   ::: moniker range="vs-2017"

    要禁用扩展，请转到“工具”  >“扩展和更新”  ，然后禁用特定扩展。

   ::: moniker-end

   ::: moniker range=">=vs-2019"

    若要禁用扩展，请转到“扩展”  >“管理扩展”  ，然后禁用特定扩展。

   ::: moniker-end

- **禁用地图模式**

    [地图模式](how-to-track-your-code-by-customizing-the-scrollbar.md#display-modes)在滚动条上以缩图形式显示代码行。 地图模式默认处于启用状态。

    要禁用地图模式，请依次转到“工具” > “选项” > “文本编辑器” > “所有语言” > “滚动条”，然后在“行为”部分中，取消选择“使用垂直滚动条的地图模式”选项      。

- **禁用自动换行**

    [自动换行](./reference/how-to-manage-word-wrap-in-the-editor.md)显示长代码行中超出代码编辑器窗口当前宽度的部分。 自动换行默认处于打开状态。

    要针对当前正在处理的项目禁用自动换行，请转到“编辑” > “高级” > “自动换行”  。 （你可以使用相同的菜单命令来切换此设置。）

    要针对所有项目禁用自动换行，请转到“工具” > “选项” > “常规” > “文本编辑器” > “所有语言” > “常规”，然后在“设置”部分中，取消选择“自动换行”选项       。

- **禁用 XAML 设计器**

    默认情况下，XAML 设计器处于启用状态，但是只会在打开 .xaml 文件时占用资源。 如果使用 XAML 文件，但不希望使用设计器功能，请禁用此功能以释放内存。

    要禁用 XAML 设计器，请转到“工具” > “选项” > “XAML 设计器” > “启用 XAML 设计器”，然后取消选择该选项   。

- **删除工作负载**

    可以使用 Visual Studio 安装程序删除不再使用的工作负载。 此操作可以跳过不再使用的包和程序集，从而优化启动和运行时的资源占用。

- 将未跟踪的文件添加到本地 .gitignore

    在将你新文件添加到存储库时，Visual Studio 对未跟踪的文件运行 Git 命令 `git status`，以提供无缝体验。 如果有大量未跟踪的文件，`git status` 会消耗额外的内存。 若要忽略这些文件并改善 `git status` 的性能，可以将这些文件或文件夹添加到你的本地 .gitignore 文件中。 若要访问该文件，请转到“Git” > “设置” >  “Git 存储库设置”  。 然后，在“Git 文件”部分中，单击“添加”以创建 .gitignore 文件，或者如果已有文件，则单击“编辑”。

## <a name="force-a-garbage-collection"></a>强制垃圾回收

CLR 使用垃圾回收内存管理系统。 在此系统中，内存有时会被不再需要的对象占用。 这一状态是临时的，垃圾回收器会基于其性能和资源使用情况试探法释放此内存。 可通过在 Visual Studio 中使用热键强制 CLR 回收任何未使用的内存。 如果有大量垃圾等待回收并已强制垃圾回收，可在“任务管理器”中看到 devenv.exe 进程的内存使用率降低。 很少需要使用此方法。 但是，在完成一个资源占用较高的操作（如完整生成、调试会话或解决方案打开事件）后，此方法有助于确定进程实际在使用的内存量。 由于 Visual Studio 属于混合型（托管和本机），因此本机分配器和垃圾回收器有时可能会竞争有限的内存资源。 在内存使用率较高的情况下，这可能有助于强制垃圾回收器运行。

要强制垃圾回收，请使用热键：Ctrl+Alt+Shift+F12，Ctrl+Alt+Shift+F12（按两次）       。

如果强制垃圾回收确实可让方案正常工作，请通过 Visual Studio 反馈工具提交报告，因为这一行为可能是一个 Bug。

有关 CLR 垃圾回收器的详细描述，请参阅[垃圾回收的基本原理](/dotnet/standard/garbage-collection/fundamentals)。

## <a name="see-also"></a>另请参阅

- [优化 Visual Studio 性能](../ide/optimize-visual-studio-performance.md)
- [更快加载解决方案（Visual Studio 博客）](https://devblogs.microsoft.com/visualstudio/load-solutions-faster-with-visual-studio-2017-version-15-6/)