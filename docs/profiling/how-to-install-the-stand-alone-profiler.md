---
title: 安装独立探查器 | Microsoft Docs
description: 了解如何安装可在未安装 Visual Studio 的情况下运行的独立探查器。 在某些情况下，不应安装 Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- performance tools, installing stand-alone profiler
- profiling tools, stand-alone profiler
ms.assetid: cae81c95-83cd-4ab6-8a98-84ef977a2f6d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: d8a5b2454e2a676dcf087becc5475219d9b98f66
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126642354"
---
# <a name="how-to-install-the-stand-alone-profiler"></a>如何：安装独立探查器
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 提供了一个基于命令行的独立探查器，它可在没有安装 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE 的情况下运行。 当计算机没有安装或无法安装开发环境时会发生这种情况。 例如，不应在生产 Web 服务器上安装开发环境。

> [!NOTE]
> 使用独立探查器收集 ASP.NET 网站的性能数据时，建议使用 [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md) 命令行工具，而非 [VSPerfCmd](../profiling/vsperfcmd.md) 工具。

### <a name="to-install-the-stand-alone-profiler"></a>安装独立探查器

1. 下载[用于 Visual Studio 的性能工具](https://visualstudio.microsoft.com/downloads/?q=performance+tools#performance-tools-for-visual-studio)。

1. 在下载性能工具的位置，找到并运行独立配置文件安装程序(vs_standaloneprofiler.exe)。

2. 将 vsinstr.exe 的路径添加到系统路径。

   > [!NOTE]
   > 若要获取分析工具的路径，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。 在 64 位计算机上，同时提供 64 位和 32 位版本的工具。 若要使用探查器命令行工具，必须将工具路径添加到命令提示符窗口的 PATH 环境变量中，或将其添加到命令本身。

3. 在命令提示符处，键入 VSInstr。

   > [!NOTE]
   > 如果显示 vsinstr.exe 的用法信息，则表明安装无误。 如果看见一条错误信息，该消息指出找不到 vsinstr.exe 或它的依赖项，请确保已经按步骤 2 中的说明正确设置了路径。

4. 通过将 _NT_SYMBOL_PATH 变量设置为 symsrv\*symsrv.dll\*c:\localcache\*https://msdl.microsoft.com/download/symbols 来设置符号服务器 

5. 使用系统环境变量设置符号服务器后，请在新的命令提示符处运行命令行探查器工具。 这将使新环境变量生效。 在命令提示符窗口中，键入以下命令：

    start %COMSPEC%

   > [!NOTE]
   > 要详细了解如何设置符号服务器包，请参阅[如何：引用 Windows 符号信息](../profiling/how-to-reference-windows-symbol-information.md)。

6. 使用 [VSPerfReport](../profiling/vsperfreport.md) 工具将符号串行化到分析数据 (.vsp) 文件中。 使用 VSPerfReport /summary:all /packsymbols 开关。 如果数据文件中未插入符号，请确保设置了 _NT_SYMBOL_PATH 环境变量。

## <a name="see-also"></a>请参阅
- [通过命令行分析](../profiling/using-the-profiling-tools-from-the-command-line.md)
- [演练：使用检测进行命令行分析](command-line-profiling-of-stand-alone-applications.md)
- [如何：引用 Windows 符号信息](../profiling/how-to-reference-windows-symbol-information.md)
- [VSPerfReport](../profiling/vsperfreport.md)
