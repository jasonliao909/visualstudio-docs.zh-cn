---
title: 如何：定义SharePoint Project项类型|Microsoft Docs
description: 了解如何在要创建自定义项目项时定义SharePoint类型。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 8d990658c669cd1e22927bc4ae95382def29defa
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122115572"
---
# <a name="how-to-define-a-sharepoint-project-item-type"></a>如何：定义SharePoint项类型
  若要创建自定义项目项，请定义项目SharePoint类型。 有关详细信息，请参阅[定义自定义SharePoint项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)。

### <a name="to-define-a-project-item-type"></a>定义项目项类型

1. 创建类库项目。

2. 添加对下列程序集的引用：

    - Microsoft.VisualStudio。SharePoint

    - System.ComponentModel.Composition

3. 创建实现 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 接口的类。

4. 将以下属性添加到 类：

    - <xref:System.ComponentModel.Composition.ExportAttribute>. 此属性使Visual Studio发现和加载 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 实现。 将 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 类型传递给属性构造函数。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. 在项目项类型定义中，此属性指定新项目项的字符串标识符。 建议使用格式"公司 *名称"。**功能* 名称，以帮助确保所有项目项都有唯一的名称。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemIconAttribute>. 此属性指定在 中为此项目项显示的 **解决方案资源管理器。** 此属性是可选的;如果未应用于类，则Visual Studio项目项的默认图标。 如果设置此属性，请传递嵌入程序集中的图标或位图的完全限定名称。

5. 在 方法的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 实现中，使用 *projectItemTypeDefinition* 参数的成员来定义项目项类型的行为。 此参数是 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> 一个对象，提供对 和 接口中定义的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents> 事件的访问。 若要访问项目项类型的特定实例，请 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> 处理 和 等 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> 事件 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized> 。

## <a name="example"></a>示例
 下面的代码示例演示如何定义简单的项目项类型。 当用户向项目添加此类型的项目项时，此项目项类型会将消息写入"输出"窗口和"错误列表"窗口。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemtype.vb" id="Snippet2":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemtype.cs" id="Snippet2":::

 此示例使用 SharePoint 项目服务将消息写入"输出 **"** 窗口和"**错误列表"** 窗口。 有关详细信息，请参阅使用[SharePoint 项目服务。](../sharepoint/using-the-sharepoint-project-service.md)

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio。SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>部署项目项
 若要使其他开发人员能够使用项目项，请创建项目模板或项目项模板。 有关详细信息，请参阅[为项目项 创建项模板SharePoint模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 若要部署项目项，请为程序集 (模板以及要随项目项分发的其他任何文件创建 VSIX) 包 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的扩展名。 有关详细信息，请参阅 在 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>请参阅
- [定义自定义SharePoint项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [为项目项创建项模板SharePoint模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [演练：使用项模板创建自定义操作项目项，第 1 部分](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [演练：使用项目模板创建站点列项目项，第 1 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [如何：将属性添加到自定义SharePoint项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [如何：将快捷菜单项添加到自定义SharePoint项目项类型](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
