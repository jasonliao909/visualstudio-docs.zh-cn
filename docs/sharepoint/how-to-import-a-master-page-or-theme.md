---
title: 如何：导入母版页或主题|Microsoft Docs
description: 在设计器中为母版页和主题SharePoint模板，然后导入Visual Studio，使SharePoint站点中的页面具有一致的外观。
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
ms.openlocfilehash: 69d304d476be4b1e0ab97500b1f13b04bd68ff1f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122093003"
---
# <a name="how-to-import-a-master-page-or-theme"></a>如何：导入母版页或主题
  可以通过创建和使用母版页和SharePoint为站点中的页面提供一致的外观。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]不提供这些元素的模板，但可以在设计器SharePoint模板，然后将它们导入 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 有关详细信息，请参阅 Microsoft 网站上 [构建基块：用户界面](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14)) 和页面。

### <a name="to-import-a-master-page-or-theme"></a>导入母版页或主题

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，创建或打开SharePoint项目。

     若要了解如何创建项目SharePoint，请参阅SharePoint[和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 在"**添加新项"** 对话框中，展开"SharePoint"**节点**，然后选择 **"2010"** 节点。

4. 在模板SharePoint，选择"模块"模板，然后指定模块的名称。

     模块包含 (文件，例如母版页或主题) ，用于部署到在 SharePoint 中指定的位置。

5. 在模块中，删除名为 的默认文件，该文件 *Sample.txt。*

6. 选择模块节点。

7. 在菜单栏上，选择  >  **Project"添加现有项**"，然后选择母版页或主题文件。

     母版页文件具有 .master 扩展名，主题文件具有 .thmx 扩展名。

8. 如果添加了母版页，请在其模块属性 **中将"部署冲突** 解决"设置更改为"自动"。 

    > [!NOTE]
    > 如果母版页的名称与标记为"默认母版页"或"自定义母版页"的现有母版页的名称相同，则可能会发生错误。 若要了解如何解决此问题，请参阅演练：导入具有映像 的自定义母版页 [和站点页](../sharepoint/walkthrough-import-a-custom-master-page-and-site-page-with-an-image.md)。

9. 在模块中 *，打开* Elements.xml。

     必须 *更新Elements.xml以* 引用添加的母版页或主题。

10. 对于母版页，请将现有模块标记替换为以下标记。

    ```xml
    <Module Name="[Module Name]" Url="_catalogs/masterpage">
        <File Path="[Module Name]\[Master Page Name].master"
          Url="[Master Page Name].master" Type="GhostableInLibrary" />
    </Module>
    ```

     对于主题，请将现有模块标记替换为以下标记。

    ```xml
    <Module Name="[Module Name]" Url="_catalogs/theme"
        <File Path="[Module Name]\[Theme Name].thmx" Url="[Theme
          Name].thmx" Type="GhostableInLibrary" />
    </Module>
    ```

     请务必将占位符值替换为模块的实际名称以及母版页或主题。

     属性指示将项添加到内容数据库，模块的 属性指定文件在内容数据库中的SharePoint `Type="GhostableInLibrary"` `Url` 位置。

11. 若要更改母版页的部署范围，解决方案资源管理器，在"功能设计器"中打开功能文件，然后从"范围"列表中选择新的 **部署** 范围。

     值为 **Web** 表示母版页仅适用于项目中当前指定的网站。 值为 **Site** 表示母版页适用于当前网站集，其中包括所有子网站和根 Web。 其他值不适用。

    > [!NOTE]
    > 由于主题仅适用于网站集级别，因此建议不要将主题的范围设置为除"站点"外 **的其他任何内容**。 如果在子站点中使用了主题，则可能会出现错误。

12. 在菜单栏上，选择"**生成部署**  >  **解决方案"。**

13. 若要验证文件是否已正确部署，请打开 SharePoint 站点，选择"站点操作"菜单，选择"站点 **设置"命令，** 然后选择"母版页"链接或"**主题"链接**。

     将显示母版页或主题的列表，其中包含已导入的母版页或主题。

## <a name="see-also"></a>请参阅
- [母版页](/previous-versions/office/developer/sharepoint-2010/ms443795(v=office.14))
- [从现有站点导入SharePoint项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [为 SharePoint 创建页](../sharepoint/creating-pages-for-sharepoint.md)
- [使用模块包括解决方案中的文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)
