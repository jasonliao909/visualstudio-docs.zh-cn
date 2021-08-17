---
title: 如何：在 C# 项目中向 VBA 公开代码
description: 如果希望两种类型的代码相互交互，Visual Basic for Applications (Visual C# 项目中的代码) VBA 代码。
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual C# [Office development in Visual Studio], exposing code to VBA
- VBA [Office development in Visual Studio], exposing code in document-level customizations
- document-level customizations [Office development in Visual Studio], exposing code
- exposing code to VBA
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 7e9c654b683c0a308fc7ead8aafeacc7b730d8720650bf0c19b7128acd2ac08f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394701"
---
# <a name="how-to-expose-code-to-vba-in-a-visual-c-project"></a>如何：在 Visual C# 项目中向 VBA 公开代码
  如果希望两种类型的代码相互交互，Visual Basic for Applications (Visual C# 项目中的代码) VBA 代码。

 Visual C# 过程不同于Visual Basic过程。 有关详细信息，请参阅[如何：向](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)项目 中的 VBA Visual Basic代码。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="expose-code-in-a-visual-c-project"></a>在 Visual C# 项目中公开代码
 若要使 VBA 代码能够调用 Visual C# 项目中的代码，请修改代码，使该代码对 COM 可见，然后在设计器中将 **ReferenceAssemblyFromVbaProject** 属性设置为 **True。**

 有关演示如何从 VBA 调用 Visual C# 项目中的方法的演练，请参阅演练：在 Visual C&#35; 项目中从 [VBA 调用代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)。

### <a name="to-expose-code-in-a-visual-c-project-to-vba"></a>向 VBA 公开 Visual C# 项目中的代码

1. 打开或创建一个文档级项目，该项目基于 Word 文档、Excel工作簿或支持宏的 Excel 模板，并且已包含 VBA 代码。

    有关支持宏的文档文件格式详细信息，请参阅合并[VBA 和文档级自定义。](../vsto/combining-vba-and-document-level-customizations.md)

   > [!NOTE]
   > 此功能无法在 Word 模板项目中使用。

2. 确保允许在不提示用户启用宏的情况下运行文档中的 VBA 代码。 通过在 Word 或 Excel 的“信任中心”设置中将 Office 项目的位置添加到受信任位置列表中，可以信任要运行的 VBA 代码。

3. 将要向 VBA 公开的成员添加到项目中的公共类，并声明该 **新成员为公共**。

4. 将以下 <xref:System.Runtime.InteropServices.ComVisibleAttribute> <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 和 属性应用于要向 VBA 公开的类。 这些特性使类对于 COM 可见，但不生成类接口。

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   [System.Runtime.InteropServices.ClassInterface(
       System.Runtime.InteropServices.ClassInterfaceType.None)]
   ```

5. 重写项目中主机项类的 **GetAutomationObject** 方法，以返回向 VBA 公开类的实例：

   - 如果要向 VBA 公开主机项类，请重写属于此类的 **GetAutomationObject** 方法，并返回类的当前实例。

     ```csharp
     protected override object GetAutomationObject()
     {
         return this;
     }
     ```

   - 如果要向 VBA 公开不是主机项的类，请重写项目中任何主机项的 **GetAutomationObject** 方法，并返回非宿主项类的实例。 例如，以下代码假定你要向 VBA 公开名为 `DocumentUtilities` 的类。

     ```csharp
     protected override object GetAutomationObject()
     {
         return new DocumentUtilities();
     }
     ```

     有关主机项详细信息，请参阅主机 [项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

6. 从要向 VBA 公开的类中提取接口。 在 **"提取接口** "对话框中，选择要包括在接口声明中的公共成员。 有关详细信息，请参阅 [提取接口重构](../ide/reference/extract-interface.md)。

7. 将 **public 关键字** 添加到接口声明。

8. 通过将以下属性添加到 接口，使接口对 COM <xref:System.Runtime.InteropServices.ComVisibleAttribute> 可见。

   ```csharp
   [System.Runtime.InteropServices.ComVisible(true)]
   ```

9. 打开 Word (的文档) 或 (工作表Excel) 在 的设计器中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

10. 在 **“属性”** 窗口中，选择 **“ReferenceAssemblyFromVbaProject”** 属性，并将值更改为 **“True”**。

    > [!NOTE]
    > 如果工作簿或文档尚未包含 VBA 代码，或者文档中的 VBA 代码不受信任的运行，则当将 **ReferenceAssemblyFromVbaProject** 属性设置为 **True** 时，将收到错误消息。 这是因为在这种情况下，Visual Studio 无法修改文档中的 VBA 项目。

11. 在显示的消息中单击 **“确定”** 。 此消息提醒你，如果在从 运行项目时将 VBA 代码添加到工作簿或文档，则 VBA 代码将在下次生成项目时 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 丢失。 这是因为每次生成项目时都会覆盖生成输出文件夹中的文档。

     此时，Visual Studio配置项目，以便 VBA 项目可以调用程序集。 Visual Studio还将名为 的方法 `GetManagedClass` 添加到 VBA 项目。 可以从 VBA 项目中的任何位置调用此方法，以访问向 VBA 公开的类。

12. 生成项目。

## <a name="see-also"></a>请参阅
- [如何：在 Office 创建Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [设计和创建Office解决方案](../vsto/designing-and-creating-office-solutions.md)
- [合并 VBA 和文档级自定义项](../vsto/combining-vba-and-document-level-customizations.md)
- [演练：在 Visual C&#35;项目中从 VBA 调用代码](../vsto/walkthrough-calling-code-from-vba-in-a-visual-csharp-project.md)
- [如何：向项目中的 VBA Visual Basic代码](../vsto/how-to-expose-code-to-vba-in-a-visual-basic-project.md)
