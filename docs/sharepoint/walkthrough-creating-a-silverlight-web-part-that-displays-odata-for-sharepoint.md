---
title: 创建显示用于 SharePoint 的 OData 的 Silverlight Web 部件
titleSuffix: ''
description: 创建显示用于 SharePoint 的 OData 的 Silverlight Web 部件。 自定义 Silverlight 应用程序，并修改和测试 Silverlight Web 部件。
ms.custom: SEO-VS-2020
ms.date: 02/22/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.SPE.SilverlightWebPart
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 03c4089706d15178425c193f9dcabd4a592db2b0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665276"
---
# <a name="walkthrough-create-a-silverlight-web-part-that-displays-odata-for-sharepoint"></a>演练：创建显示用于 SharePoint 的 OData 的 Silverlight Web 部件
  SharePoint 2010 通过 OData 公开其列表数据。 在 SharePoint 中，OData 服务由 RESTful 服务 ListData.svc 实现。 本演练演示如何创建托管 Silverlight 应用程序的 SharePoint Web 部件。 Silverlight 应用程序使用 ListData.svc 显示 SharePoint“公告”列表信息。 有关详细信息，请参阅 [SharePoint Foundation REST 接口](/previous-versions/office/developer/sharepoint-2010/ff521587(v=office.14))和 [Open Data Protocol](https://www.odata.org/)。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 Microsoft Windows 和 SharePoint 版本。

- [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)].

## <a name="create-a-silverlight-application-and-silverlight-web-part"></a>创建 Silverlight 应用程序和 Silverlight Web 部件
 首先，在 Visual Studio 中创建 Silverlight 应用程序。 Silverlight 应用程序使用 ListData.svc 服务从 SharePoint“公告”列表中检索数据。

> [!NOTE]
> Silverlight 4.0 之前的版本均不支持引用 SharePoint 列表数据所需的接口。

#### <a name="to-create-a-silverlight-application-and-silverlight-web-part"></a>创建 Silverlight 应用程序和 Silverlight Web 部件

1. 在菜单栏上，选择“文件” > “新建” > “项目”，打开“新建项目”对话框   。

2. 展开“Visual C#”或“Visual Basic”下的“SharePoint”节点，然后选择“2010”节点   。

3. 在模板窗格中，选择“SharePoint 2010 Silverlight Web 部件”模板。

4. 在“名称”框中，输入“SLWebPartTest”，然后选择“确定”按钮  。

    “SharePoint 自定义向导”对话框随即出现。

5. 在“指定用于调试的站点和安全级别”页上，输入要在其中调试站点定义的 SharePoint 服务器站点的 URL，或者使用默认位置 (http://system name/)。

6. 在“此 SharePoint 解决方案的信任级别是什么?”部分中，选择“部署为场解决方案”选项按钮 。

    虽然此示例使用场解决方案，但 Silverlight Web 部件项目可以部署为场解决方案或沙盒解决方案。 有关沙盒解决方案与场解决方案的详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

7. 在“指定 Silverlight 配置信息”页的“要如何关联 Silverlight Web 部件?”部分中，选择“新建一个 Silverlight 项目并将其与 Web 部件相关联”选项按钮  。

8. 将“名称”更改为“SLApplication”，将“语言”设置为“Visual Basic”或“Visual C#”，然后将“Silverlight 版本”设置为“Silverlight 4.0”      。

9. 选择 **“完成”** 按钮。 “解决方案资源管理器”中会显示这些项目。

     此解决方案包含两个项目：Silverlight 应用程序和 Silverlight Web 部件。 Silverlight 应用程序从 SharePoint 检索并显示列表数据，Silverlight Web 部件托管 Silverlight 应用程序，这样你就能在 SharePoint 中查看。

## <a name="customize-the-silverlight-application"></a>自定义 Silverlight 应用程序
 将代码和设计元素添加到 Silverlight 应用程序。

#### <a name="to-customize-the-silverlight-application"></a>自定义 Silverlight 应用程序

1. 在 Silverlight 应用程序中添加对 System.Windows.Data 的程序集引用。 有关详细信息，请参阅[操作说明：使用“添加引用”对话框添加或删除引用](/previous-versions/wkze6zky(v=vs.140))。

2. 在“解决方案资源管理器”中，打开“引用”的快捷菜单，然后选择“添加服务引用”  。

    > [!NOTE]
    > 如果使用的是 Visual Basic，必须选择“解决方案资源管理器”顶部的“显示所有文件”图标以显示“引用”节点  。

3. 在“添加服务引用”对话框的“地址”框中，输入 SharePoint 网站的 URL，如 http://MySPSite ，然后选择“转到”按钮  。

     当 Silverlight 查找 SharePoint OData 服务 ListData.svc 时，它会将该地址替换为完整的服务 URL。 例如，将 http://myserver 变为 http://myserver/_vti_bin/ListData.svc 。

4. 选择“确定”按钮以将服务引用添加到项目，并使用默认服务名称 ServiceReference1。

5. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

6. 根据 SharePoint 服务向项目添加新的数据源。 为此，请在菜单栏上选择“视图” > “其他窗口” > “数据源”  。

     “数据源”窗口将显示所有可用的 SharePoint 列表数据，如“任务”、“公告”和“日历”。

7. 将“公告”列表数据添加到 Silverlight 应用程序。 可以将“公告”从“数据源”窗口拖动到 Silverlight 设计器中。

     该操作会创建绑定到 SharePoint 网站的“公告”列表的网格控件。

8. 将网格控件调整为适合 Silverlight 页的大小。

9. 在 MainPage.xaml 代码文件（在 Visual C# 中为 MainPage.xaml.cs，在 Visual Basic 中为 MainPage.xaml.vb）中，添加以下命名空间引用 。

    ```vb
    ' Add the following three Imports statements.
    Imports SLApplication.ServiceReference1
    Imports System.Windows.Data
    Imports System.Data.Services.Client
    ```

    ```csharp
    // Add the following three using directives.
    using SLApplication.ServiceReference1;
    using System.Windows.Data;
    using System.Data.Services.Client;
    ```

10. 在类的顶部添加以下变量声明。

    ```vb
    Private context As TeamSiteDataContext
    Private myCollectionViewSource As CollectionViewSource
    Private announcements As New DataServiceCollection(Of AnnouncementsItem)()
    ```

    ```csharp
    private TeamSiteDataContext context;
    private CollectionViewSource myCollectionViewSource;
    DataServiceCollection<AnnouncementsItem> announcements = new DataServiceCollection<AnnouncementsItem>();
    ```

11. 将 `UserControl_Loaded` 过程替换为以下代码。

    ```vb
    Private Sub UserControl_Loaded_1(sender As Object, e As RoutedEventArgs)
        ' The URL for the OData service.
        ' Replace <server name> in the next line with the name of your SharePoint server.
        context = New TeamSiteDataContext(New Uri("http://<server name>/_vti_bin/ListData.svc"))

        ' Do not load your data at design time.
        If Not System.ComponentModel.DesignerProperties.GetIsInDesignMode(Me) Then
            'Load your data here and assign the results to the CollectionViewSource.
            myCollectionViewSource =   DirectCast(Me.Resources("announcementsViewSource"), System.Windows.Data.CollectionViewSource)
            announcements.LoadCompleted += New EventHandler(Of LoadCompletedEventArgs)(AddressOf announcements_LoadCompleted)
            announcements.LoadAsync(context.Announcements)
        End If
    End Sub
    ```

    ```csharp
    private void UserControl_Loaded_1(object sender, RoutedEventArgs e)
    {
        // The URL for the OData service.
        // Replace <server name> in the next line with the name of your
        // SharePoint server.
        context = new TeamSiteDataContext(new Uri("http://ServerName>/_vti_bin/ListData.svc"));

        // Do not load your data at design time.
        if (!System.ComponentModel.DesignerProperties.GetIsInDesignMode(this))
        {
            //Load your data here and assign the results to the CollectionViewSource.
            myCollectionViewSource = (System.Windows.Data.CollectionViewSource)this.Resources["announcementsViewSource"];
            announcements.LoadCompleted += new EventHandler<LoadCompletedEventArgs>(announcements_LoadCompleted);
            announcements.LoadAsync(context.Announcements);
        }
    }
    ```

     请确保将 ServerName 占位符替换为运行 SharePoint 的服务器的名称。

12. 添加以下错误处理过程。

    ```vb
    Private Sub announcements_LoadCompleted(sender As Object, e As LoadCompletedEventArgs)
        ' Handle any errors.
        If e.[Error] Is Nothing Then
            myCollectionViewSource.Source = announcements
        Else
            MessageBox.Show(String.Format("ERROR: {0}", e.[Error].Message))
        End If
    End Sub

    ```

    ```csharp
    void announcements_LoadCompleted(object sender, LoadCompletedEventArgs e)
    {
        // Handle any errors.
        if (e.Error == null)
        {
            myCollectionViewSource.Source = announcements;
        }
        else
        {
            MessageBox.Show(string.Format("ERROR: {0}", e.Error.Message));
        }
    }
    ```

## <a name="modify-the-silverlight-web-part"></a>修改 Silverlight Web 部件
 更改 Silverlight Web 部件项目中的属性以启用 Silverlight 调试。

#### <a name="to-modify-the-silverlight-web-part"></a>修改 Silverlight Web 部件

1. 打开 Silverlight Web 项目 (SLWebPartTest) 的快捷菜单，然后选择“属性” 。

2. 在“属性”窗口中，选择“SharePoint”选项卡 。

3. 如果尚未选中“启用 Silverlight 调试(而不是 Script 调试)”复选框，请将其选中。

4. 保存项目。

## <a name="test-the-silverlight-web-part"></a>测试 Silverlight Web 部件
 在 SharePoint 中测试新的 Silverlight Web 部件，以确保其正确显示 SharePoint 列表数据。

#### <a name="to-test-the-silverlight-web-part"></a>测试 Silverlight Web 部件

1. 按 F5，生成并运行 SharePoint 解决方案。

2. 在 SharePoint 的“网站操作”菜单上，选择“新建页” 。

3. 在“新建页”的对话框中，输入标题，如“SL Web 部件测试”，然后选择“创建”按钮  。

4. 在页面设计器的“编辑工具”选项卡中，选择“插入” 。

5. 在选项卡条上，选择“Web 部件”。

6. 在“类别”框中，选择“自定义”文件夹 。

7. 在“Web 部件”列表中，选择 Silverlight Web 部件，然后选择“添加”按钮，将该 Web 部件添加到设计器中 。

8. 向网页添加完所需的内容后，选择“页面”选项卡，然后选择工具栏上的“保存并关闭”按钮 。

     Silverlight Web 部件现在应显示来自 SharePoint 网站的公告数据。 默认情况下，该页存储在 SharePoint 的“网站页面”列表中。

    > [!NOTE]
    > 跨域访问 Silverlight 中的数据时，Silverlight 会防范可用于攻击 Web 应用程序的安全漏洞。 如果在访问 Silverlight 中的远程数据时遇到问题，请参阅[跨域边界提供服务](/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc197955(v=vs.95))。

## <a name="see-also"></a>另请参阅
- [为 SharePoint 创建 Web 部件](../sharepoint/creating-web-parts-for-sharepoint.md)
- [部署、发布和升级 SharePoint 解决方案包](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)