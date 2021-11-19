---
title: 如何：添加和移除映射文件夹 |Microsoft Docs
description: 在 SharePoint 中添加和移除映射文件夹到项目。  更改映射文件夹的部署位置。 重命名或删除映射文件夹。
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
# <a name="how-to-add-and-remove-mapped-folders"></a>如何：添加和移除映射文件夹

  SharePoint 中的一些常用文件夹（如图像和布局）在文件层次结构中深度嵌入。 您可以将这些文件夹映射到 SharePoint 项目，以便更轻松地访问它们。 映射文件夹是 SharePoint 项目中的文件夹，与 SharePoint 服务器的安装中的文件的物理位置相对应。

 部署 SharePoint 应用程序时，会将映射文件夹及其所有子文件夹的内容)  ( 复制到运行 SharePoint 在 SharePoint 文件夹树中指定位置的服务器上。 此位置由为映射文件夹设置的 **部署位置** 属性确定。 映射文件夹中的所有子文件夹都相对于映射文件夹的 **部署位置** 。 请注意， **部署位置** 属性（而不是映射文件夹的名称）确定部署项目的位置。
您可以使用菜单栏或项目的快捷菜单上的命令将映射文件夹添加到项目。 你可以使用 "**添加 SharePoint" Images "映射文件夹**，并 **添加 SharePoint" 布局 "文件夹** 命令添加最常使用的映射文件夹。 您可以通过使用快捷菜单上的 "**添加 SharePoint 映射文件夹**" 命令，然后在 "**添加 SharePoint 映射文件夹**" 对话框中指定文件夹，将任何其他可用的 SharePoint 文件夹映射到您的项目。

## <a name="add-mapped-folders-to-a-project"></a>将映射文件夹添加到项目

 下面的过程介绍如何将两个映射文件夹添加到可视 web 部件项目。 首先，创建一个可视 web 部件项目。

## <a name="to-add-mapped-folders-to-a-project"></a>将映射文件夹添加到项目

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。
::: moniker range="=vs-2017"
2. 在 "**新建 Project** " 对话框中，展开 " **Visual Basic** " 或 " **Visual c #** " 节点，展开 " **Office/SharePoint** " 节点，然后选择 " **SharePoint 解决方案**" 节点。

3. 在项目模板列表中，选择 " **SharePoint 2013" 可视 Web 部件** 模板。

4. 在 " **名称** " 框中，输入 **TestProject1**，然后选择 " **确定"** 按钮。
::: moniker-end
::: moniker range=">=vs-2019"
2. 在 "**创建新 Project** " 对话框中，选择 *SharePoint 的 Visual Web Part**，以获取已安装 SharePoint 的特定版本。 例如，如果有 SharePoint 2019 安装，请选择 " **SharePoint 2019" 可视 Web 部件** 模板。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

3. 在 " **名称** " 框中，输入 **TestProject1**
4. 然后选择 " **创建** " 按钮。
::: moniker-end

5. 在 **SharePoint 自定义向导** 中，选择 "**完成**" 按钮以保留默认设置。

6. 在 **解决方案资源管理器** 中，选择 "项目" 节点，然后在菜单栏上选择 " **Project**  >  **添加 SharePoint" Images "映射文件夹**。

     名为 **Images** 的文件夹出现在项目中，并包含名为 TestProject1 的子文件夹。 此映射文件夹将包含可视 web 部件项目的图像。

7. 在 **解决方案资源管理器** 中，选择 "项目" 节点，然后在菜单栏上选择 " **Project**  >  **添加 SharePoint 映射的文件夹**" 以显示 "**添加 SharePoint 映射文件夹**" 对话框。

8. 在可用于映射的文件夹的树视图中，选择 " **资源** " 文件夹，然后选择 " **确定"** 按钮。

     项目中会显示名为 " **资源** " 的文件夹。 此文件夹可以存储诸如字符串资源文件之类的项。 子文件夹可用于组织映射文件夹的内容，但当你使用 **add SharePoint 映射文件夹** 命令添加映射文件夹时，子文件夹不会自动创建。 若要添加子文件夹，请选择 "**资源**" 文件夹，然后在菜单栏上选择 " **Project**  >  **新文件夹**"。

## <a name="change-the-deployment-location-of-a-mapped-folder"></a>更改映射文件夹的部署位置

 默认情况下，映射的文件夹将添加到相对于令牌所表示的 SharePoint 根安装路径的特定位置 \<SharePointRoot> 。 但是，可以通过更改映射文件夹的 " **部署位置** " 属性来更改此位置。 每个映射文件夹都有其自己的 **部署位置** 属性。

### <a name="to-change-the-deployment-location-of-a-mapped-folder"></a>更改映射文件夹的部署位置

1. 在之前创建的项目中，选择一个映射文件夹。

2. 在 "**属性**" 窗口中，选择 "**部署位置**" 属性上的省略号 (![ASP.NET Mobile 设计器 "椭圆形](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")) " 按钮。

3. 在 "**添加 SharePoint 映射文件夹**" 对话框中，浏览到要将映射文件夹指向的文件夹。

4. 选择节点，然后选择 **"确定"** 按钮。

## <a name="rename-or-remove-mapped-folders"></a>重命名或删除映射的文件夹

### <a name="to-rename-or-remove-a-mapped-folder"></a>重命名或删除映射文件夹

1. 在之前创建的项目中，选择一个映射文件夹。

2. 若要重命名映射文件夹，请打开其快捷菜单，选择 " **重命名**"，输入新名称，然后选择 enter 键。

     作为替代方法，您可以选择要重命名的映射文件夹，打开 " **属性** " 窗口，然后将 " **文件夹名称** " 属性的值设置为新名称。

3. 若要从项目中删除映射的文件夹，请打开其快捷菜单，选择 " **删除**"，然后在对话框中选择 **"确定** " 按钮以确认删除。

## <a name="see-also"></a>另请参阅

- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
