---
title: 使用关联和启动窗体创建工作流
description: 在本 SharePoint 演练中，创建一个基本的顺序工作流程，其中包含关联和启动窗体的使用。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- SharePoint development in Visual Studio, workflow association forms
- workflows [SharePoint development in Visual Studio]
- association forms [SharePoint development in Visual Studio]
- initiation forms [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, workflow initiation forms
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 2f3852452d163f14e93b73e7fd894759f7aa0197
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600608"
---
# <a name="walkthrough-create-a-workflow-with-association-and-initiation-forms"></a>演练：使用关联和启动窗体创建工作流
  本演练演示了如何创建一个基本的顺序工作流程，其中包含关联和启动窗体的使用。 这些是 ASPX 窗体，当工作流首次由 SharePoint 管理员关联时（关联窗体），以及当工作流由用户启动时（启动窗体），这些窗体允许将参数添加到工作流中。

 本演练概述了这样一种情况：用户想要为满足以下要求的支出报表创建审批工作流：

- 当工作流与列表相关联时，系统会提示管理员输入关联窗体，在该窗体中输入支出报表的美元限制。

- 员工将其支出报表上传到“共享文档”列表，启动工作流，然后在工作流启动窗体中输入总支出。

- 如果员工支出报表总计超出了管理员的预定义限制，则会为该员工的经理创建一项任务以审批该支出报表。 但是，如果员工的支出报表总计小于或等于支出限制，则自动审批的消息将写入工作流的历史记录列表。

  本演练演示以下任务：

- 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中创建 SharePoint 列表定义顺序工作流项目。

- 创建工作流计划。

- 处理工作流活动事件。

- 创建工作流关联和启动窗体。

- 关联工作流。

- 手动启动工作流。

> [!NOTE]
> 虽然本演练使用顺序工作流项目，但该过程对状态机工作流而言是一样的。
>
> 此外，以下说明中的某些 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所拥有的 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 版本和所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 受支持的 [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 和 SharePoint 版本。

- Visual Studio。

## <a name="create-a-sharepoint-sequential-workflow-project"></a>创建 SharePoint 顺序工作流项目
 首先，在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中创建一个顺序工作流项目。 顺序工作流是一组步骤，这些步骤按顺序执行，直到最后一个活动完成。 在此过程中，将创建一个应用于 SharePoint 中“共享文档”列表的顺序工作流。 工作流向导允许你将工作流与网站或列表定义关联起来，并使你能够确定工作流的启动时间。

#### <a name="to-create-a-sharepoint-sequential-workflow-project"></a>创建 SharePoint 顺序工作流项目

1. 在菜单栏上，选择“文件” > “新建” > “项目”，以显示“新建项目”对话框。

2. 展开“Visual C#”或“Visual Basic”下的“SharePoint”节点，然后选择“2010”节点。

3. 在“模板”窗格中，选择“SharePoint 2010 项目” 项目模板。

4. 在“名称”框中，输入“ExpenseReport”，然后选择“确定”按钮。

     “SharePoint 自定义向导”随即出现。

5. 在“为调试指定站点和安全级别”页上，选择“部署为场解决方案”选项按钮，然后选择“完成”按钮以接受信任级别和默认站点  。

     此步骤还将解决方案的信任级别设置为场解决方案，这是工作流项目的唯一可用选项。

6. 在 **“解决方案资源管理器”** 中，选择项目节点。

7. 在菜单栏上，依次选择“项目” > “添加新项”。

8. 展开“Visual C#”或“Visual Basic”下的“SharePoint”节点，然后选择“2010”节点   。

9. 在“模板”窗格中，选择“顺序工作流(仅场解决方案)”模板，然后选择“添加”按钮  。

     “SharePoint 自定义向导”随即出现。

10. 在“指定用于调试的工作流名称”页上，接受默认名称 (ExpenseReport - Workflow1)。 保留默认工作流模板类型值（列表工作流）。 选择“下一步”按钮  。

11. 在“是否希望 Visual Studio 在调试会话中自动关联工作流?”页上，清除自动关联工作流模板的框（如果已选中）。

     此步骤允许稍后以手动方式将工作流与“共享文档”列表相关联，这将显示关联窗体。

12. 选择 **“完成”** 按钮。

## <a name="add-an-association-form-to-the-workflow"></a>向工作流添加关联窗体
 下一步，创建一个 .ASPX 关联窗体，当 SharePoint 管理员首次将工作流与支出报表文档相关联时，该窗体将出现。

#### <a name="to-add-an-association-form-to-the-workflow"></a>向工作流添加关联窗体

1. 在“解决方案资源管理器”中选择“Workflow1” 节点。

2. 在菜单栏中，依次选择“项目” > “添加新项”以显示“添加新项”对话框。

3. 在对话框树状视图中，展开“Visual C#”或“Visual Basic”（具体取决于你的项目语言），展开“SharePoint”节点，然后选择“2010”节点   。

4. 在模板列表中，选择“工作流关联窗体”模板。

5. 在“名称”文本框中，输入“ExpenseReportAssocForm.aspx” 。

6. 选择“添加”按钮，将窗体添加到项目中。

## <a name="designing-and-coding-the-association-form"></a>设计关联窗体并对其进行编码
 在此过程中，通过向关联窗体添加控件和代码来向其引入功能。

#### <a name="to-design-and-code-the-association-form"></a>设计关联窗体并对其进行编码

1. 在关联窗体 (ExpenseReportAssocForm.aspx) 中，找到具有 `ID="Main"` 的 `asp:Content` 元素。

2. 直接在此 content 元素中的第一行之后添加以下代码，以创建提示输入支出审批限制 (AutoApproveLimit) 的标签和文本框：

    ```aspx-csharp
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />

    <asp:TextBox ID="AutoApproveLimit" runat="server" />
    <br /><br />
    ```

3. 展开“解决方案资源管理器”中的“ExpenseReportAssocForm.aspx” 文件以显示其依赖文件。

    > [!NOTE]
    > 如果你的项目处于 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 中，则必须选择“查看所有文件”按钮以执行此步骤。

4. 打开 ExpenseReportAssocForm.aspx 文件的快捷菜单，然后选择“查看代码”。

5. 将 `GetAssociationData` 方法替换为：

    ```vb
    Private Function GetAssociationData() As String
        ' TODO: Return a string that contains the association data that
        ' will be passed to the workflow. Typically, this is in XML
        ' format.
        Return Me.AutoApproveLimit.Text
    End Function
    ```

    ```csharp
    private string GetAssociationData()
    {
        // TODO: Return a string that contains the association data that
        // will be passed to the workflow. Typically, this is in XML
        // format.
        return this.AutoApproveLimit.Text;
    }
    ```

## <a name="add-an-initiation-form-to-the-workflow"></a>向工作流添加启动窗体
 下一步，创建当用户根据其支出报表运行工作流时显示的启动窗体。

#### <a name="to-create-an-initiation-form"></a>创建启动窗体

1. 在“解决方案资源管理器”中选择“Workflow1” 节点。

2. 在菜单栏中，依次选择“项目” > “添加新项”以显示“添加新项”对话框。

3. 在对话框树状视图中，展开“Visual C#”或“Visual Basic”（具体取决于你的项目语言），展开“SharePoint”节点，然后选择“2010”节点   。

4. 在模板列表中，选择“工作流启动窗体”模板。

5. 在“名称”文本框中，输入“ExpenseReportInitForm.aspx” 。

6. 选择“添加”按钮，将窗体添加到项目中。

## <a name="designing-and-coding-the-initiation-form"></a>设计启动窗体并对其进行编码
 下一步，通过向启动窗体添加控件和代码来向其引入功能。

#### <a name="to-code-the-initiation-form"></a>对启动窗体进行编码

1. 在启动窗体 (ExpenseReportInitForm.aspx) 中，找到具有 `ID="Main"` 的 `asp:Content` 元素。

2. 直接在此 content 元素中的第一行之后添加以下代码，以创建一个标签和文本框，其中显示在关联窗体中输入的支出审批限制 (AutoApproveLimit)，另一个标签和文本框提示总支出 (ExpenseTotal)：

    ```aspx-csharp
    <asp:Label ID="lblAutoApproveLimit" Text="Auto Approval Limit:" runat="server" />

    <asp:TextBox ID="AutoApproveLimit" ReadOnly="true" runat="server" />
    <br /><br />
    <asp:Label ID="lblExpenseTotal" Text="Expense Total:" runat="server" />

    <asp:TextBox ID="ExpenseTotal" runat="server" />
    <br /><br />
    ```

3. 展开“解决方案资源管理器”中的“ExpenseReportInitForm.aspx” 文件以显示其依赖文件。

4. 打开 ExpenseReportInitForm.aspx 文件的快捷菜单，然后选择“查看代码”。

5. 将 `Page_Load` 方法替换为以下示例：

    ```vb
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As
      EventArgs) Handles Me.Load
        InitializeParams()
        Me.AutoApproveLimit.Text = workflowList.WorkflowAssociations(New
          Guid(associationGuid)).AssociationData
        ' Optionally, add code here to pre-populate your form fields.
    End Sub
    ```

    ```csharp
    protected void Page_Load(object sender, EventArgs e)
    {
        InitializeParams();
        this.AutoApproveLimit.Text =
          workflowList.WorkflowAssociations[new
          Guid(associationGuid)].AssociationData;
    }
    ```

6. 将 `GetInitiationData` 方法替换为以下示例：

    ```vb
    ' This method is called when the user clicks the button to start the workflow.
    Private Function GetInitiationData() As String
        Return Me.ExpenseTotal.Text
        ' TODO: Return a string that contains the initiation data that
        ' will be passed to the workflow. Typically, this is in XML
        ' format.
        Return String.Empty
    End Function
    ```

    ```csharp
    // This method is called when the user clicks the button to start the workflow.
    private string GetInitiationData()
    {
        // TODO: Return a string that contains the initiation data that
        // will be passed to the workflow. Typically, this is in XML
        // format.
        return this.ExpenseTotal.Text;
    }
    ```

## <a name="cutomize-the-workflow"></a>自定义工作流
 下一步，自定义工作流。 稍后，将两个窗体关联到工作流。

#### <a name="to-customize-the-workflow"></a>自定义工作流

1. 通过在项目中打开 Workflow1，在工作流设计器中显示工作流。

2. 在“工具箱”中，展开“Windows 工作流 v3.0”节点并查找“IfElse”活动。

3. 通过执行以下步骤之一将此活动添加到工作流中：

    - 打开“IfElse”活动的快捷菜单，选择“复制”，打开工作流设计器中“onWorkflowActivated1”活动下行的快捷菜单，然后选择“粘贴”。

    - 在工作流设计器中，从“工具箱”拖动“IfElse”活动，再将活动连接到“onWorkflowActivated1”活动下方的行  。

4. 在“工具箱”中，展开“SharePoint 工作流”节点并查找“CreateTask”活动 。

5. 通过执行以下步骤之一将此活动添加到工作流中：

    - 打开“CreateTask”活动的快捷菜单，选择“复制”，打开工作流设计器中“IfElseActivity1”内两个“在此处放置活动”区域之一的快捷菜单，然后选择“粘贴”。

    - 将“CreateTask”活动从“工具箱”拖放到“IfElseActivity1”内两个“在此处放置活动”区域之一。

6. 在“属性”窗口中，为“CorrelationToken”属性输入“taskToken”的属性值。

7. 展开“CorrelationToken”属性，方法是选择它旁边的加号 (![树状视图加号](../sharepoint/media/plus.gif "TreeView 加号"))。

8. 选择“OwnerActivityName”子属性上的下拉箭头，然后设置“Workflow1”值。

9. 选择“TaskId”属性，然后选择省略号 (![ASP.NET 移动设计器中的省略号](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")) 按钮以显示“绑定属性”对话框。

10. 依次选择“绑定到新成员”选项卡、“创建字段”选项按钮和“确定”  按钮。

11. 选择“TaskProperties”属性，然后选择省略号 (![ASP.NET 移动设计器中的省略号](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")) 按钮以显示“绑定属性”对话框。

12. 依次选择“绑定到新成员”选项卡、“创建字段”选项按钮和“确定”  按钮。

13. 在“工具箱”中，展开“SharePoint 工作流”节点并查找“LogToHistoryListActivity”活动  。

14. 通过执行以下步骤之一将此活动添加到工作流中：

    - 打开“LogToHistoryListActivity”活动的快捷菜单，选择“复制”，打开工作流设计器中“IfElseActivity1”内另一个“在此处放置活动”区域的快捷菜单，然后选择“粘贴”。

    - 从“工具箱”拖动“LogToHistoryListActivity”活动，然后将其放到“IfElseActivity1”内另一个“在此处放置活动”区域。

## <a name="add-code-to-the-workflow"></a>将代码添加到工作流
 下一步，将代码添加到工作流，使其能够正常工作。

#### <a name="to-add-code-to-the-workflow"></a>将代码添加到工作流

1. 在工作流设计器中，打开“createTask1”活动的快捷菜单，然后选择“查看代码” 。

2. 添加下面的方法：

    ```vb
    Private Sub createTask1_MethodInvoking(ByVal sender As
      System.Object, ByVal e As System.EventArgs)
        createTask1_TaskId1 = Guid.NewGuid
        createTask1_TaskProperties1.AssignedTo = "somedomain\\someuser"
        createTask1_TaskProperties1.Description = "Please approve the
          expense report"
        createTask1_TaskProperties1.Title = "Expense Report Approval
          Needed"
    End Sub
    ```

    ```csharp
    private void createTask1_MethodInvoking(object sender, EventArgs e)
    {
        createTask1_TaskId1 = Guid.NewGuid();
        createTask1_TaskProperties1.AssignedTo = "somedomain\\someuser";
        createTask1_TaskProperties1.Description = "Please approve the
          expense report";
        createTask1_TaskProperties1.Title = "Expense Report Approval
          Needed";
    }
    ```

    > [!NOTE]
    > 在代码中，将 `somedomain\\someuser` 替换为将为其创建任务的域和用户名，例如“`Office\\JoeSch`”。 为了进行测试，最简单的方法是使用开发所用的帐户。

3. 在 `MethodInvoking` 方法下添加以下示例：

    ```vb
    Private Sub checkApprovalNeeded(ByVal sender As Object, ByVal e As
      ConditionalEventArgs)
        Dim approval As Boolean = False
        If (Convert.ToInt32(workflowProperties.InitiationData) >
          Convert.ToInt32(workflowProperties.AssociationData)) Then
            approval = True
        End If
        e.Result = approval
    End Sub
    ```

    ```csharp
    private void checkApprovalNeeded(object sender, ConditionalEventArgs
      e)
    {
        bool approval = false;
        if (Convert.ToInt32(workflowProperties.InitiationData) >
          Convert.ToInt32(workflowProperties.AssociationData))
        {
            approval = true;
        }
        e.Result = approval;
    }
    ```

4. 在工作流设计器中，选择“ifElseBranchActivity1”活动。

5. 在“属性”窗口中，选择“Condition”属性的下拉箭头，然后设置“代码条件”值。

6. 通过选择“Condition”属性旁边的加号 (![树状视图加号](../sharepoint/media/plus.gif "TreeView 加号")) 将“Condition”属性展开，然后将其值设置为“checkApprovalNeeded”。

7. 在工作流设计器中，打开“logToHistoryListActivity1”活动的快捷菜单，然后选择“生成处理程序”以为 `MethodInvoking` 事件生成空方法。

8. 将 `MethodInvoking` 代码替换为以下内容：

    ```vb
    Private Sub logToHistoryListActivity1_MethodInvoking(ByVal sender As
      System.Object, ByVal e As System.EventArgs)
        Me.logToHistoryListActivity1.HistoryOutcome = ("Expense was auto
          approved for " + workflowProperties.InitiationData)
    End Sub
    ```

    ```csharp
    private void logToHistoryListActivity1_MethodInvoking(object sender,
      EventArgs e)
    {
        this.logToHistoryListActivity1.HistoryOutcome = "Expense was
          auto approved for " + workflowProperties.InitiationData;
    }
    ```

9. 选择 F5 键以调试程序。

     此操作会编译应用程序、对其进行打包、部署并激活其功能，回收 [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] 应用程序池，然后在“站点 Url”属性中指定的位置启动浏览器。

## <a name="associating-the-workflow-to-the-documents-list"></a>将工作流关联到文档列表
 下一步，通过将工作流与 SharePoint 站点上的 SharedDocuments 列表相关联来显示工作流关联窗体。

#### <a name="to-associate-the-workflow"></a>关联工作流

1. 在快速启动栏上，选择“共享文档”链接。

2. 在“库工具”选项卡上，选择“库”链接，然后选择“库设置”功能区按钮。

3. 在“权限和管理”部分中，选择“工作流设置”链接，然后选择“工作流”页上的“添加工作流”链接。

4. 在“工作流设置”页的顶部列表中，选择“ExpenseReport - Workflow1”模板。

5. 在下一个字段中，输入“ExpenseReportWorkflow”，然后选择“下一步”按钮。

     这会将工作流与“共享文档”列表相关联，并显示工作流关联窗体。

6. 在“自动审批限制”文本框中，输入“1200”，然后选择“关联工作流”按钮  。

## <a name="start-the-workflow"></a>启动工作流
 下一步，将工作流关联到“共享文档”列表中的一个文档，以显示工作流启动窗体。

#### <a name="to-start-the-workflow"></a>启动工作流

1. 在“SharePoint”页上，选择“主页”按钮。

2. 在快速启动栏上，选择“共享文档”链接以显示“共享文档”列表。

3. 在页面顶部的“库工具”选项卡上，选择“文档”链接，然后在功能区上选择“上传文档”按钮，以将新文档上传到“共享文档”列表   。

4. 在“上传文档”对话框中，依次选择“浏览”按钮、任何文档文件、“打开”按钮和“确定”按钮。

     可在此对话框中更改文档的设置，但通过选择“保存”按钮将其保留为默认值。

5. 依次选择上传的文档，显示的下拉箭头和“工作流”项。

6. 选择 ExpenseReportWorkflow 旁的图像。

     这将显示工作流启动窗体。 （请注意，“自动审批限制”框中显示的值为只读状态，因为它是在关联窗体中输入的。）

7. 在“总支出”文本框中，输入“1600”，然后选择“启动工作流”按钮  。

     这将再次显示“共享文档”列表。 名为“ExpenseReportWorkflow”且值为“已完成”的新列被添加到工作流刚启动的项中。

8. 选择上传的文档旁边的下拉箭头，然后选择“工作流”项，以显示工作流状态页。 在“已完成的工作流”下，选择“已完成” 值。 该任务在“任务”部分下列出。

9. 选择任务的标题以显示其任务详细信息。

10. 返回到“SharedDocuments”列表，并使用同一文档或其他文档重新启动工作流。

11. 在起始页上输入一个数量，该数量小于或等于在关联页上输入的数量 (**1200**)。

     出现这种情况时，将创建历史记录列表而不是任务中的条目。 该条目显示在工作流状态页的“工作流历史记录”部分中。 请注意历史记录事件的“结果”列中的消息。 它包含在 `logToHistoryListActivity1.MethodInvoking` 事件中输入的文本，其中包括已自动批准的数量。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何创建工作流模板的详细信息：

- 若要详细了解 SharePoint 工作流，请参阅 [Windows SharePoint Services 中的工作流](/previous-versions/office/developer/sharepoint-2010/ms416312(v=office.14))。

## <a name="see-also"></a>另请参阅
- [创建 SharePoint 工作流解决方案](../sharepoint/creating-sharepoint-workflow-solutions.md)
- [演练：将应用程序页添加到工作流](../sharepoint/walkthrough-add-an-application-page-to-a-workflow.md)
