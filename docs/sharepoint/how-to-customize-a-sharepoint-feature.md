---
title: 如何：自定义SharePoint功能|Microsoft Docs
description: 自定义SharePoint中的Visual Studio。 在包资源管理器或包资源管理器中添加解决方案资源管理器时，SharePoint设计器会打开。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.FeatureDesigner.SwitchView
- VS.SharePointTools.RAD.featureDesigner.Manifest
- VS.SharePointTools.RAD.FeatureDesignerProperties
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
ms.openlocfilehash: 7f4df055447221d563d4725f2a49ccb826b23002
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663843"
---
# <a name="how-to-customize-a-sharepoint-feature"></a>如何：自定义SharePoint功能
  可以使用 SharePoint Visual Studio 中的功能设计器创建和自定义Visual Studio。 例如，可以设置功能范围，并添加其他功能作为依赖项。 默认情况下，在包资源管理器或包资源管理器中添加解决方案资源管理器功能SharePoint设计器。

## <a name="opening-the-feature-designer"></a>打开功能设计器
 可以使用功能设计器将SharePoint项目项添加到功能。

#### <a name="to-open-the-feature-designer"></a>打开功能设计器

1. 在 **解决方案资源管理器** 中，展开"**功能"。**

2. 双击 *"Feature1"* 项，或打开 *"Feature1"* 项的快捷菜单，然后选择"视图设计器"。 

## <a name="view-the-packaged-manifest-file"></a>查看打包的清单文件
 可以使用功能设计器修改和生成功能设计器的打包清单文件 *(feature.xml) 。* 然后，可以在 Visual Studio 中查看此文件的 XML 代码。

#### <a name="to-view-the-packaged-manifest-file"></a>查看打包的清单文件

1. 在功能 **设计器中**，选择" **清单"** 选项卡。

#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>使用文件查看打包的清单解决方案资源管理器

1. 在 **解决方案资源管理器** 中，选择" **显示所有文件"** 图标。

2. 展开"功能"，展开"FeatureName"，展开"FeatureName.feature"，然后打开 *\<FeatureName> .Template.xml* 文件。

    > [!NOTE]
    > 打开功能模板清单 XML 文件时，将自动验证文件，并忽略"错误列表"窗口中出现的警告。

## <a name="change-the-manifest-template"></a>更改清单模板
 可以在"XML 编辑器"或"清单模板"窗格中Visual Studio"功能清单"文件的 XML 代码。 对 XML 代码的任何更改都合并到功能打包的清单文件中。 例如，可能需要更改清单模板以自定义 Feature 属性。

#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>使用 XML 编辑器更改清单模板

1. 在功能 **设计器中**，选择" **清单"** 选项卡，展开"编辑 **选项** "节点，然后选择" **在 XML 编辑器中打开"** 链接。

     对 XML 的更改将合并到打包的清单文件中。

#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>使用"清单模板"窗格更改清单模板

1. 在功能 **设计器中**，选择"清单"选项卡，展开"编辑选项"节点，然后更改"清单模板"窗格中出现的 XML。

     对 XML 的更改显示在"打包清单 **预览"窗格中** 。

## <a name="overwrite-the-packaged-manifest-file"></a>覆盖打包的清单文件
 可以禁用功能设计器并手动 *feature.xml* 文件。 首次执行此过程时，功能设计器中的当前设置将保存到功能模板 XML 文件中。 然后，可以修改或覆盖 XML 代码。

> [!NOTE]
> 如果在禁用功能设计器SharePoint XML 文件中添加或删除项目项，则这些项目项不会打包。

#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>通过禁用设计器覆盖打包的清单文件

1. 在功能 **设计器中**，选择" **清单"** 选项卡。

2. 展开" **编辑选项"** 节点，选择"覆盖生成的 **XML"，然后在"XML** 编辑器"链接中编辑清单，然后选择" **是"** 按钮。

     使用当前打包的清单文件更新模板。

## <a name="enable-the-feature-designer"></a>启用功能设计器
 可以重新启用功能设计器以 *自定义feature.xml文件* 。

#### <a name="to-re-enable-the-designer"></a>重新启用设计器

1. 在功能 **设计器中**，选择" **放弃清单编辑并重新启用** 设计器"链接，然后选择"是 **"** 按钮。

2. 使用原始文本刷新模板，并且对 XML 的任何更改都丢失。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
