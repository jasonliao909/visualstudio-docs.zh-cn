---
title: 消息枚举器|Microsoft Docs
description: 此枚举器的成员用于 TEXTOUTPROC 函数，这是 IDE 在调用 SccOpenProject 时提供的回调函数。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- message enumerator
- source control plug-ins, message enumeration
ms.assetid: 4a4faa0d-d352-40ea-a21d-c09ea286a8e1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 4f0bcffa2f0d579d101c2ebcaed92e097c9443c8d4a54c50a6ff7ac798e30258
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414137"
---
# <a name="message-enumerator"></a>消息枚举器
以下标志用于 函数，该函数是 IDE 在调用 `TEXTOUTPROC` [SccOpenProject](../extensibility/sccopenproject-function.md) (时提供的回调函数 (请参阅 [LPTEXTOUTPROC，](../extensibility/lptextoutproc.md) 详细了解回调函数) 。

 如果要求 IDE 取消该进程，则可能会收到其中一条取消消息。 在这种情况下，源代码管理插件使用 来 `SCC_MSG_STARTCANCEL` 要求 IDE 显示"取消 **"** 按钮。 之后，可以发送任何一组正常消息。 如果其中任何一个返回 `SCC_MSG_RTN_CANCEL` ，插件将退出操作并返回 。 插件还会定期轮询 `SCC_MSG_DOCANCEL` 以确定用户是否取消了操作。 完成所有操作后，或者如果用户已取消，插件将发送 `SCC_MSG_STOPCANCEL` 。 `SCC_MSG_INFO`、SCC_MSG_WARNING 和 SCC_MSG_ERROR 类型用于消息滚动列表中显示的消息。 `SCC_MSG_STATUS` 是一种特殊类型，指示文本应显示在状态栏或临时显示区域中。 它不会永久保留在列表中。

## <a name="syntax"></a>语法

```
enum { 
   SCC_MSG_RTN_CANCEL = -1, 
   SCC_MSG_RTN_OK = 0, 
   SCC_MSG_INFO = 1 
   SCC_MSG_WARNING, 
   SCC_MSG_ERROR, 
   SCC_MSG_STATUS, 
   SCC_MSG_DOCANCEL, 
   SCC_MSG_STARTCANCEL, 
   SCC_MSG_STOPCANCEL 
};
```

## <a name="members"></a>成员
 SCC_MSG_RTN_CANCEL从回调返回以指示取消。

 SCC_MSG_RTN_OK从回调返回以继续。

 SCC_MSG_INFO消息是信息性的。

 SCC_MSG_WARNING消息是警告。

 SCC_MSG_ERROR消息是一个错误。

 SCC_MSG_STATUS消息适用于状态栏。

 SCC_MSG_DOCANCEL无文本;IDE 返回 `SCC_MSG_RTN_OK` 或 `SCC_MSG_RTN_CANCEL` 。

 SCC_MSG_STARTCANCEL启动取消循环。

 SCC_MSG_STOPCANCEL停止取消循环。

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
