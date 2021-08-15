---
title: IWefDebuggingSupport 接口
description: 了解如何使用调试环境（如 Visual Studio）来简化应用程序Microsoft Office调试。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 85cc94dcb95025eae5d7d19f152b1b78001b5f317177767d36a0fc116e27adf5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121440664"
---
# <a name="iwefdebuggingsupport-interface"></a>IWefDebuggingSupport 接口
  由调试环境（如 Visual Studio）实现，以便调试 Office。 应用程序Office Word 或 Excel 从 Visual Studio 获取此接口，然后在调试会话期间的某些点调用接口上的方法。

## <a name="syntax"></a>语法

```csharp
[
    uuid(ccaf1a90-ce1c-4199-9cd6-b40c5c57a671),
    oleautomation
]
interface IWefDebuggingSupport : IUnknown
{
    HRESULT SetWefProcessId(
        [in] DWORD dwProcessId);
    HRESULT GetAutoInsertExtensions(
        [out, retval] SAFEARRAY(BSTR)* psaExtensionNames);
}
```

## <a name="methods"></a>方法
 下表列出了 IWefDebuggingSupport 接口定义的方法。

|名称|说明|
|----------|-----------------|
|[GetAutoInsertExtensions 方法](../vsto/getautoinsertextensions-method.md)|获取有关在调试Office自动插入的应用的应用的信息。|
|[SetWefProcessId 方法](../vsto/setwefprocessid-method.md)|提供将运行 Web 扩展框架的进程标识符 (WEF) 内容。|
