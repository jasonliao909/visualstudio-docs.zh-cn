---
title: 网站支持属性 |Microsoft Docs
description: 了解使用网站项目扩展 Visual Studio 的功能时所必需的网站支持属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- web site projects, registration
ms.assetid: 46d52e2c-ca2a-4bbd-8500-5b0129768aec
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: fc98f580b8619cb68ccc929b0e529dcead683e68
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122041966"
---
# <a name="web-site-support-attributes"></a>网站支持属性
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 网站项目可以扩展以提供对 Web 编程语言的支持。 语言必须自行注册， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 以便在选择该语言时，项目模板可以出现在 " **新建** 网站" 对话框中。

IronPython Studio 示例包括网站支持。 该示例包含以下特性类，可将 IronPython 注册为新 Web 项目的代码隐藏语言。

## <a name="websiteprojectattribute"></a>WebSiteProjectAttribute
 此属性放置在语言项目上。 它将语言添加到 "**新建** 网站" 对话框的 "**语言**" 列表中的 Web 编程语言列表。 例如，以下代码将 IronPython 添加到列表中：

```
[WebSiteProject("IronPython", "Iron Python")]
public class PythonProjectPackage : ProjectPackage
```

 此属性还将模板路径设置为指向 "模板" 文件夹。 有关模板文件夹位置的详细信息，请参阅网站 [支持模板](../../extensibility/internals/web-site-support-templates.md)。

## <a name="websiteprojectrelatedfilesattribute"></a>WebSiteProjectRelatedFilesAttribute
 此属性放置在语言项目上。 它允许网站项目将一种文件类型（ (相关) ）嵌套在 **解决方案资源管理器** 中 (主) 的另一文件类型下。

 例如，下面的代码指定 IronPython 代码隐藏文件与 .aspx 文件相关。 在 IronPython 网站解决方案中创建新的 .aspx 网页时，将生成一个新的 py 源文件，并将其显示为 .aspx 页面的子节点。

```
[WebSiteProjectRelatedFiles("aspx", "py")]
public class PythonProjectPackage : ProjectPackage
```

## <a name="provideintellisenseproviderattribute"></a>ProvideIntellisenseProviderAttribute
 此属性位于语言项目包上。 它选择语言的 IntelliSense 提供程序。

 例如，下面的代码指定 <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject> 应按需创建 PythonIntellisenseProvider 的实例以提供语言服务。

```
[ProvideIntellisenseProvider(typeof(PythonIntellisenseProvider), "IronPythonCodeProvider", "Iron Python", ".py", "IronPython;Python", "IronPython")]
public class PythonPackage : Package, IOleComponent
```

 当请求带有代码但未缓存的网页时，IVsIntellisenseProject 实现将处理引用并调用语言编译器。

## <a name="see-also"></a>请参阅
- [网站支持](../../extensibility/internals/web-site-support.md)
