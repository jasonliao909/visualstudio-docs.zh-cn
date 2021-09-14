---
title: 如何：向项目扩展SharePoint Project添加|Microsoft Docs
titleSuffix: ''
description: 使用SharePoint项目项扩展将属性添加到SharePoint中已安装的任何项目Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 482e0e3a797f0906792868a022bea4f7e5aa329e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600625"
---
# <a name="how-to-add-a-property-to-a-sharepoint-project-item-extension"></a>如何：向项目项扩展SharePoint属性
  可以使用项目项扩展将属性添加到SharePoint中已安装的任何项目Visual Studio。 在 " **属性"** 窗口中选择项目项时， **该属性将显示在** 解决方案资源管理器。

 以下步骤假定已创建项目项扩展名。 有关详细信息，请参阅[如何：创建SharePoint Project扩展。](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

### <a name="to-add-a-property-to-a-project-item-extension"></a>向项目项扩展添加属性

1. 使用公共属性定义一个类，该属性表示要添加到项目项类型的属性。 如果要将多个属性添加到项目项类型，可以在同一类或不同类中定义所有属性。

2. 在 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> 实现的方法 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 中，处理 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> *projectItemType* 参数的 事件。

3. 在 事件的事件处理程序中，将 properties 类的实例添加到事件参数 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemPropertiesRequestedEventArgs.PropertySources%2A> 参数的集合。

## <a name="example"></a>示例
 下面的代码示例演示如何将名为 Example **Property** 的属性添加到事件接收器项目项。

:::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionproperty.cs" id="Snippet8":::
:::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionproperty.vb" id="Snippet8":::

### <a name="understand-the-code"></a>了解代码
 为了确保每次发生事件时都使用相同的 类实例，代码示例在首次发生此事件时将 properties 对象添加到项目项 `CustomProperties` <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> 的 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 属性中。 每当再次发生此事件时，代码将检索此对象。 有关使用 属性将数据与项目项关联的 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> 详细信息，请参阅将自定义数据与SharePoint[扩展关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

 若要保留对属性值的更改，的 **set** 访问器会将新值保存到与该属性关联的 `ExampleProperty` 对象的 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> 属性中。 有关使用 属性将数据与项目项一起保存详细信息，请参阅将数据保存在项目SharePoint <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> [扩展中](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)。

### <a name="specify-the-behavior-of-custom-properties"></a>指定自定义属性的行为
 可以通过将命名空间中的属性应用于属性定义来定义自定义属性在"属性"窗口中的 <xref:System.ComponentModel> 显示和行为方式。 以下属性在许多情况下都很有用：

- <xref:System.ComponentModel.DisplayNameAttribute>：指定"属性"窗口中显示 **的属性** 的名称。

- <xref:System.ComponentModel.DescriptionAttribute>：指定在选择属性时显示在"属性"窗口底部的说明字符串。

- <xref:System.ComponentModel.DefaultValueAttribute>：指定 属性的默认值。

- <xref:System.ComponentModel.TypeConverterAttribute>：指定在"属性"窗口中显示的字符串与非字符串属性值之间的自定义转换。

- <xref:System.ComponentModel.EditorAttribute>：指定用于修改 属性的自定义编辑器。

## <a name="compile-the-code"></a>编译代码
 这些示例需要引用以下程序集的类库项目：

- Microsoft.VisualStudio。SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>部署扩展
 若要部署扩展，请为程序集 (VSIX) 包以及要随扩展一起分发的其他任何文件 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 创建扩展。 有关详细信息，请参阅 在 SharePoint 中为 Visual Studio[工具部署Visual Studio。](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)

## <a name="see-also"></a>另请参阅
- [如何：创建SharePoint项目项扩展](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [如何：向项目项扩展SharePoint快捷菜单项](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)
- [扩展SharePoint项目项](../sharepoint/extending-sharepoint-project-items.md)
- [演练：扩展SharePoint项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
