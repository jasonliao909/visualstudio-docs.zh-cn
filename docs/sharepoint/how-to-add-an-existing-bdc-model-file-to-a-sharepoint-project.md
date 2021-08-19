---
title: 如何：将现有 BDC 模型文件添加到 SharePoint Project |Microsoft Docs
titleSuffix: ''
description: 将现有的业务数据连接 (BDC) 模型文件添加到 Visual Studio 中的 SharePoint 项目，以便您可以自定义、打包和重新部署 BDC 模型。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.BDC.ImportDialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], import a model
- Business Data Connectivity service [SharePoint development in Visual Studio], reuse a model
- BDC [SharePoint development in Visual Studio], import a model
- BDC [SharePoint development in Visual Studio], remove a model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 758195e06689fe455797832d507e10096b900ca0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122148969"
---
# <a name="how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project"></a>如何：将现有 BDC 模型文件添加到 SharePoint 项目
  您可以通过使用 Visual Studio 将模型文件 (*bdcm*) 添加到任何 SharePoint 场项目，自定义、打包和重新部署业务数据连接 (BDC) 模型。 有关详细信息，请参阅[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

### <a name="to-add-a-bdc-model-file-to-a-sharepoint-project"></a>将 BDC 模型文件添加到 SharePoint 项目

1. 在 **解决方案资源管理器** 中，为 SharePoint 项目选择文件夹。

2. 在菜单栏上，选择 **Project**  >  **添加现有项**"。

3. 在 " **添加现有项** " 对话框中，浏览到要添加到项目中的模型定义文件的位置，选择该文件，然后选择 " **添加** " 按钮。

    如果该模型未定义 *.net 程序集类型的业务线 (LOB) 系统*，则 " **添加 .Net 程序集 LobSystem** " 对话框将打开。

4. 如果显示此对话框，请执行以下步骤之一：

   - 如果要编写自定义代码并使用设计器为导入的模型定义元数据，请选择 " **是"** 按钮，将系统命名为，然后选择 **"确定"** 按钮。

   - 否则，请选择 " **否** " 按钮，然后选择 " **确定"** 按钮。

     **业务数据连接模型** 项将添加到项目。

## <a name="see-also"></a>请参阅
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)
- [如何：使用资源文件指定本地化名称、属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [如何：在 BDC 功能中包含自定义程序集](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [将业务数据集成到 SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)
