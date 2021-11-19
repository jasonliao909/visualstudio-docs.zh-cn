---
title: 打包资源管理器：在包中添加与删除功能和项
titleSuffix: ''
description: 使用 Visual Studio 中的打包资源管理器在 SharePoint 包中添加与删除功能和项。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600616"
---
# <a name="how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer"></a>如何：使用打包资源管理器在包中添加与删除功能和项
  要配置包以部署 SharePoint 项和功能，可以使用打包资源管理器。 可以调整 .wsp 文件中的 SharePoint 项目项和功能。

 或者，可以使用打包设计器查看功能并重新排序以更改激活顺序。 有关详细信息，请参阅[如何：使用包设计器在包中添加与删除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)。

## <a name="open-the-packaging-explorer"></a>打开打包资源管理器
 如果 Visual Studio 解决方案至少有一个 SharePoint 项目，可以使用以下过程打开打包资源管理器。 或者，当你查看功能或包设计器时，打包资源管理器会自动打开。 关闭所有功能设计器和包设计器后，打包资源管理器也会关闭。

#### <a name="to-open-the-packaging-explorer"></a>打开打包资源管理器

1. 在菜单栏上，依次选择“视图” > “其他窗口” > “打包资源管理器”。

     “打包资源管理器”将显示在“工具箱”中。

## <a name="adding-a-feature-to-a-package"></a>向包中添加功能
 可以使用打包资源管理器向包中添加新的和现有的功能。

#### <a name="to-add-a-sharepoint-feature"></a>添加 SharePoint 功能

1. 打开“打包资源管理器”，打开项目的快捷菜单，然后选择“添加功能”。

#### <a name="to-move-an-existing-sharepoint-feature"></a>移动现有 SharePoint 功能

1. 打开“打包资源管理器”，然后执行下列步骤之一：

    - 将一项功能从一个项目拖到另一个项目中。

    - 打开一项功能的快捷菜单，选择“剪切”，打开要将功能移动到的项目的快捷菜单，然后选择“粘贴”。

    > [!NOTE]
    > 如果解决方案中包含多个 SharePoint 项目，请使用此过程。

## <a name="validate-a-feature-or-package"></a>验证功能或包
 可以通过验证文件来识别 SharePoint 功能和包中的潜在问题。 警告和错误显示在“输出”窗口和“错误列表”窗口中。

#### <a name="to-validate-a-sharepoint-feature-or-package"></a>验证 SharePoint 功能或包

1. 打开“打包资源管理器”。

2. 打开功能或包的快捷菜单，然后选择“验证”。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
