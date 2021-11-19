---
title: 定义和使用活动委托
description: 在 工作流设计器中，.NET Framework 4.5 如何包括可用于定义和使用活动委托的 InvokeDelegate 活动的开箱即用设计器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: c68e42ad-3ec0-4c2d-b104-fe36c6d83b5e
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
author: TerryGLee
ms.openlocfilehash: 150b3b3ababe9e559cc8fe07d049509348201f08
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665192"
---
# <a name="how-to-define-and-consume-activity-delegates-in-the-workflow-designer"></a>如何：在工作流设计器中定义和使用活动委托

.NET Framework 4.5 包含活动的开箱即 <xref:System.Activities.Statements.InvokeDelegate> 用设计器。 此设计器可用于将委托分配给从 <xref:System.Activities.ActivityDelegate> 派生的活动，例如 <xref:System.Activities.ActivityAction> 或 <xref:System.Activities.ActivityFunc%601>。

## <a name="define-an-activity-delegate"></a>定义活动委托

1. 创建新的工作流 **控制台应用程序** 项目。

   > [!NOTE]
   > 如果看不到工作流项目模板，请首先安装 Windows **的 Workflow Foundation** Visual Studio。 有关详细说明，请参阅[Install Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)。

3. 右键单击项目中的项目 **，解决方案资源管理器"**  >  **添加新项"。** 选择" **工作流** "类别，然后选择" **活动项"** 模板。 将新活动 **"MyForEach.xaml"** 命名，然后选择"确定 **"。**

   活动将在工作流设计器中打开。

4. 在"工作流设计器"选项卡中，单击 **"参数"** 选项卡。

5. 单击 **“创建参数”**。 将新 **参数命名** Items 。

6. 在"**参数类型"列中**，选择 **"[T] 的数组"。**

7. 在类型浏览器中，选择"**对象"，** 然后选择"确定 **"。**

8. 再次 **单击"创建参数** "。 将新参数命名 **"正文"。** 在新 **参数的"** 方向"列中，选择"属性 **"。**

9. 在"参数类型"列中，选择 **"浏览类型"**

10. 在类型浏览器中，在"**类型名称"字段中****输入 ActivityAction。** 在 **树视图中 \<T> 选择"ActivityAction"。** 在 **出现的** 下拉列表中选择"对象"，将 **ActivityAction \<Object>** 类型分配给参数。

11. 将 <xref:System.Activities.Statements.While> 活动从工具箱的 **"控件Flow** 部分拖动到设计器图面。

12. 选择 <xref:System.Activities.Statements.While> 活动，然后选择" **变量"** 选项卡。

13. 选择"**创建变量"。** 将新 **变量命名索引**。

14. 在"**变量类型"列中**，选择 **"Int32"。** 将" **作用域"** 保留 **为"While"，** 将" **默认"列** 留空。

15. 将活动的 **Condition** 属性 <xref:System.Activities.Statements.While> 设置为对 **Items.Length**<索引。

16. 将 <xref:System.Activities.Statements.InvokeDelegate> 活动从工具箱 **的"基** 元"部分拖到活动的" **正文** <xref:System.Activities.Statements.While> "。

17. 在 **委托** 下拉列表中选择"正文"。

18. 在活动的 **"** 属性" <xref:System.Activities.Statements.InvokeDelegate> 网格中，单击 **"委托** 参数"属性 **中的"..."** 按钮。

19. 在名为 Argument 的参数的 **"** 值" **列中，输入** **Items[Index]**。 单击 **"确定** "关闭 **DelegateArguments** 对话框。

20. 将 <xref:System.Activities.Statements.Assign> 活动拖到 <xref:System.Activities.Statements.InvokeDelegate> 活动的水平线下。 创建活动，并自动创建一个活动，以包含 <xref:System.Activities.Statements.Assign> <xref:System.Activities.Statements.Sequence> **MyForEach** 活动的 **"正文**"部分中的两个活动。 需要序列，因为 **"正文"** 部分只能包含单个活动。 自动创建新活动 <xref:System.Activities.Statements.Sequence> 是 .NET Framework 4.5 的新功能。

21. 将活动的 **To** 属性 <xref:System.Activities.Statements.Assign> 设置为索引。 将 Assign **活动的 Value** **属性设置为****index+1**。

    自定义 **MyForEach** 活动对通过 **Items** 集合传入的每个值调用一次任意活动，集合中的值作为活动的输入。

## <a name="use-the-custom-activity-in-a-workflow"></a>使用工作流中的自定义活动

1. 按 **Ctrl** Shift B + **生成** + **项目**。

2. 在 **解决方案资源管理器** 中，在 **设计器中打开 Workflow1.xaml。**

3. 将 **MyForEach** 活动从工具箱拖动到设计器图面。 活动位于工具箱的一部分，其名称与项目相同。

4. 将 **MyForEach 活动的** **Items** 属性设置为 **新的 Object[] {1， "abc"}**。

5. 将 <xref:System.Activities.Statements.WriteLine> 活动从工具箱 **的"基** 元"部分拖到 **MyForEach 活动的"Delegate：Body"** 部分。 

6. 将 **活动的 Text** 属性 <xref:System.Activities.Statements.WriteLine> 设置为 **Argument.ToString ()**。

执行工作流时，控制台将显示以下输出：

**1** 
**abc**
