---
title: 调试 Web 服务时超时 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
- XML Web services, timeout while debugging
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 87a2d79fc24bdb433fbb5eb1480dbf5d15520a8c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99871099"
---
# <a name="error-timeout-while-debugging-web-services"></a>错误：调试 Web 服务时超时
在从调用代码单步执行 XML Web service 时，调用有时可能会超时，结果是你无法继续调试。 您可能会看到下面这样的错误信息。

```cmd
An unhandled exception of type 'System.Net.WebException' occurred in
system.Web.services.dll
Additional information: The operation has timed-out.
```

## <a name="solution"></a>解决方案
 若要避免此问题，请将 XML Web service 调用的超时值设置为无限大，如下面的示例所示：

```csharp
Service1 obj = new Service1();
obj.TimeOut = -1; // infinite time out.
```

## <a name="see-also"></a>请参阅
- [调试 Web 应用程序：错误和疑难解答](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
