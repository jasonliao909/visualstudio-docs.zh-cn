---
title: 如何：使用模块模型包括|Microsoft Docs
description: 了解如何使用模块包括文件，该模块是一个容器，可用于将 ASPX 母版页、文本文件或图像等文件部署到SharePoint。
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
ms.openlocfilehash: a4642ac81acdc7df43e83628b05892d23bb39ad4319a8c110f1111a0d308f46b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121332022"
---
# <a name="how-to-include-files-by-using-a-module"></a>如何：使用模块包括文件
  *模块* (模块与模块) 容器，可用于将 ASPX 母版页、文本文件或图像等文件部署到 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] SharePoint。

 可以选择将文件部署到文档库或作为普通文件 (例如，default.aspx) 文档库外部。 若要将文件添加到文档库，请指定 `Type="GhostableInLibrary"` 作为 File 元素 **中的** 属性。 此设置指示SharePoint项添加到库时，创建要与文件一起使用的列表项。 若要在文档库外部署文件，请指定 `Type="Ghostable"` 或仅省略 **Type** 属性。

## <a name="add-a-module-to-a-sharepoint-solution"></a>将模块添加到SharePoint解决方案

#### <a name="to-add-a-module"></a>添加模块

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中打开或创建一个 SharePoint 项目。

     有关详细信息，请参阅SharePoint[和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

2. 在 **解决方案资源管理器** 中，选择项目节点，然后在菜单栏上选择  >  **"Project"添加新项"。**

     此时将打开“添加新项”对话框。

3. 在模板SharePoint，选择"模块"模板，然后选择"添加 **"** 按钮。

     此步骤将在项目中创建名为 Module1 的节点。

4. 在 Module1 下 *，Sample.txt文件* 。

     Sample.txt包含在所有新模块中，因此不需要。  (请注意，删除文件也会从模块的 file.Elements.xml中删除其) 

5. 如果希望文件部署到 SharePoint 中的特定文件夹结构，请通过选择 Module1 节点在 中的 Module1 下创建这些文件夹，然后在菜单栏上选择"Project"" [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] **新建文件夹"。** 

6. 选择要添加文件的文件夹，然后在菜单栏上，选择 **"Project"****添加现有项"。**

7. 选择要部署到其中的一个或多个SharePoint，然后选择"添加 **"** 按钮。

     将文件添加到项目时，其条目会自动添加到模块的Elements.xml文件。 部署项目时，文件将复制到 SharePoint 服务器，相对于项目的根目录，该根目录由 **File** 元素的 **Url** 属性（如 ）指定 `Url="Module1/New Folder/SomeFile.doc` 。 如果要更改文件的部署位置，请将其移到文件存储中的另一 **解决方案资源管理器或更改其** **URL** 设置。

8. 对于想要显示在文档库中的任何文件，将 属性追加到文档库中 `Type="GhostableInLibrary"`Elements.xml。 ** 例如，

    ```xml
    <File Path="Module1\Some Folder\SomePage.aspx" Url="Module1/Some Folder/SomePage.aspx" Type="GhostableInLibrary" />
    ```

9. 部署该项目。

     文件复制到 SharePoint 中的指定位置。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
