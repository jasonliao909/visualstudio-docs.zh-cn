---
title: 如何：标识库中的符号|Microsoft Docs
description: 了解如何通过实现方法识别库中的符号，这些方法将导航信息从符号库传递到Visual Studio管理器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Call Browser tool, identifying symbols in the library
- Call Browser tool
ms.assetid: 8fb0de61-71e7-42d1-8b41-2ad915474384
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 33000a513f4a2580bb74a0b6ed5267231739244c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122042499"
---
# <a name="how-to-identify-symbols-in-a-library"></a>如何：标识库中的符号
符号浏览工具显示符号的分层视图。 符号表示命名空间、对象、类、类成员和其他语言元素。

 层次结构中的每个符号都可以由符号库通过以下接口传递给对象管理器的导航 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 信息进行标识：

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfoNode>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes>.

 该符号在层次结构中的位置可区分符号。 它允许符号浏览工具导航到特定符号。 符号的唯一完全限定路径确定位置。 路径中的每个元素都是一个节点。 路径以顶级节点开头，以特定符号结尾。 例如，如果 M1 方法是 C1 类的成员，而 C1 位于 N1 命名空间中，则 M1 方法的完整路径为 N1。C1。M1。 此路径包含三个节点：N1、C1 和 M1。

 导航信息允许对象管理器在层次结构中查找、选择和 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 保持选中符号。 它允许从一个浏览工具导航到另一个浏览工具。 使用 **对象浏览器** 浏览项目中的符号时，可以右键单击某个方法并启动 调用浏览器 工具，以在 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 调用图中显示该方法。

 两种形式描述符号位置。 规范形式基于符号的完全限定路径。 它表示符号在层次结构中的唯一位置。 它独立于符号浏览工具。 为了获取规范表单信息，对象 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 管理器调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> 方法。 呈现形式描述符号在特定的符号浏览工具中的位置。 符号的位置相对于层次结构中其他符号的位置。 给定符号可能有几个表示路径，但只有一个规范路径。 例如，如果 C1 类继承自 C2 类，并且两个类都位于 N1 命名空间中， **则对象浏览器** 将显示以下分层树：

```
N1
    C1
        Bases and Interfaces
            C2
    C2
        Bases and Interfaces
. . . . . . . . . . .

```

 此示例中 C2 类的规范路径为 N1 + C2。 C2 的演示路径包括 C1 和"基和接口"节点：N1 + C1 + "基和接口" + C2。

 若要获取表示形式信息，对象管理器将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A> 方法。

## <a name="to-obtain-canonical-and-presentation-forms-information"></a>获取规范窗体和表示形式信息

1. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> 方法。

     对象管理器调用此方法以获取符号规范路径中包含的节点列表。

    ```vb
    Public Function EnumCanonicalNodes(ByRef ppEnum As Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes) As Integer
        Dim EnumNavInfoNodes As CallBrowserEnumNavInfoNodes = _New CallBrowserEnumNavInfoNodes(m_strMethod)
        ppEnum = CType(EnumNavInfoNodes, IVsEnumNavInfoNodes)
        Return 0
    End Function
    ```

    ```csharp
    public int EnumCanonicalNodes(out Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes ppEnum)
    {
        CallBrowserEnumNavInfoNodes EnumNavInfoNodes =
            new CallBrowserEnumNavInfoNodes(m_strMethod);
        ppEnum = (IVsEnumNavInfoNodes)(EnumNavInfoNodes);
        return 0;
    }

    ```

2. 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A> 方法。

     对象管理器调用此方法以获取符号表示路径中包含的节点列表。

## <a name="see-also"></a>请参阅
- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [如何：向对象管理器注册库](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [如何：向对象管理器公开库提供的符号列表](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
