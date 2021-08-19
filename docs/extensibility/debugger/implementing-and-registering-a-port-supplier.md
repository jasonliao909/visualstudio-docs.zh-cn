---
title: 实现和注册端口供应商|Microsoft Docs
description: 了解如何实现和注册端口供应商，该供应商跟踪和提供用于管理流程的端口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], registering port suppliers
- port suppliers, registering
ms.assetid: fb057052-ee16-4272-8e16-a4da5dda0ad4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 151f14592e0987a16b3195944d3ef7ce0f972ea1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153467"
---
# <a name="implement-and-register-a-port-supplier"></a>实现和注册端口供应商
端口供应商的角色是跟踪和提供端口，而端口又管理流程。 需要创建端口时，将使用 CoCreate 和端口供应商的 GUID 实例化端口供应商 (会话调试管理器 [SDM] 将使用用户选择的端口供应商或项目系统) 指定的端口供应商。 然后，SDM 调用 [CanAddPort](../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md) 以查看是否可添加任何端口。 如果可以添加端口，则通过调用 [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md) 并传递描述该端口的 [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md) 来请求新端口。 `AddPort` 返回由 [IDebugPort2 接口表示的新](../../extensibility/debugger/reference/idebugport2.md) 端口。

## <a name="discussion"></a>讨论 (Discussion)
 端口由与计算机或调试服务器关联的端口供应商创建。 服务器通过[EnumPortSuppliers](../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md) 方法枚举其端口供应商，端口供应商通过 [EnumPorts](../../extensibility/debugger/reference/idebugportsupplier2-enumports.md) 方法枚举其端口。

 除了典型的 COM 注册外，端口供应商必须通过将其 CLSID 和名称放在特定注册表位置Visual Studio注册到特定注册表位置。 名为 的调试 SDK 帮助程序函数可处理这种繁琐操作：将针对要注册的每个项调用一 `SetMetric` 次，因此：

```cpp
SetMetric(metrictypePortSupplier,
          <GUID of your port supplier>,
          metricCLSID,
          <CLSID of your port supplier>,
          false,
          NULL)
SetMetric(metrictypePortSupplier,
          <GUID of your port supplier>,
          metricName,
          <name of your port supplier>,
          false,
          NULL);
```

 端口供应商通过调用另一 (调试 SDK 帮助程序函数来注销自身) 注册的每个项调用一次， `RemoveMetric` 因此：

```cpp
RemoveMetric(metrictypePortSupplier,
             <GUID of your port supplier>,
             metricCLSID,
             NULL);
RemoveMetric(metrictypePortSupplier,
             <GUID of your port supplier>,
             metricName,
             NULL);
```

> [!NOTE]
> 用于 [调试 和 的 SDK 帮助](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)程序是在 `SetMetric` `RemoveMetric` *dbgmetric.h* 中定义的静态函数，并编译为 *ad2de.lib*。 `metrictypePortSupplier` `metricCLSID` `metricName` *dbgmetric.h* 中也定义了 、 和 帮助程序。

 端口供应商可以通过方法 [GetPortSupplierName](../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md) 和 [GetPortSupplierId](../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)分别提供其名称和 GUID。

## <a name="see-also"></a>请参阅
- [实现端口供应商](../../extensibility/debugger/implementing-a-port-supplier.md)
- [用于调试的 SDK 帮助程序](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [端口供应商](../../extensibility/debugger/port-suppliers.md)
