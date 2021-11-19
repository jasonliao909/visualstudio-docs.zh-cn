---
title: 如何：添加和删除功能依赖项 | Microsoft Docs
description: 查看如何使用 Visual Studio 中的功能设计器向 SharePoint 解决方案添加和删除功能依赖项。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- MICROSOFT.VISUALSTUDIO.SHAREPOINT.DESIGNERS.CUSTOMDEPENDENCYWINDOW
- VS.SHAREPOINTTOOLS.RAD.FEATUREDESIGNERDEPENDENCY
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 30df44d4972f596204c5c6c9fd4a91ee23948c99
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665014"
---
# <a name="how-to-add-and-remove-feature-dependencies"></a>如何：添加和删除功能依赖项
  你的 SharePoint 功能可能依赖于功能或数据的其他功能。 在这些情况下，可以将这些其他功能标记为该功能的依赖项。 这样，SharePoint 服务器可确保在激活功能之前激活依赖功能。

## <a name="add-dependencies"></a>添加依赖项
 可以在解决方案中添加其他功能作为依赖项。 这样可确保在安装功能之前安装并激活所需的功能。

#### <a name="to-add-a-dependency-on-a-feature-in-the-solution"></a>为解决方案中的功能添加依赖项

1. 打开功能设计器，展开“功能激活依赖项”节点，然后选择“添加”按钮 。

2. 在“添加功能激活依赖项”对话框中，选择“在解决方案中添加功能的依赖项”选项按钮，再选择要添加为依赖项的功能的标题，然后选择“添加”按钮  。

     通过在按住 Ctrl 键的同时选择多个标题，可以添加多个功能。

## <a name="addi-custom-dependencies"></a>添加自定义依赖项
 可以添加已部署在 SharePoint 服务器上的功能作为依赖项。 这样，SharePoint 激活过程会进行检查，以确保在安装功能之前激活所有依赖功能。

#### <a name="to-add-a-dependency-by-the-feature-id"></a>按功能 ID 添加依赖项

1. 打开功能设计器，展开“功能激活依赖项”节点，然后选择“添加”按钮 。

2. 在“添加功能激活依赖项”对话框中，选择“添加自定义依赖项”选项按钮 。

3. 在“功能 ID”文本框中，输入要标记为激活依赖项的功能的 GUID，然后选择“添加”按钮 。

## <a name="edit-custom-dependencies"></a>编辑自定义依赖项
 可以编辑之前添加的自定义依赖项。 但是，解决方案中的依赖功能只能删除，不能编辑。

#### <a name="to-change-a-dependency-on-a-feature-in-the-solution"></a>更改解决方案中功能的依赖项

1. 打开功能设计器，然后展开“功能激活依赖项”节点。

2. 选择要编辑的功能的名称，然后选择“编辑”按钮。

3. 在“编辑自定义功能激活依赖项”对话框中，更改标题、功能 ID 或说描述，然后选择“提交”按钮 。

## <a name="remove-dependencies"></a>删除依赖项

#### <a name="to-remove-a-dependency-on-a-feature-in-the-solution"></a>删除解决方案中功能的依赖项

1. 在功能设计器，展开“功能激活依赖项”节点，选择要删除的功能的名称，然后选择“删除”按钮 。

## <a name="see-also"></a>另请参阅
- [创建 SharePoint 功能](../sharepoint/creating-sharepoint-features.md)
- [如何：自定义 SharePoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [如何：在 SharePoint 功能中添加和删除项](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
