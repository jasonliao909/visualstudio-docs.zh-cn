---
title: 消除 ~SAK 文件|Microsoft Docs
description: 了解如何从源代码管理插件 API 1.2 中消除 ~SAK 文件，以及如何将其替换为功能标志和新函数。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- temporary files
- ~sak files
- source control plug-ins, ~SAK files
ms.assetid: 5277b5fa-073b-4bd1-8ba1-9dc913aa3c50
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 02dfc179add2d138df5b8ab876329da2fc1f0f1d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664383"
---
# <a name="elimination-of-sak-files"></a>消除 ~SAK 文件
在源代码管理插件 API 1.2 中 *，~SAK* 文件已替换为功能标志和用于检测源代码管理插件是否支持 *MSSCCPRJ* 文件和共享签出的新函数。

## <a name="sak-files"></a>~SAK 文件
Visual Studio .NET 2003 创建了前缀为 *~SAK 的临时文件*。 这些文件用于确定源代码管理插件是否支持：

- *MSSCCPRJ.SCC* 文件。

- 多个 (共享) 结帐。

对于支持源代码管理插件 API 1.2 中提供的高级功能的插件，IDE 可以通过使用新功能、标志和函数来检测这些功能，而无需创建临时文件，如以下部分所述。

## <a name="new-capability-flags"></a>新功能标志
 `SCC_CAP_SCCFILE`

 `SCC_CAP_MULTICHECKOUT`

## <a name="new-functions"></a>新函数
- [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)

- [SccIsMultiCheckoutEnabled](../../extensibility/sccismulticheckoutenabled-function.md)

 如果源代码管理插件支持多个 (共享) 签出，则它会声明功能 `SCC_CAP_MULTICHECKOUT` 并实现 `SccIsMultiCheckOutEnabled` 函数。 只要在任何源代码管理的项目上执行签出操作，就会调用此函数。

 如果源代码管理插件支持创建和使用 *MSSCCPRJ.SCC* 文件，则它会声明该功能并 `SCC_CAP_SCCFILE` 实现 [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)。 使用文件列表调用此函数。 函数返回每个文件，以指示Visual Studio `TRUE' or 'FALSE` *MSSCCPRJ.SCC* 文件。 如果源代码管理插件选择不支持这些新功能和函数，它可以使用以下注册表项来禁用这些文件的创建：

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl]DoNotCreateTemporaryFilesInSourceControl**  =  *dword：00000001*

> [!NOTE]
> 如果此注册表项设置为 *dword：00000000，* 则它等效于不存在的密钥，Visual Studio仍尝试创建临时文件。 但是，如果注册表项设置为 *dword：00000001*，Visual Studio不会尝试创建临时文件。 相反，它假定源代码管理插件不支持 *MSSCCPRJ.SCC* 文件，并且不支持共享签出。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
