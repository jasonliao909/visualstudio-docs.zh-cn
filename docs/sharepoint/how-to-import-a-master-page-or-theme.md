---
title: 如何：导入母版页或主题 | Microsoft Docs
description: 在 SharePoint Designer 中为母版页和主题制作模板，然后导入 Visual Studio 以便在 SharePoint 站点的页面上提供一致的外观。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664158"
---
# <a name="how-to-import-a-master-page-or-theme"></a>如何：导入母版页或主题
  可以通过创建和使用母版页和主题来在 SharePoint 站点的页面上提供一致的外观。 虽然 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 不会为这些元素提供模板，但是可以在 SharePoint Designer 创建这些模板，然后将其导入 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 有关详细信息，请参阅 Microsoft 网站上的[生成块：页面和用户界面](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14))。

### <a name="to-import-a-master-page-or-theme"></a>若要导入母版页或主题

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，创建或打开一个 SharePoint 项目。

     有关如何创建 SharePoint 项目的信息，请参阅 [SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 在“添加新项”对话框中，展开“SharePoint”节点，然后选择“2010”节点。

4. 在 SharePoint 模板列表中，选择“模块”模板，然后指定模块的名称。

     模块包含用于部署到在 SharePoint 中指定的位置的文件（例如，母版页或主题文件）。

5. 在模块中，删除名为 Sample.txt 的默认文件。

6. 选择模块节点。

7. 在菜单栏上，选择“项目” > “添加现有项”，然后选择母版页或主题文件。

     母版页文件具有 .master 扩展，主题文件具有 .thmx 扩展。

8. 如果添加了母版页，请在模块的属性中将其“部署冲突解决方案”设置更改为“自动”。 

    > [!NOTE]
    > 如果母版页的名称与现有母版页的名称（标记为“默认母版页”或“自定义母版页”）相同，则会发生错误。 有关如何解决该问题的信息，请参阅[演练：导入带有图像的自定义母版页和网站页面](../sharepoint/walkthrough-import-a-custom-master-page-and-site-page-with-an-image.md)。

9. 在模块中，打开 Elements.xml。

     必须更新 Elements.xml 文件，才能引用添加的母版页或主题。

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

     请确保将占位符值替换为模块、母版页或主题的实际名称。

     特性 `Type="GhostableInLibrary"` 指示已将项添加到内容数据中，模块的 `Url` 特性指定在 SharePoint 内容数据库中存储文件的位置。

11. 若要更改母版页的部署范围，请在“解决方案资源管理器”的“功能设计器”中打开功能文件，然后从“范围”列表选择新的部署范围。 

     Web 值表示母版页仅应用于当前在项目中指定的网站。 “站点”值表示母版页应用于当前网站集，其中包含所有子网站和根目录 Web。 其他值不适用。

    > [!NOTE]
    > 由于主题仅应用于网站集，我们建议不要将主题范围设置为除“站点”之外的其他任何内容。 如果在子网站中使用了主题，则可能会出现错误。

12. 在菜单栏上，选择“生成” > “部署解决方案”。

13. 若要验证是否已正确部署这些文件，请打开 SharePoint 站点，依次选择“站点操作”菜单和“站点设置”命令，然后选择“母版页”链接或“主题”链接。   

     将显示母版页列表或主题列表，其中包含已导入的母版页或主题。

## <a name="see-also"></a>另请参阅
- [母版页](/previous-versions/office/developer/sharepoint-2010/ms443795(v=office.14))
- [从现有的 SharePoint 网站导入项](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [为 SharePoint 创建页](../sharepoint/creating-pages-for-sharepoint.md)
- [使用模块包括解决方案中的文件](../sharepoint/using-modules-to-include-files-in-the-solution.md)
