---
title: 从其他 VSTO 解决方案调用外接程序Office代码
description: 了解如何将外接程序中的对象公开VSTO其他解决方案，包括其他Microsoft Office解决方案。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], calling code in application-level add-ins
- application-level add-ins [Office development in Visual Studio], calling code from other solutions
- calling add-in code
- add-ins [Office development in Visual Studio], calling code from other solutions
- interoperability [Office development in Visual Studio]
- calling code from VBA
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 857cff3d396cfa08d45d7c15bc9b045f7fe23f0c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083695"
---
# <a name="call-code-in-vsto-add-ins-from-other-office-solutions"></a>从其他 VSTO 解决方案调用外接程序Office代码
  可以向其他解决方案（包括其他 Microsoft Office 解决方案）公开 VSTO 外接程序中的对象。 如果 VSTO 外接程序提供了你希望使其他解决方案能够使用的服务，这一点非常有用。 例如，如果 VSTO 的 Microsoft Office Excel 外接程序对来自 Web 服务的财务数据执行计算，则其他解决方案可以通过运行时调用 Excel VSTO 外接程序来执行这些计算。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

 此过程包括以下两个主要步骤：

- 在 VSTO 外接程序中，向其他解决方案公开对象。

- 在其他解决方案中，访问由 VSTO 外接程序公开的对象，然后调用对象的成员。

## <a name="types-of-solutions-that-can-call-code-in-an-add-in"></a>可在外接程序中调用代码的解决方案类型
 可以将外接程序中的对象VSTO以下类型的解决方案中：

- 在与 VSTO 外接程序相同的应用程序进程中加载的文档中的 Visual Basic for Applications (VBA) 代码。

- 在与 VSTO 外接程序相同的应用程序进程中加载的文档级自定义项。

- 使用 Visual Studio 中的 Office 项目模板创建的其他 VSTO 外接程序。

- COM VSTO 外接程序（即直接实现 <xref:Extensibility.IDTExtensibility2> 接口的 VSTO 外接程序）。

- 在不同于 VSTO 外接程序的进程中运行的任何解决方案（这些类型的解决方案也称为 *进程外客户端*）。 其中包括使 Office 应用程序实现自动化的应用程序（例如 Windows 窗体或控制台应用程序），以及在其他进程中加载的 VSTO 外接程序。

## <a name="expose-objects-to-other-solutions"></a>向其他解决方案公开对象
 若要向其他解决方案公开 VSTO 外接程序中的对象，请在 VSTO 外接程序中执行下列步骤：

1. 定义要向其他解决方案公开的类。

2. 重写 <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> 类中的 `ThisAddIn` 方法。 返回要向其他解决方案公开的类的实例。

### <a name="define-the-class-you-want-to-expose-to-other-solutions"></a>定义要向其他解决方案公开的类
 要公开的类必须至少是公共类，必须将 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性设置为 **true**，并且必须公开 [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) 接口。

 建议通过执行以下步骤公开 [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) 接口：

1. 定义一个接口，该接口声明要向其他解决方案公开的成员。 可以在 VSTO 外接程序项目中定义此接口。 但是，如果要向非 VBA 解决方案公开类，以便调用 VSTO 外接程序的解决方案无需引用 VSTO 外接程序项目即可引用此接口，则可能需要在单独的类库项目中定义此接口。

2. 将 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性应用到此接口，并将此属性设置为 **true**。

3. 修改你的类以实现此接口。

4. 将 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 属性应用于类，将此属性设置为 枚举的 **None** <xref:System.Runtime.InteropServices.ClassInterfaceType> 值。

5. 如果要向进程外客户端公开此类，可能还需要执行以下操作：

   - 从 <xref:System.Runtime.InteropServices.StandardOleMarshalObject>派生类。 有关详细信息，请参阅 [向进程外客户端公开类](#outofproc)。

   - 在定义此接口的项目中设置“为 COM 互操作注册”  属性。 只有在希望使客户端能够使用早期绑定来调用外接程序VSTO此属性才是必需的。

   下面的代码示例演示一个 `AddInUtilities` 类，该类具有可由其他解决方案调用的 `ImportData` 方法。 若要在更大演练的上下文中查看此代码，请参阅演练：从 VBA 调用VSTO[外接程序中的代码](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)。

   :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/AddInUtilities.cs" id="Snippet3":::
   :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/AddInUtilities.vb" id="Snippet3":::

### <a name="expose-classes-to-vba"></a>向 VBA 公开类
 执行上述步骤时，VBA 代码只能调用在接口中声明的方法。 VBA 代码无法调用类中的任何其他方法，包括类从基类（如 <xref:System.Object>）中获取的方法。

 或者，可以通过将 属性设置为 枚举的 [AutoDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) 或 AutoDual 值来公开 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> IDispatch <xref:System.Runtime.InteropServices.ClassInterfaceType> 接口。 如果公开接口，则不需要在单独的接口中声明方法。 不过，VBA 代码可以调用类中的任何公共方法和非静态方法，包括从基类（如 <xref:System.Object>）获取的方法。 此外，使用早期绑定的进程外客户端不能调用你的类。

### <a name="expose-classes-to-out-of-process-clients"></a><a name="outofproc"></a> 向进程外客户端公开类
 如果要向进程外客户端公开 VSTO 外接程序中的类，则应从 <xref:System.Runtime.InteropServices.StandardOleMarshalObject> 派生该类，以确保进程外客户端可以调用公开的 VSTO 外接程序对象。 否则，尝试在进程外客户端中获取已公开对象的实例可能会意外失败。

 此失败是因为必须在主 UI 线程上对 Office 应用程序的对象模型进行的所有调用，但从进程外客户端到对象的调用将到达任意 RPC (远程过程调用) 线程。 .NET Framework 中的 COM 封送处理机制不会切换线程，而是尝试将对你的对象的调用封送到传入 RPC 线程（而不是主 UI 线程）中。 如果你的对象是从 <xref:System.Runtime.InteropServices.StandardOleMarshalObject>派生的类的实例，则对你的对象的传入调用会自动封送到用于创建公开对象的线程中，该线程将是主机应用程序的主 UI 线程。

 有关在解决方案中Office线程的更多信息，请参阅 中的线程[Office。](../vsto/threading-support-in-office.md)

### <a name="override-the-requestcomaddinautomationservice-method"></a>重写 RequestComAddInAutomationService 方法
 以下代码示例演示了如何重写 VSTO 外接程序中 <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> 类中的 `ThisAddIn` 。 该示例假定已定义一个名为 `AddInUtilities` 的类，该类要向其他解决方案公开。 若要在更大演练的上下文中查看此代码，请参阅演练：从 VBA 调用VSTO[外接程序中的代码](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/ThisAddIn.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/ThisAddIn.vb" id="Snippet1":::

 加载 VSTO 外接程序后， [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 将调用 <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> 方法。 运行时将返回的对象分配给表示外接程序VSTO COMAddIn.Object <xref:Microsoft.Office.Core.COMAddIn> 属性。 此 <xref:Microsoft.Office.Core.COMAddIn> 对象可供其他 Office 解决方案以及使 Office 实现自动化的解决方案使用。

## <a name="access-objects-from-other-solutions"></a>从其他解决方案访问对象
 若要调用 VSTO 外接程序中公开的对象，请在客户端解决方案中执行下列步骤：

1. 获取表示公开的 VSTO 外接程序的 <xref:Microsoft.Office.Core.COMAddIn> 对象。 通过在主机 Office 应用程序的对象模型中使用 `Application.COMAddIns` 属性，客户端可以访问所有可用的 VSTO 外接程序。

2. 访问 对象的 COMAddIn.Object <xref:Microsoft.Office.Core.COMAddIn> 属性。 此属性从 VSTO 外接程序返回公开的对象。

3. 调用已公开对象的成员。

   使用 COMAddIn.Object 属性的返回值的方式对于 VBA 客户端和非 VBA 客户端是不同的。 对于进程外客户端，需要其他代码以避免可能的争用情况。

### <a name="access-objects-from-vba-solutions"></a>从 VBA 解决方案访问对象
 下面的代码示例演示如何使用 VBA 调用由外接程序VSTO公开的方法。 此 VBA 宏调用名为 的方法，该方法在名为 `ImportData` **ExcelImportData** VSTO外接程序中定义。 若要在更大演练的上下文中查看此代码，请参阅演练：从 VBA 调用VSTO[外接程序中的代码](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)。

```vb
Sub CallVSTOMethod()
    Dim addIn As COMAddIn
    Dim automationObject As Object
    Set addIn = Application.COMAddIns("ExcelImportData")
    Set automationObject = addIn.Object
    automationObject.ImportData
End Sub
```

### <a name="access-objects-from-non-vba-solutions"></a>从非 VBA 解决方案访问对象
 在非 VBA 解决方案中，必须将 COMAddIn.Object 属性值强制转换到它所实现接口，然后可以调用接口对象上公开的方法。 以下代码示例演示了如何从不同的 VSTO 外接程序中调用 `ImportData` 方法，这些外接程序是通过使用 Visual Studio 中的 Office 开发人员工具创建的。

```vb
Dim addIn As Office.COMAddIn = Globals.ThisAddIn.Application.COMAddIns.Item("ExcelImportData")
Dim utilities As ExcelImportData.IAddInUtilities = TryCast( _
    addIn.Object, ExcelImportData.IAddInUtilities)
utilities.ImportData()
```

```csharp
object addInName = "ExcelImportData";
Office.COMAddIn addIn = Globals.ThisAddIn.Application.COMAddIns.Item(ref addInName);
ExcelImportData.IAddInUtilities utilities = (ExcelImportData.IAddInUtilities)addIn.Object;
utilities.ImportData();
```

 此示例中，如果尝试将 COMAddIn.Object 属性的值强制转换到 类而不是 接口，代码 `AddInUtilities` `IAddInUtilities` 将引发 <xref:System.InvalidCastException> 。

## <a name="see-also"></a>请参阅
- [程序VSTO外接程序](../vsto/programming-vsto-add-ins.md)
- [演练：从 VBA 调用VSTO外接程序中的代码](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)
- [开发Office解决方案](../vsto/developing-office-solutions.md)
- [如何：在 Office 创建Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [使用扩展性接口自定义 UI 功能](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)
