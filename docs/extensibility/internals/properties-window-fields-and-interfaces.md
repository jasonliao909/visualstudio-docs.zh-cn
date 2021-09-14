---
title: 属性窗口字段和接口|Microsoft Docs
description: 了解根据 IDE 中具有焦点的窗口确定属性窗口中显示的信息的选择Visual Studio信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Properties window, fields and interfaces
ms.assetid: 0328f0e5-2380-4a7a-a872-b547cb775050
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 99185ac6fe9d54a21e22fd2ea291089315ed0946
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602569"
---
# <a name="properties-window-fields-and-interfaces"></a>Properties Window Fields and Interfaces
用于确定"属性"窗口中显示的信息的选择模型基于IDE 中具有焦点的窗口。 每个窗口和所选窗口中的对象都可以将选择上下文对象推送到全局选择上下文。 当窗口具有焦点时，环境使用窗口框架中的值更新全局选择上下文。 当焦点更改时，选择上下文也更改。

## <a name="tracking-selection-in-the-ide"></a>在 IDE 中跟踪选择
 IDE 拥有的窗口框架或站点具有名为 的服务 <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> 。 以下步骤显示如何实现由用户将焦点更改为另一个打开窗口或在 解决方案资源管理器 中选择其他项目 **项** 引起的选择更改，以更改"属性"窗口中 **显示的内容** 。

1. VSPackage 创建的对象（位于所选窗口中）调用 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> 以调用 <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> 。

2. 所选窗口提供的选择容器将创建自己的 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 对象。 当选择更改时，VSPackage 会调用 来通知环境中的任何侦听器，包括"属性 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> "窗口的更改。  它还提供对层次结构和与新选择相关的项信息的访问。

3. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection.OnSelectChange%2A> 并传递参数中选定的层次结构 `VSHPROPID_BrowseObject` 项将填充 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 对象。

4. 返回从[IDispatch 接口派生的对象](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch)[，__VSHPROPID。VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>)请求的项，并且环境将其包装到 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> (，请参阅以下步骤) 。 如果调用失败，环境将再次调用 ，将选择容器传递给 `IVsHierarchy::GetProperty` [__VSHPROPID。VSHPROPID_SelContainer](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_SelContainer>) 层次结构项或项提供的信息。

    项目 VSPackage 不会创建，因为实现它的环境提供的窗口 VSPackage (例如，解决方案资源管理器) <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 代表它 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 构造。

5. 环境调用 的方法， <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 以基于接口获取 对象 `IDispatch` 以填充"属性 **"** 窗口。

   更改"属性 **"窗口中** 的值时，VSPackage 实现 和 以报告 `IVsTrackSelectionEx::OnElementValueChangeEx` `IVsTrackSelectionEx::OnSelectionChangeEx` 元素值的变化。 然后，环境调用 或 ，使"属性"窗口中 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> **显示的信息** 与属性值保持同步。 有关详细信息，请参阅 [更新属性窗口中的属性值](#updating-property-values-in-the-properties-window)。

   除了在 解决方案资源管理器 中选择其他项目项以显示与该项相关的属性外，还可使用"属性"窗口上的下拉列表从窗体或文档窗口中选择 **不同的对象**。 有关详细信息，请参阅属性 [窗口对象列表](../../extensibility/internals/properties-window-object-list.md)。

   可以更改"属性"窗口网格中信息的显示方式，从字母顺序更改为分类，如果可用，还可以单击"属性"窗口上的相应按钮打开所选 **对象的属性页**。 有关详细信息，请参阅属性[窗口按钮和](../../extensibility/internals/properties-window-buttons.md)[属性页](../../extensibility/internals/property-pages.md)。

   最后，"属性 **"** 窗口底部还包含"属性"窗口网格中所选 **字段** 的说明。 有关详细信息，请参阅从 ["属性"窗口获取字段说明](#getting-field-descriptions-from-the-properties-window)。

## <a name="updating-property-values-in-the-properties-window"></a><a name="updating-property-values-in-the-properties-window"></a> 更新"属性"窗口中的属性值
有两种方法可以保持“属性”  窗口与属性值更改同步。 第一种是调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> 接口，从而提供对基本窗口化功能的访问，包括访问和创建由环境提供的工具窗口和文档窗口。 下面的步骤介绍了此同步过程。

### <a name="updating-property-values-using-ivsuishell"></a>使用 IVsUIShell 更新属性值

#### <a name="to-update-property-values-using-the-ivsuishell-interface"></a>使用 IVsUIShell 接口更新属性值

1. 任何时候，只要 Vspackage、项目或编辑器需要创建或枚举工具或文档窗口，就调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>（通过 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> 服务）。

2. 实现 ，使"属性"窗口与项目属性更改保持同步 ("属性"窗口浏览的其他任何选定对象) 不实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.RefreshPropertyBrowser%2A> 和 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> 触发 <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink.OnChanged%2A> 事件。

3. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.AdviseHierarchyEvents%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.UnadviseHierarchyEvents%2A> 分别创建和禁用层次结构事件的客户端通知，而不要求层次结构实现 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>。

### <a name="updating-property-values-using-iconnection"></a>使用 IConnection 更新属性值
 第二种保持“属性”  窗口与属性值更改同步的方法是，实现可连接对象上的 `IConnection` ，以指示输出接口是否存在。 如果希望本地化属性名，请从 <xref:System.ComponentModel.ICustomTypeDescriptor> 派生对象。 <xref:System.ComponentModel.ICustomTypeDescriptor> 实现可以修改其返回的属性说明符和更改属性名。 若要本地化说明，请创建一个派生自 <xref:System.ComponentModel.DescriptionAttribute> 的属性并重写 Description 属性。

#### <a name="considerations-in-implementing-the-iconnection-interface"></a>实现 IConnection 接口的注意事项

1. `IConnection` 提供对具有 <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> 接口的枚举器子对象的访问权限。 它还提供对所有连接点的子对象的访问权限，每个子对象均实现 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> 接口。

2. 任何浏览对象都对实现 <xref:Microsoft.VisualStudio.OLE.Interop.IPropertyNotifySink> 事件负责。  “属性”窗口通过 `IConnection`为事件集提供建议。

3. 连接点用于控制在其实现 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.Advise%2A> 时允许的连接数（一个还是多个）。 只允许一个接口的连接点可以通过 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint.EnumConnections%2A> 方法返回 <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL>。

4. 客户端可以调用 `IConnection` 接口，以获得对具有 <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> 接口的枚举器子对象的访问权限。 随后可以调用 <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnectionPoints> 接口，从而为每个输出接口 ID (IID) 枚举连接点。

5. 此外，还可以调用 `IConnection` 从而为每个输出 IID 获取对具有 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> 接口的连接点子对象的访问权限。 通过 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> 接口，客户端启动或终止具有可连接对象和客户端自己的同步的公告循环。客户端还可以调用 接口来获取具有 接口的枚举器对象，以枚举 <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPoint> <xref:Microsoft.VisualStudio.OLE.Interop.IEnumConnections> 它知道的连接。

## <a name="getting-field-descriptions-from-the-properties-window"></a><a name="getting-field-descriptions-from-the-properties-window"></a> 从"属性"窗口获取字段说明
在“属性”  窗口底部，说明区域显示了与所选属性字段相关的信息。 默认情况下此功能处于开启状态。 如果你想要隐藏说明字段，右键单击“属性”  窗口并单击“说明” 。 执行此操作还会删除“菜单”窗口中“说明”  标题旁的复选标记。 你可以按照将“说明”  切换回开启状态的步骤来再次显示该字段。

 说明字段中的信息来自 <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo>。 每个方法、接口、组件类等在类型库中均可拥有一个未本地化的 `helpstring` 特性。 " **属性** "窗口从 检索字符串 <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo.GetDocumentation%2A> 。

### <a name="to-specify-localized-help-strings"></a>指定本地化的帮助字符串

1. 将 `helpstringdll` 特性添加到类型库中的库语句（`typelib`）。

   > [!NOTE]
   > 如果类型库位于对象库 (.olb) 文件中，则此步骤是可选的。

2. 为字符串指定 `helpstringcontext` 特性。 你还可以指定 `helpstring` 特性。

    这些特性不同于包含在实际 .chm 文件帮助主题中的 `helpfile` 和 `helpcontext` 特性。

   若要检索为突出显示的属性名称显示的说明信息，"属性"窗口将调用所选属性，并指定输出 <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2.GetDocumentation2%2A> `lcid` 字符串的所需属性。 在内部，<xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2> 查找 `helpstringdll` 特性中指定的 .dll 文件，并在该 .dll 文件上调用 `DLLGetDocumentation` 与指定的内容和 `lcid` 特性。

   `DLLGetDocumentation` 的签名和实现为：

```cpp
STDAPI DLLGetDocumentation
(
   ITypeLib * /* ptlib */,
   ITypeInfo * /* ptinfo */,
   LCID /* lcid */,
   DWORD dwCtx,
   BSTR * pbstrHelpString
);
```

 `DLLGetDocumentation` 函数必须是在 .def 文件中为 DLL 定义的导出。

 在内部，会创建一个实际为 DLL 的 .olb 文件。 此 DLL 包含一个资源（类型库 (.tlb) 文件）和一个导出的函数（ `DLLGetDocumentation`）。

 就 .olb 文件而言， `helpstringdll` 特性是可选的，因为它是包含 .tlb 文件本身的同一文件。

 若要获取显示在“说明”  窗格中的字符串，为此你至少需要在类型库中指定 `helpstring` 特性。 如果你希望本地化这些字符串，则必须指定 `helpstringdll` （可选）特性和 `helpstringcontext` （必需）特性，并实现 `DLLGetDocumentation`。

 通过 idl 的 `helpstringcontext` 特性和 `DLLGetDocumentation`获取本地化的信息时，没有需要实现的其他接口。

 获取某一属性的本地化名称和说明的另一方法是实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.GetLocalizedPropertyInfo%2A>。 有关此方法的实现的详细信息，请参阅 [Properties Window Fields and Interfaces](../../extensibility/internals/properties-window-fields-and-interfaces.md)。

## <a name="see-also"></a>另请参阅

- [扩展属性](../../extensibility/internals/extending-properties.md)
