---
title: 使用 IntelliTrace 调试 SharePoint 应用程序
description: 使用 IntelliTrace 更轻松地调试和修复 SharePoint 应用程序。 创建代码并将其添加到功能接收器。 测试项目。 收集 IntelliTrace 数据。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- IntelliTrace [SharePoint development in Visual Studio]
- standalone data collector
- SharePoint development in Visual Studio, IntelliTrace
- data collector
- IntelliTrace
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 60a177fec8edf3b2e201eaff63ee0ff0ed4c8d72
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665269"
---
# <a name="walkthrough-debug-a-sharepoint-application-by-using-intellitrace"></a>演练：使用 IntelliTrace 调试 SharePoint 应用程序

通过使用 IntelliTrace，可以更轻松地调试 SharePoint 解决方案。 传统的调试程序仅提供当前解决方案的快照。 但是，可以使用 IntelliTrace 查看解决方案中过去发生的事件及其发生时的上下文，并导航到代码。

 本演练演示如何使用 Microsoft Monitoring Agent 从已部署的应用程序中收集 IntelliTrace 数据，以在 Visual Studio 中调试 SharePoint 项目。 若要分析这些数据，必须使用 Visual Studio Enterprise。 此项目包含一个功能接收器，当激活该功能时，该接收器将向 Task 列表中添加一个任务，向 Announcements 列表中添加一个公告。 停用此功能后，该任务将标记为“已完成”，Announcements 列表中将添加第二个公告。 但是，该过程有一个逻辑错误，该错误会阻止项目正常运行。 通过使用 IntelliTrace，可以找到并更正该错误。

 **适用于：** 本主题中的信息适用于在 Visual Studio 中创建的 SharePoint 解决方案。

 本演练演示以下任务：

- [创建功能接收器](#create-a-feature-receiver)

- [向功能接收器中添加代码](#add-code-to-the-feature-receiver)

- [测试项目](#test-the-project)

- [使用 Microsoft Monitoring Agent 收集 IntelliTrace 数据](#collect-intellitrace-data-by-using-microsoft-monitoring-agent)

- [调试并修复 SharePoint 解决方案](#debug-and-fix-the-sharepoint-solution)

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件

您需要满足以下条件才能完成本演练：

- 支持的 Windows 和 SharePoint 版本。

- Visual Studio Enterprise。

## <a name="create-a-feature-receiver"></a>创建功能接收器

首先，创建一个具有功能接收器的空 SharePoint 项目。

1. 针对安装的 SharePoint 版本创建一个 SharePoint 解决方案项目，并将其命名为“IntelliTraceTest”。

     此时将显示“SharePoint 自定义向导”，你可以在其中指定项目的 SharePoint 站点和解决方案的信任级别。

2. 选择“部署为场解决方案”选项按钮，然后选择“完成”按钮 。

     IntelliTrace 仅在场解决方案上运行。

3. 在解决方案资源管理器中，打开“功能”节点的快捷菜单，然后选择“添加功能”  。

     此时将显示“Feature1.feature”。

4. 打开 Feature1.feature 的快捷菜单，然后选择“添加事件接收器”以向该功能添加代码模块。

## <a name="add-code-to-the-feature-receiver"></a>向功能接收器添加代码

接下来，向功能接收器中的两个方法（`FeatureActivated` 和 `FeatureDeactivating`）添加代码。 每当在 SharePoint 中激活或停用功能时，都会触发这些方法。

1. 在 `Feature1EventReceiver` 类的顶部，添加以下代码，该代码声明用于指定 SharePoint 站点和子站点的变量：

    ```vb
    ' SharePoint site and subsite.
    Private siteUrl As String = "http://localhost"
    Private webUrl As String = "/"
    ```

    ```csharp
    // SharePoint site and subsite.
    private string siteUrl = "http://localhost";
    private string webUrl = "/";
    ```

2. 将 `FeatureActivated`方法替换为以下代码：

    ```vb
    Public Overrides Sub FeatureActivated(ByVal properties As SPFeatureReceiverProperties)
        Try
            Using site As New SPSite(siteUrl)
                Using web As SPWeb = site.OpenWeb(webUrl)
                    ' Reference the lists.
                    Dim announcementsList As SPList = web.Lists("Announcements")
                    Dim taskList As SPList = web.Lists("Tasks")

                    ' Add an announcement to the Announcements list.
                    Dim listItem As SPListItem = announcementsList.Items.Add()
                    listItem("Title") = "Activated Feature: " & Convert.ToString(properties.Definition.DisplayName)
                    listItem("Body") = Convert.ToString(properties.Definition.DisplayName) & " was activated on: " & DateTime.Now.ToString()
                    listItem.Update()

                    ' Add a task to the Task list.
                    Dim newTask As SPListItem = taskList.Items.Add()
                    newTask("Title") = "Deactivate feature: " & Convert.ToString(properties.Definition.DisplayName)
                    newTask.Update()
                End Using
            End Using

        Catch e As Exception
            Console.WriteLine("Error: " & e.ToString())
        End Try

    End Sub
    ```

    ```csharp
    public override void FeatureActivated(SPFeatureReceiverProperties properties)
    {
        try
        {
            using (SPSite site = new SPSite(siteUrl))
            {
                using (SPWeb web = site.OpenWeb(webUrl))
                {
                    // Reference the lists.
                    SPList announcementsList = web.Lists["Announcements"];
                    SPList taskList = web.Lists["Tasks"];

                    // Add an announcement to the Announcements list.
                    SPListItem listItem = announcementsList.Items.Add();
                    listItem["Title"] = "Activated Feature: " + properties.Definition.DisplayName;
                    listItem["Body"] = properties.Definition.DisplayName + " was activated on: " + DateTime.Now.ToString();
                    listItem.Update();

                    // Add a task to the Task list.
                    SPListItem newTask = taskList.Items.Add();
                    newTask["Title"] = "Deactivate feature: " + properties.Definition.DisplayName;
                    newTask.Update();
                }
            }
        }

        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.ToString());
        }

    }
    ```

3. 将 `FeatureDeactivating`方法替换为以下代码：

    ```vb
    Public Overrides Sub FeatureDeactivating(ByVal properties As SPFeatureReceiverProperties)
        ' The following line induces an error to demonstrate debugging.
        ' Remove this line later for proper operation.
        Throw New System.InvalidOperationException("Serious error occurred!")
        Try
            Using site As New SPSite(siteUrl)
                Using web As SPWeb = site.OpenWeb(webUrl)
                    ' Reference the lists.
                    Dim taskList As SPList = web.Lists("Tasks")
                    Dim announcementsList As SPList = web.Lists("Announcements")

                    ' Add an announcement that the feature was deactivated.
                    Dim listItem As SPListItem = announcementsList.Items.Add()
                    listItem("Title") = "Deactivated Feature: " & Convert.ToString(properties.Definition.DisplayName)
                    listItem("Body") = Convert.ToString(properties.Definition.DisplayName) & " was deactivated on: " & DateTime.Now.ToString()
                    listItem.Update()

                    ' Find the task that the feature receiver added to the Task list when the
                    ' feature was activated.
                    Dim qry As New SPQuery()
                    qry.Query = "<Where><Contains><FieldRef Name='Title' /><Value Type='Text'>Deactivate</Value></Contains></Where>"
                    Dim taskItems As SPListItemCollection = taskList.GetItems(qry)

                    For Each taskItem As SPListItem In taskItems
                        ' Mark the task as complete.
                        taskItem("PercentComplete") = 1
                        taskItem("Status") = "Completed"
                        taskItem.Update()
                    Next
                End Using

            End Using

        Catch e As Exception
            Console.WriteLine("Error: " & e.ToString())
        End Try

    End Sub
    ```

    ```csharp
    public override void FeatureDeactivating(SPFeatureReceiverProperties properties)
    {
        // The following line induces an error to demonstrate debugging.
        // Remove this line later for proper operation.
        throw new System.InvalidOperationException("A serious error occurred!");
        try
        {
            using (SPSite site = new SPSite(siteUrl))
            {
                using (SPWeb web = site.OpenWeb(webUrl))
                {
                    // Reference the lists.
                    SPList taskList = web.Lists["Tasks"];
                    SPList announcementsList = web.Lists["Announcements"];

                    // Add an announcement that the feature was deactivated.
                    SPListItem listItem = announcementsList.Items.Add();
                    listItem["Title"] = "Deactivated Feature: " + properties.Definition.DisplayName;
                    listItem["Body"] = properties.Definition.DisplayName + " was deactivated on: " + DateTime.Now.ToString();
                    listItem.Update();

                    // Find the task that the feature receiver added to the Task list when the
                    // feature was activated.
                    SPQuery qry = new SPQuery();
                    qry.Query = "<Where><Contains><FieldRef Name='Title' /><Value Type='Text'>Deactivate</Value></Contains></Where>";
                    SPListItemCollection taskItems = taskList.GetItems(qry);

                    foreach (SPListItem taskItem in taskItems)
                    {
                        // Mark the task as complete.
                        taskItem["PercentComplete"] = 1;
                        taskItem["Status"] = "Completed";
                        taskItem.Update();
                    }
                }
            }

        }

        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.ToString());
        }
    }
    ```

## <a name="test-the-project"></a>测试项目

将代码添加到功能接收器并运行数据收集器后，请部署并运行 SharePoint 解决方案，以测试其是否正常工作。

> [!IMPORTANT]
> 在此示例中，FeatureDeactivating 事件处理程序中会引发错误。 在本演练的后面部分，将使用数据收集器创建的 .iTrace 文件查找此错误。

1. 将解决方案部署到 SharePoint，然后在浏览器中打开 SharePoint 站点。

     此功能将自动激活，使其功能接收器开始添加公告和任务。

2. 显示 Announcements 和 Tasks 列表的内容。

     Announcements 列表应包含一个名为“Activated feature: IntelliTraceTest_Feature1”的新公告，而 Tasks 列表应包含一个名为“Deactivate feature: IntelliTraceTest_Feature1”的新任务 。 如果缺少上述任何一项，请验证该功能是否已激活。 如果未激活，请激活它。

3. 通过执行以下步骤停用此功能：

   1. 在 SharePoint 的“站点操作”菜单上，选择“站点设置” 。

   2. 在“站点操作”下，选择“管理站点功能”链接 。

   3. 在“IntelliTraceTest Feature1”旁边，选择“停用”按钮 。

   4. 在“警告”页上，选择“停用此功能”链接。

      FeatureDeactivation() 事件处理程序引发错误。

## <a name="collect-intellitrace-data-by-using-microsoft-monitoring-agent"></a>使用 Microsoft Monitoring Agent 收集 IntelliTrace 数据

如果在运行 SharePoint 的系统上安装 Microsoft Monitoring Agent，则可以使用比 IntelliTrace 返回的一般信息更具体的数据来调试 SharePoint 解决方案。 该代理在 Visual Studio 之外使用 PowerShell cmdlet 在 SharePoint 解决方案运行时捕获调试信息。

> [!NOTE]
> 本部分中的配置信息特定于本示例。 有关其他配置选项的详细信息，请参阅[使用 IntelliTrace 独立收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)。

1. 在运行 SharePoint 的计算机上，[设置 Microsoft Monitoring Agent 并开始监视解决方案](../debugger/using-the-intellitrace-stand-alone-collector.md)。

2. 停用此功能：

   1. 在 SharePoint 的“站点操作”菜单上，选择“站点设置” 。

   2. 在“站点操作”下，选择“管理站点功能”链接 。

   3. 在“IntelliTraceTest Feature1”旁边，选择“停用”按钮 。

   4. 在“警告”页上，选择“停用此功能”链接。

      发生错误（在本例中，是因为 FeatureDeactivation() 事件处理程序中引发了错误）。

3. 在 PowerShell 窗口中，运行 [Stop-WebApplicationMonitoring](/previous-versions/system-center/powershell/system-center-2012-r2/dn472753(v=sc.20)) 命令以创建 .iTrace 文件、停止监视并重启 SharePoint 解决方案。

     **Stop-WebApplicationMonitoring**  *"\<SharePointSite>\\<SharePointAppName\>"*

## <a name="debug-and-fix-the-sharepoint-solution"></a>调试和修复 SharePoint 解决方案

现在，你可以在 Visual Studio 中查看 IntelliTrace 日志文件，查找并修复 SharePoint 解决方案中的错误。

1. 在 \IntelliTraceLogs 文件夹中，在 Visual Studio 中打开 .iTrace 文件。

     此时将显示“IntelliTrace 摘要”页。 由于错误未得到处理，在“分析”部分的未经处理的异常区域中会显示 SharePoint 相关 ID (GUID)。 如果要查看发生错误的调用堆栈，请选择“调用堆栈”按钮。

2. 选择“调试异常”按钮。

     如果系统提示，请加载符号文件。 在 IntelliTrace 窗口中，异常突出显示为“Thrown: Serious error occurred!”。

     在 IntelliTrace 窗口中，选择该异常以显示失败的代码。

3. 若要修复此错误，请打开 SharePoint 解决方案，然后注释掉或删除 FeatureDeactivation() 过程顶部的 throw 语句。

4. 在 Visual Studio 中重新生成解决方案，然后将其重新部署到 SharePoint。

5. 通过执行以下步骤停用此功能：

    1. 在 SharePoint 的“站点操作”菜单上，选择“站点设置” 。

    2. 在“站点操作”下，选择“管理站点功能”链接 。

    3. 在“IntelliTraceTest Feature1”旁边，选择“停用”按钮 。

    4. 在“警告”页上，选择“停用此功能”链接。

6. 打开 Tasks 列表，验证 Deactivate 任务的“Status”值为“Completed”，其“% Complete”值为 100% 。

     代码现在可以正常运行。

## <a name="see-also"></a>另请参阅

- [验证和调试 SharePoint 代码](../sharepoint/verifying-and-debugging-sharepoint-code.md)
- [IntelliTrace](../debugger/intellitrace.md)
- [演练：使用单元测试验证 SharePoint 代码](/previous-versions/visualstudio/visual-studio-2010/gg599006\(v\=vs.100\))
