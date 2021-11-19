---
title: 定义和使用活动委托
description: 在工作流设计器中，了解 .NET Framework 4.5 如何包含 InvokeDelegate 活动的现成可用的设计器，以便定义和使用活动委托。
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

.NET Framework 4.5 包括用于 <xref:System.Activities.Statements.InvokeDelegate> 活动的现成可用的设计器。 此设计器可用于将委托分配给从 <xref:System.Activities.ActivityDelegate> 派生的活动，例如 <xref:System.Activities.ActivityAction> 或 <xref:System.Activities.ActivityFunc%601>。

## <a name="define-an-activity-delegate"></a>定义活动委托

1. 创建新的“工作流控制台应用程序”项目。

   > [!NOTE]
   > 如果不想查看“工作流”项目模板，请首先安装 Visual Studio 的 Windows Workflow Foundation 组件。 有关详细说明，请参阅[安装 Windows Workflow Foundation](developing-applications-with-the-workflow-designer.md#install-windows-workflow-foundation)。

3. 在“解决方案资源管理器”中右键单击该项目，然后选择“添加” > “新建项”。 选择“工作流”类别，然后选择“活动”项模板。 将新活动命名为 MyForEach.xaml，然后选择“确定”。

   活动将在工作流设计器中打开。

4. 在工作流设计器中，单击“参数”选项卡。

5. 单击 **“创建参数”**。 将新参数命名为 Items。

6. 在“参数类型”列中，选择“[T] 数组”。

7. 在类型浏览器中，选择“对象”，然后选择“确定”。

8. 再次单击“创建参数”。 将新参数命名为 Body。 在新参数的“方向”列中，选择“属性”。

9. 在“参数类型”列中，选择“浏览类型”

10. 在类型浏览器中，在“类型名称”字段中输入 ActivityAction。 在树视图中选择“ActivityAction\<T>”。 在显示的下拉列表中选择“对象”，将类型 ActivityAction\<Object> 分配给参数。

11. 将 <xref:System.Activities.Statements.While> 活动从工具箱的“控制流”部分拖放到设计器图面中。

12. 选择 <xref:System.Activities.Statements.While> 活动，然后选择“变量”选项卡。

13. 选择“创建变量”。 将新变量命名为 Index。

14. 在“变量类型”列中，选择“Int32”。 将“范围”保留为“While”，将“默认值”列保留为空。

15. 将 <xref:System.Activities.Statements.While> 活动的“条件”属性设置为“index < Items.Length;”。

16. 将 <xref:System.Activities.Statements.InvokeDelegate> 活动从工具箱的“基元”部分拖放到 <xref:System.Activities.Statements.While> 活动的“正文”。

17. 在委托下拉列表中选择“正文”。

18. 在 <xref:System.Activities.Statements.InvokeDelegate> 活动的“属性”网格中，单击“委托参数”属性中的“…”按钮。

19. 在命名为“Argument”的参数的“值”列中，输入 Items[Index]。 单击“确定”以关闭“DelegateArguments”对话框。

20. 将 <xref:System.Activities.Statements.Assign> 活动拖到 <xref:System.Activities.Statements.InvokeDelegate> 活动的水平线下。 将创建 <xref:System.Activities.Statements.Assign> 活动，并且将自动创建 <xref:System.Activities.Statements.Sequence> 活动以包含 MyForEach 活动的“正文”部分中的两个活动。 需要序列，因为“正文”部分只能包含一个活动。 自动创建新的 <xref:System.Activities.Statements.Sequence> 活动是 .NET Framework 4.5 的一个新功能。

21. 将 <xref:System.Activities.Statements.Assign> 活动的“到”属性设置为“index”。 将“Assign”活动的“值”属性设置为“index+1”。

    自定义 MyForEach 活动为通过 Items 集合（集合中的值作为活动的输入）传递给它的每个值调用一次任意活动。

## <a name="use-the-custom-activity-in-a-workflow"></a>使用工作流中的自定义活动

1. 按 Ctrl+Shift+B 生成项目。

2. 在“解决方案资源管理器”中，打开设计器中的“Workflow1.xaml”。

3. 将“MyForEach”活动从工具箱拖到设计器图面。 该活动位于工具箱的某个部分，其名称与项目名称相同。

4. 将 MyForEach 活动的“项”属性设置为“new Object[] {1, "abc"}”。

5. 将 <xref:System.Activities.Statements.WriteLine> 活动从工具箱的“基元”部分拖放到 MyForEach 活动的“Delegate:Body”部分。

6. 将 <xref:System.Activities.Statements.WriteLine> 活动的“文本”属性设置为“Argument.ToString()”。

当执行工作流时，控制台将显示以下输出：

1
abc
