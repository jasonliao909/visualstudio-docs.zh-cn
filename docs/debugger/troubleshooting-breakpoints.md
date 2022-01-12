---
title: 在调试器中对断点进行故障排除 | Microsoft Docs
description: 如果断点已禁用或无法设置，则它显示为空心圆。 在此处查看有关设置断点时可能发生的问题的信息。
ms.date: 01/10/2022
ms.topic: troubleshooting
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.custom: devdivchpfy22
ms.openlocfilehash: dc2f7ccd780c8675a7812d370f6dce9ff744eaa8
ms.sourcegitcommit: 965372ad0d75f015403c1af508080bf799914ce3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "135805243"
---
# <a name="troubleshoot-breakpoints-in-the-visual-studio-debugger"></a>在 Visual Studio 调试器中对断点进行故障排除

## <a name="breakpoint-warnings"></a>断点警告

调试时，断点有两种可能的可视状态：

* 如果调试器在目标进程中成功设置了断点，则为实心红色圆圈。
* 在 (设置断点) 断点时，断点被禁用或出现警告时，空心) 白色填充的圆。

若要确定差异，请将鼠标悬停在断点上，看是否有警告。 以下两个部分介绍主要警告及其解决方法。

### <a name="no-symbols-have-been-loaded-for-this-document"></a>“尚未为此文档加载任何符号”

转到“模块”窗口（“调试” > “窗口” > “模块”），然后检查模块是否已加载。

* 如果模块已加载，请检查“符号状态”列以查看符号是否已加载。
  * 如果未加载符号，请检查符号状态以诊断问题。 在"模块"窗口中模块的上下文菜单中，选择"符号加载信息 **..."，** 查看调试器尝试和加载符号的位置。 有关加载符号的详细信息，请参阅[指定符号 (.pdb) 和源文件](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)。
  * 如果加载符号，则 PDB 不包含有关源文件的信息。 一些可能的原因包括：
    * 如果源文件是最近添加的，请确认是否在加载模块的最新版本。
    * 使用 **/PDBSTRIPPED** 链接器选项可以创建去除的 PDB。 去除的 PDB 不包含源文件信息。 确认使用完整的 PDB，而不是去除的 PDB。
    * PDB 文件已部分损坏。 删除文件并运行模块的干净版本以尝试解决此问题。

* 如果未加载模块，请检查以下各项以找出原因：
  * 确认正在调试正确的进程。
  * 检查是否正在调试正确的代码。 你可以在“进程”窗口（“调试” > “窗口” > “进程”）中找到调试器被配置调试的代码类型。 例如，如果尝试调试 C# 代码，请确认为 .NET (的适当类型和版本配置了调试器，例如托管 (v4) 与托管 \* (v2 /v3) 与托管 \* (\* CoreCLR) ) 。

### <a name="-the-current-source-code-is-different-from-the-version-built-into"></a>"… 当前源代码与 中内置的版本不同...”

如果源文件已更改，并且源不再与正在调试的代码匹配，则默认情况下调试器不会在代码中设置断点。 通常情况下，当源文件发生更改，但源代码未重新生成时，会发生此问题。 若要解决此问题，请重新生成项目。 如果生成系统认为项目已是最新的，即使项目不是最新的，可以强制重新生成项目系统。 重新生成项目，可以再次保存源文件，或在生成前清除生成输出。

在极少数情况下，你可能需要在没有匹配的源代码的情况下进行调试。 在没有匹配的源代码的情况下进行调试可能会导致令人困惑的调试体验，因此请确保要如何继续。

按照以下选项之一禁用这些安全检查：

* 若要修改单个断点，请将鼠标悬停在编辑器中的断点图标上，然后选择齿轮 (图标) 设置。 一个查看窗口将添加到编辑器中。 速览窗口顶部有一个超链接，指示断点的位置。 选择超链接以允许修改断点位置，并选中"允许源代码 **不同于原始 "。**
* 若要为所有断点修改此设置，请转到“调试” > “选项和设置”。 在 **“调试”/“常规”** 页上，清除 **“要求源文件与原始版本完全匹配”** 选项。 完成调试后，请确保重新启用此选项。

## <a name="the-breakpoint-was-successfully-set-no-warning-but-didnt-hit"></a>断点已成功设置为 (无) ，但没有命中

本部分提供有关在调试器不显示任何警告时排查问题的信息 - 断点在主动调试时为实心红色圆圈，但不会命中断点。

可以检查以下项：

1. 如果代码在多进程或多台计算机中运行，请确保正在调试正确的进程或计算机。
2. 确认代码正在运行。 若要测试代码是否正在运行，请向尝试设置断点的代码行添加对 (C#/VB) 或 (C++) 的调用，然后 `System.Diagnostics.Debugger.Break` `__debugbreak` 重新生成项目。
3. 如果要调试优化的代码，请确保设置断点的函数未内lined到另一个函数中。 前面检查中介绍的 `Debugger.Break` 测试也可以用来测试此问题。

## <a name="i-deleted-a-breakpoint-but-i-continue-to-hit-it-when-i-start-debugging-again"></a>我删除了断点，但在再次启动调试时继续命中该断点

如果在调试时删除了断点，则可能会在下次启动调试时再次命中该断点。 要停止命中此断点，请确保从 **“断点”** 窗口删除该断点的所有实例。
