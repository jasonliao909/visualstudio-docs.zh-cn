---
title: 演练：向工作流中添加应用程序页 | Microsoft Docs
description: 本演练将应用程序页添加到 SharePoint 工作流解决方案。 修改工作流代码。 创建、编码和测试应用程序页。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, adding applications page to workflow
- application page [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 50017d9a7c368bdc9cbcfa5438aec09a63d4508b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664144"
---
# <a name="walkthrough-add-an-application-page-to-a-workflow"></a>演练：将应用程序页添加到工作流
  本演练演示如何将显示从工作流派生的数据的应用程序页添加到工作流项目。 它建立在主题[演练：创建具有关联和启动窗体的工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)中所述项目的基础上。

 本演练演示了下列任务：

- 将 ASPX 应用程序页添加到 SharePoint 项目。

- 从工作流项目获取数据并对其进行操作。

- 在应用程序页上的表中显示数据。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 受支持的 [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 和 SharePoint 版本。

- Visual Studio。

- 你还需要完成主题[演练：创建具有关联和启动窗体的工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)中的项目。

## <a name="amend-the-workflow-code"></a>修改工作流代码
 首先，向工作流添加一行代码，以将“结果”列的值设置为支出报表的金额。 稍后在支出报表摘要计算中会用到此值。

#### <a name="to-set-the-value-of-the-outcome-column-in-the-workflow"></a>在工作流中设置结果列的值

1. 从主题[演练：创建具有关联和启动窗体的工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)中将完整项目加载到 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中。

2. 打开 Workflow1.cs 或 Workflow1.vb 的代码（具体取决于你的编程语言）。

3. 将以下代码添加到 `createTask1_MethodInvoking` 方法底部：

    ```vb
    createTask1_TaskProperties1.ExtendedProperties("Outcome") =
      workflowProperties.InitiationData
    ```

    ```csharp
    createTask1_TaskProperties1.ExtendedProperties["Outcome"] =
      workflowProperties.InitiationData;
    ```

## <a name="create-an-application-page"></a>创建应用程序页
 接下来，向项目添加 ASPX 窗体。 此窗体将显示从支出报表工作流项目获取的数据。 为此，需要添加一个应用程序页。 应用程序页使用与其他 SharePoint 页相同的母版页，这意味着它将与 SharePoint 站点上的其他页类似。

#### <a name="to-add-an-application-page-to-the-project"></a>向项目添加应用程序页

1. 选择“ExpenseReport”项目，然后在菜单栏上选择“项目” > “添加新项” 。

2. 在“模板”窗格中，选择“应用程序页”模板，使用项目项的默认名称 (ApplicationPage1.aspx)，然后选择“添加”按钮   。

3. 在 ApplicationPage1.aspx 的 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] 中，将 `PlaceHolderMain` 部分替换为以下内容：

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
        <asp:Label ID="Label1" runat="server" Font-Bold="True"
            Text="Expenses that exceeded allotted amount" Font-Size="Medium"></asp:Label>
        <br />
        <asp:Table ID="Table1" runat="server">
        </asp:Table>
    </asp:Content>
    ```

     此代码将表与标题一起添加到页面。

4. 通过将 `PlaceHolderPageTitleInTitleArea` 部分替换为以下内容，向应用程序页添加一个标题：

    ```aspx-csharp
    <asp:Content ID="PageTitleInTitleArea" ContentPlaceHolderID="PlaceHolderPageTitleInTitleArea" runat="server" >
        Expense Report Summary
    </asp:Content>
    ```

## <a name="code-the-application-page"></a>对应用程序页进行编码
 接下来，将代码添加到支出报表摘要应用程序页。 当你打开页面时，代码会扫描 SharePoint 中的“任务”列表，以检查超出分配的支出限制的支出。 报表将列出每个项以及支出的总和。

#### <a name="to-code-the-application-page"></a>对应用程序页进行编码

1. 选择“ApplicationPage1.aspx”节点，然后在菜单栏上选择“查看” > “代码”  以显示应用程序页后面的代码。

2. 将类顶部的 using 或 Import 语句（具体取决于你的编程语言）替换为以下内容 ：

    ```vb
    Imports System
    Imports Microsoft.SharePoint
    Imports Microsoft.SharePoint.WebControls
    Imports System.Collections
    Imports System.Data
    Imports System.Web.UI
    Imports System.Web.UI.WebControls
    Imports System.Web.UI.WebControls.WebParts
    Imports System.Drawing
    Imports Microsoft.SharePoint.Navigation
    ```

    ```csharp
    using System;
    using Microsoft.SharePoint;
    using Microsoft.SharePoint.WebControls;
    using System.Collections;
    using System.Data;
    using System.Web.UI;
    using System.Web.UI.WebControls;
    using System.Web.UI.WebControls.WebParts;
    using System.Drawing;
    using Microsoft.SharePoint.Navigation;
    ```

3. 将以下代码添加到 `Page_Load` 方法中：

    ```vb
    Try
        ' Reference the Tasks list on the SharePoint site.
        ' Replace "TestServer" with a valid SharePoint server name.
        Dim site As SPSite = New SPSite("http://TestServer")
        Dim list As SPList = site.AllWebs(0).Lists("Tasks")
        ' string text = "";
        Dim sum As Integer = 0
        Table1.Rows.Clear()
        ' Add table headers.
        Dim hr As TableHeaderRow = New TableHeaderRow
        hr.BackColor = Color.LightBlue
        Dim hc1 As TableHeaderCell = New TableHeaderCell
        Dim hc2 As TableHeaderCell = New TableHeaderCell
        hc1.Text = "Expense Report Name"
        hc2.Text = "Amount Exceeded"
        hr.Cells.Add(hc1)
        hr.Cells.Add(hc2)
        ' Add the TableHeaderRow as the first item
        ' in the Rows collection of the table.
        Table1.Rows.AddAt(0, hr)
        ' Iterate through the tasks in the Task list and collect those
        ' that have values in the "Related Content" and "Outcome" fields
        ' - the fields written to when expense approval is required.
        For Each item As SPListItem In list.Items
            Dim s_relContent As String = ""
            Dim s_outcome As String = ""
            Try
                ' Task has the fields - treat as expense report.
                s_relContent = item.GetFormattedValue("Related Content")
                s_outcome = item.GetFormattedValue("Outcome")
            Catch erx As System.Exception
                ' Task does not have fields - skip it.
                Continue For
            End Try
            ' Convert amount to an int and keep a running total.
            If (Not String.IsNullOrEmpty(s_relContent) And Not
              String.IsNullOrEmpty(s_outcome)) Then
                sum = (sum + Convert.ToInt32(s_outcome))
                Dim relContent As TableCell = New TableCell
                relContent.Text = s_relContent
                Dim outcome As TableCell = New TableCell
                outcome.Text = ("$" + s_outcome)
                Dim dataRow2 As TableRow = New TableRow
                dataRow2.Cells.Add(relContent)
                dataRow2.Cells.Add(outcome)
                Table1.Rows.Add(dataRow2)
            End If
        Next
        ' Report the sum of the reports in the table footer.
        Dim tfr As TableFooterRow = New TableFooterRow
        tfr.BackColor = Color.LightGreen
        ' Create a TableCell object to contain the
        ' text for the footer.
        Dim ftc1 As TableCell = New TableCell
        Dim ftc2 As TableCell = New TableCell
        ftc1.Text = "TOTAL: "
        ftc2.Text = ("$" + Convert.ToString(sum))
        ' Add the TableCell object to the Cells
        ' collection of the TableFooterRow.
        tfr.Cells.Add(ftc1)
        tfr.Cells.Add(ftc2)
        ' Add the TableFooterRow to the Rows
        ' collection of the table.
        Table1.Rows.Add(tfr)
    Catch errx As Exception
        System.Diagnostics.Debug.WriteLine(("Error: " + errx.ToString))
    End Try
    ```

    ```csharp
    try
    {
        // Reference the Tasks list on the SharePoint site.
        // Replace "TestServer" with a valid SharePoint server name.
        SPSite site = new SPSite("http://TestServer");
        SPList list = site.AllWebs[0].Lists["Tasks"];

        // string text = "";
        int sum = 0;

        Table1.Rows.Clear();

        // Add table headers.
        TableHeaderRow hr = new TableHeaderRow();
        hr.BackColor = Color.LightBlue;
        TableHeaderCell hc1 = new TableHeaderCell();
        TableHeaderCell hc2 = new TableHeaderCell();
        hc1.Text = "Expense Report Name";
        hc2.Text = "Amount Exceeded";
        hr.Cells.Add(hc1);
        hr.Cells.Add(hc2);
        // Add the TableHeaderRow as the first item
        // in the Rows collection of the table.
        Table1.Rows.AddAt(0, hr);

        // Iterate through the tasks in the Task list and collect those
        // that have values in the "Related Content" and "Outcome"
        // fields - the fields written to when expense approval is
        // required.
        foreach (SPListItem item in list.Items)
        {
            string s_relContent = "";
            string s_outcome = "";

            try
            {
                // Task has the fields - treat as expense report.
                s_relContent = item.GetFormattedValue("Related
                  Content");
                s_outcome = item.GetFormattedValue("Outcome");
            }
            catch
            {
                // Task does not have fields - skip it.
                continue;
            }

            if (!String.IsNullOrEmpty(s_relContent) &&
              !String.IsNullOrEmpty(s_outcome))
            {
                // Convert amount to an int and keep a running total.
                sum += Convert.ToInt32(s_outcome);
                TableCell relContent = new TableCell();
                relContent.Text = s_relContent;
                TableCell outcome = new TableCell();
                outcome.Text = "$" + s_outcome;
                TableRow dataRow2 = new TableRow();
                dataRow2.Cells.Add(relContent);
                dataRow2.Cells.Add(outcome);
                Table1.Rows.Add(dataRow2);
            }
        }

        // Report the sum of the reports in the table footer.
           TableFooterRow tfr = new TableFooterRow();
        tfr.BackColor = Color.LightGreen;

        // Create a TableCell object to contain the
        // text for the footer.
        TableCell ftc1 = new TableCell();
        TableCell ftc2 = new TableCell();
        ftc1.Text = "TOTAL: ";
        ftc2.Text = "$" + Convert.ToString(sum);

        // Add the TableCell object to the Cells
        // collection of the TableFooterRow.
        tfr.Cells.Add(ftc1);
        tfr.Cells.Add(ftc2);

        // Add the TableFooterRow to the Rows
        // collection of the table.
        Table1.Rows.Add(tfr);
    }

    catch (Exception errx)
    {
        System.Diagnostics.Debug.WriteLine("Error: " + errx.ToString());
    }
    ```

    > [!WARNING]
    > 请务必将代码中的“TestServer”替换为运行 SharePoint 的有效服务器的名称。

## <a name="test-the-application-page"></a>测试应用程序页
 接下来，确定应用程序页是否正确显示支出数据。

#### <a name="to-test-the-application-page"></a>测试应用程序页

1. 按 F5 运行项目并将项目部署到 SharePoint。

2. 选择“主页”按钮，然后选择快速启动栏上的“共享文档”链接以显示 SharePoint 站点上的“共享文档”列表。

3. 若要展示本例中的支出报表，请选择页面顶部“库工具”选项卡上的“文档”链接，然后在工具功能区上选择“上传文档”按钮，将一些新文档上传到“文档”列表中  。

4. 上传完一些文档后，选择页面顶部“库工具”选项卡上的“库”链接，然后在工具功能区上选择“库设置”按钮来实例化工作流  。

5. 在“文档库设置”页的“权限和管理”部分中，选择“工作流设置”链接  。

6. 在“工作流设置”页上，选择“添加工作流”链接 。

7. 在“添加工作流”页中，选择“ExpenseReport - Workflow1”工作流，为工作流输入名称，如“ExpenseTest”，然后选择“下一步”按钮   。

    工作流“关联”窗体随即显示。 使用它来报告支出限制金额。

8. 在“关联”窗体中，在“自动审批限制”框中输入“1000”，然后选择“关联工作流”按钮  。

9. 选择“主页”按钮可返回 SharePoint 主页。

10. 在快速启动栏上，选择“共享文档”链接。

11. 选择一个已上传的文档以显示下拉箭头，选择它，然后选择“工作流”项。

12. 选择 ExpenseTest 旁边的图像以显示工作流“启动”窗体。

13. 在“总支出”文本框中，输入一个大于 1000 的值，然后选择“启动工作流”按钮 。

     当报告的支出超过分配的支出金额时，系统会将一个任务添加到任务列表。 名为“ExpenseTest”且值为“已完成”的列被添加到“共享文档”列表中的支出报表项中。

14. 对“共享文档”列表中的其他文档重复步骤 11 - 13。 （文档的确切数量并不重要。）

15. 在 Web 浏览器中打开以下 URL 以显示支出报表摘要应用程序页： http://SystemName/_layouts/ExpenseReport/ApplicationPage1.aspx。

     支出报表摘要页列出了超出已分配金额的所有支出报表、超出的金额以及所有报表的总额。

## <a name="next-steps"></a>后续步骤
 有关 SharePoint 应用程序页的详细信息，请参阅[为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)。

 可以使用以下主题中 Visual Studio 中的 Visual Web 设计器，了解如何设计 SharePoint 页面内容：

- [为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)。

- [为 Web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)。

## <a name="see-also"></a>另请参阅

- [演练：使用关联和启动窗体创建工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)
- [如何：创建应用程序页](../sharepoint/how-to-create-an-application-page.md)
- [为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)