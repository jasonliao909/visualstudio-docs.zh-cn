---
description: 此函数将打开现有源代码管理项目或创建一个新的源代码管理项目。
title: SccOpenProject 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccOpenProject
helpviewer_keywords:
- SccOpenProject function
ms.assetid: d609510b-660a-46d7-b93d-2406df20434d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 8fcd8ba5b7c3fc1759432d0b33d7b49aa3a257cd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110041"
---
# <a name="sccopenproject-function"></a>SccOpenProject 函数
此函数将打开现有源代码管理项目或创建一个新的源代码管理项目。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccOpenProject (
   LPVOID        pvContext,
   HWND          hWnd,
   LPSTR         lpUser,
   LPCSTR        lpProjName,
   LPCSTR        lpLocalProjPath,
   LPSTR         lpAuxProjPath,
   LPCSTR        lpComment,
   LPTEXTOUTPROC lpTextOutProc,
   LONG          dwFlags
);
```

#### <a name="parameters"></a>参数
 pvContext

[in]源代码管理插件上下文结构。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 lpUser

[in， out]用户名不能超过 (，SCC_USER_SIZE NULL 终止符) 。

 lpProjName

[in]标识项目名称的字符串。

 lpLocalProjPath

[in]项目的工作文件夹的路径。

 lp一文ProjPath

[in， out]一个可选的辅助字符串，用于标识 (不超过SCC_AUXPATH_SIZE，包括 NULL 终止符) 。

 lpComment

[in]对正在创建的新项目进行注释。

 lpTextOutProc

[in]一个可选的回调函数，用于显示来自源代码管理插件的文本输出。

 dwFlags 

[in]指示在源代码管理插件未知时是否需要创建新项目。 值可以是 和 `SCC_OP_CREATEIFNEW` 的组合 `SCC_OP_SILENTOPEN.`

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|成功打开项目。|
|SCC_E_INITIALIZEFAILED|Project无法初始化。|
|SCC_E_INVALIDUSER|用户无法登录到源代码管理系统。|
|SCC_E_COULDNOTCREATEPROJECT|调用之前项目不存在; `SCC_OPT_CREATEIFNEW` 已设置 标志，但无法创建项目。|
|SCC_E_PROJSYNTAXERR|项目语法无效。|
|SCC_E_UNKNOWNPROJECT|源代码管理插件不知道该项目，并且 `SCC_OPT_CREATEIFNEW` 未设置 标志。|
|SCC_E_INVALIDFILEPATH|文件路径无效或不可用。|
|SCC_E_NOTAUTHORIZED|不允许用户执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。 建议重试。|
|SCC_E_NONSPECFICERROR|非特定故障;未初始化源代码管理系统。|

## <a name="remarks"></a>备注
 IDE 可能会将用户名 () ，也可以直接将指针传递到 `lpUser` 空字符串。 如果存在用户名，源代码管理插件应将其用作默认值。 但是，如果未传递任何名称，或者登录失败且具有给定名称，则插件应提示用户登录，并将在收到有效登录名时返回 中的有效名称。因为插件可能会更改用户名字符串，IDE 将始终分配大小 `lpUser` `.` 为 (+1 或 SCC_USER_SIZE 的缓冲区，其中包括 null 终止符 `SCC_USER_LEN`) 的空间。

> [!NOTE]
> 可能需要 IDE 执行的第一个操作可能是调用 函数 `SccOpenProject` 或 [SccGetProjPath](../extensibility/sccgetprojpath-function.md)。 因此，两者具有相同的 `lpUser` 参数。

 `lpAuxProjPath``lpProjName`和 从解决方案文件中读取，或者从对 函数的调用返回 `SccGetProjPath` 。 这些参数包含源代码管理插件与项目关联且仅对插件有意义的字符串。 如果解决方案文件中没有此类字符串，并且未提示用户浏览 (这会通过函数) 返回字符串，则 IDE 会为 和 传递空字符串，并期望此函数返回时插件更新 `SccGetProjPath` `lpAuxProjPath` `lpProjName` 这些值。

 `lpTextOutProc` 是指向 IDE 提供的回调函数的指针，该回调函数指向用于显示命令结果输出的源代码管理插件。 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)中详细介绍了此回调函数。

> [!NOTE]
> 如果源代码管理插件打算利用此功能，它必须在 `SCC_CAP_TEXTOUT` [SccInitialize 中设置 标志](../extensibility/sccinitialize-function.md)。 如果未设置该标志，或者 IDE 不支持此功能， `lpTextOutProc` 则 将为 `NULL` 。

 `dwFlags`参数控制正在打开的项目当前不存在时的结果。 它由两个位标志 和 `SCC_OP_CREATEIFNEW` 组成 `SCC_OP_SILENTOPEN` 。 如果打开的项目已存在，则函数只需打开项目并返回 `SCC_OK` 。 如果项目不存在，并且标志为 on，则源代码管理插件可以在源代码管理系统中创建项目，将其打开并 `SCC_OP_CREATEIFNEW` 返回 `SCC_OK` 。 如果项目不存在，并且标志关闭，插件应检查 `SCC_OP_CREATEIFNEW` 标志 `SCC_OP_SILENTOPEN` 。 如果该标志未打开，插件可能会提示用户输入项目名称。 如果该标志为 on，插件应只返回 `SCC_E_UNKNOWNPROJECT` 。

## <a name="calling-order"></a>调用顺序
 在正常事件过程中，将首先调用 [SccInitialize](../extensibility/sccinitialize-function.md) 以打开源代码管理会话。 会话可能包含对 的调用，后跟其他源代码管理插件 API 函数调用，并且将终止对 `SccOpenProject` [SccCloseProject 的调用](../extensibility/scccloseproject-function.md)。 在调用 [SccUninitialize](../extensibility/sccuninitialize-function.md) 之前，可以多次重复此类会话。

 如果源代码管理插件在 中设置 `SCC_CAP_REENTRANT` 位，则 `SccInitialize` 上述会话序列可能会并行重复多次。 `pvContext`不同的结构跟踪不同的会话，其中每个会话一次与 `pvContext` 一个打开的项目相关联。 根据 参数，插件可以确定在任何特定调用 `pvContext` 中引用的项目。 如果未设置功能位，则不可访问的源代码管理插件处理多个 `SCC_CAP_REENTRANT` 项目的能力受到限制。

> [!NOTE]
> 该 `SCC_CAP_REENTRANT` 位是在源代码管理插件 API 版本 1.1 中引入的。 它在版本 1.0 中未设置或被忽略，并且所有版本 1.0 源代码管理插件都假定为不可访问。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccCloseProject](../extensibility/scccloseproject-function.md)
- [SccGetProjPath](../extensibility/sccgetprojpath-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccUninitialize](../extensibility/sccuninitialize-function.md)
- [字符串长度限制](../extensibility/restrictions-on-string-lengths.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
