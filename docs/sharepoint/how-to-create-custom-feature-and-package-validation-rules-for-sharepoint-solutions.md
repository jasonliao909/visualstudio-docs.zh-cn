---
title: 为 SharePoint 解决方案创建功能和包验证
titleSuffix: ''
description: 创建自定义验证规则来验证 Visual Studio 生成的解决方案包或验证整个功能。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
- SharePoint development in Visual Studio, validation rules
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: a8cf9b5aa392e04865b0755fdc7dc8933c77bac1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663844"
---
# <a name="create-feature-and-package-validations-for-sharepoint-solutions"></a>为 SharePoint 解决方案创建功能和包验证

  可以创建自定义验证规则来验证 Visual Studio 生成的解决方案包。 可以通过从包的上下文菜单或“打包资源管理器”的功能中选择“验证”来对整个功能或包执行完全验证。 向项目添加新的 SharePoint 项目项或功能以确定包或功能是否处于有效状态时，将执行部分验证。

### <a name="to-create-a-custom-package-validation-rule"></a>创建自定义包验证规则

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio.SharePoint

    - System.ComponentModel.Composition

3. 创建实现以下接口之一的类：

    - 若要创建包验证规则，请实现 <xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule> 接口。

    - 若要创建功能验证规则，请实现 <xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule> 接口。

4. 将 <xref:System.ComponentModel.Composition.ExportAttribute> 添加到类。 此属性使 Visual Studio 能够发现并加载验证规则。 将 <xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule> 或 <xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule> 类型传递给属性构造函数。

## <a name="example"></a>示例
 下列代码示例演示了如何创建自定义功能验证规则。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/featurevalidation/extension/customvalidationrule.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/featurevalidation/extension/customfeaturevalidationrule.cs" id="Snippet1":::

## <a name="compile-the-code"></a>编译代码
 本示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint.

- System.ComponentModel.Composition.

## <a name="deploy-the-extension"></a>部署扩展
 若要部署扩展，请为程序集以及要随扩展分发的任何其他文件创建 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (VSIX) 包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
