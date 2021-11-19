---
title: 如何：创建 BDC 模型 | Microsoft Docs
description: 使用 Visual Studio 模板为此类项目创建业务数据连接 (BDC) 模型，然后将该模型添加到任何 SharePoint 项目。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], creating a model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 4180821b1b37c2d9f0e9e2fcd5cadb8780c0a86c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126667482"
---
# <a name="how-to-create-a-bdc-model"></a>如何：创建 BDC 模型

  可以使用模板为此类项目创建业务数据连接 (BDC) 模型，然后将该模型添加到任何 SharePoint 项目。 有关详细信息，请参阅[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。 有关如何设计模型的详细信息，请参阅[设计业务数据连接模型](../sharepoint/designing-a-business-data-connectivity-model.md)。

## <a name="to-create-a-bdc-project"></a>创建 BDC 项目的步骤

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。
::: moniker range="=vs-2017"
   > [!NOTE]
   > 如果 IDE 设置为使用 Visual Basic 开发设置，请选择“文件” > “新建项目” 。

  **“新建项目”** 对话框随即打开。

2. 在 Visual Basic 或 Visual C# 下，选择 Office/SharePoint、SharePoint 解决方案   。

3. 在“模板”窗格中，选择“SharePoint 2013 - 空项目”项，然后选择“确定”按钮  。

     “SharePoint 自定义向导”随即打开。
::: moniker-end
::: moniker range=">=vs-2019"
2. 在“创建新项目”对话框中，为已安装的 SharePoint 的特定版本选择“SharePoint 空项目”。 例如，如果安装了 SharePoint 2019，请选择“SharePoint 2019 - 空项目”模板。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

3. 将项目名称更改为所需名称，然后选择“创建”按钮。

::: moniker-end
4. 在“为调试指定站点和安全级别”页面上，指定本地计算机上 SharePoint 站点的 URL，选择“部署为场解决方案”选项按钮，然后选择“完成”按钮  。

     将在指定的站点测试 SharePoint 模型。

    > [!IMPORTANT]
    > 必须将项目部署为场解决方案，因为 BDC 模型仅支持场解决方案。

     将创建一个空的 SharePoint 项目。

5. 在菜单栏上，依次选择“项目” > “添加新项”。

6. 在“添加新项”对话框中，选择 Office/SharePoint 节点 。

7. 在 SharePoint 模板列表中，选择“业务数据连接模型(仅限场解决方案)”。

8. 在“名称”框中，指定 BDC 模型的名称，然后选择“添加”按钮 。

     “业务数据连接模型”项将添加到项目。 默认情况下，模型显示在 BDC 设计器中。 有关详细信息，请参阅[创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)。

## <a name="see-also"></a>另请参阅

- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [如何：将现有 BDC 模型文件添加到 SharePoint 项目](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [如何：使用资源文件指定本地化名称、属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [如何：在 BDC 功能中包含自定义程序集](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [将业务数据集成到 SharePoint 中](../sharepoint/integrating-business-data-into-sharepoint.md)
