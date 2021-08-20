---
title: 演练：导入在窗体中设计的Outlook
description: 了解如何在 Microsoft Outlook 中设计窗体区域，然后使用"新建窗体区域"向导Outlook VSTO窗体区域导入到外接程序项目中。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- importing form regions
- form regions [Office development in Visual Studio], importing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 6182f28e8f18689caf38ca581bf84df26cfe0ce3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122068499"
---
# <a name="walkthrough-import-a-form-region-that-is-designed-in-outlook"></a>演练：导入在窗体中设计的Outlook
  此演练演示如何在 Microsoft Office Outlook 中设计窗体区域，然后通过使用“新建窗体区域”  向导将窗体区域导入 Outlook VSTO 外接程序项目。 通过在 Outlook 中设计窗体区域，可以将本机 Outlook 控件添加到绑定到 Outlook 数据的窗体区域。 导入窗体区域后，可以处理每个控件的事件。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 本演练演示以下任务：

- 使用 Outlook 中的窗体区域设计器来设计窗体区域。

- 向 Outlook VSTO 外接程序项目导入窗体区域。

- 处理窗体区域中的控件的事件。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Outlook_15_short](../vsto/includes/outlook-15-short-md.md)] 或 [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)]。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="design-a-form-region-by-using-the-form-region-designer-in-outlook"></a>使用窗体中的窗体区域设计器设计Outlook
 在此步骤中，将在 Outlook 中设计一个窗体区域。 然后将该窗体区域保存到一个易于查找的位置，以便将其导入 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

 此示例窗体区域可完全代替常用的任务窗体。 它提供了一种方法来跟踪在执行主要任务之前必须完成的所有任务的进度（系统必备任务）。 窗体区域显示系统必备任务列表，并显示列表中每项任务的完成状态。 用户可以将任务添加到列表中，也可以将其删除。 还可以刷新每项任务的完成状态。

### <a name="to-design-a-form-region-by-using-the-form-region-designer-in-outlook"></a>通过使用 Outlook 中的窗体区域设计器来设计窗体区域

1. 启动 Microsoft Office Outlook。

2. 在 Outlook 中，在“开发人员”  选项卡中，单击“设计窗体” 。 有关详细信息，请参阅 [功能区 上的"如何：显示开发人员"选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

3. 在“设计窗体”  框中，单击“任务” ，然后单击“打开” 。

4. 在 Outlook 中，在“开发人员”  选项卡中，在“设计”  组中，单击“新建窗体区域” 。

     随即会打开一个新窗体区域。 如果未出现 **字段选择器** ，请单击“工具”  组中的 **字段选择器** 。

5. 将“主题”  字段和“完成百分比”  字段从 **字段选择器** 拖动到窗体区域。

6. 在“工具”  组中，单击 **控件工具箱** 以打开 **工具箱**。

7. 将控件从 **工具箱** 拖动到窗体区域。 将标签置于“主题”  和“完成百分比”  字段下方。

8. 右击该标签，然后单击“高级属性” 。

9. 在“属性”  窗口中，将“标题”  属性设置为“此任务依赖于以下任务” ，将“宽度”  属性设置为 **200**，然后单击“应用” 。

10. 将 ListBox 控件从 **工具箱** 拖动到窗体区域。 将列表框置于“此任务依赖于以下任务”  标签下方。

11. 选择刚才添加的列表框。

12. 在“属性”  窗口中，将“宽度”  设置为 **300**，然后单击“应用” 。

13. 将控件从 **工具箱** 拖动到窗体区域。 将标签置于列表框下方。

14. 选择刚才添加的标签。

15. 在“属性”  窗口中，将“标题”  属性设置为“选择一项要添加到依赖任务列表中的任务” ，将“宽度”  属性设置为 **200**，然后单击“应用” 。

16. 将 ComboBox 控件从 **工具箱** 拖动到窗体区域。 将组合框置于“选择一项要添加到依赖任务列表中的任务”  标签下方。

17. 选择刚才添加的组合框。

18. 在“属性”  窗口中，将“宽度”  属性设置为 **300**，然后单击“应用” 。

19. 将 CommandButton 控件从 **工具箱** 拖动到窗体区域。 将命令按钮置于组合框旁。

20. 选择刚才添加的命令按钮。

21. 在“属性”  窗口中，将“名称”  设置为 **AddDependentTask**，将“标题”  设置为“添加依赖任务” ，将“宽度”  设置为 **100**，然后单击“应用” 。

22. 在 **字段选择器** 中，单击“新建” 。

23. 在“新建字段”  对话框中，在“名称”  字段中键入 **hiddenField** ，然后单击“确定” 。

24. 将“hiddenField”  字段从 **字段选择器** 拖动到窗体区域。

25. 在“属性”  窗口中，将“可见”  设置为 **0 - False**，然后单击“应用” 。

26. 在 Outlook 中，在“开发人员”  选项卡中，在“设计”  组中，单击“保存”  按钮，然后单击“将窗体区域另存为” 。

     命名窗体区域 **TaskFormRegion** 并将其保存到计算机的本地目录中。

     Outlook将窗体区域保存为 Outlook 窗体存储 (*.ofs)* 文件。 窗体区域以名称 *TaskFormRegion.ofs 保存*。

27. 退出 Outlook。

## <a name="create-a-new-outlook-add-in-project"></a>创建新的Outlook外接程序项目
 在此步骤中，将创建一个 Outlook VSTO 外接程序项目。 在本演练的后面部分，将向项目中导入窗体区域。

### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>创建新的 Outlook VSTO 外接程序项目

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中，创建名为 **TaskAddIn** 的 Outlook VSTO 外接程序项目。

2. 在 **“新建项目”** 对话框中，选择 **“创建解决方案的目录”**。

3. 将项目保存到默认项目目录中。

     有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

## <a name="import-the-form-region"></a>导入窗体区域
 可使用“新建 Outlook 窗体区域”  向导将 Outlook 中设计的窗体区域导入 Outlook VSTO 外接程序项目。

### <a name="to-import-the-form-region-into-the-outlook-vsto-add-in-project"></a>向 Outlook VSTO 外接程序项目导入窗体区域

1. 在 **解决方案资源管理器** 中右击 **TaskAddIn** 项目，指向“添加” ，然后单击“新建项” 。

2. 在“模板”  窗格中，选择“Outlook 窗体区域” ，将文件命名为 **TaskFormRegion**，然后单击“添加” 。

     **NewOutlook 窗体区域向导** 将启动。

3. 在“选择窗体区域的创建方式”  页上单击“导入 Outlook 窗体存储 (.ofs) 文件” ，然后单击“浏览” 。

4. 在“现有 Outlook 窗体区域文件位置”  对话框中，浏览到 *TaskFormRegion.ofs* 的位置，选择 **TaskFormRegion.ofs**，单击“打开” ，然后单击“下一步” 。

5. 在“选择要创建的窗体区域的类型”  页上，单击“全部替换” ，然后单击“下一步” 。

     “全部替换”  窗体区域将替换整个 Outlook 窗体。 有关窗体区域类型的信息，请参阅创建Outlook[区域](../vsto/creating-outlook-form-regions.md)。

6. 在“提供说明性文本并选择显示首选项”  页上，单击“下一步” 。

7. 在“标识将显示此窗体区域的邮件类”  页上的 **哪些自定义邮件类将显示此窗体区域** 字段中，键入 **IPM.Task.TaskFormRegion**，然后单击“完成” 。

     将 *TaskFormRegion.cs* 或 *TaskFormRegion.vb* 文件添加到项目中。

## <a name="handle-the-events-of-controls-on-the-form-region"></a>处理窗体区域上的控件事件
 现在，你的项目中有了窗体区域，可以添加代码来处理添加到 Outlook 中窗体区域的按钮的 `Microsoft.Office.Interop.Outlook.OlkCommandButton.Click` 事件。

 此外，将代码添加到 <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> 事件以在窗体区域出现时更新窗体区域上的控件。

### <a name="to-handle-the-events-of-controls-on-the-form-region"></a>若要处理窗体区域中的控件的事件

1. 在解决方案资源管理器中，右键单击 *"TaskFormRegion.cs"* 或 *"TaskFormRegion.vb"，* 然后单击"**查看代码"。** 

    *TaskFormRegion.cs* 或 *TaskFormRegion.vb* 在代码编辑器中打开。

2. 将以下代码添加到 `TaskFormRegion` 类。 此代码用 Outlook 任务文件夹中每项任务的主题行来填充窗体区域上的组合框。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb" id="Snippet1":::

3. 将以下代码添加到 `TaskFormRegion` 类。 此代码执行以下任务：

   - 通过调用 `FindTaskBySubjectName` 帮助器方法并传递所需任务的主题来找到任务文件夹中的 `Microsoft.Office.Interop.Outlook.TaskItem`。 下一步将添加 `FindTaskBySubjectName` 帮助器方法。

   - 将 `Microsoft.Office.Interop.Outlook.TaskItem.Subject` 和 `Microsoft.Office.Interop.Outlook.TaskItem.PercentComplete` 值添加到依赖任务列表框。

   - 将任务的主题添加到窗体区域中的隐藏字段。 隐藏字段将这些值存储为 Outlook 项目的一部分。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb" id="Snippet2":::

4. 将以下代码添加到 `TaskFormRegion` 类。 此代码提供了之前步骤中所述的帮助器方法 `FindTaskBySubjectName` 。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs" id="Snippet3":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb" id="Snippet3":::

5. 将以下代码添加到 `TaskFormRegion` 类。 此代码执行以下任务：

   - 刷新窗体区域的列表框中每项依赖任务的当前完成状态。

   - 分析隐藏的文本字段，以获取每项依赖任务的主题。 然后，它通过调用帮助程序方法并传递每个任务的主题，在 `Microsoft.Office.Interop.Outlook.TaskItem` *Tasks* `FindTaskBySubjectName` 文件夹中查找每个任务。

   - 将 `Microsoft.Office.Interop.Outlook.TaskItem.Subject` 和 `Microsoft.Office.Interop.Outlook.TaskItem.PercentComplete` 值添加到依赖任务列表框。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb" id="Snippet4":::

6. 将 `TaskFormRegion_FormRegionShowing` 事件处理程序替换为以下代码。 此代码执行以下任务：

   - 出现窗体区域时，用任务主题填充窗体区域中的组合框。

   - 出现窗体区域时调用 `RefreshTaskListBox` 帮助器方法。 从而将显示以前打开项目时已添加到列表框中的任何依赖任务。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb" id="Snippet5":::

## <a name="test-the-outlook-form-region"></a>测试Outlook区域
 若要测试窗体区域，请将任务添加到窗体区域中的系统必备任务列表中。 更新系统必备任务的完成状态，然后查看系统必备任务列表中任务的已更新完成状态。

### <a name="to-test-the-form-region"></a>测试窗体区域

1. 按 **F5** 运行项目。

     Outlook 启动。

2. 在 Outlook 中，在“主页”  选项卡上，单击“新建项” ，然后单击“任务” 。

3. 在任务窗体中，在“主题”  字段中键入“依赖任务”  。

4. 在功能 **区的"** 任务"选项卡上的"操作"组中，单击"保存 **&关闭"。**

5. 在 Outlook 中，在“主页”  选项卡上，依次单击“新建项” 、“更多项” ，然后单击“选择窗体” 。

6. 在“选择窗体”  对话框中，单击“TaskFormRegion” ，然后单击“打开” 。

     随即显示“TaskFormRegion”  窗体区域。 此窗体将替换整个任务窗体。 用任务文件夹中的其他任务填充“选择一项要添加到依赖任务列表中的任务”  组合框。

7. 在任务窗体中，在“主题”  字段中键入“主要任务” 。

8. 在“选择一项要添加到依赖任务列表中的任务”  组合框中，选择“依赖任务” ，然后单击“添加依赖任务” 。

     “此任务依赖于以下任务” 列表框中出现“0% 完成 -- 依赖任务”  。 这就说明你已成功处理该按钮的 `Microsoft.Office.Interop.Outlook.OlkCommandButton.Click` 事件。

9. 保存并关闭“主要任务”  项目。

10. 在 Outlook 中重新打开依赖任务项。

11. 在依赖任务窗体中，将“完成百分比”  字段改为 **50%**。

12. 在"**依赖任务**"功能区的"任务"选项卡上的"操作"**组中，单击**"保存&**关闭"。**

13. 在 Outlook 中重新打开“主要任务”  项。

     “此任务依赖于以下任务” 列表框中出现“50% 完成 -- 依赖任务”  。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何自定义 Outlook 应用程序 UI 的详细信息：

- 若要详细了解如何将托管控件拖动到可视化设计器上来设计窗体区域的外观，请参阅演练：设计Outlook[区域](../vsto/walkthrough-designing-an-outlook-form-region.md)。

- 若要了解如何自定义项目的功能区Outlook，请参阅[为自定义功能区Outlook。](../vsto/customizing-a-ribbon-for-outlook.md)

- 若要详细了解如何将自定义任务窗格添加到Outlook，请参阅[自定义任务窗格](../vsto/custom-task-panes.md)。

## <a name="see-also"></a>请参阅
- [运行时访问窗体区域](../vsto/accessing-a-form-region-at-run-time.md)
- [创建Outlook窗体区域](../vsto/creating-outlook-form-regions.md)
- [创建表单Outlook指南](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [演练：设计Outlook区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [如何：将窗体区域添加到Outlook外接程序项目](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [将窗体区域与Outlook类关联](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
- [窗体Outlook中的自定义操作](../vsto/custom-actions-in-outlook-form-regions.md)
- [如何：Outlook窗体区域](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)
