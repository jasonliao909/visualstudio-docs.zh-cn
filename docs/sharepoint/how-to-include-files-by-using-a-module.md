---
title: 如何：使用模块包括文件 | Microsoft Docs
description: 了解如何使用模块包括文件，该模块是一个容器，可用于将 ASPX 母版页、文本文件或图像等文件部署到 SharePoint。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, modules
- modules [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: d5f229d09ea5a4cceaa0f85dc89612636c072471
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664149"
---
# <a name="how-to-include-files-by-using-a-module"></a>如何：使用模块包括文件
  模块（不要与 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 模块混淆）是一个容器，可用于将 ASPX 母版页、文本文件或图像等文件部署到 SharePoint。

 你可以选择将文件部署到文档库，或者作为文档库外部的一个普通文件（例如，default.aspx）。 若要将文件添加到文档库，请指定 `Type="GhostableInLibrary"` 作为 File 元素中的一个属性。 此设置指示 SharePoint 在文件被添加到库时，创建一个要与该文件一起使用的列表项。 若要在文档库外部署文件，请指定 `Type="Ghostable"` 或仅省略 Type 属性。

## <a name="add-a-module-to-a-sharepoint-solution"></a>将模块添加到 SharePoint 解决方案

#### <a name="to-add-a-module"></a>添加模块

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中打开或创建一个 SharePoint 项目。

     有关详细信息，请参阅 [SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

2. 在解决方案资源管理器中，选择项目节点，然后在菜单栏上选择“项目” > “添加新项”  。

     此时将打开“添加新项”对话框。

3. 在 SharePoint 模板列表中，选择“模块”模板，然后选择“添加”按钮 。

     此步骤将在项目中创建名为 Module1 的节点。

4. 在 Module1 下，删除 Sample.txt 文件。

     Sample.txt 包含在所有新模块中，用于举例说明，因此不需要它。 （请注意，删除文件时，也会从模块的 Elements.xml 文件中删除其条目。）

5. 如果希望将文件部署到 SharePoint 中的特定文件夹结构，请在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的 Module1 下创建这些文件夹，方法是先选择 Module1 节点，然后在菜单栏上依次选择“项目”、“新建文件夹” 。

6. 选择要在其中添加文件的文件夹，然后在菜单栏上依次选择“项目”、“添加现有项” 。

7. 选择一个或多个要部署到 SharePoint 的文件，然后选择“添加”按钮。

     将文件添加到项目时，其条目会自动添加到模块的 Elements.xml 文件中。 部署项目时，文件被复制到 SharePoint 服务器，相对于项目的根目录，根目录由 File 元素的 URL 属性（如 `Url="Module1/New Folder/SomeFile.doc`）指定。 如果要更改文件的部署位置，请在解决方案资源管理器中将其移到另一个文件夹中，或更改其 URL  设置。

8. 对于你想要显示在文档库中的任何文件，将 `Type="GhostableInLibrary"` 属性追加到 Elements.xml 中的条目。 例如，

    ```xml
    <File Path="Module1\Some Folder\SomePage.aspx" Url="Module1/Some Folder/SomePage.aspx" Type="GhostableInLibrary" />
    ```

9. 部署该项目。

     文件将在 SharePoint 中复制到指定位置。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
