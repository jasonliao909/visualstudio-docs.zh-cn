---
title: "\"选项页\"页的自动化|Microsoft Docs"
description: 了解如何使 VSPackage 中的自定义"工具选项"页可用于Visual Studio模型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Tools Options pages [Visual Studio SDK], automation support
- automation [Visual Studio SDK], creating Tools Options pages
ms.assetid: 0b25b82c-7432-4e0a-9e84-350269ba8260
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5a4f6b33b7a5e17c610831db5d4387065915ea00
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901651"
---
# <a name="automation-support-for-options-pages"></a>"选项"页的自动化支持
VSPackages 可以将自定义"选项"对话框提供给"工具" ("选项"页) ，并使它们 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 可用于自动化模型。

## <a name="tools-options-pages"></a>工具选项页
 若要创建 **"工具选项** "页，VSPackage 必须通过 VSPackage 的 方法实现提供返回到环境的用户 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> 控件实现。  (或，对于托管代码，为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> method.) 

 允许通过自动化模型访问此新页面是可选的，但强烈建议这样做。 可通过以下步骤执行此操作：

1. 通过 <xref:EnvDTE._DTE.Properties%2A> 实现 IDispatch 派生的对象来扩展 对象。

2. 返回方法的实现 (或对于托管代码，该方法) <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> <xref:Microsoft.VisualStudio.Shell.Package.GetAutomationObject%2A> IDispatch 派生的对象。

3. 当自动化使用者在自定义 Option 属性页上调用 方法时，环境使用 方法获取自定义"工具选项" <xref:EnvDTE._DTE.Properties%2A>  <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> 页的自动化实现。 

4. 然后，VSPackage 的自动化对象用于提供 <xref:EnvDTE.Property> 返回的每个 <xref:EnvDTE._DTE.Properties%2A> 。

   有关实现自定义工具 **选项页的示例** ，请参阅 [VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)。

## <a name="see-also"></a>另请参阅
- [公开项目对象](../../extensibility/internals/exposing-project-objects.md)
