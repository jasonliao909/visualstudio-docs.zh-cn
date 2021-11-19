---
title: 工作流设计器：向工作流项目添加新项
description: 了解如何创建工作流项目后，如何将工作流活动、设计器Visual Studio熟悉的项目添加到项目。
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
# <a name="how-to-add-a-new-item-to-a-workflow-project"></a>如何：向工作流项目添加新项

创建工作流项目后，可以将工作流活动、设计器和其他熟悉的Visual Studio添加到项目。

下表列出了 WF Windows的 (工作流) 添加到工作流项目的项：

| 名称 | 说明 |
|-| - |
| 活动 | 由其他活动组成的活动。 选择此项会将与选择新项目的活动库模板时获取的 XAML 文件相同的XAML 文件添加到项目中。 有关此过程的信息，请参阅 [创建工作流项目](creating-a-workflow-project.md)。 |
| 活动设计器 | 用于自定义活动的设计时体验的设计器。 选择此项会将与为新项目选择活动设计器库模板时获得的文件相同的文件添加到项目中。 |
| Code 活动 | 一个采用代码编写执行逻辑的活动。 已为你生成一个源代码文件，该文件带有 <xref:System.Activities.CodeActivity.Execute%2A> 方法的重写。 |
| WCF 工作流服务 | 使用工作流活动生成的 [!INCLUDE[indigo2](../workflow-designer/includes/indigo2_md.md)] 服务。 选择此项会将与为新项目选择 **WCF** 工作流服务应用程序模板时获得的文件相同的文件添加到项目中。 有关此过程的详细信息，请参阅 [如何：创建 WCF 工作流服务应用程序](creating-a-workflow-project.md)。 |

## <a name="to-add-a-new-item-to-a-workflow-project"></a>向工作流项目添加新项

1. 在“项目”菜单上，选择“添加新项”。

   此时将打开“添加新项”对话框。

1. 在左侧窗格中，选择"工作流 **"** 类别，然后选择工作流项模板。

   > [!NOTE]
   > 如果看不到"工作流 **"类别，** 请首先安装 Windows **的 Workflow Foundation** Visual Studio。 有关详细说明，请参阅[Install Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)。

1. 在对话框底部的"名称 **"** 框中输入项的名称。

1. 选择 **"** 添加"，将项添加到项目。

## <a name="see-also"></a>另请参阅

- [创建工作流项目](../workflow-designer/creating-a-workflow-project.md)
