---
title: 创建和调试 SharePoint 工作流解决方案
description: 在本演练中，创建和调试 SharePoint 工作流解决方案。 创建基本的顺序工作流模板。 创建工作流活动并处理事件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.Workflow.WorkflowConditions
- VS.SharePointTools.Workflow.WorkflowList
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: e96987734a3414f0e55f75fb221124de79573acd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665271"
---
# <a name="walkthrough-create-and-debug-a-sharepoint-workflow-solution"></a>演练：创建和调试 SharePoint 工作流解决方案
  本演练演示了如何创建基本的顺序工作流模板。 工作流会检查共享文档库的属性，以确定文档是否已被审阅。 如果文档已被审阅，则工作流将完成。

 本演练演示以下任务：

- 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中创建 SharePoint 列表定义顺序工作流项目。

- 创建工作流活动。

- 处理工作流活动事件。

> [!NOTE]
> 虽然本演练使用顺序工作流项目，但该过程对状态机工作流项目而言是相同的。
>
> 此外，以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 Microsoft Windows 和 SharePoint 版本。

- Visual Studio。

## <a name="add-properties-to-the-sharepoint-shared-documents-library"></a>将属性添加到 SharePoint 共享文档库
 为了跟踪共享文档库中文档的审阅状态，我们将在 SharePoint 网站上为共享文档创建三个新属性：`Status`、`Assignee` 和 `Review Comments`。 我们将这些属性定义在共享文档库中。

#### <a name="to-add-properties-to-the-sharepoint-shared-documents-library"></a>将属性添加到 SharePoint 共享文档库

1. 在 Web 浏览器中打开 SharePoint 网站，如 http://\<system name>/SitePages/Home.aspx。

2. 在快速启动栏上，选择“SharedDocuments”。

3. 在“库工具”功能区上选择“库”，然后选择功能区中的“创建列”按钮，以创建新列。

4. 将列命名为“文档状态”，将其“类型”设置为“选择(可供选择的菜单)”，指定以下三个选项，然后选择“确定”按钮：

    - 需要审阅

    - 审阅完成

    - 已请求更改

5. 再创建两列，将其分别命名为“代理人”和“查看注释”。 将“代理人”列类型设置为单行文本，将“查看注释”列类型设置为多行文本。

## <a name="enable-documents-to-be-edited-without-requiring-a-check-out"></a>无需签出文档即可对其进行编辑
 如果无需签出文档即可对其进行编辑，就可以更轻松地测试工作流模板。在下一过程中，你将配置 SharePoint 站点以启用该功能。

#### <a name="to-enable-documents-to-be-edited-without-checking-them-out"></a>无需签出文档即可对其进行编辑

1. 在快速启动栏上，选择“共享文档”链接。

2. 在“库工具”功能区上，选择“库”选项卡，然后选择“库设置”按钮以显示“文档库设置”页。

3. 在“常规设置”部分中，选择“版本控制设置”链接，以显示“版本控制设置”页。

4. 确认“要求必须在编辑文件前将其签出”的设置为“否”。 如果不是，请将其更改为“否”，然后选择“确定”按钮 。

5. 关闭浏览器。

## <a name="create-a-sharepoint-sequential-workflow-project"></a>创建 SharePoint 顺序工作流项目
 顺序工作流是一组步骤，这些步骤按顺序执行，直到最后一个活动完成。 在此过程中，我们将创建一个将应用于共享文档列表的顺序工作流。 工作流向导允许你将工作流与网站定义或列表定义关联起来，并使你能够确定工作流的启动时间。

#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>创建 SharePoint 顺序工作流项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，选择“文件” > “新建” > “项目”，打开“新建项目”对话框。

3. 展开“Visual C#”或“Visual Basic”下的“SharePoint”节点，然后选择“2010”节点   。

4. 在“模板”窗格中，选择“SharePoint 2010 项目”模板 。

5. 在“名称”框中，输入“MySharePointWorkflow”，然后选择“确定”按钮  。

     “SharePoint 自定义向导”随即出现。

6. 在“为调试指定站点和安全级别”页上，选择“部署为场解决方案”选项按钮，然后选择“完成”按钮以接受信任级别和默认站点  。

     此步骤将解决方案的信任级别设置为场解决方案，这是工作流项目的唯一可用选项。 有关详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 在解决方案资源管理器中，选择项目节点，然后在菜单栏上选择“项目” > “添加新项”  。

8. 在 Visual C# 或 Visual Basic 下，展开 SharePoint 节点，然后选择“2010”节点   。

9. 在“模板”窗格中，选择“顺序工作流(仅场解决方案)”模板，然后选择“添加”按钮  。

     “SharePoint 自定义向导”随即出现。

10. 在“指定用于调试的工作流名称”页上，接受默认名称 (MySharePointWorkflow - Workflow1)。 保留默认工作流模板类型值“列表工作流”，然后选择“下一步”按钮。

11. 在“是否希望 Visual Studio 在调试会话中自动关联工作流?”页上，选择“下一步”按钮以接受所有默认设置。

     此步骤会自动将工作流与共享文档库相关联。

12. 在“指定工作流的启动方式的条件”页上，保留“你希望工作流如何启动?”部分中选择的默认选项，然后选择“完成”按钮。

     此页面允许你指定工作流的启动时间。 默认情况下，当用户在 SharePoint 中手动启动工作流或创建与工作流关联的项时，工作流将启动。

## <a name="create-workflow-activities"></a>创建工作流活动
 工作流包含一个或多个表示要执行的操作的活动。 使用工作流设计器可以为工作流安排活动。 在此过程中，我们将向工作流添加两个活动：HandleExternalEventActivity 和 OnWorkFlowItemChanged。 这些活动用于监视“共享文档”列表中文档的审阅状态

#### <a name="to-create-workflow-activities"></a>创建工作流活动

1. 工作流应显示在工作流设计器中。 如果不是，则在“解决方案资源管理器”中打开“Workflow1.cs”或“Workflow1.vb”。

2. 在设计器中，选择“OnWorkflowActivated1”活动。

3. 在“属性”窗口中，在“调用”属性旁输入“onWorkflowActivated”，然后选择 Enter 键。

     将打开代码编辑器，并将名为 onWorkflowActivated 的事件处理程序方法添加到 Workflow1 代码文件中。

4. 切换回工作流设计器，打开工具箱，然后展开“Windows Workflow v3.0”节点。

5. 在“工具箱”的“Windows Workflow v3.0”节点中，执行以下一组步骤 ：

    1. 打开“While”活动的快捷菜单，然后选择“复制” 。 在工作流设计器中，打开“onWorkflowActivated1”活动下方的行的快捷菜单，然后选择“粘贴” 。

    2. 将“工具箱”的“While”活动拖动到工作流设计器，并将活动连接到“onWorkflowActivated1”活动下方的行  。

6. 选择“WhileActivity1”活动。

7. 在“属性”窗口中，将“条件”设置为代码条件 。

8. 展开“条件”属性，在“条件”子属性旁输入“isWorkflowPending”，然后选择 Enter 键。

     将打开代码编辑器，并将名为 isWorkflowPending 的方法添加到 Workflow1 代码文件中。

9. 切换回工作流设计器，打开工具箱，然后展开“SharePoint 工作流”节点。

10. 在“工具箱”的“SharePoint 工作流”节点中，执行以下一组步骤 ：

    - 打开“OnWorkflowItemChanged”活动的快捷菜单，然后选择“复制” 。 在工作流设计器中，打开“whileActivity1”活动内行的快捷菜单，然后选择“粘贴” 。

    - 将“工具箱”的“OnWorkflowItemChanged”活动拖动到工作流设计器，并将活动连接到“whileActivity1”活动内的行  。

11. 选择“onWorkflowItemChanged1”活动。

12. 在“属性”窗口中，如下表中所示设置属性。

    |属性|值|
    |--------------|-----------|
    |CorrelationToken|workflowToken|
    |**Invoked**|onWorkflowItemChanged|

## <a name="handle-activity-events"></a>处理活动事件
 最后，检查每个活动中文档的状态。 如果文档已被审阅，则工作流将完成。

#### <a name="to-handle-activity-events"></a>处理活动事件

1. 在“Workflow1.cs”或“Workflow1.vb”中，将以下字段添加到 `Workflow1` 类的顶部。 此字段用于活动中，以确定工作流是否已完成。

    ```vb
    Dim workflowPending As Boolean = True
    ```

    ```csharp
    Boolean workflowPending = true;
    ```

2. 将以下方法添加到 `Workflow1` 类。 此方法检查“文档”列表的 `Document Status` 属性的值，以确定文档是否已被审阅。 如果 `Document Status` 属性设置为 `Review Complete`，则 `checkStatus` 方法将 `workflowPending` 字段设置为 false，以指示工作流已准备就绪。

    ```vb
    Private Sub checkStatus()
        If CStr(workflowProperties.Item("Document Status")) = "Review Complete" Then
            workflowPending = False
        End If
    End Sub
    ```

    ```csharp
    private void checkStatus()
    {
        if ((string)workflowProperties.Item["Document Status"] == "Review Complete")
        workflowPending = false;
    }
    ```

3. 将以下代码添加到 `onWorkflowActivated` 和 `onWorkflowItemChanged` 方法，以调用 `checkStatus` 方法。 工作流启动时，`onWorkflowActivated` 方法会调用 `checkStatus` 方法，以确定该文档是否已被审阅。 如果尚未审阅，则工作流将继续。 保存文档时，`onWorkflowItemChanged` 方法会再次调用 `checkStatus` 方法，以确定该文档是否已被审阅。 当 `workflowPending` 字段设置为 true 时，工作流将继续运行。

    ```vb
    Private Sub onWorkflowActivated(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ExternalDataEventArgs)
        checkStatus()
    End Sub

    Private Sub onWorkflowItemChanged(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ExternalDataEventArgs)
        checkStatus()
    End Sub
    ```

    ```csharp
    private void onWorkflowActivated(object sender, ExternalDataEventArgs e)
    {
        // Check the status.
        checkStatus();
    }

    private void onWorkflowItemChanged(object sender, ExternalDataEventArgs e)
    {
        // Check the status.
        checkStatus();
    }
    ```

4. 将以下代码添加到 `isWorkflowPending` 方法以检查属性 `workflowPending` 的状态。 每次保存文档时，whileActivity1 活动都会调用 `isWorkflowPending` 方法。 此方法检查 <xref:System.Workflow.Activities.ConditionalEventArgs> 对象的 <xref:System.Workflow.Activities.ConditionalEventArgs.Result%2A> 属性，以确定 WhileActivity1 活动是应继续还是完成。 如果将该属性设置为 true，则活动将继续。 否则，活动将完成，工作流也将完成。

    ```vb
    Private Sub isWorkflowPending(ByVal sender As System.Object, ByVal e As System.Workflow.Activities.ConditionalEventArgs)
        e.Result = workflowPending
    End Sub
    ```

    ```csharp
    private void isWorkflowPending(object sender, ConditionalEventArgs e)
    {
        e.Result = workflowPending;
    }
    ```

5. 保存项目。

## <a name="test-the-sharepoint-workflow-template"></a>测试 SharePoint 工作流模板
 启动调试器时，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将工作流模板部署到 SharePoint 服务器，并关联工作流与“共享文档”列表。 若要测试工作流，请从“共享文档”列表中的文档启动工作流的实例。

#### <a name="to-test-the-sharepoint-workflow-template"></a>测试 SharePoint 工作流模板

1. 在“Workflow1.cs”或“Workflow1.vb”中，将断点设置在“onWorkflowActivated”方法旁。

2. 选择 F5 键生成并运行解决方案。

     SharePoint 网站随即出现。

3. 在 SharePoint 的导航窗格中选择“共享文档”链接。

4. 在“共享文档”页中，在“库工具”选项卡上选择“文档”链接，然后选择“上传文档”按钮。

5. 在“上传文档”对话框中，依次选择“浏览”按钮、任何文档文件、“打开”按钮和“确定”按钮。

     这会将所选文档上传到“共享文档”列表并启动工作流。

6. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，确认调试程序在 `onWorkflowActivated` 方法旁的断点处停止。

7. 按 F5 键继续执行。

8. 可在此处更改文档的设置，但通过选择“保存”按钮暂时将其保留为默认值。

     这会将你返回到默认 SharePoint 网站的“共享文档”页。

9. 在“共享文档”页中，确认“MySharePointWorkflow - Workflow1”列下方的值是否设置为“正在进行”。 这表示工作流正在进行中，并且文档正在等待审阅。

10. 在“共享文档”页中，依次选择文档、出现的箭头，然后选择“编辑属性”菜单项。

11. 将“文档状态”设置为“审阅完成”，然后选择“保存”按钮。

     这会将你返回到默认 SharePoint 网站的“共享文档”页。

12. 在“共享文档”页中，确认“文档状态”列下方的值是否设置为“审阅完成”。 刷新“共享文档”页，并确认“MySharePointWorkflow - Workflow1”列下方的值是否设置为“已完成”。 这表示工作流已完成，并且文档已被审阅。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何创建工作流模板的详细信息：

- 若要详细了解 SharePoint 工作流活动，请参阅 [SharePoint Foundation 的工作流活动](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14))。

- 若要详细了解 Windows Workflow Foundation 活动，请参阅 [System.Workflow.Activities 命名空间](/dotnet/api/system.windows.media.color)。

## <a name="see-also"></a>另请参阅
- [创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
