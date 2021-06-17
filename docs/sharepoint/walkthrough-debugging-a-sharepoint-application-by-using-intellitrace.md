---
title: 使用 IntelliTrace 调试 SharePoint 应用程序
description: 使用 IntelliTrace 可以更轻松地调试和修复 SharePoint 应用程序。 创建代码并将其添加到功能接收器。 测试项目。 收集 IntelliTrace 数据。
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
ms.workload:
- office
ms.openlocfilehash: cf7fa6c7255e05c465d6c209db5e9581a49aee64
ms.sourcegitcommit: 1f27f33852112702ee35fbc0c02fba37899e4cf5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2021
ms.locfileid: "112112837"
---
# <a name="walkthrough-debug-a-sharepoint-application-by-using-intellitrace"></a>演练：使用 IntelliTrace 调试 SharePoint 应用程序

通过使用 IntelliTrace，可以更轻松地调试 SharePoint 解决方案。 传统调试器目前仅提供解决方案的快照。 但是，可以使用 IntelliTrace 查看解决方案中发生的过去事件及其发生上下文，并导航到代码。

 本演练演示如何使用 Visual Studio 从已部署的应用程序Microsoft Monitoring Agent IntelliTrace 数据，在 Visual Studio 中调试 SharePoint 项目。 若要分析该数据，必须使用Visual Studio Enterprise。 此项目包含一个功能接收器，在激活该功能时，它将任务添加到"任务"列表，并将公告添加到"公告"列表。 停用该功能后，任务将标记为已完成，第二个公告将添加到"公告"列表中。 但是，该过程包含阻止项目正常运行的逻辑错误。 通过使用 IntelliTrace，你将找到并更正错误。

 **适用于：** 本主题中的信息适用于在 Visual Studio 中创建的 SharePoint 解决方案。

 本演练演示以下任务：

- [创建功能接收器](#create-a-feature-receiver)

- [向功能接收器中添加代码](#add-code-to-the-feature-receiver)

- [测试项目](#test-the-project)

- [使用应用程序收集 IntelliTrace Microsoft Monitoring Agent](#collect-intellitrace-data-by-using-microsoft-monitoring-agent)

- [调试并修复 SharePoint 解决方案](#debug-and-fix-the-sharepoint-solution)

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件

您需要满足以下条件才能完成本演练：

- 支持的 Windows 和 SharePoint 版本。

- Visual Studio Enterprise。

## <a name="create-a-feature-receiver"></a>创建功能接收器

首先，创建一个空的 SharePoint 项目，该项目具有功能接收器。

1. 创建面向已安装的 SharePoint 版本的 SharePoint 解决方案项目，并命名 **IntelliTraceTest**。

     将出现 **SharePoint 自定义** 向导，可在其中指定项目的 SharePoint 站点和解决方案的信任级别。

2. 选择" **部署为场解决方案"** 选项按钮，然后选择"完成 **"** 按钮。

     IntelliTrace 仅对场解决方案运行。

3. 在 **解决方案资源管理器** 中，打开"功能"节点的快捷菜单，然后选择"**添加功能"。**

     *将显示 Feature1.feature。*

4. 打开 Feature1.feature 的快捷菜单，然后选择" **添加事件接收器** "，将代码模块添加到该功能。

## <a name="add-code-to-the-feature-receiver"></a>将代码添加到功能接收器

接下来，将代码添加到功能接收器中的两个方法： `FeatureActivated` 和 `FeatureDeactivating` 。 这些方法分别在 SharePoint 中激活或停用功能时触发。

1. 在 类的顶部，添加以下代码，该代码声明 `Feature1EventReceiver` 指定 SharePoint 站点和子站点的变量：

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

现在，代码已添加到功能接收器并且数据收集器正在运行，请部署并运行 SharePoint 解决方案，以测试它是否正常工作。

> [!IMPORTANT]
> 对于此示例，在 FeatureDeactivating 事件处理程序中引发错误。 本演练稍后使用数据收集器创建的 .iTrace 文件找到此错误。

1. 将解决方案部署到 SharePoint，然后在浏览器中打开 SharePoint 站点。

     该功能会自动激活，导致其功能接收方添加公告和任务。

2. 显示"公告"和"任务"列表的内容。

     公告列表应具有名为"已激活功能：IntelliTraceTest_Feature1"的新公告，"任务"列表应具有名为"停用功能"的新任务 **：IntelliTraceTest_Feature1。** 如果缺少其中任一项，请验证是否激活了该功能。 如果未激活，请激活它。

3. 通过执行以下步骤来停用该功能：

   1. 在 SharePoint **的"站点操作**"菜单上，选择"**站点设置"。**

   2. 在 **"站点操作"** 下， **选择"管理站点功能"** 链接。

   3. 在 **IntelliTraceTest Feature1 旁边**，选择" **停用"** 按钮。

   4. 在"警告"页上，选择" **停用此功能"** 链接。

      FeatureDeactivating () 事件处理程序引发错误。

## <a name="collect-intellitrace-data-by-using-microsoft-monitoring-agent"></a>使用应用程序收集 IntelliTrace Microsoft Monitoring Agent

如果在运行 SharePoint 的Microsoft Monitoring Agent安装 SharePoint 解决方案，可以使用比 IntelliTrace 返回的一般信息更具体的数据来调试 SharePoint 解决方案。 在 SharePoint 解决方案运行时Visual Studio PowerShell cmdlet 捕获调试信息，代理在外部工作。

> [!NOTE]
> 本部分中的配置信息特定于此示例。 有关其他配置选项的详细信息，请参阅使用 [IntelliTrace 独立收集器](../debugger/using-the-intellitrace-stand-alone-collector.md)。

1. 在运行 SharePoint 的计算机上，设置Microsoft Monitoring Agent [并开始监视解决方案](../debugger/using-the-intellitrace-stand-alone-collector.md)。

2. 停用该功能：

   1. 在 SharePoint **的"站点操作**"菜单上，选择"**站点设置"。**

   2. 在 **"站点操作"** 下， **选择"管理站点功能"** 链接。

   3. 在 **IntelliTraceTest Feature1 旁边**，选择" **停用"** 按钮。

   4. 在"警告"页上，选择" **停用此功能"** 链接。

      在这种情况下， (，因为 FeatureDeactivating () 事件处理程序中) 。

3. 在 PowerShell 窗口中，运行 [Stop-WebApplicationMonitoring](/previous-versions/system-center/powershell/system-center-2012-r2/dn472753(v=sc.20)) 命令以创建 .iTrace 文件、停止监视并重启 SharePoint 解决方案。

     **Stop-WebApplicationMonitoring***"<\<SharePointSite> \\ SharePointAppName \> "*  

## <a name="debug-and-fix-the-sharepoint-solution"></a>调试和修复 SharePoint 解决方案

现在，可以在 Visual Studio 中查看 IntelliTrace 日志文件，以查找并修复 SharePoint 解决方案中的错误。

1. 在 \IntelliTraceLogs 文件夹中，打开 Visual Studio 中的 .iTrace 文件。

     将显示 **"IntelliTrace 摘要"** 页。 由于错误未处理，因此"分析" (未处理的异常区域中) GUID 的 **SharePoint** 关联 ID。 若要查看 **发生错误的** 调用堆栈，请选择"调用堆栈"按钮。

2. 选择" **调试异常"** 按钮。

     如果系统提示，请加载符号文件。 在 **IntelliTrace** 窗口中，异常突出显示为"已引发：发生严重错误！"。

     在 IntelliTrace 窗口中，选择异常以显示失败的代码。

3. 通过打开 SharePoint 解决方案，然后注释掉或删除 FeatureDeactivating  () 语句来修复此错误。

4. 在 Visual Studio 中重新生成解决方案，然后将它重新部署到 SharePoint。

5. 通过执行以下步骤来停用该功能：

    1. 在 SharePoint **的"站点操作**"菜单上，选择"**站点设置"。**

    2. 在 **"站点操作"** 下， **选择"管理站点功能"** 链接。

    3. 在 **IntelliTraceTest Feature1 旁边**，选择" **停用"** 按钮。

    4. 在"警告"页上，选择" **停用此功能"** 链接。

6. 打开"任务"列表，验证停用任务的"状态"值为"已完成"，其 **"完成百分比**"值为 100%。

     代码现在可正常运行。

## <a name="see-also"></a>另请参阅

- [验证和调试 SharePoint 代码](../sharepoint/verifying-and-debugging-sharepoint-code.md)
- [IntelliTrace](../debugger/intellitrace.md)
- [演练：使用单元测试验证 SharePoint 代码](/previous-versions/visualstudio/visual-studio-2010/gg599006\(v\=vs.100\))
