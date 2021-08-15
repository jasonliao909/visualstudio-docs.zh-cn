---
description: 此函数确定指定项目的父项目路径。
title: SccGetParentProjectPath 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGetParentProjectPath
helpviewer_keywords:
- SccGetParentProjectPath function
ms.assetid: 62a71579-36b3-48b9-a1c8-04ab100efa08
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 20479eec7cce78996c70a98045747dd5132112fe3f81ec72ffefca3e118e9aa9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121321030"
---
# <a name="sccgetparentprojectpath-function"></a>SccGetParentProjectPath 函数
此函数确定指定项目的父项目路径。 当用户将项目添加到源代码管理Visual Studio调用此函数。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccGetParentProjectPath(
   LPVOID pContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPCSTR lpProjPath,
   LPSTR  lpAuxProjPath,
   LPSTR  lpParentProjPath
);
```

### <a name="parameters"></a>参数
 pContext

[in]源代码管理插件上下文指针。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 lpUser

[in， out]用户名最多 (，SCC_USER_SIZE NULL 终止符) 。

 lpProjPath

[in]标识项目路径的 (，SCC_PRJPATH_SIZE NULL 终止符) 。

 lp一文ProjPath

[in， out]辅助字符串，用于标识 (项目SCC_PRJPATH_SIZE，包括 NULL 终止符) 。

 lpParentProjPath

[in， out]输出字符串，用于标识父项目 (路径，SCC_PRJPATH_SIZE NULL 终止符) 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|已成功获取父项目路径。|
|SCC_E_INITIALIZEFAILED|Project无法初始化。|
|SCC_E_INVALIDUSER|用户无法登录到源代码管理插件。|
|SCC_E_UNKNOWNPROJECT|Project源代码管理插件未知。|
|SCC_E_INVALIDFILEPATH|文件路径无效或不可用。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。 建议重试。|
|SCC_E_PROJSYNTAXERR|项目语法无效。|
|SCC_E_CONNECTIONFAILURE|存储连接问题。|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|非特定故障。|

## <a name="remarks"></a>备注
 此函数返回成功或失败代码，如果成功，则使用指定项目的完整 `lpParentProjPath` 项目路径填充变量。

 此函数返回现有项目的父项目路径。 对于根项目，该函数返回传入项目 (，即同一根项目路径) 。 请注意，项目路径是仅对源代码管理插件有意义的字符串。

 IDE 已准备好接受对 和 `lpUser` `lpAuxProjPath` 参数的更改。 当用户将来打开此项目时，IDE 将保留这些字符串，并传递给[SccOpenProject。](../extensibility/sccopenproject-function.md) 因此，这些字符串为源代码管理插件提供了一种跟踪与项目关联的信息的方法。

 此函数类似于 [SccGetProjPath，](../extensibility/sccgetprojpath-function.md)只不过它不会提示用户选择项目。 它从不创建新项目，但仅适用于现有项目。

 调用 `SccGetParentProjectPath` 时， `lpProjPath` 和 `lpAuxProjPath` 将不为空，并且 将对应于有效的项目。 这些字符串通常由 IDE 从对函数的上一次调用 `SccGetProjPath` 接收。

 `lpUser`参数是用户名。 IDE 将传递以前从函数接收的同一用户名，源代码管理插件应 `SccGetProjPath` 使用该名称作为默认值。 如果用户已与插件建立打开的连接，则插件应尝试消除任何提示，以确保函数以静默方式工作。 但是，如果登录失败，插件应提示用户输入登录名，并且收到有效登录名时，将名称传回 `lpUser` 。 由于插件可能会更改此字符串，因此 IDE 将始终分配大小为 `SCC_USER_LEN` (+1) 。 如果更改了字符串，则新字符串必须是有效的登录名 (与旧字符串一样) 。

## <a name="technical-notes-for-scccreatesubproject-and-sccgetparentprojectpath"></a>SccCreateSubProject 和 SccGetParentProjectPath 的技术说明
 在源代码管理中添加解决方案和项目的过程已简化Visual Studio以最大程度地减少提示用户在源代码管理系统中选择位置的时间。 如果源代码管理插件Visual Studio [SccCreateSubProject](../extensibility/scccreatesubproject-function.md)和 函数这两个新函数，则这些更改由用户 `SccGetParentProjectPath` 激活。 但是，以下注册表项可用于禁用这些更改，并还原到上一Visual Studio (源代码管理插件 API 版本 1.1) 行为：

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl]"DoNotCreateSolutionRootFolderInSourceControl"=dword：00000001**

 如果此注册表项不存在或设置为 dword：000000000，Visual Studio尝试使用新函数 `SccCreateSubProject` 和 `SccGetParentProjectPath` 。

 如果注册表项设置为 dword：00000001，Visual Studio 不会尝试使用这些新函数，并且添加到源代码管理的操作会像在早期版本的 Visual Studio 中一样工作。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccCreateSubProject](../extensibility/scccreatesubproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
