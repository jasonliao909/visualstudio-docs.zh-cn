---
title: 源代码 &apos; 管理插件 API 1.3 中的新增功能
description: 了解源代码管理插件 API 版本 1.3 中的新增功能，该版本引入了新函数以提供更高级的控制。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, what's new in API v1.3
- what's new [Visual Studio SDK], source control plug-ins
ms.assetid: 7dfb2227-6e1d-4028-bce9-f8967456a993
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 5b7b200a45dd0fe87ff399917e196e00b3c365cdff854c5caa01ba22ab30672d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359112"
---
# <a name="what39s-new-in-the-source-control-plug-in-api-version-13"></a>源代码&#39;API 版本 1.3 中的新增功能
源代码管理插件 API 版本 1.3 引入了以下新函数，以提供更高级的控制。

## <a name="changes"></a>更改
 以下函数是源代码管理插件 API 版本 1.3 的新增功能：

|函数|概述|
|--------------|--------------|
|[SccGetExtendedCapabilities](../../extensibility/sccgetextendedcapabilities-function.md)|允许报告其他功能位|
|[SccEnumChangedFiles](../../extensibility/sccenumchangedfiles-function.md)|允许检查版本控制数据库中比本地磁盘上版本更新的文件|
|[SccQueryChanges](../../extensibility/sccquerychanges-function.md)|允许检查名称更改的状态 (重命名、添加和删除) 指定文件|
|[SccPopulateDirList](../../extensibility/sccpopulatedirlist-function.md)|允许检查版本控制数据库中的目录和文件|
|[SccAddFilesFromSCC](../../extensibility/sccaddfilesfromscc-function.md)|将指定文件列表从版本控制数据库添加到当前项目|
|[SccBackgroundGet](../../extensibility/sccbackgroundget-function.md)|对指定的文件执行无提示"get" (未显示用户界面) |
|[SccGetUserOption](../../extensibility/sccgetuseroption-function.md)|允许访问特定于用户的选项|

## <a name="see-also"></a>另请参阅
- [入门](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
- [源代码管理插件 API 版本 1.2 中的新增功能](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
