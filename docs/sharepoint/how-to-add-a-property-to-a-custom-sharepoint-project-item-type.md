---
title: 将属性添加到自定义 SharePoint 项目项类型
description: 将属性添加到自定义 SharePoint 项目项类型。 在“解决方案资源管理器”中选择项目项时，属性将显示在“属性”窗口中。
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
ms.openlocfilehash: cde438dc6a43f158d119ac380a28bd276c04c7e1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600623"
---
# <a name="how-to-add-a-property-to-a-custom-sharepoint-project-item-type"></a>如何：将属性添加到自定义 SharePoint 项目项类型
  定义自定义 SharePoint 项目项类型时，可以将属性添加到项目项。 在“解决方案资源管理器”中选择项目项时，属性将显示在“属性”窗口中。 

 以下步骤假定你已定义了自己的 SharePoint 项目项类型。 有关详细信息，请参阅[如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

### <a name="to-add-a-property-to-a-definition-of-a-project-item-type"></a>若要将属性添加到项目项类型的定义中

1. 使用公共属性定义一个类，用来表示要添加到自定义项目项类型中的属性。 如果要将多个属性添加到自定义项目项类型，则可以在同一个类或不同的类中定义所有属性。

2. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 实现的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 方法中，处理 projectItemTypeDefinition 参数的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> 事件。

3. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> 事件的事件处理程序中，将自定义属性类的实例添加到事件自变量参数的 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemPropertiesRequestedEventArgs.PropertySources%2A> 集中。

## <a name="example"></a>示例
 下面的代码示例演示了如何向自定义项目项类型添加名为“示例属性”的属性。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb" id="Snippet11":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs" id="Snippet11":::

### <a name="understand-the-code"></a>了解代码
 若要确保每次 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> 事件发生时都使用 `CustomProperties` 类的相同实例，代码示例会在第一次发生该事件时将属性对象保存到项目项的 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性中。 每当该事件再次发生时，代码都将检索此对象。 有关使用 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性保存具有项目项的数据的更多信息，请参阅[将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

 若要保留对属性值的更改，`ExampleProperty` 的 set 访问器将新值保存到与属性关联的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> 对象的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> 属性中。 有关使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> 属性保存具有项目项的数据的详细信息，请参阅[在 SharePoint 项目系统的扩展中保存数据](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

### <a name="specify-the-behavior-of-custom-properties"></a>指定自定义属性的行为
 可以通过将来自 <xref:System.ComponentModel> 命名空间的属性应用到属性定义来定义自定义属性的显示方式以及在“属性”窗口中的行为。 以下属性在许多情况下都很有用：

- <xref:System.ComponentModel.DisplayNameAttribute>：指定显示在“属性”窗口中的属性的名称。

- <xref:System.ComponentModel.DescriptionAttribute>：在选择属性时，指定显示在“属性”窗口底部的描述字符串。

- <xref:System.ComponentModel.DefaultValueAttribute>：指定属性的默认值。

- <xref:System.ComponentModel.TypeConverterAttribute>：指定显示在“属性”窗口中的字符串和非字符串属性值之间的自定义转换。

- <xref:System.ComponentModel.EditorAttribute>：指定用于修改属性的自定义编辑器。

## <a name="compile-the-code"></a>编译代码
 这些节点示例需要一个类库项目，其中包含对以下程序集的引用：

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>部署项目项
 若要使其他开发人员能使用你的项目项，请创建项目模板或项目项模板。 有关详细信息，请参阅[为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 若要部署项目项，请为程序集、模板以及要随项目项分发的任何其他文件创建 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (VSIX) 包。 有关详细信息，请参阅[在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅
- [如何：定义 SharePoint 项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [如何：将快捷菜单项添加到自定义 SharePoint 项目项类型](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
