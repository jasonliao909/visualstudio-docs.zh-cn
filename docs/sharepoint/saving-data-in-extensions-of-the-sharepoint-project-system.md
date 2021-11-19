---
title: 在 SharePoint Project 系统的扩展中保存数据 |Microsoft Docs
titleSuffix: ''
description: 了解如何保存在关闭包含扩展的 SharePoint 项目后保留的字符串数据。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
helpviewer_keywords:
- SharePoint project items, saving string data
- project items [SharePoint development in Visual Studio], saving string data
- projects [SharePoint development in Visual Studio], saving string data
- SharePoint projects, saving string data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 671571551483c4eff71c1324e1c53c7cbb43ff9c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602532"
---
# <a name="save-data-in-extensions-of-the-sharepoint-project-system"></a>在 SharePoint 项目系统的扩展中保存数据
  在扩展 SharePoint 项目系统时，可以保存在关闭 SharePoint 项目后保留的字符串数据。 数据通常与特定项目项或项目本身相关联。

 如果你有不需要保留的数据，则可以将数据添加到实现该接口 SharePoint 工具对象模型中的任何对象 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> 。 有关详细信息，请参阅[将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)。

## <a name="save-data-that-is-associated-with-a-project-item"></a>保存与项目项关联的数据
 如果有与特定 SharePoint 项目项关联的数据（如添加到项目项的属性的值），则可以将数据保存到项目项的 *spdata* 文件。 为此，请使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> 对象的属性 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> 。 你添加到此属性的数据将保存在项目项的 *spdata* 文件的 **ExtensionData** 元素中。 有关详细信息，请参阅 [ExtensionData 元素](../sharepoint/extensiondata-element.md)。

 下面的代码示例演示如何使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> 属性保存自定义 SharePoint 项目项类型中定义的字符串属性的值。 若要在更大的示例上下文中查看此示例，请参阅[如何：将属性添加到自定义 SharePoint 项目项类型](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb" id="Snippet14":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs" id="Snippet14":::

## <a name="save-data-that-is-associated-with-a-project"></a>保存与项目关联的数据
 如果你具有项目级数据（如你添加到 SharePoint 项目中的属性的值），则可以将数据保存到项目文件 (*.csproj* 文件或 *.vbproj* 文件) 或者 *.vbproj* 文件的项目用户选项文件 *(，)* 。 您选择用于保存数据的文件取决于您希望数据的使用方式：

- 如果希望数据对打开 SharePoint 项目的所有开发人员可用，请将数据保存到项目文件。 此文件始终签入到源代码管理数据库中，因此，此文件中的数据可供签出该项目的其他开发人员使用。

- 如果希望数据仅对在 Visual Studio 中打开 SharePoint 项目的当前开发人员可用，请将数据保存到 project 用户选项文件中。 此文件通常不会签入到源代码管理数据库中，因此，此文件中的数据不可供其他签出该项目的开发人员使用。

### <a name="save-data-to-the-project-file"></a>将数据保存到项目文件
 若要将数据保存到项目文件，请将 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> 对象转换为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> 对象，然后使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> 方法。 下面的代码示例演示如何使用此方法将项目属性的值保存到项目文件。 若要在更大的示例上下文中查看此示例，请参阅[如何：将属性添加到 SharePoint 项目](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb" id="Snippet3":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs" id="Snippet3":::

 有关将 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> 对象转换为 Visual Studio 自动化对象模型或集成对象模型中的其他类型的详细信息，请参阅在[SharePoint 项目系统类型和其他 Visual Studio 项目类型之间转换](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)。

### <a name="save-data-to-the-project-user-option-file"></a>将数据保存到项目用户选项文件
 若要将数据保存到项目用户选项文件，请使用 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A> 对象的属性 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> 。 下面的代码示例演示如何使用此属性将项目属性的值保存到项目用户选项文件中。 若要在更大的示例上下文中查看此示例，请参阅[如何：将属性添加到 SharePoint 项目](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb" id="Snippet2":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs" id="Snippet2":::

## <a name="see-also"></a>另请参阅
- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
- [将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
- [SharePoint 项目系统类型和其他 Visual Studio 项目类型之间进行转换](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
