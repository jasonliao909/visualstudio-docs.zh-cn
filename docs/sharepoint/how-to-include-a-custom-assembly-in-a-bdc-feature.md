---
title: 如何：在 BDC 功能包中包括自定义|Microsoft Docs
description: 将自定义程序集包括在业务数据连接 (BDC) 功能中，以便项目可以引用同一解决方案中其他项目中的程序集。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.BDC.Add_Assemblies_Dialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], add reference
- Business Data Connectivity service [SharePoint development in Visual Studio], custom assembly
- BDC [SharePoint development in Visual Studio], custom assembly
- BDC [SharePoint development in Visual Studio], add reference
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 14026e6de7a376e4548723b4b540d314e499bbf1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122092990"
---
# <a name="how-to-include-a-custom-assembly-in-a-bdc-feature"></a>如何：在 BDC 功能中包括自定义程序集
  项目可以引用同一解决方案中其他项目中的程序集。 但是，必须使用"将引用的程序集分配到 **LobSystems"** 对话框，将这些程序集添加到项目的功能文件。

### <a name="to-include-a-custom-assembly-in-a-business-data-connectivity-bdc-feature"></a>在业务数据连接中包括自定义程序集 (BDC) 功能

1. 在 **解决方案资源管理器** 中，选择包含 BDC 模型的文件夹。

2. 在 **“视图”** 菜单上，单击 **“属性窗口”** 。

3. 在"**属性"** 窗口中，选择"**程序集**"属性，然后选择"移动设计器" (ASP.NET 省略 ![号](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")) 。

     将出现 **"将引用的程序集分配到 LobSystems"** 对话框。

4. 在" **选择程序集"** 列表中，选择自定义程序集。

    > [!NOTE]
    > 只有在添加了对包含程序集的项目的引用时，程序集才出现在"将引用的程序集分配给 **LobSystems"** 对话框中。 有关详细信息，请参阅 [如何：使用"](/previous-versions/wkze6zky(v=vs.140))添加引用"对话框添加或删除引用。

5. 在" **引用属性** "组中，打开为 **LobSystem Scope** 属性显示的列表，选择使用自定义程序集的方法的 LOB 系统，然后选择"确定 **"** 按钮。

    > [!NOTE]
    > 若要调试自定义程序集中的代码，必须将该程序集添加到解决方案包。 有关详细信息，请参阅 [如何：添加和删除其他程序集](../sharepoint/how-to-add-and-remove-additional-assemblies.md)。

## <a name="see-also"></a>请参阅
- [如何：使用资源文件指定本地化名称、属性和权限](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [如何：将现有 BDC 模型文件添加到 SharePoint 项目](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [创建业务数据连接模型](../sharepoint/creating-a-business-data-connectivity-model.md)
- [如何：创建 BDC 模型](../sharepoint/how-to-create-a-bdc-model.md)
- [将业务数据集成到SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)