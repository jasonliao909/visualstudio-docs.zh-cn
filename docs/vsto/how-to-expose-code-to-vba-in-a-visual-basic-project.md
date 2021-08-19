---
title: 如何：在 Visual Basic 项目中向 VBA 公开代码
description: 了解如何在 Visual Basic 项目中公开代码，以在两种类型的代码彼此交互的情况中 Visual Basic for Applications (VBA) 代码。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- Visual Basic [Office development in Visual Studio], exposing code to VBA
- exposing code to VBA
- host items [Office development in Visual Studio], exposing code to VBA
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: a943688945ab7134742ff85ec63e7fad5a4f11c6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122122808"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-basic-project"></a>如何：在 Visual Basic 项目中向 VBA 公开代码
  [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]如果希望两种类型的代码彼此交互，可以在项目中公开代码，以便 Visual Basic for Applications (的 VBA) 代码。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Visual Basic 过程不同于 Visual c # 过程。 有关详细信息，请参阅 [如何：在 Visual C&#35; 项目中向 VBA 公开代码](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)。

 对于主机项类中的代码，该进程与其他类中的代码的进程不同：

- [公开主机项类中的代码](#HostItemCode)

- [公开不在主机项类中的代码](#NonHostItem)

## <a name="expose-code-in-a-host-item-class"></a><a name="HostItemCode"></a> 公开主机项类中的代码
 若要使 VBA 代码能够调用主机项类中 Visual Basic 代码，请将主机项的 **EnableVbaCallers** 属性设置为 **True**。

 有关演示如何公开主机项类的方法，然后从 vba 中调用该方法的演练，请参阅[演练：在 Visual Basic 项目中调用 VBA 中的代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)。 有关宿主项的详细信息，请参阅 [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

#### <a name="to-expose-code-in-a-host-item-to-vba"></a>向 VBA 公开主机项中的代码

1. 打开或创建一个文档级 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 项目，该项目基于 Word 文档、Excel 工作簿或支持宏且已经包含 VBA 代码的 Excel 模板。

     有关支持宏的文档文件格式的详细信息，请参阅 [结合 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)。

    > [!NOTE]
    > 此功能无法在 Word 模板项目中使用。

2. 确保在不提示用户启用宏的情况下允许文档中的 VBA 代码运行。 通过在 Word 或 Excel 的“信任中心”设置中将 Office 项目的位置添加到受信任位置列表中，可以信任要运行的 VBA 代码。

3. 将你想要向 VBA 公开的属性、方法或事件添加到项目中的某个主机项类，然后将该新成员声明为 **公共** 成员。 类的名称取决于应用程序：

    - 在 Word 项目中，默认情况下，主机项类命名为 `ThisDocument` 。

    - 在 Excel 项目中，默认情况下，主机项类命名为 `ThisWorkbook` 、 `Sheet1` 、 `Sheet2` 和 `Sheet3` 。

4. 将主机项的 **EnableVbaCallers** 属性设置为 **True**。 当宿主项在设计器中处于打开状态时，此属性将出现在 " **属性** " 窗口中。

     设置此属性后，Visual Studio 会自动将 **ReferenceAssemblyFromVbaProject** 属性设置为 **True**。

    > [!NOTE]
    > 如果工作簿或文档尚未包含 VBA 代码，或者文档中的 VBA 代码不受信任，无法运行，则将 **EnableVbaCallers** 属性设置为 **True** 时，你将收到一条错误消息。 这是因为在这种情况下，Visual Studio 无法修改文档中的 VBA 项目。

5. 在显示的消息中单击 **“确定”** 。 此消息提醒你，如果在从运行项目时向工作簿或文档添加 VBA 代码，则在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 下次生成项目时，vba 代码将丢失。 这是因为每次生成项目时，都会覆盖生成输出文件夹中的文档。

     此时，Visual Studio 配置项目，以便 VBA 项目可以调入程序集。 Visual Studio 还会将一个名为的属性添加 `CallVSTOAssembly` 到 `ThisDocument` `ThisWorkbook` VBA 项目中的、、、 `Sheet1` `Sheet2` 或 `Sheet3` 模块。 您可以使用此属性来访问向 VBA 公开的类的公共成员。

6. 生成项目。

## <a name="expose-code-that-is-not-in-a-host-item-class"></a><a name="NonHostItem"></a> 公开不在主机项类中的代码
 若要使 VBA 代码能够调用不在宿主项类中 Visual Basic 代码，请修改代码，使其对 VBA 可见。

### <a name="to-expose-code-that-is-not-in-a-host-item-class-to-vba"></a>向 VBA 公开不在主机项类中的代码

1. 打开或创建一个文档级 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] 项目，该项目基于 Word 文档、Excel 工作簿或支持宏且已经包含 VBA 代码的 Excel 模板。

     有关支持宏的文档文件格式的详细信息，请参阅 [结合 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)。

    > [!NOTE]
    > 此功能无法在 Word 模板项目中使用。

2. 确保在不提示用户启用宏的情况下允许文档中的 VBA 代码运行。 通过在 Word 或 Excel 的“信任中心”设置中将 Office 项目的位置添加到受信任位置列表中，可以信任要运行的 VBA 代码。

3. 将要向 VBA 公开的成员添加到项目中的公共类，并将新成员声明为 **公共** 成员。

4. 将以下和属性应用于要 <xref:System.Runtime.InteropServices.ComVisibleAttribute> <xref:Microsoft.VisualBasic.ComClassAttribute> 向 VBA 公开的类。 这些属性使类对 VBA 可见。

    ```vb
    <Microsoft.VisualBasic.ComClass()> _
    <System.Runtime.InteropServices.ComVisibleAttribute(True)> _
    ```

5. 替代项目中主机项类的 **GetAutomationObject** 方法，以返回要向 VBA 公开的类的实例。 下面的代码示例假定你向 VBA 公开一个名为的类 `DocumentUtilities` 。

    ```vb
    Protected Overrides Function GetAutomationObject() As Object
        Return New DocumentUtilities()
    End Function
    ```

6. 打开 (Word) 或工作表 (用于 Excel) 设计器中的文档 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

7. 在 **“属性”** 窗口中，选择 **“ReferenceAssemblyFromVbaProject”** 属性，并将值更改为 **“True”**。

    > [!NOTE]
    > 如果工作簿或文档尚未包含 VBA 代码，或者文档中的 VBA 代码不受信任，无法运行，则将 **ReferenceAssemblyFromVbaProject** 属性设置为 **True** 时，你将收到一条错误消息。 这是因为在这种情况下，Visual Studio 无法修改文档中的 VBA 项目。

8. 在显示的消息中单击 **“确定”** 。 此消息提醒你，如果在从运行项目时向工作簿或文档添加 VBA 代码，则在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 下次生成项目时，vba 代码将丢失。 这是因为每次生成项目时，都会覆盖生成输出文件夹中的文档。

     此时，Visual Studio 配置项目，以便 VBA 项目可以调入程序集。 Visual Studio 还会将一个名为的方法添加 `GetManagedClass` 到 VBA 项目。 可以从 VBA 项目中的任何位置调用此方法，以访问向 VBA 公开的类。

9. 生成项目。

## <a name="see-also"></a>请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [合并 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)
- [演练：在 Visual Basic 项目中调用 VBA 中的代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-basic-project.md)
- [如何：在 Visual C&#35; 项目中向 VBA 公开代码](../vsto/how-to-expose-code-to-vba-in-a-visual-csharp-project.md)
