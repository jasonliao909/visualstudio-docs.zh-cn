---
title: 为解决方案创建SharePoint验证
titleSuffix: ''
description: 创建自定义验证规则以验证由 Visual Studio生成的解决方案包或验证整个功能。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122135892"
---
# <a name="create-feature-and-package-validations-for-sharepoint-solutions"></a>为解决方案创建SharePoint验证

  可以创建自定义验证规则来验证由应用程序生成Visual Studio。 可以通过从包的上下文菜单中选择"验证"或 **"PackagingExplorer"** 中的"功能"，对整个功能或包执行完全验证。  向项目添加新项目项SharePoint功能时，将执行部分验证，以确定包或功能是否将位于有效状态。

### <a name="to-create-a-custom-package-validation-rule"></a>创建自定义包验证规则

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio。SharePoint

    - System.ComponentModel.Composition

3. 创建实现以下接口之一的类：

    - 若要创建包验证规则，请实现 <xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule> 接口。

    - 若要创建功能验证规则，请实现 <xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule> 接口。

4. 将 <xref:System.ComponentModel.Composition.ExportAttribute> 添加到 类。 此属性使Visual Studio发现和加载验证规则。 将 <xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule> 或 <xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule> 类型传递给属性构造函数。

## <a name="example"></a>示例
 下面的代码示例演示如何创建自定义功能验证规则。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/featurevalidation/extension/customvalidationrule.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/featurevalidation/extension/customfeaturevalidationrule.cs" id="Snippet1":::

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio。SharePoint。

- System.ComponentModel.Composition。

## <a name="deploy-the-extension"></a>部署扩展
 若要部署扩展，请为程序集 (VSIX) 包以及要随扩展一起分发的其他任何文件 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建扩展。 有关详细信息，请参阅 在 Visual Studio 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>请参阅
- [扩展SharePoint打包和部署](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
