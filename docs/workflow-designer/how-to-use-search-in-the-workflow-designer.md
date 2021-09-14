---
title: 如何：在工作流设计器中使用搜索
description: 了解如何在工作流中工作流设计器关键字查找项，以便创建更大、更复杂的工作流。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: f42d3115-2ed2-4941-8f1e-92dac41c30fa
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 846fbcae4cde785234048696d43466251a663f57
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664677"
---
# <a name="how-to-use-search-in-the-workflow-designer"></a>如何：在工作流设计器中使用搜索

为了便于创建更大、更复杂的工作流，可以在工作流中搜索工作流设计器关键字查找项。 请注意，设计器不支持替换。

## <a name="quick-find"></a>快速查找

快速查找在设计器中查找以下内容：

- <xref:System.Activities.Activity> 对象、<xref:System.Activities.Statements.FlowNode> 对象、<xref:System.Activities.Statements.State> 对象、转换以及其他自定义流控制项的属性。

- 变量

- 参数

- 表达式

### <a name="use-quick-find"></a>使用快速查找

1. 打开工作流设计器后，按 **Ctrl+F，** 或选择 **"编辑**  >  **查找和替换**  >  **快速查找"。**

2. 在"查找内容"文本框中 **输入搜索** 词，然后单击"查找下 **一个"。**

3. 搜索词位于当前工作流中。 下图显示了位于设计器中的活动显示名称：

   ![在工作流设计器中搜索结果](../workflow-designer/media/designersearch.png)

## <a name="find-in-files"></a>在文件中查找

"在文件中查找"可查找工作流文件（包括 XAML 文件）中的字符串。

### <a name="use-find-in-files"></a>使用"在文件中查找"

1. 在Visual Studio中，按 **Ctrl** + **Shift** + **F，** 或选择"编辑  >  **在文件中查找和**  >  **替换查找"。**

2. 在"查找内容"文本框中 **输入搜索** 项，然后单击"**查找全部"。**

3. 查找结果显示在"查找结果 **"** 视图中。 双击结果项将导航到工作流设计器中包含匹配项的活动。