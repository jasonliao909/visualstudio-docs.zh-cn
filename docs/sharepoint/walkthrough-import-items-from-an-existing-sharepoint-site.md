---
title: 演练：从现有站点站点SharePoint导入|Microsoft Docs
titleSuffix: ''
description: 在此演练中，将现有项目站点中的SharePoint导入到Visual Studio SharePoint项目中。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- importing items [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 17f16b02749fe1431f1016334c96855ee505a0a7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122115351"
---
# <a name="walkthrough-import-items-from-an-existing-sharepoint-site"></a>演练：从现有的 SharePoint 网站导入项
  本演练演示如何将现有项目站点中的SharePoint导入到SharePoint [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 项目中。

 本演练演示了下列任务：

- 通过添加SharePoint站点列来自定义站点 (也称为字段 *。*

- 将SharePoint导出到 .wsp 文件。

- 使用 .wsp 导入SharePoint [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 .wsp 文件导入到文件中。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- 支持的 和 [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] SharePoint。

- Visual Studio。

## <a name="customize-a-sharepoint-site"></a>自定义SharePoint站点
 对于此示例，你将通过向子SharePoint一个新的站点列，并创建另一个子站点供以后使用来创建和自定义该子站点。 稍后，你将第一个子站点导出到 .wsp 文件，然后使用 .wsp Import 项目将自定义站点列导入第二个子站点。

### <a name="to-create-and-customize-a-sharepoint-site"></a>创建和自定义SharePoint站点

1. 使用 Web SharePoint（例如系统名称<em></em>/SitePages/Home.aspx）http:// 站点。

2. 打开"站点操作"菜单，然后选择"新建SharePoint **站点"，** 在主站点外 **创建子站点**。

3. 在站点的"创建 **"** 对话框中，选择" **空白站点类型** "。

4. 在" **标题"** 框中，输入 **"站点列测试 1";** 在 **"URL 名称"** 框中，输入 **columntest1**;将其他设置保留为默认值;然后选择"创建 **"** 按钮。

5. 创建站点后，在浏览器中导航回主站点，http://<em></em>/SitePages/Home.aspx。

6. 同样，通过打开"站点操作"菜单，选择"新建站点"，然后选择"空白站点类型"，在主站点SharePoint创建 **一个空白子** 站点。

7. 在" **标题"** 框中，输入 **"站点列测试 2";** 在 **"URL 名称"** 框中，输入 **columntest2**;将其他设置保留为默认值;然后选择"创建 **"** 按钮。

8. 导航回第一个子站点，http://<em>SystemName</em>/columntest1/default.aspx。

9. 在"**站点操作"** 菜单上，选择"站点 **设置** 以显示"站点设置页。

10. 在" **库"** 部分中，选择" **站点列"** 链接。

11. 在"站点列 **库"页的顶部** ，选择"创建 **"** 按钮。

12. 在" **列名称"** 框中， **输入"测试列**"，保留其他默认值，然后选择"确定 **"** 按钮。

13. " **测试列** "列显示在"站点列库"的"自定义列"标题下。

## <a name="exporting-the-sharepoint-site"></a>导出SharePoint站点
 接下来，SharePoint一 (.wsp) 文件，其中包含要导入到 SharePoint 项目中的 SharePoint 项 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和元素。 如果还没有 .wsp 文件，则必须从现有站点创建一SharePoint文件。 对于此示例，将默认站点SharePoint导出到 .wsp 文件中。

> [!IMPORTANT]
> 如果在执行以下过程时收到运行时错误，你必须在有权访问该站点SharePoint过程。

### <a name="to-export-an-existing-sharepoint-site"></a>导出现有 SharePoint 站点

1. 在 SharePoint 站点中，选择 **"站点** 设置 **选项卡** 上的"站点""站点"，以显示"站点设置页。

2. 在"**站点"** 页的"站点操作设置，选择"将 **站点另存为模板"** 链接。

3. 在"**文件名"** 框中，输入 **ExampleSite**，在"**模板名称"框中** 输入 **"示例站点"。**

4. 对于此示例，请清除 **"包括内容** "复选框。

     如果选中此框， [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 则会将所有列表和文档库及其内容保存到 .wsp 文件。 尽管在某些情况下这很有用，但此示例不需要这样做。

5. 操作成功完成后，选择 **解决方案库** 链接以查看 .wsp 文件。

     若要稍后查看解决方案库页，请打开"站点操作"菜单，选择"站点 **设置"，** 选择"网站集管理"部分中的"转到顶层站点设置"链接，然后选择"库"部分中的"解决方案 **"链接。** 

6. 在解决方案库中，选择 **"ExampleSite"** 链接。

7. 在"**文件下载**"对话框中，选择"保存"按钮，将文件默认保存到本地系统下载文件夹中。

## <a name="import-the-wsp-file"></a>导入 .wsp 文件
 现在，你有一个 *.wsp* 文件，其中包含要重复使用的项 (自定义站点列测试列) ，导入 *.wsp* 文件以访问它。

### <a name="to-import-a-wsp-file"></a>导入 .wsp 文件

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的菜单栏上，选择"文件  >    >  **""** 新建Project以显示"新建Project对话框。 如果 IDE 设置为使用Visual Basic设置，在菜单栏上，选择"文件""新建  >  **Project"。**

2. 在 Visual **C#** SharePoint下展开"Visual Basic"**节点**，然后选择 **"2010"** 节点。

3. 在"模板SharePoint中选择"导入 **2010** 解决方案包"模板，将项目名称保留为 WspImportProject1，然后选择"确定 **"** 按钮。

    将显示 **SharePoint自定义向导**。

4. 在 **"指定用于** 调试的站点和安全级别"页上，为之前创建的SharePoint [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 子站点输入 。 将新的自定义字段项（http://<em>名称</em>/columntest2）添加到该子站点。

5. 在"**此解决方案的信任级别SharePoint？"** 部分中，将所选内容保留为"部署 **为沙盒解决方案"。**

6. 在 **"指定新项目源** "页中，浏览到系统上以前 *保存 .wsp* 文件的位置，然后选择"下一步 **"** 按钮。

   > [!NOTE]
   > 如果在此页上 **选择** "完成"按钮，将导入 *.wsp* 文件的所有可用项。

7. 在" **选择要导入的项** "框中，清除列表中除"测试列"之外的所有复选框 **，然后选择**"完成 **"** 按钮。

    由于列表包含多个项，因此可以选择 **Ctrl** A 键以选择列表中的所有项，选择空格键以清除所有复选框，然后仅选中"测试列"项旁边的复选框。 +  

    导入操作完成后，将创建名为 **WspImportProject1** 的新项目，其中包含名为 **Fields 的文件夹**。 在此文件夹中，自定义站点列"测试 **列** " *及其定义文件* Elements.xml。

## <a name="deploy-the-project"></a>部署项目
 最后，将 **WspImportProject1** 部署到SharePoint创建的第二个子站点，以查看自定义站点列。

### <a name="to-deploy-the-project"></a>部署项目

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，选择要部署和运行 *.wsp* 导入项目的 **F5** 密钥。

2. 在SharePoint，打开"**站点** 操作"菜单，然后选择"站点 **设置以显示"** 站点设置页。

3. 在" **库"** 部分中，选择" **站点列"** 链接。

4. 向下滚动到"自定义 **列"** 部分。

     请注意，从第一个站点导入的自定义SharePoint显示在列表中。

## <a name="see-also"></a>请参阅
- [从现有的 SharePoint 网站导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [为 Web 部件或应用程序页创建可重用控件](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
