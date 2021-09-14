---
title: System.Activities，选择工具箱项
description: 在工作流设计器中，了解"System.Activities"选项卡如何显示可用的 Windows Workflow Foundation (WF) 活动、模板和项的列表。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.CHOOSEITEMS.SYSTEM.ACTIVITIES_COMPONENTS
- VS.CHOOSEITEMS.SYSTEM.ACTIVITIES COMPONENTS
ms.assetid: cef390cd-eeda-42e6-9d2e-18c8325a4f06
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 29074e32fb232af7e89581368a6067b9db668da1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664910"
---
# <a name="systemactivities-tab-choose-toolbox-items-dialog-box"></a>"System.Activities"选项卡，"选择工具箱项"对话框

"选择工具箱 **项**"对话框的此选项卡显示 WF Windows工作流基础 () 活动、模板和项的列表。 若要显示此列表，请从"工具"菜单中选择"选择工具箱项"，或者右键单击"工具箱"，然后选择"选择项"以显示"选择工具箱 **项**"对话框，然后选择其 **"System.Activities"** 选项卡。  列表包含 System.Activities、System.ServiceModel.Activities 和 System.Activities.Core.Presentation 程序集中的工作流活动;但是，默认情况下仅检查系统提供的活动以及通过工具箱中显示的其他程序集添加的活动。  单击对话框中的"确定"时，将自动选中最近添加的活动，并出现在 **"工具箱"** 中。 此外，这些项显示在"工具箱 **"中与** 活动/项/模板所在的命名空间相对应的新类别下。

> [!WARNING]
> 如果您试图添加未包含任何工作流活动的程序集，则将显示一个错误对话框，指出该程序集没有包含任何活动。

此对话框与项目无关，因此 **"System.Activities"** 选项卡将继续显示在独立 XAML 或非工作流项目类型中。

筛选在每个选项卡上完成，无法通过 **".NET** 组件" 选项卡添加工作流活动。通过 **"System.Activities"选项卡本身** 添加它们。

可以取消选中不希望在此对话框选项卡的"工具箱"中查看的任何项，或者，可以使用"工具箱"中的"删除右键单击"菜单选项来这样做，取消引用程序集不会从"工具箱"中删除 **该项**。 

通过将活动拖放到设计器上来实例化该活动会自动将包含该项的程序集添加到引用的程序集列表中。 此外，如果该活动引用程序集 C，它不会将 C 添加到引用的程序集列表中。 程序集 C 必须在同一个 GAC 或与活动 B 相同的目录中。在独立情况下，程序集必须输入 GAC 或 VS 的探测路径。 只有在那时，您可以拖动和删除工作流设计器图面上的活动。

**工具箱** 设置默认保存为用户选项，因此下次打开"工具箱"时，它会显示工作流活动的自定义列表。 这样做的一个副作用是，如果通过"选择工具箱项"对话框将特定域项添加到"工具箱"，则当你在工作流控制台应用程序中操作时，仍将继续看到这些项。 如果不想看到它们，则使用右键单击菜单删除它们，或者通过"选择工具箱项"对话框取消选中它们，如前所述。

此对话框中的列包含以下信息：

名称\
列出当前已在您的本地计算机上注册的工作流活动的名称。

Namespace\
显示定义活动结构的 .NET 命名空间的层次结构。

程序集名称\
显示包含活动的 .NET 程序集的名称和版本。

Directory\
显示包含工作流活动的 .NET 程序集的位置。 所有程序集的默认位置是全局程序集缓存。

若要对所列组件排序，请选择任意列标题。
