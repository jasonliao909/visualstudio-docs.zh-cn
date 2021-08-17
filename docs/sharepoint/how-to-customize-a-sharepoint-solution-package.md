---
title: 如何：自定义 SharePoint 解决方案包|Microsoft Docs
description: 使用包设计器创建和自定义 SharePoint 解决方案包 (.wsp) 。 查看或覆盖打包的清单文件。 更改清单模板。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.PackageDesignerAdvanced
- VS.SharePointTools.RAD.PackageDesigner.Manifest
- VS.SharePointTools.RAD.PackageDesignerProperties
- VS.SharePointTools.RAD.PackageDesigner.SwitchView
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
ms.openlocfilehash: ca3341b252f94a4415904744840f24cb05b56b56
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122026942"
---
# <a name="how-to-customize-a-sharepoint-solution-package"></a>如何：自定义 SharePoint 解决方案包
  可以使用包设计器创建和自定义 *.wsp* (包) 。 例如，可以添加SharePoint项和功能，指定在部署解决方案时是否重置 Web 服务器，并设置部署服务器类型。

## <a name="open-the-package-designer"></a>打开包设计器

#### <a name="to-open-the-package-designer"></a>打开包设计器

- 在 **解决方案资源管理器** 中，双击"包"，**或选择视图设计器** 菜单上的"包 **"。** 

## <a name="view-the-packaged-manifestffile"></a>查看打包的 manifestfFile
 可以使用包设计器来修改和生成打包的清单文件。 然后，可以在文件中查看此文件的 XML Visual Studio。

#### <a name="to-view-the-xml-source-file"></a>查看 XML 源文件

1. 在包 **设计器中，** 选择"清单 **"。**

#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>使用文件查看打包的清单解决方案资源管理器

1. 在“解决方案资源管理器”中，选择“显示所有文件”。

2. 展开"包"，展开"Package.package"， *然后打开Package.Template.xml* 文件。

    > [!NOTE]
    > 打开包模板的清单 XML 文件时，将自动验证这些文件，你可以忽略"错误列表"窗口中出现的警告。

## <a name="change-the-manifest-template"></a>更改清单模板
 可以在"XML 编辑器"或"清单模板"窗格中Visual Studio打包清单文件的 XML 代码。 对 XML 代码的任何更改都合并到包的打包清单文件中。

#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>使用 XML 编辑器更改清单模板

1. 在包 **设计器中**，选择"清单 **"** 选项卡，展开"编辑 **选项** "节点，然后选择" **在 XML 编辑器中打开"** 链接。

     对 XML 的更改将合并到打包的清单文件中。

#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>使用"清单模板"窗格更改清单模板

1. 在包 **设计器中**，选择"清单"选项卡，展开"编辑选项"节点，然后更改"清单模板"窗格中出现的 XML。

     对 XML 的更改显示在"打包清单 **预览"窗格中** 。

## <a name="overwrite-the-packaged-manifest-file"></a>覆盖打包的清单文件
 可以禁用包设计器并手动 *manifest.xml* 文件。 首次执行此过程时，包设计器中的当前设置将保存到包模板 XML 文件中。 然后，可以修改或覆盖 XML 代码。

> [!NOTE]
> 如果在禁用包设计器SharePoint XML 文件中添加或删除项目项和功能，则这些项目项和功能不会打包。

#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>通过禁用设计器覆盖打包的清单文件

1. 在包 **设计器中**，选择" **清单"** 选项卡。

2. 展开" **编辑选项"** 节点，选择"覆盖生成的 **XML"，然后在"XML** 编辑器"链接中编辑清单，然后选择" **是"** 按钮。

     使用当前打包的清单文件更新模板。

## <a name="enable-the-package-designer"></a>启用包设计器
 可以重新启用包设计器以 *自定义manifest.xml文件* 。

#### <a name="to-re-enable-the-designer"></a>重新启用设计器

1. 在包 **设计器中**，选择" **放弃清单编辑并重新启用** 设计器"链接，然后选择"是 **"** 按钮。

     使用原始文本刷新模板，并且对 XML 的任何更改都丢失。

## <a name="see-also"></a>请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
