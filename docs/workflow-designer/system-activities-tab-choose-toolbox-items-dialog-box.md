---
title: System.object，选择工具箱项
description: 在工作流设计器中，了解 "系统活动" 选项卡如何显示可供你使用的 Windows Workflow Foundation (WF) 活动、模板和项的列表。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122091976"
---
# <a name="systemactivities-tab-choose-toolbox-items-dialog-box"></a>"系统活动" 选项卡，"选择工具箱项" 对话框

"**选择工具箱项**" 对话框的此选项卡显示可用 Windows Workflow Foundation (WF) 活动、模板和项目的列表。 若要显示此列表，请从 "**工具**" 菜单中选择 "**工具箱项**"，或通过右键单击 **工具箱** 并选择 "**选择项**" 以显示 "**选择工具箱项**" 对话框，然后选择其 "**系统**" 选项卡。从现成的列表中，列表包含来自 System.object、system.web 和 System.object 程序集的工作流活动;但是，默认情况下，仅检查显示的系统提供的活动和通过 **工具箱** 中显示的其他程序集添加的活动。 当你在对话框上单击 **"确定"** 时，将自动检查并显示最近 **添加的活动**。 此外，这些项将显示在 **工具箱** 中与活动/项/模板所在的命名空间对应的新类别中。

> [!WARNING]
> 如果您试图添加未包含任何工作流活动的程序集，则将显示一个错误对话框，指出该程序集没有包含任何活动。

此对话框与项目无关，因此 " **系统活动** " 选项卡继续显示在独立 XAML 或非工作流项目类型中。

筛选是在每个选项卡上完成的，并且不能通过 " **.Net 组件** " 选项卡添加工作流活动。通过 " **系统活动** " 选项卡本身添加它们。

您可以在此对话框选项卡中取消选中不希望在 **工具箱** 中看到的任何项，也可以使用 "**工具箱**" 中的 "**删除**" 右键单击菜单选项来取消引用程序集，而不会从 **工具箱** 中移除该项。

通过将活动拖放到设计器上来实例化该活动会自动将包含该项的程序集添加到引用的程序集列表中。 此外，如果该活动引用程序集 C，它不会将 C 添加到引用的程序集列表中。 程序集 C 必须位于 GAC 中或与活动 B 相同的目录中。在独立情况下，程序集必须位于 GAC 中或 VS 的探测路径中。 只有在那时，您可以拖动和删除工作流设计器图面上的活动。

默认情况下，**工具箱** 设置作为用户选项保存，因此当您打开 "**工具箱**" 时，它会显示您自定义的工作流活动列表。 这种情况的一个副作用是，如果已通过 "**选择工具箱项**" 对话框将特定的域项添加到 "**工具箱**" 中，则在工作流控制台应用程序中工作时仍将继续查看这些项。 如果你不想看到它们，请使用右键单击菜单删除它们，或通过 " **选择工具箱项** " 对话框取消选中，如前文所述。

此对话框中的列包含以下信息：

名称\
列出当前已在您的本地计算机上注册的工作流活动的名称。

名称
显示定义活动结构的 .NET 命名空间的层次结构。

程序集名称 \
显示包含活动的 .NET 程序集的名称和版本。

文件夹
显示包含工作流活动的 .NET 程序集的位置。 所有程序集的默认位置是全局程序集缓存。

若要对所列组件排序，请选择任意列标题。
