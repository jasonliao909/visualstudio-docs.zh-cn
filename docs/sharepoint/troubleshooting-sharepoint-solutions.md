---
title: SharePoint 解决方案疑难解答 | Microsoft Docs
description: 了解使用 Visual Studio 调试器调试 SharePoint 解决方案时可能会出现的问题或警报。
ms.custom: SEO-VS-2020
ms.date: 02/22/2017
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Tools.SharePoint.Errors.Debugging
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, troubleshooting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: f4c69d5464d23fdeacbb77fb5af7b178a70d2fa5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663820"
---
# <a name="troubleshoot-sharepoint-solutions"></a>SharePoint 解决方案疑难解答
  使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 调试器调试 SharePoint 解决方案时可能会出现以下问题或警报。 有关详细信息，请参阅[调试 SharePoint 2007 工作流解决方案](/previous-versions/bb386166(v=vs.100))。

## <a name="token-restrictions-in-sandboxed-visual-web-parts"></a>沙盒可视 Web 部件中的令牌限制
 沙盒解决方案中的可视 Web 部件无法处理标准标记，例如 SharePoint 运行时支持的 $SPUrl。 因此不会解析 URL，并且如果您直接在脚本元素中引用 URL，则无法在可视 Web 部件设计器的“设计”视图中预览内容：

```xml
<script src="<% $SPUrl:~site/SiteAssets/ListOperations.js %>"></script>
```

 若要解决此限制并解析标记，请使用以下文本引用标记：

```xml
<asp:literal ID="Literal1" runat="server" Text="<script src='" />
<asp:literal ID="Literal2" runat="server" Text="<% $SPUrl:~site/SiteAssets/ListOperations.js %>" />
<asp:literal ID="Literal3" runat="server" Text="' type='text/javascript' ></script>" />
```

## <a name="character-restrictions-in-names-of-projects-and-project-items"></a>项目和项目项名称中的字符限制
 在 SharePoint 2010 中，项目和项目项名称只能包含部署路径中有效的字符。 不允许其他字符。

### <a name="error-message"></a>错误消息
 “无效字符”错误消息。

### <a name="resolution"></a>解决方法
 对于 SharePoint 项目和项目项名称，仅使用以下字符：

- 字母数字 ASCII 字符

- Space

- 句点 (.)

- 逗号 (,)

- 下划线 (_)

- 短划线 (-)

- 反斜杠 (\\)

  在打包项目时，验证规则将验证要部署的每个文件的部署路径属性是否只包含上述有效字符。

## <a name="errors-when-creating-custom-fields"></a>创建自定义字段时出错
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的自定义字段是使用 XML 定义的。 如果未使用特定格式定义或引用字段，则会出错。

### <a name="error-message"></a>错误消息
 打包时出现“无效字符”错误消息。

### <a name="resolution"></a>解决方法
 如下面的示例所示，字段定义的 ID 必须是大括号括起来的 GUID：

```xml
<Field ID="{5744d18c-305e-4632-8bd1-09d134f4830d}"
    Type="Note"
    Name="PatientName"
    DisplayName="Patient Name"
    Group="A Custom Group">
</Field>.
```

 下面的示例表明，内容类型中的字段引用必须用空元素格式 (\<FieldRef />) 而不是开始/结束元素 (\<FieldRef>\</FieldRef>) 进行定义：

```xml
<FieldRef ID="{5744d18c-305e-4632-8bd1-09d134f4830d}"
    Name="PatientName"
    DisplayName="Patient Name"
    Required="TRUE"/>
```

 如果字段的源 XML 格式不正确、不是有效的 XML 文件或出现一些其他问题，则会出现“无法分析文件”错误。

## <a name="new-non-english-site-definitions-do-not-appear-in-site-creation-page-after-deployment"></a>部署后，新的非英语站点定义不会出现在站点创建页中
 使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的非英语版本（即区域设置 [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] 不是 1033 的版本）创建和部署站点定义后，“SharePoint 自定义”选项卡不显示在“模板选择”框中，并且新的站点模板不显示在“新建 SharePoint 网站”页中。

### <a name="error-message"></a>错误消息
 无。

### <a name="resolution"></a>解决方法
 发生此问题的原因是 webtemp 站点定义配置文件（例如 webtemp_SiteDefinitionProject1.xml）的 Path 属性中的值不正确。 在 webtemp 文件的 Path 属性（位于“部署位置”下）中，将 1033 更改为相应的区域设置 [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]。 例如，若要使用日语区域设置，请将值更改为 1041。 有关详细信息，请参阅 [Microsoft 分配的区域设置 ID](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)。

## <a name="error-appears-when-a-workflow-project-is-deployed-on-a-clean-system"></a>在干净系统上部署工作流项目时出现错误
 如果在干净系统上部署 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的工作流项目，则会发生此问题。 干净系统是指以全新方式安装了 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和 SharePoint 但未部署工作流项目的计算机。

### <a name="error-message"></a>错误消息
 找不到 SharePoint 列表：工作流历史记录。

### <a name="resolution"></a>解决方法
 发生此错误是因为缺少工作流历史记录列表。 由于开发环境是一个干净的系统，因此不会部署任何工作流，并且工作流历史记录列表尚不存在。 若要解决此问题，请重新打开工作流向导，这将导致创建工作流历史记录列表。

##### <a name="to-reenter-the-workflow-wizard"></a>重新进入工作流向导

1. 在解决方案资源管理器中，选择工作流节点。

2. 在“属性”窗口中，选择具有省略号按钮的任何属性上的省略号 (...) 按钮。

## <a name="user-must-refresh-application-page-in-browser-while-debugging-to-view-updated-image"></a>用户调试时必须在浏览器中刷新应用程序页，以查看更新后的图像
 如果要调试包含具有显示图像的控件（如 [!INCLUDE[TLA2#tla_html](../sharepoint/includes/tla2sharptla-html-md.md)] 图像控件）的应用程序页的 SharePoint 解决方案，则必须在浏览器中刷新页面以显示对图像进行的任何更改。

## <a name="error-the-site-location-is-not-valid"></a>错误：站点位置无效
 如果未安装 [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]，则可能会出现此问题。 如果对“SharePoint 自定义向导”中指定的 SharePoint 网站没有管理员访问权限，也可能会发生此错误。

### <a name="error-message"></a>错误消息

- SharePoint 站点位置无效。

### <a name="resolution"></a>解决方法

- 安装 [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]。

- 确保你具有对 SharePoint 网站的管理员访问权限。 有关详细信息，请参阅 [!INCLUDE[TLA2#tla_office](../sharepoint/includes/tla2sharptla-office-md.md)] 联机文章[在 SharePoint Server 中分配或删除服务应用程序的管理员](/sharepoint/administration/assign-or-remove-administrators-of-service-applications)。

## <a name="site-deletion-web-event-does-not-occur-in-event-receiver-project"></a>站点删除 Web 事件不会在事件接收器项目中发生
 创建事件接收器项目并选择某些 Web 事件（例如“正在删除站点”）时，永远不会发生该事件。

### <a name="error-message"></a>错误消息
 无。

### <a name="resolution"></a>解决方法
 发生此问题的原因是，功能范围必须是“站点”以处理站点级事件，但事件接收器项目的默认功能范围是“Web”。 受影响的 Web 事件包括：

- 正在删除站点 (WebDeleting)

- 已删除站点 (WebDeleted)

- 正在移动站点 (WebMoving)

- 已移动站点 (WebMoved)

  若要解决此问题，请更改事件接收器的功能范围，如下所示。

##### <a name="to-change-the-feature-scope-of-the-event-receiver"></a>更改事件接收器的功能范围

1. 在解决方案资源管理器的“功能设计器”中，通过双击文件或打开其快捷菜单并选择“打开”来打开事件接收器的 .feature 文件。 

2. 选择“范围”旁边的箭头，然后在显示的列表中选择“站点”。 

## <a name="deployment-error-appears-after-the-name-of-an-identifier-in-a-business-data-connectivity-model-project-is-changed"></a>更改业务数据连接模型项目中标识符的名称后，会出现部署错误
 如果更改业务数据连接 (BDC) 模型中的实体的标识符名称，然后尝试部署解决方案，则会出现此问题。

### <a name="error-messages"></a>错误消息

- \<*model name*> 具有以下外部内容类型激活错误...

- 名为“\<*model name*>”的 IMetadataObject 在“名称”字段中具有重复值...

### <a name="resolution"></a>解决方法
 若要解决此问题，请手动删除模型，然后再次部署解决方案。  可以使用以下工具之一删除模型：

- SharePoint 2010 管理中心。 有关详细信息，请参阅 Microsoft TechNet 网站上的 [BDC 模型管理](/previous-versions/office/sharepoint-server-2010/ee524073(v=office.14)#delete-a-bdc-model)。

- Windows PowerShell。 可以通过在命令提示符下键入以下命令来删除模型：Remove-SPBusinessDataCatalogModel。 有关详细信息，请参阅 Microsoft TechNet 网站上的[常规 cmdlet (SharePoint Server 2010)](/powershell/module/sharepoint-server)。

## <a name="an-error-appears-when-you-try-to-view-a-visual-web-part-in-sharepoint"></a>尝试在 SharePoint 中查看可视 Web 部件时，会出现错误
 如果用户控件的 Path 属性不以字符串“CONTROLTEMPLATES\\”开头，则会出现此问题。

### <a name="error-messages"></a>错误消息

- 文件“/_CONTROLTEMPLATES/\<project name>/\<Web Part name>/\<user control name>.ascx”不存在。

- '/' 应用程序中出现服务器错误。

### <a name="resolution"></a>解决方法

##### <a name="to-resolve-this-issue"></a>解决方法

1. 在解决方案资源管理器中，选择文件扩展名是 .ascx 的用户控件文件。

2. 在菜单栏上，选择“视图” > “属性窗口”。

3. 在“属性”窗口中，展开“部署位置”节点。 

4. 确保“路径”属性的值以字符串“CONTROLTEMPLATES\\”开头。

## <a name="error-appears-when-an-imported-reusable-workflow-that-contains-a-task-form-field-is-run"></a>运行包含任务窗体字段的导入可重用工作流时出现错误
 如果导入包含具有字段的任务窗体的工作流，然后在导入该工作流的同一系统运行新工作流，则会出现此问题。

### <a name="error-message"></a>错误消息
 部署步骤“激活功能”出错：在当前站点集或子站点中找到了在功能 [guid] 中定义的 Id 为 [Guid] 的字段。

### <a name="resolution"></a>解决方法
 发生此错误的原因是，由于 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的“导入可重用工作流”项目不会更改任务窗体字段 ID 而发生字段 ID 冲突。 如果在包含原始工作流的同一服务器上部署导入的工作流，则会发生字段 ID 冲突。

 若要解决此问题，请使用“查找和替换”功能更改所有导入的工作流文件中的“字段 ID”属性的值。

## <a name="error-appears-when-a-renamed-imported-list-instance-is-run"></a>运行重命名的导入列表实例时出现错误
 如果重命名导入的列表实例，然后在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中运行，则会出现此问题。

### <a name="error-message"></a>错误消息
 生成错误：部署步骤“激活功能”发生错误：文件 Template\Features\\[导入项目<em>功能</em>名称]\Files\Lists\\[旧<em>列表名称</em>]\Schema.xml 不存在。

### <a name="resolution"></a>解决方法
 导入列表实例时，名为 CustomSchema 的属性将添加到列表实例的 Elements.xml 文件。 Elements.xml 包含列表实例的自定义 schema.xml 的路径。 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中重命名列表实例时，自定义 schema.xml 的部署路径会更改，但 CustomSchema 属性的路径值不会更新。 因此，当激活该功能时，列表实例在 CustomSchema 属性指定的旧路径中找不到 schema.xml 文件。

 若要解决此问题，请在 CustomSchema 属性中更新 schema.xml 文件的部署位置的路径。

## <a name="sharepoint-debugging-session-terminated-by-iis"></a>IIS 终止了 SharePoint 调试会话
 如果您在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 解决方案中设置一个断点，再选择 F5 键运行该解决方案，然后在断点处停留 90 秒以上，则会发生此问题。

### <a name="error-message"></a>错误消息
 正在调试的 Web 服务器进程已被 Internet Information Services (IIS) 终止。 您可通过在 IIS 中配置应用程序池 Ping 设置来避免此问题。 有关更多详细信息，请参阅帮助。

### <a name="resolution"></a>解决方法
 默认情况下，IIS 应用程序池等待 90 秒，以使应用程序在关闭应用程序之前做出响应。 此过程称为正在对应用程序执行“ping”。 若要解决此问题，可以增加等待时间或完全禁用应用程序 ping。

##### <a name="to-access-the-iis-app-pool-settings"></a>访问 IIS 应用池设置

1. 打开 IIS 管理器。

2. 在“连接”窗格中展开 SharePoint 服务器节点，然后选择“应用程序池”节点。 

3. 在“应用程序池”页上，选择“SharePoint 应用程序池”（通常为“SharePoint - 80”），然后在“操作”窗格中选择“高级设置”链接。

4. 若要增加 IIS 超时前的等待时间，请将“Ping 最大响应时间(秒)”的值更改为一个大于 90 秒的值。

5. 若要禁用 IIS ping，请将“启用 Ping”设置为“False”。

## <a name="auto-retract-leaves-orphaned-list-instance-in-sharepoint"></a>自动收回将孤立列表实例留在 SharePoint 中
 如果执行以下步骤，会出现此问题。

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中创建具有列表实例的列表定义。

2. 选择 F5 键以运行该解决方案。

3. 停止调试或关闭 SharePoint 站点。

4. 重新打开 SharePoint 站点并打开列表实例。

### <a name="error-message"></a>错误消息
 '/' 应用程序中出现服务器错误。

### <a name="resolution"></a>解决方法
 发生这种情况的原因是，关闭 SharePoint 解决方案的调试会话后，自动收回功能会收回解决方案。 收回会从 SharePoint 中删除列表定义，但不会删除列表的实例。 列表实例需要基础列表定义。

 若要解决此问题，请在菜单栏上依次选择“生成” > “部署”以部署解决方案。  （不要通过选择 F5 键调试解决方案。）然后，在 SharePoint 中删除列表实例。

## <a name="original-sharepoint-solution-is-replaced-by-an-exported-version"></a>原始 SharePoint 解决方案将替换为导出的版本
 如果导出 SharePoint 解决方案，将解决方案导入 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，然后将解决方案部署回导出它的同一站点，将替换原始 SharePoint 解决方案。 如果将解决方案部署到未激活原始解决方案的服务器，则不会发生此问题。

### <a name="error-message"></a>错误消息
 无。

### <a name="resolution"></a>解决方法
 若要避免替代从其中导出解决方案的站点上的解决方案，请更改 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 项目中所有导入功能的 SolutionID 的 GUID 和功能 ID。

## <a name="error-appears-when-debugging-starts"></a>开始调试时出错
 在 Visual Studio 中开始调试 SharePoint 解决方案时出现错误，表明由于字典中没有给定键，Visual Studio 无法加载 Web.config 文件。

### <a name="error-message"></a>错误消息
 无法加载 Web.config 配置文件。 检查文件中是否有格式错误的 XML 元素，然后重试。 发生以下错误：字典中不存在给定键。

### <a name="resolution"></a>解决方法
 若要解决此问题，请确保 Visual Studio 中的 SharePoint 项目的“站点 URL”属性值与分配给 Web 应用程序的备用访问映射的默认区域的 URL 一致。 对 URL 使用其他区域（如 Intranet）将无法解决此错误。 项目的站点 URL 与默认区域中的 URL 必须一致。 要访问备用访问映射，请打开 SharePoint 2010 管理中心实用工具，选择“应用程序管理”链接，然后，在“Web 应用程序”下，选择“配置备用访问映射”链接。   有关详细信息，请参阅[为 Web 应用程序创建区域](/previous-versions/office/sharepoint-2007-products-and-technologies/cc263087(v=office.12))。

## <a name="see-also"></a>另请参阅

- [SharePoint 打包和部署疑难解答](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [在 Visual Studio 中进行调试](../debugger/debugger-feature-tour.md)