---
title: IWefDebuggingSupport 接口
description: 了解如何使用 Visual Studio 之类的调试环境，以便对 Microsoft Office 应用程序进行调试。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9fc319429414c8976d748a30ecdd1e164ce22b63
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99962257"
---
# <a name="iwefdebuggingsupport-interface"></a>IWefDebuggingSupport 接口
  由调试环境（如 Visual Studio）实现，以便为 Office 应用程序进行调试。 Office 应用程序（如 Word 或 Excel）从 Visual Studio 获取此接口，然后在调试会话过程中的特定点调用接口上的方法。

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

|“属性”|说明|
|----------|-----------------|
|[GetAutoInsertExtensions 方法](../vsto/getautoinsertextensions-method.md)|获取有关在调试过程中将自动插入的 Office 相关应用程序的信息。|
|[SetWefProcessId 方法](../vsto/setwefprocessid-method.md)|提供将 (WEF) 内容运行 Web 扩展框架的进程标识符。|
