---
title: 取消生成的代码的 Code Analysis 冲突
ms.date: 05/13/2019
description: 了解如何禁止显示所生成代码的代码分析警告。 请参阅如何防止 Visual Studio 显示有关生成的代码的旧分析警告。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122098003"
---
# <a name="how-to-suppress-code-analysis-warnings-for-generated-code"></a>如何：取消生成的代码的代码分析警告

生成的代码包括通过托管代码编译器或第三方工具添加到你的项目中的代码。 你可能想要查看代码分析在生成的代码中发现的规则冲突。 但是，由于无法查看和维护包含冲突的代码，因此你可能不想看到它们。

项目的 "代码分析" 属性页上的 " **禁止显示生成的代码结果** " 复选框使您可以选择是否显示第三方工具生成的代码的代码分析警告。

> [!NOTE]
> 当生成的代码所产生的代码分析错误和警告出现在窗体和模板中时，此选项不会取消显示它们。 可以查看和维护窗体或模板的源代码。

### <a name="to-suppress-warnings-for-generated-code-in-a-project"></a>禁止显示项目中生成的代码的警告

1. 右键单击 " **解决方案资源管理器** 中的项目，然后单击" **属性**"。

2. 选择 " **Code Analysis** " 选项卡。

3. 选中 " **禁止显示生成的代码结果** " 复选框。

> [!IMPORTANT]
> 您只能禁止显示旧分析中的警告。 已不推荐使用该设置的属性页，并将在将来的产品版本中将其删除。 目前不能取消 [分析器](roslyn-analyzers-overview.md)中的代码分析警告。
