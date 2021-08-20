---
description: 检索指定代理 ID 的属性代理接口。
title: IPropertyProxyProvider：：GetPropertyProxy |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyProvider::GetPropertyProxy
helpviewer_keywords:
- IPropertyProxyProvider::GetPropertyProxy
ms.assetid: 3ebb7515-5bfe-48f4-9b8d-721b8f664eb6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f9d28e897af9493e499b69a6748793de45ba3a69
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122118146"
---
# <a name="ipropertyproxyprovidergetpropertyproxy"></a>IPropertyProxyProvider::GetPropertyProxy
检索指定代理 ID 的属性代理接口。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPropertyProxy(
   DWORD                  dwID,
   IPropertyProxyEESide** proxy
);
```

```csharp
int GetPropertyProxy(
   uint                     dwID,
   out IPropertyProxyEESide proxy
);
```

## <a name="parameters"></a>参数
`dwID`\
[in]所需属性代理的 ID。

`proxy`\
[out]返回 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 为了支持外部类型可视化工具，此方法通常将调用转发到 [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md) 方法。 请参阅 [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md) ，详细了解如何获取 IEEVisualizerService。

## <a name="see-also"></a>请参阅
- [IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)
- [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)
