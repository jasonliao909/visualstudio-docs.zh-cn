---
title: 如何：将属性添加到 SharePoint 项目 | Microsoft Docs
description: 使用项目扩展将属性添加到 SharePoint 项目。 当你在“解决方案资源管理器”中选择项目时，属性将显示在“属性”窗口中。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 9daebc52f63acdf6e165ea162c90189fab534193
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600622"
---
# <a name="how-to-add-a-property-to-sharepoint-projects"></a>如何：将属性添加到 SharePoint 项目
  可以使用项目扩展将属性添加到任意 SharePoint 项目。 在“解决方案资源管理器”中选择项目时，属性将显示在“属性”窗口中。 

 以下步骤假设已创建项目扩展。 有关更多信息，请参阅[操作说明：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)。

### <a name="to-add-a-property-to-a-sharepoint-project"></a>若要将属性添加到 SharePoint 项目

1. 使用公共属性定义一个类，用来表示要添加到 SharePoint 项目中的属性。 如果要添加多个属性，则可以在同一个类或不同的类中定义所有属性。

2. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 实现的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> 方法中，处理 projectService 参数的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> 事件。

3. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> 事件的事件处理程序中，将属性类的实例添加到事件自变量参数的 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectPropertiesRequestedEventArgs.PropertySources%2A> 集中。

## <a name="example"></a>示例
 以下代码示例演示了如何将两个属性添加到 SharePoint 项目。 其中一个属性将其数据保留在项目用户选项文件（.csproj.user 文件或 .vbproj.user 文件）中。 另一个属性将其数据保存在项目文件（.csproj 文件或 .vbproj 文件 ）中。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs" id="Snippet1":::

### <a name="understand-the-code"></a>了解代码
 若要确保每次 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> 事件发生时都使用 `CustomProjectProperties` 类的相同实例，代码示例会在第一次发生该事件时将属性对象添加到项目的 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性中。 每当该事件再次发生时，代码都将检索此对象。 有关使用 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性将项目与数据关联的更多信息，请参阅[将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

 若要将更改保存到属性值，属性的 set 访问器使用以下 API：

- `CustomUserFileProperty` 使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A> 属性将其值保存到项目用户选项文件。

- `CustomProjectFileProperty` 使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> 方法将其值保存到项目文件。

  有关在这些文件中保存数据的详细信息，请参阅[在 SharePoint 项目系统的扩展中保存数据](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

### <a name="specify-the-behavior-of-custom-properties"></a>指定自定义属性的行为
 可以通过将来自 <xref:System.ComponentModel> 命名空间的属性应用到属性定义来定义自定义属性的显示方式以及在“属性”窗口中的行为。 以下属性在许多情况下都很有用：

- <xref:System.ComponentModel.DisplayNameAttribute>：指定显示在“属性”窗口中的属性的名称。

- <xref:System.ComponentModel.DescriptionAttribute>：在选择属性时，指定显示在“属性”窗口底部的描述字符串。

- <xref:System.ComponentModel.DefaultValueAttribute>：指定属性的默认值。

- <xref:System.ComponentModel.TypeConverterAttribute>：指定显示在“属性”窗口中的字符串和非字符串属性值之间的自定义转换。

- <xref:System.ComponentModel.EditorAttribute>：指定用于修改属性的自定义编辑器。

## <a name="compile-the-code"></a>编译代码
 本示例需要引用以下程序集：

- Microsoft.VisualStudio.SharePoint

- Microsoft.VisualStudio.Shell

- Microsoft.VisualStudio.Shell.Interop

- Microsoft.VisualStudio.Shell.Interop.8.0

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署扩展，请为程序集以及要随扩展分发的任何其他文件创建 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (VSIX) 包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 项目](../sharepoint/extending-sharepoint-projects.md)
- [操作说明：创建 SharePoint 项目扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [操作说明：将快捷菜单项添加到 SharePoint 项目](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
