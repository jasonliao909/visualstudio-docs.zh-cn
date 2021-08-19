---
title: 向工具箱添加活动
description: 在工作流设计器中，了解如何通过从当前项目中添加活动或从其他项目引用活动，将活动添加到解决方案中的工具箱。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122114727"
---
# <a name="how-to-add-activities-to-the-toolbox"></a>如何：向工具箱添加活动

可以通过多种不同 **方式将活动** 添加到解决方案中的工具箱。 您可以从当前项目中添加活动，也可以从另一个项目或从另一个程序集引用活动。

## <a name="to-add-an-activity-from-within-your-current-project"></a>从当前项目中添加活动

1. 将新的自定义活动添加到当前工作流项目。 有关向项目添加新自定义活动的详细信息，请参阅如何：将新项[添加到工作流Project。](../workflow-designer/how-to-add-a-new-item-to-a-workflow-project.md)

2. 向活动添加自定义逻辑。

3. 生成项目。 如果生成成功，则显示工具箱中名为""的新类别，该类别中包含自定义 \<*project name*> 活动。

    > [!NOTE]
    > 如果重置工具箱中，则将删除自定义活动，即使重新生成解决方案。 若要在重置工具箱后使用自定义活动重新填充该工具箱，请重启Visual Studio。

    > [!NOTE]
    > 工具箱只能显示具有给定名称的一个活动。 如果来自不同程序集的两个活动具有相同的类名称，将显示一个活动。

    > [!NOTE]
    > 在编辑器实例间共享应用程序域；如果使用静态变量，也将在编辑器实例间共享它们。 如果这不是所需的行为，应使用一个服务跟踪变量实例。 有关 [在设计器内使用服务的信息](/dotnet/framework/windows-workflow-foundation/using-the-modelitem-editing-context) ，请参阅使用 ModelItem 编辑上下文。

## <a name="to-add-an-activity-from-within-a-different-project"></a>从另一个项目中添加活动

1. 打开包含至少一个工作流项目（自定义活动库项目或定义自定义活动的另一个工作流项目）的解决方案。

2. 生成这两个项目。 如果生成成功，则显示工具箱中名为""的新类别，该类别中包含自定义 \<*project name*> 活动。

## <a name="to-add-an-activity-to-the-toolbox-from-an-assembly"></a>从程序集中将活动添加到工具箱

1. 打开工作流解决方案。

2. 在"**工具"菜单中**，选择 **"选择工具箱项"。**

3. 在"**选择工具箱项**"对话框中，选择 **"System.Activities 组件**"选项卡，然后单击"浏览"以导航到包含要添加的自定义活动的程序集。

4. 选择程序集，然后单击"确定 **"。** 自定义活动组件将添加到组件列表中并自动处于选中状态。

    1. 单击 **“确定”**，关闭对话框。

5. 若要显示工具箱，请从"视图 **"菜单中** 选择 **"工具箱** "。

6. 自定义活动显示在添加项之前焦点类别下的"工具箱"中。 例如，如果在添加工具箱项之前在"工具箱"中选择了"常规"类别，则活动将显示在"常规"**类别** 下。

## <a name="see-also"></a>请参阅

- [使用工作流设计器](developing-applications-with-the-workflow-designer.md)
