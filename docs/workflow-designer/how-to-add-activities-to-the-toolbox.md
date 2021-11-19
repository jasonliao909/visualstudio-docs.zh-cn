---
title: 向工具箱添加活动
description: 在工作流设计器中，了解如何将活动添加到解决方案中的工具箱，方法是从当前项目中添加或从其他项目中引用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: b3a8a785-5928-457a-8a50-30267e29503d
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 80535ec883db07e1a431b90ca18e6fbfd53023ad
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665659"
---
# <a name="how-to-add-activities-to-the-toolbox"></a>如何：向工具箱添加活动

有多种方法可将活动添加到解决方案的“工具箱”中。 您可以从当前项目中添加活动，也可以从另一个项目或从另一个程序集引用活动。

## <a name="to-add-an-activity-from-within-your-current-project"></a>从当前项目中添加活动

1. 将新的自定义活动添加到当前工作流项目。 有关向项目添加新的自定义活动的详细信息，请参阅[如何向工作流项目添加新项](../workflow-designer/how-to-add-a-new-item-to-a-workflow-project.md)。

2. 向活动添加自定义逻辑。

3. 生成项目。 如果生成成功，将在“工具箱”中显示一个名为“\<*project name*>”的新类别，该类别中包含相应自定义活动。

    > [!NOTE]
    > 如果重置工具箱中，则将删除自定义活动，即使重新生成解决方案。 要在重置后使用自定义活动重新填充工具箱，请重新启动 Visual Studio。

    > [!NOTE]
    > 工具箱只能显示具有给定名称的一个活动。 如果来自不同程序集的两个活动具有相同的类名称，将显示一个活动。

    > [!NOTE]
    > 在编辑器实例间共享应用程序域；如果使用静态变量，也将在编辑器实例间共享它们。 如果这不是所需的行为，应使用一个服务跟踪变量实例。 有关在设计器中使用服务的信息，请参阅 [使用 ModelItem 编辑上下文](/dotnet/framework/windows-workflow-foundation/using-the-modelitem-editing-context)。

## <a name="to-add-an-activity-from-within-a-different-project"></a>从另一个项目中添加活动

1. 打开包含至少一个工作流项目（自定义活动库项目或定义自定义活动的另一个工作流项目）的解决方案。

2. 生成这两个项目。 如果生成成功，将在“工具箱”中显示一个名为“\<*project name*>”的新类别，该类别中包含相应自定义活动。

## <a name="to-add-an-activity-to-the-toolbox-from-an-assembly"></a>从程序集中将活动添加到工具箱

1. 打开工作流解决方案。

2. 从“工具”菜单中选择“选择工具箱项” 。

3. 在“选择工具箱项”对话框中，选择“System.Activities 组件”选项卡，然后单击“浏览”导航到包含要添加的自定义活动的程序集  。

4. 选择该程序集，然后单击“确定”。 自定义活动组件将添加到组件列表中并自动处于选中状态。

    1. 单击 **“确定”**，关闭对话框。

5. 若要显示工具箱，请从“视图”菜单中选择“工具箱” 。

6. 该自定义活动将显示在添加该项之前“工具箱”中焦点所在的类别下。 例如，如果在添加工具箱项之前选中了“工具箱”中的“常规”类别，则该活动将显示在“常规”类别下  。

## <a name="see-also"></a>另请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
