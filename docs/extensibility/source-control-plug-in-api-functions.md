---
title: 源代码管理插件 API 函数|Microsoft Docs
description: 了解源代码管理插件 API 提供的函数，这些函数必须由源代码管理插件实现。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- source control plug-ins, functions
ms.assetid: 4b0536dd-4f92-4ef2-9031-4548281f37aa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 369acd0f0b459aa4d5e5691c0159087c0bdf152edeb5388d3f62d3978f58ac30
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121431456"
---
# <a name="source-control-plug-in-api-functions"></a>源代码管理插件 API 函数
源代码管理插件 API 提供以下函数，这些函数必须由源代码管理插件根据此 API 实现。 本参考中详细介绍了每个函数的签名以及与位标志和其他参数关联的语义。

## <a name="initialization-and-housekeeping-functions"></a>初始化和清理函数

|函数|说明|
|--------------|-----------------|
|[SccCloseProject](../extensibility/scccloseproject-function.md)|关闭项目。|
|[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)|提示用户输入给定命令的高级选项。|
|[SccGetVersion](../extensibility/sccgetversion-function.md)|返回源代码管理插件的版本。|
|[SccInitialize](../extensibility/sccinitialize-function.md)|初始化源代码管理插件。 它针对插件的每个实例调用一次。|
|[SccOpenProject](../extensibility/sccopenproject-function.md)|打开项目。|
|[SccSetOption](../extensibility/sccsetoption-function.md)|用于设置各种选项的泛型函数。 每个选项以 开头 `SCC_OPT_xxx` ，并有自己的定义值集。|
|[SccUninitialize](../extensibility/sccuninitialize-function.md)|在需要拔下源代码管理插件时调用一次。|

## <a name="core-source-control-functions"></a>核心源代码管理功能

|函数|说明|
|--------------|-----------------|
|[SccAdd](../extensibility/sccadd-function.md)|将完全限定的路径名称指定的文件数组添加到源代码管理系统。|
|[SccAddFromScc](../extensibility/sccaddfromscc-function.md)|允许用户浏览源代码管理系统中已有的文件，然后将这些文件作为当前项目的一部分。|
|[SccCheckin](../extensibility/scccheckin-function.md)|检查文件数组。|
|[SccCheckout](../extensibility/scccheckout-function.md)|签出文件数组。|
|[SccDiff](../extensibility/sccdiff-function.md)|显示由完全限定的路径名称指定的本地用户文件与源代码管理下的版本之间的差异。|
|[SccGet](../extensibility/sccget-function.md)|检索一组文件的只读副本。|
|[SccGetEvents](../extensibility/sccgetevents-function.md)|检查调用方通过查询请求 (文件 `SccQueryInfo`) 。|
|[SccGetProjPath](../extensibility/sccgetprojpath-function.md)|使源代码管理插件提示用户输入对插件有意义的项目路径。|
|[SccHistory](../extensibility/scchistory-function.md)|显示完全限定的本地文件名数组的历史记录。|
|[SccPopulateList](../extensibility/sccpopulatelist-function.md)|检查文件列表，了解其当前状态。 此外， 使用 `pfnPopulate` 函数在文件与 的条件不匹配时通知调用方 `nCommand` 。|
|[SccProperties](../extensibility/sccproperties-function.md)|显示完全限定文件的属性。|
|[SccQueryInfo](../extensibility/sccqueryinfo-function.md)|检查完全限定文件的列表，了解其当前状态。|
|[SccRemove](../extensibility/sccremove-function.md)|从源代码管理系统中删除完全限定文件的数组。|
|[SccRename](../extensibility/sccrename-function.md)|将给定文件重命名为源代码管理系统中的新名称。|
|[SccRunScc](../extensibility/sccrunscc-function.md)|访问源代码管理系统的全部功能。|
|[SccUncheckout](../extensibility/sccuncheckout-function.md)|撤消签出文件数组。|

## <a name="functions-that-support-additional-capability-version-12-of-the-source-control-plug-in-api"></a>支持源代码管理插件 API (版本 1.2 的其他功能的函数) 
 这组函数定义了源代码管理插件 API 版本 1.2 中包含的附加功能。 它们提供对更高级源代码管理特性和功能的访问权限。

|函数|说明|
|--------------|-----------------|
|[SccBeginBatch](../extensibility/sccbeginbatch-function.md)|启动批处理操作。|
|[SccCreateSubProject](../extensibility/scccreatesubproject-function.md)|在现有的父项目下创建具有给定名称的子项目。|
|[SccDirDiff](../extensibility/sccdirdiff-function.md)|显示由完全限定的路径名称指定的本地用户的目录与源代码管理数据库位置之间的差异。|
|[SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)|检查完全限定目录的列表，了解其当前状态。|
|[SccEndBatch](../extensibility/sccendbatch-function.md)|结束批处理操作。|
|[SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)|返回给定项目的父路径 (项目必须存在于) 。|
|[SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md)|检查是否允许对文件进行多次签出。|
|[SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md)|检查插件是否将创建 MSSCCPRJ。SCC 文件。|

## <a name="functions-that-support-advanced-capability-version-13-of-the-source-control-plug-in-api"></a>支持源代码管理插件 API (版本 1.3 的高级功能的函数) 
 这组函数定义了源代码管理插件 API 版本 1.3 中包含的附加功能。 它们提供对更高级源代码管理特性和功能的访问权限。

|函数|说明|
|--------------|-----------------|
|[SccAddFilesFromSCC](../extensibility/sccaddfilesfromscc-function.md)|将文件列表从源代码管理添加到当前项目。|
|[SccBackgroundGet](../extensibility/sccbackgroundget-function.md)|从没有用户界面的源代码管理中检索文件列表。|
|[SccEnumChangedFiles](../extensibility/sccenumchangedfiles-function.md)|检索源代码管理中与本地文件不同的文件列表。|
|[SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md)|检索指定源代码管理插件支持的扩展功能的标志。|
|[SccGetUserOption](../extensibility/sccgetuseroption-function.md)|检索特定于用户的选项。|
|[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)|检查受源代码管理的项目或项目中的目录和文件列表。 找到的每个目录和文件名都传递给回调函数。|
|[SccQueryChanges](../extensibility/sccquerychanges-function.md)|检查对文件列表进行的名称更改。 每个文件名都传递给具有其更改状态的回调函数。|

## <a name="requirements"></a>要求
 标头：scc.h

  (环境 SDK common includes 文件夹中提供，默认 *为 [drive]* \Program Files\VSIP 8.0\EnvSDK\common\inc;还在 VSIP 文件夹中提供 MSSCCI 示例 *[drive]* \Program Files\VSIP 8.0\MSSCCI) 。

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md)
