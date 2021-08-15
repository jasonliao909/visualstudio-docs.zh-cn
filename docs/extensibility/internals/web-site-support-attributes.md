---
title: 网站支持属性|Microsoft Docs
description: 了解使用网站项目扩展 Visual Studio功能所需的网站支持属性。
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
ms.openlocfilehash: e5eb1af28c7a8dd7dccf2c161474f821f004c07e06f11b554f898190971837a0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414177"
---
# <a name="web-site-support-attributes"></a>网站支持属性
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 可以扩展网站项目以提供对 Web 编程语言的支持。 语言必须使用 注册自身，以便项目模板可以在选择语言时显示在"新建网站" [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 对话框中。 

IronPython Studio 示例包括网站支持。 此示例包含以下属性类，用于将 IronPython 注册为新 Web 项目的代码后发语言。

## <a name="websiteprojectattribute"></a>WebSiteProjectAttribute
 此属性放置在语言项目上。 它将语言添加到"新建网站"对话框的" **语言"列表中的** Web **编程语言** 列表中。 例如，以下代码将 IronPython 添加到列表中：

```
[WebSiteProject("IronPython", "Iron Python")]
public class PythonProjectPackage : ProjectPackage
```

 此属性还将模板路径设置为指向 templates 文件夹。 有关 templates 文件夹的位置详细信息，请参阅 [网站支持模板](../../extensibility/internals/web-site-support-templates.md)。

## <a name="websiteprojectrelatedfilesattribute"></a>WebSiteProjectRelatedFilesAttribute
 此属性放置在语言项目上。 它允许网站项目将一个文件类型嵌套 (文件) 嵌套在 解决方案资源管理器 的主 () **下。**

 例如，以下代码指定 IronPython 代码后发文件与 .aspx 文件相关。 在 IronPython 网站解决方案中新建 .aspx 网页时，将生成新的 .py 源文件，并显示为 .aspx 页的子节点。

```
[WebSiteProjectRelatedFiles("aspx", "py")]
public class PythonProjectPackage : ProjectPackage
```

## <a name="provideintellisenseproviderattribute"></a>ProvideIntellisenseProviderAttribute
 此属性放置在语言项目包上。 它选择语言的 IntelliSense 提供程序。

 例如，以下代码指定应按需创建实现 的 PythonIntellisenseProvider 实例 <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject> 以提供语言服务。

```
[ProvideIntellisenseProvider(typeof(PythonIntellisenseProvider), "IronPythonCodeProvider", "Iron Python", ".py", "IronPython;Python", "IronPython")]
public class PythonPackage : Package, IOleComponent
```

 IVsIntellisenseProject 实现在请求包含代码的网页但不缓存时处理引用并调用语言编译器。

## <a name="see-also"></a>另请参阅
- [网站支持](../../extensibility/internals/web-site-support.md)
