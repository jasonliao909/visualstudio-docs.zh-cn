---
title: 打包资源管理器：添加&删除&项的功能
titleSuffix: ''
description: 使用包包中的打包资源管理器SharePoint包中添加和删除功能和Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.PackagingExplorer
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 0b40b21377c0ab566bb33adf3ac0d0f617f0c53c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122106821"
---
# <a name="how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer"></a>如何：使用打包资源管理器向包添加和删除功能和项
  若要配置包以部署SharePoint项和功能，可以使用打包资源管理器。 可以调整 .wsp SharePoint项目项和功能。

 或者，可以使用打包设计器查看功能并重排序以更改激活顺序。 有关详细信息，请参阅如何：使用包设计器 向包 [添加和删除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)。

## <a name="open-the-packaging-explorer"></a>打开打包资源管理器
 如果包解决方案至少有一个打包Visual Studio，可以使用以下过程打开SharePoint资源管理器。 或者，当你查看功能或包设计器时，打包资源管理器会自动打开。 关闭所有功能设计器和包设计器后，打包资源管理器也会关闭。

#### <a name="to-open-the-packaging-explorer"></a>打开打包资源管理器

1. 在菜单栏上，选择"**查看** 其他Windows  >    >  **打包资源管理器"。**

     打包 **资源管理器显示在** 工具箱 **中**。

## <a name="adding-a-feature-to-a-package"></a>将功能添加到包
 可以使用打包资源管理器将新的和现有的功能添加到包。

#### <a name="to-add-a-sharepoint-feature"></a>添加SharePoint功能

1. 打开打包 **资源管理器**，打开项目的快捷菜单，然后选择"**添加功能"。**

#### <a name="to-move-an-existing-sharepoint-feature"></a>移动现有 SharePoint 功能

1. 打开 **打包资源管理器**，然后执行以下步骤之一：

    - 将功能 **从** 一个项目拖动到另一个项目。

    - 打开"功能"的快捷菜单，选择"剪切"，打开要移动该功能的项目的快捷菜单，然后选择"粘贴 **"。**

    > [!NOTE]
    > 如果解决方案中包含多个 SharePoint 项目，请使用此过程。

## <a name="validate-a-feature-or-package"></a>验证功能或包
 可以通过验证文件来识别SharePoint功能和包中的潜在问题。 警告和错误显示在"输出"窗口和"错误列表"窗口中。

#### <a name="to-validate-a-sharepoint-feature-or-package"></a>验证SharePoint或包

1. 打开打包 **资源管理器**。

2. 打开功能或包的快捷菜单，然后选择"验证 **"。**

## <a name="see-also"></a>请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
