---
title: 演练：将应用程序页添加到工作流|Microsoft Docs
description: 在此演练中，将应用程序页添加到SharePoint解决方案。 修改工作流代码。 创建、编码和测试应用程序页。
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
  本演练演示如何将显示从工作流派生的数据的应用程序页添加到工作流项目。 它基于主题演练：创建具有关联和启动窗体 [的工作流中所述的项目](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)。

 本演练演示了下列任务：

- 将 ASPX 应用程序页添加到SharePoint项目。

- 从工作流项目获取数据并对其进行操作。

- 在应用程序页上的表中显示数据。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 和 [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] SharePoint。

- Visual Studio。

- 还必须完成主题演练：创建具有关联和启动窗体 [的工作流中的项目](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)。

## <a name="amend-the-workflow-code"></a>修改工作流代码
 首先，向工作流添加一行代码，以将"结果"列的值设置为支出报表的金额。 稍后在支出报表摘要计算中会使用此值。

#### <a name="to-set-the-value-of-the-outcome-column-in-the-workflow"></a>在工作流中设置结果列的值

1. 将主题演练：创建具有关联和启动窗体的工作流 [中已完成的项目加载到](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md) [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中。

2. 打开 *Workflow1.cs* 或 *Workflow1.vb* (，具体取决于编程语言) 。

3. 在 方法的底部 `createTask1_MethodInvoking` ，添加以下代码：

    ```vb
    createTask1_TaskProperties1.ExtendedProperties("Outcome") =
      workflowProperties.InitiationData
    ```

    ```csharp
    createTask1_TaskProperties1.ExtendedProperties["Outcome"] =
      workflowProperties.InitiationData;
    ```

## <a name="create-an-application-page"></a>创建应用程序页
 接下来，向项目添加 ASPX 窗体。 此窗体将显示从支出报表工作流项目获取的数据。 为此，需要添加应用程序页。 应用程序页使用与其他页面相同的母版页SharePoint，这意味着它将类似于应用程序站点上SharePoint页。

#### <a name="to-add-an-application-page-to-the-project"></a>向项目添加应用程序页

1. 选择 ExpenseReport 项目，然后在菜单栏上选择  >  **"Project"添加新项"。**

2. 在"**模板"** 窗格中，选择"应用程序页"模板，使用 **ApplicationPage1.aspx** (项目项的默认) ，然后选择"**添加**"按钮。

3. 在 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ApplicationPage1.aspx 的 中，将 `PlaceHolderMain` 部分替换为以下内容：

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

4. 将 部分替换为以下内容，将标题 `PlaceHolderPageTitleInTitleArea` 添加到应用程序页：

    ```aspx-csharp
    <asp:Content ID="PageTitleInTitleArea" ContentPlaceHolderID="PlaceHolderPageTitleInTitleArea" runat="server" >
        Expense Report Summary
    </asp:Content>
    ```

## <a name="code-the-application-page"></a>对应用程序页进行编码
 接下来，将代码添加到支出报表摘要应用程序页。 打开页面时，代码会扫描"任务"列表中的SharePoint，以检查超出分配的支出限制的支出。 报表将列出每个项以及支出的总和。

#### <a name="to-code-the-application-page"></a>对应用程序页进行编码

1. 选择 **ApplicationPage1.aspx** 节点，然后在菜单栏上选择"查看代码"以显示  >  应用程序页后面的代码。

2. 将 **using 或** **Import** (替换为以下) ，具体取决于类顶部的编程语言：

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
    > 请务必将代码中的"TestServer"替换为运行该代码的有效服务器SharePoint。

## <a name="test-the-application-page"></a>测试应用程序页
 接下来，确定应用程序页是否正确显示支出数据。

#### <a name="to-test-the-application-page"></a>测试应用程序页

1. 选择 **F5** 键以运行项目，并部署到SharePoint。

2. 选择"**主页**"按钮，然后选择"快速启动"栏上的"共享文档"链接，在 SharePoint列表。

3. 若要表示此示例的费用报表，请通过选择页面顶部的"库 **""** 工具"选项卡上的"文档"链接，然后选择工具功能区上的"Upload 文档"按钮，将一些 **新文档上传到"文档**"列表中。

4. 上传一些文档后，通过选择页面顶部的"库 **""** 工具"选项卡上的"库"链接，然后选择工具功能区上的"库"设置按钮 **来实例** 化工作流。 

5. 在"**文档库设置** 页中，选择"权限 **设置"** 部分中的"工作流 **"链接**。

6. 在"**工作流设置** 页中，选择"**添加工作流"** 链接。

7. 在" **添加工作流"** 页中，选择 **"ExpenseReport - Workflow1"** 工作流，输入工作流的名称，例如 **ExpenseTest，** 然后选择"下一 **步"** 按钮。

    将显示工作流"关联"窗体。 使用它来报告支出限制金额。

8. 在"关联"窗体的"自动批准限制"框中输入 **1000，** 然后选择"关联 **工作流"** 按钮。

9. 选择 **"主页**"按钮以返回到SharePoint主页。

10. 选择" **快速启动"** 栏上的"共享文档"链接。

11. 选择其中一个上传的文档以显示下拉箭头，选择它，然后选择"工作流 **"** 项。

12. 选择 ExpenseTest 旁边的图像以显示工作流"启动"窗体。

13. 在" **支出总计** "文本框中，输入大于 1000 的值，然后选择"启动 **工作流"** 按钮。

     当报告的支出超过分配的费用金额时，任务将添加到任务列表。 值为 **Completed** **的名为 ExpenseTest** 的列也会添加到"共享文档"列表中的支出报表项。

14. 对"共享文档"列表中的其他文档重复步骤 11 - 13。  (文档的确切数量不很重要。) 

15. 在 Web 浏览器中打开以下 URL 以显示支出报表摘要应用程序页 **：http://**<em>SystemName</em>**/_layouts/ExpenseReport/ApplicationPage1.aspx**。

     "支出报表摘要"页列出了超出已分配金额的所有支出报表、超出该金额的金额以及所有报表的总额。

## <a name="next-steps"></a>后续步骤
 有关应用程序页SharePoint，请参阅[为应用程序创建SharePoint。](../sharepoint/creating-application-pages-for-sharepoint.md)

 可以在以下主题中SharePoint Visual Web 设计器，详细了解如何Visual Studio页面内容：

- [为 SharePoint。](../sharepoint/creating-web-parts-for-sharepoint.md)

- [为 Web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)。

## <a name="see-also"></a>另请参阅

- [演练：使用关联和启动窗体创建工作流](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)
- [如何：创建应用程序页](../sharepoint/how-to-create-an-application-page.md)
- [为 SharePoint 创建应用程序页](../sharepoint/creating-application-pages-for-sharepoint.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)