---
title: 运行时访问窗体区域
description: 了解如何以各种项目类型和版本的窗体区域Microsoft Office运行时访问窗体区域。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Inspectors [Office development in Visual Studio]
- Explorers [Office development in Visual Studio]
- form regions [Office development in Visual Studio], accessing at run time
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 45b09372438fbe25f35f5b96bf711f0fdd387881
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122047343"
---
# <a name="access-a-form-region-at-run-time"></a>运行时访问窗体区域

|适用于|
|----------------|
|本主题中的信息仅适用于以下项目类型和 Microsoft Office 版本。 有关详细信息，请参阅应用程序[类型和项目Office提供的功能](../vsto/features-available-by-office-application-and-project-type.md)。<br /><br /> **Project类型**<br /><br /> - VSTO外接程序项目<br /><br /> **Microsoft Office 版本**<br /><br /> -   [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)]|

 使用 `Globals` 类可以从 Outlook 项目中的任何位置访问窗体区域。 有关 类详细信息，请参阅对项目 中的对象的 `Globals` [全局Office访问](../vsto/global-access-to-objects-in-office-projects.md)。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="access-form-regions-that-appear-in-a-specific-outlook-inspector-window"></a>访问特定"检查器"窗口中Outlook区域
 若要访问在特定 Outlook 检查器中显示的所有窗体区域，请调用 `FormRegions` 类的 `Globals` 属性，并传入一个表示该检查器的 <xref:Microsoft.Office.Interop.Outlook.Inspector> 对象。

 下面的示例获取在当前获得焦点的检查器中显示的窗体区域的集合。 然后，此示例访问名为 `formRegion1` 的集合中的窗体区域，并将文本框中显示的文本设置为 `Hello World`。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb" id="Snippet2":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs" id="Snippet2":::

## <a name="access-form-regions-that-appear-in-a-specific-outlook-explorer-window"></a>访问特定"资源管理器"窗口中Outlook区域
 若要访问在特定 Outlook 资源管理器中显示的所有窗体区域，请调用 `FormRegions` 类的 `Globals` 属性，并传入一个表示该资源管理器的 <xref:Microsoft.Office.Interop.Outlook.Explorer> 对象。

 下面的示例获取在当前获得焦点的资源管理器中显示的窗体区域的集合。 然后，此示例访问名为 `formRegion1` 的集合中的窗体区域，并将文本框中显示的文本设置为 `Hello World`。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb" id="Snippet3":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs" id="Snippet3":::

## <a name="access-all-form-regions"></a>访问所有窗体区域
 若要访问在所有资源管理器和所有检查器中显示的所有窗体区域，请调用 `FormRegions` 类的 `Globals` 属性。

 下面的示例获取在所有资源管理器和所有检查器中显示的窗体区域的集合。 然后，此示例访问名为 `formRegion1` 的窗体区域，并将文本框中显示的文本设置为 `Hello World`。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Access_O12/ThisAddIn.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Access_O12/ThisAddIn.cs" id="Snippet1":::

## <a name="access-controls-on-a-form-region"></a>窗体区域上的访问控制
 若要使用 `Globals` 类来访问窗体区域中的控件，必须使窗体区域代码文件外部的代码可以访问控件。

### <a name="form-regions-designed-in-the-form-region-designer"></a>在窗体区域设计器中设计的窗体区域
 对于 C#，更改要访问的每个控件的修饰符。 若要执行此操作，请在窗体区域设计器中选择每个控件，然后在“属性”  窗口中将“Modifiers”  属性更改为“Internal”  或“public”  。 例如，如果将 **的“Modifier”**`textBox1` 属性更改为“Internal” ，则可以通过键入 `textBox1` 来访问 `Globals.FormRegions.FormRegion1.textBox1`。

 对于 Visual Basic，不需要更改修饰符。

### <a name="imported-form-regions"></a>导入的窗体区域
 如果导入在 Outlook 中设计的窗体区域，则窗体区域中每个控件的访问修饰符变为专用。 因为无法使用窗体区域设计器来修改导入的窗体区域，所以无法在“属性”  窗口更改控件的修饰符。

 若要能够从窗体区域代码文件外部访问控件，请在窗体区域代码文件中创建属性来返回该控件。

 若要详细了解如何在 C# 中创建属性，请参阅如何：声明和使用 C &#40;编程&#35;中的读写[&#41;。 ](/dotnet/csharp/programming-guide/classes-and-structs/how-to-declare-and-use-read-write-properties)

 若要详细了解如何在 Visual Basic 创建属性，请参阅[如何：](/dotnet/visual-basic/programming-guide/language-features/procedures/how-to-create-a-property)使用 (Visual Basic) 。

## <a name="see-also"></a>请参阅
- [创建表单Outlook指南](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [演练：设计Outlook区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [如何：将窗体区域添加到Outlook外接程序项目](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [窗体Outlook中的自定义操作](../vsto/custom-actions-in-outlook-form-regions.md)
- [将窗体区域与Outlook类关联](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
- [演练：导入在窗体中设计的Outlook](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
- [如何：Outlook窗体区域](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)
- [创建Outlook窗体区域](../vsto/creating-outlook-form-regions.md)
- [运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
