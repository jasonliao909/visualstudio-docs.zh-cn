---
title: 禁止显示所生成代码的代码分析冲突
ms.date: 05/13/2019
description: 了解如何禁止显示所生成代码的代码分析警告。 了解如何防止 Visual Studio 显示有关生成代码的旧分析警告。
ms.custom: SEO-VS-2020
ms.topic: how-to
ms.assetid: 3a96434e-d419-43a7-81ba-95cccac835b8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 214c7ca6bd7dcf648060383462fa2dfef24a3618
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601291"
---
# <a name="how-to-suppress-code-analysis-warnings-for-generated-code"></a>如何：禁止显示所生成代码的代码分析警告

生成的代码包括由托管代码编译器或第三方工具添加到项目的代码。 你可能想要查看代码分析在生成的代码中发现的规则冲突。 但是，由于无法查看和维护包含冲突的代码，你可能不希望看到这些冲突。

通过项目的代码分析属性页上的“禁止显示由生成代码产生的结果”复选框，可以选择是否显示第三方工具生成的代码的代码分析警告。

> [!NOTE]
> 当生成的代码所产生的代码分析错误和警告出现在窗体和模板中时，此选项不会取消显示它们。 可以查看和维护窗体或模板的源代码。

### <a name="to-suppress-warnings-for-generated-code-in-a-project"></a>禁止显示项目中生成的代码的警告

1. 右键单击“解决方案资源管理器”中的项目，然后单击“属性” 。

2. 选择“代码分析”选项卡。

3. 选择“禁止显示由生成代码产生的结果”复选框。

> [!IMPORTANT]
> 只能禁止显示旧分析中的警告。 具有此设置的属性页已弃用，并将在之后的产品版本中删除。 目前，无法禁止显示[分析器](roslyn-analyzers-overview.md)中的代码分析警告。
