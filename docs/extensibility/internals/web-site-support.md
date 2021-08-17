---
title: 网站支持|Microsoft Docs
description: 了解通过将模板和注册属性添加到现有项目系统而创建的网站项目系统。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web site projects
ms.assetid: ce9f4266-bb64-4c09-be88-4bd6413f60d0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 0cd561e9c1585380a4321801cf8bd21ff40e4d41
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122041901"
---
# <a name="web-site-support"></a>网站支持
网站项目系统是创建 Web 项目的项目系统。 Web 项目反过来会创建 Web 应用程序。 网站项目为具有关联代码的每个网页生成一个可执行文件。 其他可执行文件从 /App_Code 文件夹中的源代码文件生成。

 通过将模板和注册属性添加到现有项目系统，可创建网站项目系统。 其中一个属性为语言选择 IntelliSense 提供程序。 当请求未缓存的智能网页时，IntelliSense 提供程序实现将处理引用并调用语言编译器。

 用于编译网页的语言编译器必须注册到 [!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)] 。 可以使用 Web.config[ \<compiler> ](/dotnet/framework/configure-apps/file-schema/compiler/compiler-element)中的 元素注册编译器，如以下示例所示：

```
<system.codedom>  <compilers>    <compiler language="py;IronPython" extension=".py"       type="IronPython.CodeDom.PythonProvider, IronPython,       Version=1.0.2391.18146, Culture=neutral,       PublicKeyToken=b03f5f7f11d50a3a" />  </compilers></system.codedom>
```

## <a name="in-this-section"></a>本节内容
- [网站支持模板](../../extensibility/internals/web-site-support-templates.md)

 列出可用于创建新网站项目和关联项的模板。

- [网站支持属性](../../extensibility/internals/web-site-support-attributes.md)

 显示将网站项目连接到 和 的注册 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 属性 [!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)] 。

## <a name="related-sections"></a>相关章节
- [Web 项目](../../extensibility/internals/web-projects.md)

 概述了两种类型的 Web 项目：网站项目和 Web 应用程序项目。
