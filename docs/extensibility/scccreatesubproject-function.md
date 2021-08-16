---
description: 此函数在 lpParentProjPath 参数指定的现有父项目下创建具有给定名称的子项目。
title: SccCreateSubProject 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccCreateSubProject
helpviewer_keywords:
- SccCreateSubProject function
ms.assetid: 08154aed-ae5c-463c-8694-745d0e332965
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 4f108439082152627024666e0bcd3b751e1d88d221e308de6f50767ca1d5c49c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121305173"
---
# <a name="scccreatesubproject-function"></a>SccCreateSubProject 函数
此函数在参数指定的现有父项目下创建具有给定名称的子 `lpParentProjPath` 项目。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccCreateSubProject(
   LPVOID pContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPCSTR lpParentProjPath,
   LPCSTR lpSubProjName,
   LPSTR  lpAuxProjPath,
   LPSTR  lpSubProjPath
);
```

### <a name="parameters"></a>参数
 pContext

[in]源代码管理插件上下文指针。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 lpUser

[in， out]用户名 (，SCC_USER_SIZE NULL 终止符) 。

 lpParentProjPath

[in]一个字符串，用于标识父项目的路径 (，SCC_PRJPATH_SIZE NULL 终止符) 。

 lpSubProjName

[in]建议的子项目名称最多 (个SCC_PRJPATH_SIZE，包括 NULL 终止符) 。

 lp一文ProjPath

[in， out]辅助字符串，用于标识 (项目SCC_PRJPATH_SIZE，包括 NULL 终止符) 。

 lpSubProjPath

[in， out]输出字符串，用于标识子项目路径 (，SCC_PRJPATH_SIZE NULL 终止符) 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功创建子项目。|
|SCC_E_INITIALIZEFAILED|无法初始化父项目。|
|SCC_E_INVALIDUSER|用户无法登录到源代码管理系统。|
|SCC_E_COULDNOTCREATEPROJECT|无法创建子项目。|
|SCC_E_PROJSYNTAXERR|项目语法无效。|
|SCC_E_UNKNOWNPROJECT|源代码管理插件不知道父项目。|
|SCC_E_INVALIDFILEPATH|文件路径无效或不可用。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。 建议重试。|
|SCC_E_CONNECTIONFAILURE|存在源代码管理插件连接问题。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 如果已存在名称为 的子项目，则函数可以更改默认名称以创建唯一名称，例如，通过向它添加"_ \<number> "。 调用方必须准备好接受对 `lpUser` 、 和 `lpSubProjPath` 的更改 `lpAuxProjPath` 。 然后 `lpSubProjPath` `lpAuxProjPath` ，在调用 [SccOpenProject 时](../extensibility/sccopenproject-function.md)，使用 和 参数。 调用方不应在返回时修改它们。 这些字符串为源代码管理插件提供了一种跟踪与项目关联的信息的方法。 调用方 IDE 在返回时不会显示这两个参数，因为插件可以使用可能不适合查看的格式化字符串。 函数返回成功或失败代码，如果成功，则使用新项目的完整 `lpSubProjPath` 项目路径填充变量。

 此函数类似于 [SccGetProjPath，](../extensibility/sccgetprojpath-function.md)只不过它会以无提示方式创建项目，而不是提示用户选择一个项目。 调用 `SccCreateSubProject` 函数时， `lpParentProjName` `lpAuxProjPath` 和 将不为空，并且 将对应于有效的项目。 这些字符串通常由 IDE 从之前对函数的调用或 `SccGetProjPath` [SccGetParentProjectPath 接收](../extensibility/sccgetparentprojectpath-function.md)。

 `lpUser`参数是用户名。 IDE 将传递以前从 接收的同一用户名，源代码管理插件应 `SccGetProjPath` 使用该名称作为默认值。 如果用户已与插件建立打开的连接，则插件应尝试消除任何提示，以确保函数以静默方式工作。 但是，如果登录失败，插件应提示用户输入登录名，并且收到有效登录名时，将名称传回 `lpUser` 。 由于插件可能会更改此字符串，因此 IDE 将始终分配大小为 (SCC_USER_LEN+1 或 SCC_USER_SIZE 的缓冲区，其中包括 null 终止符) 。 如果更改了字符串，则新字符串必须是有效的登录名 (与旧字符串一样) 。

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>SccCreateSubProject 和 SccGetParentProjectPath 的技术说明
 在源代码管理中添加解决方案和项目的过程已简化Visual Studio以最大程度地减少提示用户在源代码管理系统中选择位置的时间。 如果源代码管理插件同时Visual Studio 和 这两个新函数，则这些更改由用户 `SccCreateSubProject` 激活 `SccGetParentProjectPath` 。 但是，以下注册表项可用于禁用这些更改并还原到以前的Visual Studio (源代码管理插件 API 版本 1.1) 行为：

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl]"DoNotCreateSolutionRootFolderInSourceControl"=dword：00000001**

 如果此注册表项不存在或设置为 dword：000000000，Visual Studio尝试使用新函数 `SccCreateSubProject` 和 `SccGetParentProjectPath` 。

 如果注册表项设置为 dword：00000001，Visual Studio 不会尝试使用这些新函数，并且添加到源代码管理的操作会像在早期版本的 Visual Studio 中一样工作。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
