---
title: 如何：向"项目"SharePoint添加|Microsoft Docs
description: 使用项目扩展将属性添加到SharePoint项目。 在项目中选择属性窗口时，属性将显示在解决方案资源管理器。
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
ms.openlocfilehash: c6b7e0d5a361321f1173688c8501a97d14b7e326119c4854c0fcd4310f1ac5ea
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121425331"
---
# <a name="how-to-add-a-property-to-sharepoint-projects"></a>如何：向项目SharePoint属性
  可以使用项目扩展将属性添加到任何SharePoint项目。 在 "属性 **"** 窗口中选择项目时， 属性 **解决方案资源管理器。**

 以下步骤假定已创建项目扩展。 有关详细信息，请参阅[如何：创建SharePoint扩展。](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

### <a name="to-add-a-property-to-a-sharepoint-project"></a>向项目添加SharePoint

1. 使用公共属性定义一个类，该属性表示要添加到项目SharePoint属性。 如果要添加多个属性，可以在同一类或不同类中定义所有属性。

2. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> 实现的方法 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 中，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> *projectService 参数* 的 事件。

3. 在 事件的事件处理程序中，将 properties 类的实例添加到事件参数 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectPropertiesRequestedEventArgs.PropertySources%2A> 参数的集合。

## <a name="example"></a>示例
 下面的代码示例演示如何向项目添加两SharePoint属性。 一个属性将数据持久保存于 *.csproj.user 文件或 .vbproj.user*  (中的项目用户选项) 。 另一个属性在 *.csproj 文件或 .vbproj* 文件 (中保存其) 。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs" id="Snippet1":::

### <a name="understand-the-code"></a>了解代码
 为了确保每次发生事件时都使用相同的 类实例，代码示例在首次发生此事件时将 properties 对象添加到项目的 `CustomProjectProperties` <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性中。 每当再次发生此事件时，代码将检索此对象。 有关使用 属性将数据与项目关联的详细信息，请参阅将自定义数据与 SharePoint <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> [工具扩展关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

 若要保留对属性值的更改，属性的 **set** 访问器使用以下 API：

- `CustomUserFileProperty` 使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A> 属性将其值保存到项目用户选项文件中。

- `CustomProjectFileProperty` 使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> 方法将其值保存到项目文件中。

  有关在这些文件中保存数据的信息，请参阅将数据保存在项目SharePoint[扩展中](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

### <a name="specify-the-behavior-of-custom-properties"></a>指定自定义属性的行为
 可以通过将命名空间中的属性应用于属性定义来定义自定义属性在"属性"窗口中的 <xref:System.ComponentModel> 显示和行为方式。 以下属性在许多情况下都很有用：

- <xref:System.ComponentModel.DisplayNameAttribute>：指定"属性"窗口中显示 **的属性** 的名称。

- <xref:System.ComponentModel.DescriptionAttribute>：指定在选择属性时显示在"属性"窗口底部的说明字符串。

- <xref:System.ComponentModel.DefaultValueAttribute>：指定 属性的默认值。

- <xref:System.ComponentModel.TypeConverterAttribute>：指定在"属性"窗口中显示的字符串与非字符串属性值之间的自定义转换。

- <xref:System.ComponentModel.EditorAttribute>：指定用于修改 属性的自定义编辑器。

## <a name="compile-the-code"></a>编译代码
 此示例需要引用以下程序集：

- Microsoft.VisualStudio。SharePoint

- Microsoft.VisualStudio.Shell

- Microsoft.VisualStudio.Shell.Interop

- Microsoft.VisualStudio.Shell.Interop.8.0

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署扩展，请为程序集 (VSIX) 包以及要随扩展一起分发的其他任何文件 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建扩展。 有关详细信息，请参阅在 Visual Studio 中为 SharePoint[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>另请参阅
- [扩展SharePoint项目](../sharepoint/extending-sharepoint-projects.md)
- [如何：创建SharePoint扩展](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [如何：向项目添加SharePoint菜单项](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
