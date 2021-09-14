---
title: 将属性添加到自定义SharePoint项目项类型
description: 向自定义项目项SharePoint属性。 在项目中选择属性窗口项时，属性将显示在解决方案资源管理器。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600623"
---
# <a name="how-to-add-a-property-to-a-custom-sharepoint-project-item-type"></a>如何：将属性添加到自定义SharePoint项目项类型
  定义自定义项目SharePoint类型时，可以将属性添加到项目项。 在 "**属性"** 窗口中选择项目项时， 属性 **解决方案资源管理器。**

 以下步骤假定已定义自己的项目SharePoint类型。 有关详细信息，请参阅[如何：定义SharePoint项目项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)。

### <a name="to-add-a-property-to-a-definition-of-a-project-item-type"></a>向项目项类型的定义添加属性

1. 使用公共属性定义一个类，该属性表示要添加到自定义项目项类型的属性。 如果要将多个属性添加到自定义项目项类型，可以在同一类或不同类中定义所有属性。

2. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> 实现的方法 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 中，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> *projectItemTypeDefinition 参数* 的 事件。

3. 在 事件的事件处理程序中，将自定义属性类的实例 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> 添加到 <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemPropertiesRequestedEventArgs.PropertySources%2A> 事件参数参数的集合。

## <a name="example"></a>示例
 下面的代码示例演示如何将名为 Example **Property** 的属性添加到自定义项目项类型。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb" id="Snippet11":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs" id="Snippet11":::

### <a name="understand-the-code"></a>了解代码
 为了确保每次发生事件时都使用相同的 类实例，代码示例在首次发生此事件时将 properties 对象保存到项目项 `CustomProperties` <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> 的 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性中。 每当再次发生此事件时，代码将检索此对象。 有关使用 属性通过项目项保存数据的信息， <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 请参阅将自定义数据与SharePoint[扩展关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

 若要保留对属性值的更改，的 **set** 访问器会将新值保存到与该属性关联的 `ExampleProperty` 对象的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> 属性中。 有关使用 属性将数据与项目项一起保存详细信息，请参阅将数据保存在项目SharePoint <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> [扩展中](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

### <a name="specify-the-behavior-of-custom-properties"></a>指定自定义属性的行为
 可以通过将命名空间中的属性应用于属性定义来定义自定义属性在"属性"窗口中的 <xref:System.ComponentModel> 显示和行为方式。 以下属性在许多情况下都很有用：

- <xref:System.ComponentModel.DisplayNameAttribute>：指定"属性"窗口中显示 **的属性** 的名称。

- <xref:System.ComponentModel.DescriptionAttribute>：指定在选择属性时显示在"属性"窗口底部的说明字符串。

- <xref:System.ComponentModel.DefaultValueAttribute>：指定 属性的默认值。

- <xref:System.ComponentModel.TypeConverterAttribute>：指定在"属性"窗口中显示的字符串与非字符串属性值之间的自定义转换。

- <xref:System.ComponentModel.EditorAttribute>：指定用于修改 属性的自定义编辑器。

## <a name="compile-the-code"></a>编译代码
 这些代码示例需要引用以下程序集的类库项目：

- Microsoft.VisualStudio。SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>部署项目项
 若要使其他开发人员能够使用项目项，请创建项目模板或项目项模板。 有关详细信息，请参阅[为项目项 创建项模板SharePoint模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 若要部署项目项，请为程序集 (模板以及要随项目项分发的其他任何文件创建 VSIX) 包 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的扩展名。 有关详细信息，请参阅 在 SharePoint 中为 Visual Studio[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>另请参阅
- [如何：定义SharePoint项类型](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [如何：将快捷菜单项添加到自定义SharePoint项目项类型](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
- [定义自定义SharePoint项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
