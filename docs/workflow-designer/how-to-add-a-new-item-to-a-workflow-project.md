---
title: 工作流设计器：向工作流项目添加新项目
description: 了解如何在创建工作流项目之后将工作流活动、设计器和其他熟悉的 Visual Studio 项添加到项目中。
ms.custom: SEO-VS-2020
ms.date: 06/25/2018
ms.topic: how-to
ms.assetid: 5c6180ca-af10-4513-b0cb-7d478fd84eab
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: d09699c345878d27eecba518c54f8ff0cfd44d1b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666980"
---
# <a name="how-to-add-a-new-item-to-a-workflow-project"></a>如何向工作流项目添加新项目

创建工作流项目之后，可以将工作流活动、设计器和其他熟悉的 Visual Studio 项添加到项目中。

下表列出了可添加到工作流项目中的 Windows Workflow Foundation (WF) 项：

| 名称 | 说明 |
|-| - |
| 活动 | 由其他活动组成的活动。 在为新项目选择“活动库”模板时，选择此项可将相同的 XAML 文件添加到要获得的项目。 有关此过程的更多信息，请参阅[创建工作流项目](creating-a-workflow-project.md)。 |
| 活动设计器 | 用于自定义活动的设计时体验的设计器。 在为新项目选择“活动设计器库”模板时，选择此项可将相同的文件添加到要获得的项目。 |
| Code 活动 | 一个采用代码编写执行逻辑的活动。 已为你生成一个源代码文件，该文件带有 <xref:System.Activities.CodeActivity.Execute%2A> 方法的重写。 |
| WCF 工作流服务 | 使用工作流活动生成的 [!INCLUDE[indigo2](../workflow-designer/includes/indigo2_md.md)] 服务。 在为新项目选择“WCF 工作流服务应用程序”模板时，选择此项可将相同文件添加到要获得的项目。 有关此过程的更多信息，请参阅[如何创建 WCF 工作流服务应用程序](creating-a-workflow-project.md)。 |

## <a name="to-add-a-new-item-to-a-workflow-project"></a>向工作流项目添加新项

1. 在“项目”菜单上，选择“添加新项”。

   此时将打开“添加新项”对话框。

1. 在左侧窗格中，选择“工作流”类别，然后选择工作流项模板。

   > [!NOTE]
   > 如果不想查看“工作流”类别，请首先安装 Visual Studio 的 Windows Workflow Foundation 组件。 有关详细说明，请参阅[安装 Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)。

1. 在对话框底部的“名称”框中，为项输入名称。

1. 选择“添加”，将项添加到项目。

## <a name="see-also"></a>另请参阅

- [创建工作流项目](../workflow-designer/creating-a-workflow-project.md)
