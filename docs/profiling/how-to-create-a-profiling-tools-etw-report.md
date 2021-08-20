---
title: 创建分析工具 ETW 报表 | Microsoft Docs
description: 了解如何创建 Windows 事件跟踪 (ETW) 报告。 本部分列出了在 Visual Studio 分析工具性能会话中记录的 ETW 事件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: bf5547b3-f6c7-4989-9d47-2fe4f1261444
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 687e813b449f469386d1c2fce9a7b79ae7467497
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122150230"
---
# <a name="how-to-create-a-profiling-tools-etw-report"></a>如何：创建分析工具 ETW 报告
Windows 事件跟踪 (ETW) 报告列出 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 分析工具的性能会话中所记录的 ETW 事件。 ETW 数据收集在二进制 (.etl) 文件中。 有关此报告的详细信息，请参阅 [Windows 事件跟踪 (ETW) 报告](../profiling/event-tracing-for-windows-etw-report.md)。

> [!NOTE]
> 不能在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的接口中显示 ETW 报告。

- 有关如何使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的接口收集 ETW 数据的详细信息，请参阅[如何：收集 Windows 事件跟踪 (ETW) 数据](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)。

- 有关如何从命令提示符收集 ETW 数据的信息，请参阅 [VSPerfCmd](../profiling/vsperfcmd.md) 和[事件](../profiling/events-vsperfcmd.md)。

  使用 **VSReport/summary:etw** 命令生成 ETW 报告。 包含 ETW 数据的 .etl 必须与分析数据文件（.vsp 或 .vsps）位于同一目录中  。 报告默认生成为逗号分隔值文件 (.csv)。 有关详细信息，请参阅 [VSPerfReport](../profiling/vsperfreport.md)。

### <a name="to-generate-an-etw-report"></a>创建 ETW 报告

- 在“命令提示符”窗口中，键入以下命令行：

     *ToolsPath* **VSPerfReport** *VSPFile*  **/Summary:ETW [/Xml]**

    |项|描述|
    |-|-|
    |*ToolsPath*|分析工具实用工具的路径。 有关详细信息，请参阅[指定命令行工具的路径](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)。|
    |*VSPFile*|分析数据文件（vsp 或 vsps） 。 接受完整和部分路径。|
    |Xml|生成 XML 格式的报告。|
