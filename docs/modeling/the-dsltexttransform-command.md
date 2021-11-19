---
title: DslTextTransform 命令
description: 了解 DslTextTransform.cmd 是一个调用 TextTransform.exe 并使用常用选项运行它的脚本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, commands
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: ae937c45d0bb768bf25ef562132db136b8462805
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663863"
---
# <a name="the-dsltexttransform-command"></a>DslTextTransform 命令
DslTextTransform.cmd 是一个调用 TextTransform.exe 并使用常用选项运行它的脚本。 可以使用 DslTextTransformation.cmd 自动执行 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 项目的夜间生成。 有关详细信息，请参阅[使用 TextTransform 实用工具生成文件](../modeling/generating-files-with-the-texttransform-utility.md)。

 DslTextTransform.cmd 位于以下目录中：

 \<Visual Studio SDK Installation Path>\VisualStudioIntegration\Tools\Bin

 可以指定以下参数作为 DslTextTransform.cmd 的输入：

- 域模型项目的输出目录。

- 设计器定义项目的输出目录。

- 文本模板文件的位置。

  DslTextTransform.cmd 使用默认指令处理器和程序集处理指定的文本模板文件。 如果你要创建自定义指令处理器，则可以创建你自己的批处理文件来调用 TextTransform.exe。 在此批处理文件中，可以指定程序集和关联的自定义指令处理器。
