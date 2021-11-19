---
title: 如何在 SharePoint 项目中使用资源文件 | Microsoft Docs
titleSuffix: ''
description: 在 SharePoint 项目中使用资源文件，使你可为 BDC 模型中定义的对象提供本地化的名称、定义属性并应用权限。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], localize strings
- BDC [SharePoint development in Visual Studio], localize strings
- BDC [SharePoint development in Visual Studio], resource file
- Business Data Connectivity service [SharePoint development in Visual Studio], resource strings
- BDC [SharePoint development in Visual Studio], properties
- Business Data Connectivity service [SharePoint development in Visual Studio], properties
- Business Data Connectivity service [SharePoint development in Visual Studio], resource file
- BDC [SharePoint development in Visual Studio], resource strings
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: a909462908c26e6ed1af7fbf6458a54b57e901f1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665277"
---
# <a name="how-to-use-a-resource-file-in-a-sharepoint-project"></a>如何在 SharePoint 项目中使用资源文件

  通过使用资源文件，您可以对在业务数据连接 (BDC) 模型中定义的对象提供本地化名称、定义属性和应用权限。 若要指定此信息，请向包含“业务数据连接模型”项的项目添加“业务数据连接资源”项 。 然后通过编辑资源文件的 XML 来指定名称、属性和权限。

### <a name="to-add-a-bdc-resource-file-to-a-sharepoint-project"></a>将 BDC 资源文件添加到 SharePoint 项目

1. 在解决方案资源管理器中，展开 SharePoint 项目的文件夹，然后选择包含 BDC 模型的文件夹。

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 展开“SharePoint”节点，然后选择“2010”节点 。

4. 在“添加新项”对话框中，选择“业务数据连接资源项” 。

5. 在“名称”框中，指定资源文件的名称，然后选择“添加”按钮 。

     扩展名为 .bdcr 的资源文件将添加到项目中并打开以进行编辑。

6. 添加 XML 以定义要应用 BDC 模型的本地化名称、属性和权限。

     有关如何定义这些元素的信息，请参阅[模型和资源文件](/previous-versions/office/developer/sharepoint-2010/aa674515(v=office.14))。

## <a name="see-also"></a>另请参阅
- [如何：将现有 BDC 模型文件添加到 SharePoint 项目](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)
- [如何：在 BDC 功能中引入自定义程序集](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [将业务数据集成到 SharePoint 中](../sharepoint/integrating-business-data-into-sharepoint.md)
