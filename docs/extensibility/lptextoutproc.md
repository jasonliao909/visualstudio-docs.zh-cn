---
title: LPTEXTOUTPROC |Microsoft Docs
description: 了解 LPTEXTOUTPROC 函数指针。 IDE Visual Studio IDE 实现 用于显示错误和状态的 函数。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- LPTEXTOUTPROC
helpviewer_keywords:
- SccMsgDataOnMessage structure
- SccMsgDataOnBeforeGetFile structure
- SccMsgDataIsCancelled structure
- LPTEXTOUTPROC callback function
- SccMsgDataOnAfterGetFile structure
ms.assetid: 2025c969-e3c7-4cf4-a5c5-099d342895ea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b266ea06ce79d0028e289210c7bfc11c62ea5ccde0f5050e246b38a4f06f5b16
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121321189"
---
# <a name="lptextoutproc"></a>LPTEXTOUTPROC

当用户从集成开发环境 (IDE) 内部执行源代码管理操作时，源代码管理插件可能希望传达与操作相关的错误或状态消息。 插件可以出于此目的显示自己的消息框。 但是，为了进行更无缝的集成，插件可以将字符串传递给 IDE，然后 IDE 以本机方式显示状态信息。 此的机制是 `LPTEXTOUTPROC` 函数指针。 IDE 实现此函数 (下面详细介绍) 显示错误和状态。

调用 `lpTextOutProc` [SccOpenProject](../extensibility/sccopenproject-function.md)时，IDE 会将指向此函数的函数指针作为 参数传递给源代码管理插件。 例如，在 SCC 操作期间，在调用涉及多个文件的 [SccGet](../extensibility/sccget-function.md) 期间，插件可以调用 函数，并定期传递要显示的 `LPTEXTOUTPROC` 字符串。 IDE 可能会视情况在状态栏、输出窗口或单独的消息框中显示这些字符串。 （可选）IDE 可能能够显示具有"取消"按钮 **的某些** 消息。 这使用户可以取消操作，并且 IDE 能够将此信息传递回插件。

## <a name="signature"></a>签名
 IDE 的输出函数具有以下签名：

```cpp
typedef LONG (*LPTEXTOUTPROC) (
   LPSTR display_string,
   LONG mesg_type
);
```

## <a name="parameters"></a>参数

display_string

要显示的文本字符串。 不应使用回车符或换行符终止此字符串。

mesg_type

消息的类型。 下表列出了此参数支持的值。

|值|说明|
|-----------|-----------------|
|`SCC_MSG_INFO, SCC_MSG_WARNING, SCC_MSG_ERROR`|该消息被视为"信息"、警告或"错误"。|
|`SCC_MSG_STATUS`|该消息显示状态，可以显示在状态栏中。|
|`SCC_MSG_DOCANCEL`|发送时没有消息字符串。|
|`SCC_MSG_STARTCANCEL`|开始显示"取消 **"** 按钮。|
|`SCC_MSG_STOPCANCEL`|停止显示"取消 **"** 按钮。|
|`SCC_MSG_BACKGROUND_IS_CANCELLED`|询问 IDE 是否取消后台操作：如果取消操作，IDE 返回 `SCC_MSG_RTN_CANCEL` ;否则返回 `SCC_MSG_RTN_OK` 。 `display_string`参数被强制转换为[SccMsgDataIsCancelled](#LinkSccMsgDataIsCancelled)结构，该结构由源代码管理插件提供。|
|`SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE`|在从版本控制中检索文件之前，告知 IDE 有关该文件的信息。 `display_string`参数被强制转换为[SccMsgDataOnBeforeGetFile](#LinkSccMsgDataOnBeforeGetFile)结构，该结构由源代码管理插件提供。|
|`SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE`|从版本控制中检索文件后，告知 IDE 有关该文件的信息。 参数 `display_string` 被强制转换为 [SccMsgDataOnAfterGetFile](#LinkSccMsgDataOnAfterGetFile) 结构，该结构由源代码管理插件提供。|
|`SCC_MSG_BACKGROUND_ON_MESSAGE`|告知 IDE 后台操作的当前状态。 `display_string`参数被强制转换为[SccMsgDataOnMessage](#LinkSccMsgDataOnMessage)结构，该结构由源代码管理插件提供。|

## <a name="return-value"></a>返回值

|值|说明|
|-----------|-----------------|
|SCC_MSG_RTN_OK|字符串已显示或操作已成功完成。|
|SCC_MSG_RTN_CANCEL|用户想要取消操作。|

## <a name="example"></a>示例
 假设 IDE 使用 20 个文件名调用[SccGet。](../extensibility/sccget-function.md) 源代码管理插件希望防止在文件获取过程中取消操作。 获取每个文件后，它会调用 ，将每个文件的状态信息传递给该文件，并发送一条消息（如果该文件没有 `lpTextOutProc` `SCC_MSG_DOCANCEL` 报告状态）。 如果插件随时从 IDE 收到返回值 ，它会立即取消获取操作，以便 `SCC_MSG_RTN_CANCEL` 不再检索文件。

## <a name="structures"></a>结构

### <a name="sccmsgdataiscancelled"></a><a name="LinkSccMsgDataIsCancelled"></a> SccMsgDataIsCancelled

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
} SccMsgDataIsCancelled;
```

 此结构随消息一 `SCC_MSG_BACKGROUND_IS_CANCELLED` 起发送。 它用于传达已取消的后台操作 ID。

### <a name="sccmsgdataonbeforegetfile"></a><a name="LinkSccMsgDataOnBeforeGetFile"></a> SccMsgDataOnBeforeGetFile

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
} SccMsgDataOnBeforeGetFile;
```

 此结构随消息一 `SCC_MSG_BACKGROUND_ON_BEFORE_GET_FILE` 起发送。 它用于传达要检索的文件的名称以及执行检索的后台操作 ID。

### <a name="sccmsgdataonaftergetfile"></a><a name="LinkSccMsgDataOnAfterGetFile"></a> SccMsgDataOnAfterGetFile

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szFile;
   SCCRTN sResult;
} SccMsgDataOnAfterGetFile;
```

 此结构随消息一 `SCC_MSG_BACKGROUND_ON_AFTER_GET_FILE` 起发送。 它用于传达检索指定文件的结果，以及执行检索的后台操作 ID。 有关可给出的结果，请参阅 [SccGet](../extensibility/sccget-function.md) 的返回值。

### <a name="sccmsgdataonmessage"></a><a name="LinkSccMsgDataOnMessage"></a> SccMsgDataOnMessage

```cpp
typedef struct {
   DWORD dwBackgroundOperationID;
   PCSTR szMessage;
   BOOL bIsError;
} SccMsgDataOnMessage;
```

 此结构随消息一 `SCC_MSG_BACKGROUND_ON_MESSAGE` 起发送。 它用于传达后台操作的当前状态。 状态表示为 IDE 要显示的字符串，并指示错误消息消息 (警告或信息性消息的严重性 `bIsError` `TRUE` `FALSE`) 。 还会提供发送状态的后台操作 ID。

## <a name="code-example"></a>代码示例
 下面是调用 以发送消息的简短示例，演示了如何 `LPTEXTOUTPROC` `SCC_MSG_BACKGROUND_ON_MESSAGE` 强制转换调用的结构。

```cpp
LONG SendStatusMessage(
    LPTEXTOUTPROC pTextOutProc,
    DWORD         dwBackgroundID,
    LPCTSTR       pStatusMsg,
    BOOL          bIsError)
{
    SccMsgDataOnMessage msgData = { 0 };
    LONG                result  = 0;

    msgData.dwBackgroundOperationID = dwBackgroundID;
    msgData.szMessage               = pStatusMsg;
    msgData.bIsError                = bIsError;

    result = pTextOutProc(reinterpret_cast<LPCTSTR>(&msgData), SCC_MSG_BACKGROUND_ON_MESSAGE);
    return result;
}
```

## <a name="see-also"></a>另请参阅
- [由 IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
