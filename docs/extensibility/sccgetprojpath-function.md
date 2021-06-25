---
description: 此函数会提示用户输入项目路径，这是一个仅对源代码管理插件有意义的字符串。
title: SccGetProjPath 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGetProjPath
helpviewer_keywords:
- SccGetProjPath function
ms.assetid: 1079847e-d45f-4cb8-9d92-1e01ce5d08f6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 93266464249b8de037a618bab55ede31988384cb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901066"
---
# <a name="sccgetprojpath-function"></a>SccGetProjPath 函数
此函数会提示用户输入项目路径，这是一个仅对源代码管理插件有意义的字符串。 当用户为：

- 创建新项目

- 将现有项目添加到版本控制

- 尝试查找现有版本控制项目

## <a name="syntax"></a>语法

```cpp
SCCRTN SccGetProjPath (
   LPVOID pvContext,
   HWND   hWnd,
   LPSTR  lpUser,
   LPSTR  lpProjName,
   LPSTR  lpLocalPath,
   LPSTR  lpAuxProjPath,
   BOOL   bAllowChangePath,
   LPBOOL pbNew
);
```

### <a name="parameters"></a>参数
 pvContext

[in]源代码管理插件上下文结构。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 lpUser

[in， out]用户名不能 (，SCC_USER_SIZE NULL 终止符) 

 lpProjName

[in， out]IDE 项目、项目工作区或生成文件的名称 (不超过SCC_PRJPATH_SIZE，包括 NULL 终止符) 。

 lpLocalPath

[in， out]项目的工作路径。 如果 `bAllowChangePath` 为 ，则源代码管理插件可以修改此字符串 (不超过 `TRUE` _MAX_PATH，包括 null 终止符) 。

 lp一文ProjPath

[in， out]返回的项目路径的缓冲区 (不超过 SCC_PRJPATH_SIZE，包括 NULL 终止符) 。

 bAllowChangePath

[in]如果这是 `TRUE` ，则源代码管理插件可以提示输入和修改 `lpLocalPath` 字符串。

 pbNew

[in， out]值即将进入指示是否创建新项目。 返回的值指示成功创建项目：

|传入|解释|
|--------------|--------------------|
|TRUE|用户可以创建新项目。|
|FALSE|用户可能不会创建新项目。|

|传出|解释|
|--------------|--------------------|
|TRUE|创建了一个新项目。|
|FALSE|已选择现有项目。|

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|已成功创建或检索项目。|
|SCC_I_OPERATIONCANCELED|该操作已取消。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。|
|SCC_E_CONNECTIONFAILURE|尝试连接到源代码管理系统时出现问题。|
|SCC_E_NONSPECIFICERROR|发生了未指定的错误。|

## <a name="remarks"></a>备注
 此函数的用途是让 IDE 获取 参数 `lpProjName` 和 `lpAuxProjPath` 。 源代码管理插件提示用户输入此信息后，会将这两个字符串传递回 IDE。 每当用户打开此项目时，IDE 会将这些字符串保留在其解决方案文件中，并传递给[SccOpenProject。](../extensibility/sccopenproject-function.md) 这些字符串使插件能够跟踪与项目关联的信息。

 首次调用函数时， `lpAuxProjPath` 设置为空字符串。 `lProjName` 可能也为空，或者可能包含源代码管理插件可能使用或忽略的 IDE 项目名称。 当函数成功返回时，插件将返回两个相应的字符串。 IDE 不做出有关这些字符串的假设，不会使用它们，并且不允许用户修改它们。 如果用户想要更改设置，IDE 将再次调用 ，并传递前一次 `SccGetProjPath` 收到的相同值。 这使插件可以完全控制这两个字符串。

 对于 `lpUser` ，IDE 可以传递用户名，也可以只传递指向空字符串的指针。 如果有用户名，源代码管理插件应将其用作默认值。 但是，如果未传递任何名称，或者登录失败且具有给定名称，则插件应提示用户输入登录名，并接收有效登录名时重新传入 `lpUser` 该名称。 由于插件可能会更改此字符串，因此 IDE 将始终分配大小为 `SCC_USER_LEN` +1 (的缓冲区) 。

> [!NOTE]
> IDE 执行的第一个操作可能是调用 `SccOpenProject` 函数或 `SccGetProjPath` 函数。 因此，这两者具有相同的参数，这使源代码管理插件能够在任一时间 `lpUser` 将用户登录。 即使函数的返回指示失败，插件也必须用有效的登录名填充此字符串。

 `lpLocalPath` 是用户保留项目的目录。 它可能是一个空字符串。 如果当前没有定义目录 (如用户尝试从源代码管理系统) 下载项目的情况一样，并且如果 为 ，则源代码管理插件可以提示用户输入或使用某种其他方法将其字符串放入 `bAllowChangePath` `TRUE` `lpLocalPath` 。 如果 `bAllowChangePath` `FALSE` 为 ，插件不应更改字符串，因为用户已在指定的目录中工作。

 如果用户创建了一个要置于源代码管理下的新项目，则源代码管理插件在调用 时实际上可能不会在源代码管理系统 `SccGetProjPath` 中创建它。 相反，它会传递回字符串以及 的非零值，指示将在源代码管理系统 `pbNew` 中创建项目。

 例如，如果 Visual Studio 中"新建项目"向导中的用户将其项目添加到源代码管理，Visual Studio 将调用此函数，插件将确定在源代码管理系统中创建新项目是否可包含 Visual Studio 项目。 如果用户在完成向导 **之前** 单击"取消"，则永远不会创建项目。 如果用户单击 **"确定**"，Visual Studio调用 ，并传递 ，此时将创建源代码 `SccOpenProject` `SCC_OPT_CREATEIFNEW` 管理项目。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
