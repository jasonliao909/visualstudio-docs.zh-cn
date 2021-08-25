---
title: 在调试器中对断点进行故障排除 | Microsoft Docs
description: 如果断点已禁用或无法设置，它将显示为空心圆圈。 在此处查看有关设置断点时可能发生的问题的信息。
ms.custom: SEO-VS-2020
ms.date: 01/23/2018
ms.topic: troubleshooting
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 0caeb4a9a37497922af5c5b7d94f539859644c02
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122096812"
---
# <a name="troubleshoot-breakpoints-in-the-visual-studio-debugger"></a>在 Visual Studio 调试器中对断点进行故障排除

## <a name="breakpoint-warnings"></a>断点警告

调试时，断点具有两种可能的可视状态：红色实心圆和空心（填充白色）圆。 如果调试器能够在目标进程中成功设置断点，它将保持红色实心圆状态。 如果断点是空心圆，则表示尝试设置断点时断点被禁用或出现警告。 若要进行区分，请将鼠标悬停在断点上，查看是否有警告。

以下两个部分介绍主要警告及其解决方法。

### <a name="no-symbols-have-been-loaded-for-this-document"></a>“尚未为此文档加载任何符号”

转到“模块”窗口（“调试” > “窗口” > “模块”），然后检查模块是否已加载。
* 如果模块已加载，请检查“符号状态”列以查看符号是否已加载。
  * 如果未加载符号，请检查符号状态以诊断问题。 在“模块”窗口中某个模块的上下文菜单中，单击“符号加载信息...”，查看调试器尝试加载符号的位置。 有关加载符号的详细信息，请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。
  * 如果已加载符号，则 PDB 不包含有关源文件的信息。 以下是几个可能的原因：
    * 如果源文件是最近添加的，请确认是否在加载模块的最新版本。
    * 可以使用“/PDBSTRIPPED”链接器选项创建去除的 PDB。 去除的 PDB 不包含源文件信息。 确认使用的是完整的 PDB，而不是去除的 PDB。
    * PDB 文件已部分损坏。 删除文件并执行模块清理生成，以尝试解决问题。

* 如果模块未加载，请检查以下项以查找原因：
  * 确认正在调试正确的进程。
  * 检查是否正在调试正确的代码类型。 你可以在“进程”窗口（“调试” > “窗口” > “进程”）中找到调试器被配置调试的代码类型。 例如，如果尝试调试 C# 代码，请确认已针对 .NET 的相应类型和版本（例如，托管[v4\*]与托管[v2\*/v3\*]与托管[CoreCLR]）配置调试器。

### <a name="-the-current-source-code-is-different-from-the-version-built-into"></a>"… 当前源代码与 中内置的版本不同...”

如果源文件已更改，并且源不再与要调试的代码匹配，则默认情况下，调试器不会在代码中设置断点。 通常，在更改源文件但未重新生成源代码的情况下会发生此问题。 若要解决此问题，请重新生成项目。 如果生成系统在项目未处于最新状态的情况下认为项目已处于最新状态，则可以通过重新保存源文件或在生成之前清除项目的生成输出来强制项目系统重新生成。

在极少数情况下，你可能需要在没有匹配的源代码的情况下进行调试。 在没有匹配的源代码的情况下进行调试会导致混乱的调试体验，因此，请确保这是你想要执行的操作。

若要禁用这些安全检查，请执行以下操作之一：
* 若要修改单个断点，请将鼠标悬停在编辑器中的断点图标上，然后单击设置（齿轮）图标。 一个查看窗口将添加到编辑器中。 查看窗口的顶部有一个超链接，其指示断点的位置。 单击超链接以允许修改断点位置，然后选中“允许源代码与原始版本不同”。
* 若要为所有断点修改此设置，请转到“调试” > “选项和设置”。 在 **“调试”/“常规”** 页上，清除 **“要求源文件与原始版本完全匹配”** 选项。 完成调试后，请确保重新启用此选项。

## <a name="the-breakpoint-was-successfully-set-no-warning-but-didnt-hit"></a>已成功设置断点（无警告），但未命中

本部分提供有关在调试器未显示任何警告的情况下对问题进行故障排除的信息：断点在主动进行调试时显示为红色实心圆，但未命中该断点。

可以检查以下项：
1. 如果你的代码在多个进程中或多台计算机上运行，请确保正在调试正确的进程或计算机。
2. 确认代码正在运行。 若要测试代码是否正在运行，请在尝试设置断点的代码行中添加对 `System.Diagnostics.Debugger.Break` (C#/VB) 或 `__debugbreak` (C++) 的调用，然后重新生成项目。
3. 如果要调试经过优化的代码，请确保未将其中设置了断点的函数内联到另一个函数中。 前面检查中介绍的 `Debugger.Break` 测试也可以用来测试此问题。

## <a name="i-deleted-a-breakpoint-but-i-continue-to-hit-it-when-i-start-debugging-again"></a>我删除了断点，但在再次启动调试时继续命中该断点

如果在调试时删除了断点，则可能会在下次启动调试时再次命中该断点。 要停止命中此断点，请确保从 **“断点”** 窗口删除该断点的所有实例。
