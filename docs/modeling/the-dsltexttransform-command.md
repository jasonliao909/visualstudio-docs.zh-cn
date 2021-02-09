---
title: DslTextTransform 命令
description: 了解 DslTextTransform 是一个脚本，它调用 TextTransform.exe 并使用常用选项运行它。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, commands
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f51d1a5cbefc3c2cf60559075a9c9a299664ed07
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99924507"
---
# <a name="the-dsltexttransform-command"></a>DslTextTransform 命令
DslTextTransform 是一个脚本，它调用 TextTransform.exe 并使用常用选项运行它。 可以使用 DslTextTransformation 自动执行项目的夜间生成 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 。 有关详细信息，请参阅 [用 TextTransform 实用工具生成文件](../modeling/generating-files-with-the-texttransform-utility.md)。

 DslTextTransform 位于以下目录中：

 **\<Visual Studio SDK Installation Path>\VisualStudioIntegration\Tools\Bin**

 可以将以下参数指定为 DslTextTransform 的输入：

- 域模型项目的输出目录。

- 设计器定义项目的输出目录。

- 文本模板文件的位置。

  DslTextTransform 使用默认指令处理器和程序集处理指定的文本模板文件。 如果创建自定义指令处理器，则可以创建自己的批处理文件来调用 TextTransform.exe。 在此批处理文件中，可以指定程序集和关联的自定义指令处理器。
