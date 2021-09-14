---
title: 创建&调试SharePoint工作流解决方案
description: 在此演练中，创建和调试SharePoint工作流解决方案。 创建基本顺序工作流模板。 创建工作流活动并处理事件。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665271"
---
# <a name="walkthrough-create-and-debug-a-sharepoint-workflow-solution"></a>演练：创建和调试 SharePoint 工作流解决方案
  本演练演示如何创建基本的顺序工作流模板。 工作流检查共享文档库的属性，以确定是否已审阅文档。 如果已查看文档，则工作流完成。

 本演练演示以下任务：

- 在 中SharePoint列表定义顺序工作流项目 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

- 创建工作流活动。

- 处理工作流活动事件。

> [!NOTE]
> 尽管本演练使用顺序工作流项目，但该过程对于状态机工作流项目是相同的。
>
> 此外，在下列说明中，你的计算机可能会显示Visual Studio用户界面元素的不同名称或位置。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 Microsoft Windows 和 SharePoint 版本。

- Visual Studio。

## <a name="add-properties-to-the-sharepoint-shared-documents-library"></a>将属性添加到SharePoint文档库
 为了跟踪共享文档库中文档的审阅状态，我们将为共享站点上的共享文档创建三SharePoint属性：、 `Status` 和 `Assignee` `Review Comments` 。 我们在共享文档库中 **定义** 这些属性。

#### <a name="to-add-properties-to-the-sharepoint-shared-documents-library"></a>向共享文档库SharePoint属性

1. 在 Web SharePoint打开一个站点，例如 http:// \<system name> /SitePages/Home.aspx。

2. 在"快速启动"栏上，选择"**共享""文档"。**

3. 在 **"** 库工具 **"功能** 区上选择"库"，然后选择功能区上的"创建列"按钮以创建新列。

4. 将列 **设置为"文档** 状态"， ("选项"菜单) ，指定以下三个选项，然后选择"确定 **"** 按钮：

    - **需要评审**

    - **查看完成**

    - **请求的更改**

5. 再创建两列，并将其命名 **为"被分配者"和****"审阅注释"。** 将"被分配者"列类型设置为单行文本，将"审阅注释"列类型设置为多行文本。

## <a name="enable-documents-to-be-edited-without-requiring-a-check-out"></a>使文档无需签出即可编辑
 当无需签出文档即可编辑文档时，可以更轻松地测试工作流模板。下一过程中，将配置SharePoint站点以启用该配置。

#### <a name="to-enable-documents-to-be-edited-without-checking-them-out"></a>在不签出文档的情况下允许编辑文档

1. 在"快速启动"栏上，选择" **共享文档"** 链接。

2. 在"**库工具"** 功能区上，选择"库"选项卡，然后选择"库 **设置按钮以显示**"文档库 **设置页。**

3. 在"**常规设置"** 部分中，选择"版本控制 **设置"链接** 以显示"版本控制 **设置** 页。

4. 验证"需要 **先签出文档才能编辑文档"的设置是否** 为"**否"。** 如果不是，请更改为"否 **"，** 然后选择"确定 **"** 按钮。

5. 关闭浏览器。

## <a name="create-a-sharepoint-sequential-workflow-project"></a>创建SharePoint工作流项目
 顺序工作流是一组按顺序执行的步骤，直到最后一个活动完成。 在此过程中，我们将创建一个将应用于"共享文档"列表的顺序工作流。 工作流向导允许将工作流与站点定义或列表定义关联，并允许您确定工作流何时启动。

#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>创建一个SharePoint工作流项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，选择"**文件**  >    >  **""新建Project** 以显示"新建Project对话框。

3. 在 Visual **C#** SharePoint下展开"Visual Basic"**节点**，然后选择 **"2010"** 节点。

4. 在"**模板"窗格中**，选择SharePoint **2010 Project** 模板。

5. 在" **名称"** 框中，输入 **MySharePointWorkflow，** 然后选择"确定 **"** 按钮。

     将显示 **SharePoint自定义向导**。

6. 在"**指定** 用于调试的站点和安全级别"页中，选择"部署 **为** 场解决方案"选项按钮，然后选择"完成"按钮以接受信任级别和默认站点。

     此步骤将解决方案的信任级别设置为场解决方案，这是工作流项目的唯一可用选项。 有关详细信息，请参阅 [沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 在 **解决方案资源管理器"** 中，选择项目节点，然后在菜单栏上选择  >  **"Project"添加新项"。**

8. 在 **Visual C#** 或 **Visual Basic** 下，展开 **SharePoint节点，** 然后选择 **"2010"** 节点。

9. 在" **模板"窗格中** ，选择"仅场解决方案 (**顺序** 工作流) 模板，然后选择"添加 **"** 按钮。

     将显示 **SharePoint自定义向导**。

10. 在" **指定调试的工作流** 名称"页中，接受 **MySharePointWorkflow - Workflow1** (的默认) 。 保留默认的工作流模板类型值" **列出工作流**"，然后选择"下一步 **"** 按钮。

11. 在 **"是否希望Visual Studio会话中自动** 关联工作流？"页中，选择"下一步"按钮以接受所有默认设置。

     此步骤会自动将工作流与共享文档库关联。

12. 在 **"指定工作流的** 启动条件"页中，保留"希望工作流如何启动 **？"** 部分中选择的默认选项，然后选择"完成 **"** 按钮。

     通过此页可以指定工作流的启动时间。 默认情况下，工作流在用户手动启动工作流SharePoint或创建工作流关联的项时启动。

## <a name="create-workflow-activities"></a>创建工作流活动
 工作流包含一个或多个 *表示* 要执行的操作的活动。 使用工作流设计器排列工作流的活动。 在此过程中，我们将向工作流添加两个活动：HandleExternalEventActivity 和 OnWorkFlowItemChanged。 这些活动监视"共享文档"列表中的 **文档的审阅** 状态

#### <a name="to-create-workflow-activities"></a>创建工作流活动

1. 工作流应显示在工作流设计器中。 如果不是，则打开 中的 **Workflow1.cs** 或 **Workflow1.vb****解决方案资源管理器。**

2. 在设计器中，选择 **OnWorkflowActivated1** 活动。

3. 在"**属性"** 窗口中，输入"已调用"属性旁边的 **"onWorkflowActivated"，** 然后选择 Enter 键。 

     代码编辑器随即打开，名为 onWorkflowActivated 的事件处理程序方法将添加到 Workflow1 代码文件中。

4. 切换回工作流设计器，打开工具箱，然后展开Windows **Workflow v3.0** 节点。

5. 在Windows的"工作流 **v3.0"** 节点中，执行下列步骤集之一：

    1. 打开 While 活动的 **快捷菜单**，然后选择"复制 **"。** 在工作流设计器中，打开 **onWorkflowActivated1** 活动下行的快捷菜单，然后选择"粘贴 **"。**

    2. 将 **While** 活动从 **"工具箱** "拖动到工作流设计器，并将活动连接到 **onWorkflowActivated1** 活动下的行。

6. 选择 **WhileActivity1** 活动。

7. 在" **属性"** 窗口中，将 **"条件"设置为** "代码条件"。

8. 展开"**条件**"属性，输入子"条件"属性 **旁边的"isWorkflowPending"，** 然后选择 Enter 键。 

     代码编辑器随即打开，名为 isWorkflowPending 的方法将添加到 Workflow1 代码文件中。

9. 切换回工作流设计器，打开工具箱，然后展开"SharePoint **工作流"** 节点。

10. 在 **"SharePoint"** 的"工作流"节点中，执行下列步骤集之一：

    - 打开 **OnWorkflowItemChanged 活动的快捷菜单**，然后选择"复制 **"。** 在工作流设计器中，打开 **whileActivity1** 活动内行的快捷菜单，然后选择"粘贴 **"。**

    - 将 **OnWorkflowItemChanged** 活动从"工具箱"拖动到工作流设计器，并将活动连接到 **whileActivity1** 活动内的行。

11. 选择 **onWorkflowItemChanged1** 活动。

12. 在 **"属性** "窗口中，设置属性，如下表所示。

    |Property|值|
    |--------------|-----------|
    |**CorrelationToken**|**workflowToken**|
    |**Invoked**|**onWorkflowItemChanged**|

## <a name="handle-activity-events"></a>处理活动事件
 最后，检查每个活动中文档的状态。 如果已查看文档，则工作流已完成。

#### <a name="to-handle-activity-events"></a>处理活动事件

1. 在 *Workflow1.cs* 或 *Workflow1.vb* 中，将以下字段添加到 类 `Workflow1` 的顶部。 此字段用于活动中，以确定工作流是否已完成。

    ```vb
    Dim workflowPending As Boolean = True
    ```

    ```csharp
    Boolean workflowPending = true;
    ```

2. 将以下方法添加到 `Workflow1` 类。 此方法检查"文档 `Document Status` "列表的 属性的值，以确定文档是否已审阅。 如果 `Document Status` 属性设置为 `Review Complete` ，则 方法 `checkStatus` 将 字段设置为 `workflowPending` **false，** 以指示工作流已准备就绪。

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

3. 将以下代码添加到 `onWorkflowActivated` 和 `onWorkflowItemChanged` 方法以调用 `checkStatus` 方法。 工作流启动时， `onWorkflowActivated` 方法调用 `checkStatus` 方法，以确定是否已审阅文档。 如果尚未查看，则工作流将继续。 保存文档时， `onWorkflowItemChanged` 方法将再次调用 `checkStatus` 方法，以确定文档是否已审阅。 当 `workflowPending` 字段设置为 **true 时**，工作流将继续运行。

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

4. 将以下代码添加到 `isWorkflowPending` 方法以检查属性 `workflowPending` 的状态。 每次保存文档时 **，whileActivity1** 活动都调用 `isWorkflowPending` 方法。 此方法检查 对象的 <xref:System.Workflow.Activities.ConditionalEventArgs.Result%2A> 属性 <xref:System.Workflow.Activities.ConditionalEventArgs> ，以确定 **WhileActivity1** 活动是应继续还是完成。 如果 属性设置为 **true，** 则活动将继续。 否则，活动完成，工作流完成。

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

## <a name="test-the-sharepoint-workflow-template"></a>测试SharePoint模板
 启动调试器时，将工作流模板部署到SharePoint服务器，并关联工作流 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 与"共享 **文档"** 列表。 若要测试工作流，请从"共享文档"列表中的文档 **启动工作流** 的实例。

#### <a name="to-test-the-sharepoint-workflow-template"></a>测试SharePoint模板

1. 在 *Workflow1.cs* 或 *Workflow1.vb* 中，设置 **onWorkflowActivated 方法旁边的断** 点。

2. 选择 **F5** 键以生成并运行解决方案。

     将显示SharePoint站点。

3. 在导航窗格中，SharePoint"**共享文档"** 链接。

4. 在"**共享文档"** 页中，选择"库工具"选项卡上的"文档"链接，然后选择"Upload **文档"** 按钮。

5. 在 **"Upload"对话框中**，选择"浏览"按钮，选择任何文档文件，选择"打开"按钮，然后选择"确定 **"** 按钮。

     这会将所选文档上传到" **共享文档"列表** 并启动工作流。

6. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，验证调试器是否停止在 方法旁边的断 `onWorkflowActivated` 点处。

7. 选择 **F5** 键以继续执行。

8. 可在此处更改文档的设置，但通过选择"保存"按钮将其保留 **为默认值。**

     这会将你返回到 **默认** 登录网站的"共享SharePoint页。

9. 在"**共享文档"** 页中，验证 **"MySharePointWorkflow - Workflow1"** 列下方的值是否设置为"正在进行 **"。** 这表示工作流正在进行，并且文档正在等待审阅。

10. 在" **共享文档"** 页中，选择文档，选择出现的箭头，然后选择"编辑 **属性"** 菜单项。

11. 将 **"文档状态"****设置为"查看完成**"，然后选择"保存 **"** 按钮。

     这会将你返回到 **默认** 登录网站的"共享SharePoint页。

12. 在"**共享文档"** 页中，验证"文档状态"列 **下方的值是否** 设置为"**查看完成"。** 刷新"**共享文档"** 页，并验证 **MySharePointWorkflow - Workflow1** 列下的值是否设置为 **"已完成"。** 这表示工作流已完成，并且文档已审阅。

## <a name="next-steps"></a>后续步骤
 可以从以下主题详细了解如何创建工作流模板：

- 若要详细了解工作流SharePoint，请参阅 SharePoint Foundation[的工作流活动](/previous-versions/office/developer/sharepoint-2010/ms446847(v=office.14))。

- 若要详细了解 Workflow Foundation Windows，请参阅[System.Workflow.Activities 命名空间](/dotnet/api/system.windows.media.color)。

## <a name="see-also"></a>另请参阅
- [创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [SharePoint项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
