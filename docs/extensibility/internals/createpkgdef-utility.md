---
title: CreatePkgDef 实用工具|Microsoft Docs
description: 了解 CreatePkgDef 实用工具，该实用工具将 .dll 扩展名的 Visual Studio .dll 文件作为参数，并创建一个 .pkgdef 文件作为 .dll 文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- package definition
- create pkgdef
- pkgdef
- createpkgdef
ms.assetid: c745cb76-47a6-49ff-9eed-16af0f748e35
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 17e561a155e13b7857573894041e79e4d6ca90c1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122086750"
---
# <a name="createpkgdef-utility"></a>CreatePkgDef 实用工具
将.dll扩展插件的 Visual Studio 文件作为参数，并创建一个 *.pkgdef* 文件以 *.dll* 文件。 *.pkgdef* 文件包含安装扩展时将写入系统注册表的所有信息。

> [!NOTE]
> 在生成过程中，Visual Studio SDK 中包含的大多数项目模板会自动创建 *.pkgdef* 文件。 本文档适用于想要手动创建包或转换现有包以使用 *.pkgdef 部署*  的人。

## <a name="syntax"></a>语法

```
CreatePkgDef /out=<FileName> [/codebase] [/assembly] <AssemblyPath>
```

## <a name="arguments"></a>参数
**/out= &lt; FileName&gt;**\
必需。 将 *.pkgdef 输出* 文件的名称设置为 &lt; FileName &gt; 。

**/codebase**\
可选。 强制注册 **CodeBase** 实用工具。

**/assembly**\
强制注册 **程序集** 实用工具。

**&lt;AssemblyPath&gt;**\
要从 *.dll* *.pkgdef* 的文件的路径。

## <a name="remarks"></a>备注
使用 *.pkgdef* 文件的扩展部署取代了早期版本的 Visual Studio。

::: moniker range=">=vs-2019"

*.pkgdef* 文件必须安装在以下位置之一：

- *%localappdata%\Microsoft\Visual Studio\16.0\Extensions\\*

- *%vsinstalldir%\Common7\IDE\Extensions\\*

如果安装文件夹为 *%localappdata%\Microsoft\Visual Studio\16.0\Extensions， \\* 则扩展被 Visual Studio 识别，但默认处于禁用状态。 用户可以使用"管理扩展"来 **启用扩展**。

如果安装文件夹为 *%vsinstalldir%\Common7\IDE\Extensions， \\* 则默认启用扩展。

> [!NOTE]
> 除非 **将扩展** 作为 VSIX 包的一部分进行安装，否则不能使用管理扩展工具来访问扩展。

::: moniker-end

::: moniker range="vs-2017"

*.pkgdef* 文件必须安装在以下位置之一：

- *%localappdata%\Microsoft\Visual Studio\15.0\Extensions\\*

- *%vsinstalldir%\Common7\IDE\Extensions\\*

如果安装文件夹为 *%localappdata%\Microsoft\Visual Studio\15.0\Extensions， \\* 则扩展被 Visual Studio 识别，但默认处于禁用状态。 用户可以使用"扩展和更新"来 **启用扩展**。

如果安装文件夹为 *%vsinstalldir%\Common7\IDE\Extensions， \\* 则默认启用扩展。

> [!NOTE]
> 扩展 **和更新工具** 不能用于访问扩展，除非它是作为 VSIX 包的一部分安装的。

::: moniker-end

## <a name="see-also"></a>请参阅
- [CreateExpInstance 实用工具](../../extensibility/internals/createexpinstance-utility.md)
