---
title: 操作说明：添加和删除映射文件夹 | Microsoft Docs
description: 在 SharePoint 中为项目添加和删除映射文件夹。  更改映射文件夹的部署位置。 重命名或删除映射文件夹。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.Project.MappedFolder
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, mapped folders
- mapped folders [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: b632b9e261b2420d932be71e0cbc1216ae94b6ef
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600604"
---
# <a name="how-to-add-and-remove-mapped-folders"></a>操作说明：添加和删除映射文件夹

  SharePoint 中的一些常用文件夹（如 Images 和 Layouts）深度嵌入在文件层次结构中。 你可以将这些文件夹映射到 SharePoint 项目，以便更轻松地访问它们。 映射文件夹是 SharePoint 项目中的文件夹，与 SharePoint Server 安装中的文件的物理位置相对应。

 部署 SharePoint 应用程序时，解决方案包 (.wsp) 会将映射文件夹及其所有子文件夹的内容复制到在 SharePoint 文件夹树中的指定位置运行 SharePoint 的服务器上。 此位置由为映射文件夹设置的“部署位置”属性确定。 映射文件夹中的任何子文件夹都相对于映射文件夹的“部署位置”。 请注意，“部署位置”属性（而不是映射文件夹的名称）决定了项的部署位置。
可以使用菜单栏或项目快捷菜单上的命令将映射文件夹添加到项目。 可以使用“添加 SharePoint‘Images’映射文件夹”和添加“SharePoint‘Layouts’文件夹”命令添加最常用的映射文件夹。 可以使用快捷菜单上的"添加 SharePoint 映射文件夹”命令，然后在“添加 SharePoint 映射文件夹”对话框中指定文件夹，将任何其他可用的 SharePoint 文件夹映射到项目。

## <a name="add-mapped-folders-to-a-project"></a>将映射文件夹添加到项目

 下面的过程介绍如何将两个映射文件夹添加到可视 Web 部件项目。 首先，创建一个可视 Web 部件项目。

## <a name="to-add-mapped-folders-to-a-project"></a>将映射文件夹添加到项目

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。
::: moniker range="=vs-2017"
2. 在“新建项目”对话框中，展开“Visual Basic”或“Visual C#”节点，展开“Office/SharePoint”节点，然后选择“SharePoint 解决方案”节点。

3. 在项目模板列表中，选择“SharePoint 2013 可视 Web 部件”模板。

4. 在“名称”框中，输入“TestProject1”，然后选择“确定”按钮。
::: moniker-end
::: moniker range=">=vs-2019"
2. 在“创建新项目”对话框中，为已安装的 SharePoint 的特定版本选择“SharePoint 可视 Web 部件”。 例如，如果安装了 SharePoint 2019，请选择“SharePoint 2019 可视 Web 部件”模板。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

3. 在“名称”框中，输入“TestProject1”
4. 然后选择“创建”按钮。
::: moniker-end

5. 在“SharePoint 自定义向导”中，选择“完成”按钮以保留默认设置。

6. 在“解决方案资源管理器”中，选择项目节点，然后在菜单栏上选择“项目” > “添加 SharePoint‘Images’映射文件夹”。

     名为 Images 的文件夹显示在项目中，其中包含名为 TestProject1 的子文件夹。 此映射文件夹将包含可视 Web 部件项目的映像。

7. 在“解决方案资源管理器”中，选择项目节点，然后在菜单栏上选择“项目” > 添加 SharePoint 映射文件夹”以显示“添加SharePoint映射文件夹”对话框。

8. 在可用于映射的文件夹的树视图中，选择“Resources”文件夹，然后选择“确定”按钮。

     名为“Resources”的文件夹将显示在项目中。 此文件夹可以存储诸如字符串资源文件之类的项。 子文件夹可用于组织映射文件夹的内容，但当你使用“添加 SharePoint 映射文件夹”命令添加映射文件夹时，子文件夹不会自动创建。 若要添加子文件夹，请选择“Resources”文件夹，然后在菜单栏上选择“项目” > “新建文件夹”。

## <a name="change-the-deployment-location-of-a-mapped-folder"></a>更改映射文件夹的部署位置

 默认情况下，映射文件夹将添加到相对于令牌 \<SharePointRoot> 所表示的 SharePoint 根安装路径的特定位置。 但是，可以通过更改映射文件夹的“部署位置”属性来更改此位置。 每个映射文件夹都有自己的“部署位置”属性。

### <a name="to-change-the-deployment-location-of-a-mapped-folder"></a>更改映射文件夹的部署位置

1. 在之前创建的项目中，选择一个映射文件夹。

2. 在“属性”窗口中，选择“部署位置”属性上的省略号（![ASP.NET 移动设计器中的省略号](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")）按钮。

3. 在“SharePoint 映射文件夹”对话框中，浏览到希望映射文件夹指向的文件夹。

4. 选择节点，然后选择“确定”按钮。

## <a name="rename-or-remove-mapped-folders"></a>重命名或删除映射文件夹

### <a name="to-rename-or-remove-a-mapped-folder"></a>重命名或删除映射文件夹

1. 在之前创建的项目中，选择一个映射文件夹。

2. 若要重命名映射文件夹，请打开其快捷菜单，选择“重命名”，输入新名称，然后按 Enter 键。

     或者，可以选择要重命名的映射文件夹，打开“属性”窗口，然后将“文件夹名称”属性的值设置为新名称。

3. 若要从项目中删除映射文件夹，请打开其快捷菜单，选择“删除”，然后选择对话框中的“确定”按钮确认删除。

## <a name="see-also"></a>另请参阅

- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
