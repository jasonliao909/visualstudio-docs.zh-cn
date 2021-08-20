---
title: 如何：更改域特定语言的命名空间
description: 提供有关如何更改域特定语言的命名空间的信息。
ms.date: 10/31/2018
ms.topic: how-to
titleSuffix: ''
helpviewer_keywords:
- Domain-Specific Language, namespace
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: 66ce1219f3a18c65e23c2ddc420449a0d8bc7b3c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122157483"
---
# <a name="how-to-change-the-namespace-of-a-domain-specific-language"></a>如何：更改域特定语言的命名空间

您可以更改域特定语言的命名空间。 在 **Dsl 资源管理器**、dsl 包项目的属性和程序集信息中进行更改。

## <a name="to-change-the-namespace-of-a-domain-specific-language"></a>更改域特定语言的命名空间

1. 在 " **Dsl 资源管理器**" 中，选择 **DSL** 节点。

2. 在 " **属性** " 窗口中，更改 **命名空间** 属性。

3. 保存解决方案并转换模板。

4. 在 " **Project** " 菜单上，选择 " **Dsl 属性**"。

   将显示项目的属性。

5. 选择“应用程序”选项卡。

6. 将 " **默认命名空间** " 属性更改为新的命名空间名称。

7. 如果还想要更改程序集的名称，请更改 **程序集名称属性。**

8. 如果更改了程序集名称，请打开 DslPackage\Package.tt 并更新此行：

   `string dslAssembly = "YourDSLassembly.Dsl.dll";`

9. 如果已编写任何自定义代码，请确保在代码文件中更改命名空间和类引用。

10. 重置 Visual Studio 实验实例。

    1. 删除 **\Users \\**_{name}_**\AppData\Local\Microsoft\VisualStudio \\ \* Exp**。

    2. 在 Windows **开始**"菜单上，选择"**所有程序**"  >  **Microsoft Visual Studio 2010 SDK**  >  **工具**  >  **" 重置实验实例 "**。

11. 在 " **生成** " 菜单上，选择 " **重新生成解决方案**"。

## <a name="see-also"></a>请参阅

[域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))