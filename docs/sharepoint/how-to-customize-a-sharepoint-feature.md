---
title: 如何：自定义 SharePoint 功能 | Microsoft Docs
description: 在 Visual Studio 中自定义 SharePoint 功能。 在解决方案资源管理器或 SharePoint 包资源管理器中添加新功能时，功能设计器会打开。
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
# <a name="how-to-customize-a-sharepoint-feature"></a>如何：自定义 SharePoint 功能
  可以使用 Visual Studio 中的功能设计器创建和自定义 SharePoint 功能。 例如，可以设置功能范围，并添加其他功能作为依赖项。 默认情况下，在解决方案资源管理器或 SharePoint 包资源管理器中添加新功能时，功能设计器会打开。

## <a name="opening-the-feature-designer"></a>打开功能设计器
 可以使用功能设计器将 SharePoint 项目项添加到功能或从其中删除。

#### <a name="to-open-the-feature-designer"></a>若要打开功能设计器

1. 在“解决方案资源管理器”中，展开“功能” 。

2. 双击“Feature1”项或打开“Feature1”项的快捷菜单，然后选择“查看设计器”。 

## <a name="view-the-packaged-manifest-file"></a>查看打包的清单文件
 可以使用功能设计器修改和生成功能的打包清单文件 (feature.xml)。 然后，可以在 Visual Studio 中查看此文件的 XML 代码。

#### <a name="to-view-the-packaged-manifest-file"></a>若要查看打包的清单文件

1. 在“功能设计器”中，选择“清单”选项卡 。

#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>若要使用解决方案资源管理器查看打包的清单文件

1. 在“解决方案资源管理器”中，选择“显示所有文件”图标。

2. 依次展开 Features、FeatureName 和 FeatureName.feature，然后打开 \<FeatureName>.Template.xml 文件。

    > [!NOTE]
    > 打开功能模板清单 XML 文件时，将自动验证文件，并能忽略“错误列表”窗口中出现的警告。

## <a name="change-the-manifest-template"></a>更改清单模板
 可以在 Visual Studio XML 编辑器或“清单模板”窗格中更改“功能”清单文件的 XML 文件。 对 XML 代码的任何更改都会合并到“功能”的打包清单文件中。 例如，可能想要更改清单模板以自定义“功能”属性。

#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>若要使用 XML 编辑器更改清单模板

1. 在“功能设计器”中，选择“清单”选项卡，展开“编辑选项”节点，然后选择“在 XML 编辑器中打开”链接。   

     对 XML 的更改将合并到打包的清单文件中。

#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>若要使用“清单模板”窗格更改清单模板

1. 在“功能设计器”中，选择“清单”选项卡，展开“编辑选项”节点，然后更改显示在“清单模板”窗格中的 XML。  

     对 XML 的更改显示在“打包的清单的预览”窗格中。

## <a name="overwrite-the-packaged-manifest-file"></a>覆盖打包的清单文件
 可以手动禁用功能设计器并创建 feature.xml 文件。 首次执行此过程时，功能设计器中的当前设置将保存到功能模板 XML 文件中。 然后，可以修改或覆盖 XML 代码。

> [!NOTE]
> 如果在禁用功能设计器时在 XML 文件中添加或删除 SharePoint 项目项，则这些项目项不会打包。

#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>若要通过禁用设计器来覆盖打包的清单文件

1. 在“功能设计器”中，选择“清单”选项卡 。

2. 展开“编辑选项”节点，选择“覆盖生成的 XML 并在 XML 编辑器中编辑清单”列表，然后选择“是”按钮。  

     使用当前打包的清单文件更新模板。

## <a name="enable-the-feature-designer"></a>启用功能设计器
 可以重新启用功能设计器以自定义 feature.xml 文件。

#### <a name="to-re-enable-the-designer"></a>如要重新启用设计器

1. 在“功能设计器”中，选择“放弃清单编辑和重新启用设计器”链接，然后选择“是”按钮。  

2. 使用原始文本刷新模板，对 XML 的任何更改都会丢失。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
