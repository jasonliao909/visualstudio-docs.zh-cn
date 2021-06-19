---
title: DslTextTransform 命令
description: 了解 DslTextTransform.cmd 是调用 TextTransform.exe并运行其常用选项的脚本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, commands
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 65d1e1d02c5b7d13c2e86343c6307306542d00e2
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388641"
---
# <a name="the-dsltexttransform-command"></a>DslTextTransform 命令
DslTextTransform.cmd 是一个脚本，它调用 TextTransform.exe，然后使用常用选项运行它。 可以使用 DslTextTransformation.cmd 自动执行项目的夜间 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 生成。 有关详细信息，请参阅使用 [TextTransform](../modeling/generating-files-with-the-texttransform-utility.md)实用工具 生成文件。

 DslTextTransform.cmd 位于以下目录中：

 **\<Visual Studio SDK Installation Path>\VisualStudioIntegration\Tools\Bin**

 可以指定以下参数作为 DslTextTransform.cmd 的输入：

- 域模型项目的输出目录。

- 设计器定义项目的输出目录。

- 文本模板文件的位置。

  DslTextTransform.cmd 使用默认指令处理器和程序集处理指定的文本模板文件。 如果创建自定义指令处理器，可以创建自己的批处理文件来调用TextTransform.exe。 在此批处理文件中，可以指定程序集和关联的自定义指令处理器。
