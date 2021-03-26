---
description: 标识自定义查看器或类型可视化工具的结构。
title: DEBUG_CUSTOM_VIEWER |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_CUSTOM_VIEWER
helpviewer_keywords:
- DEBUG_CUSTOM_VIEWER structure
ms.assetid: 8e0ef3f0-0107-48e8-a037-6e52b4c4ed9d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 76c02956acd9277f203c67bede7369d6bb7a603a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105096273"
---
# <a name="debug_custom_viewer"></a>DEBUG_CUSTOM_VIEWER
标识自定义查看器或类型可视化工具的结构。

## <a name="syntax"></a>语法

```cpp
typedef struct tagDEBUG_CUSTOM_VIEWER {
    DWORD dwID;
    BSTR  bstrMenuName;
    BSTR  bstrDescription;
    GUID  guidLang;
    GUID  guidVendor;
    BSTR  bstrMetric;
} DEBUG_CUSTOM_VIEWER;
```

```csharp
public struct DEBUG_CUSTOM_VIEWER {
    public uint   dwID;
    public string bstrMenuName;
    public string bstrDescription;
    public Guid   guidLang;
    public Guid   guidVendor;
    public string bstrMetric;
};
```

## <a name="members"></a>成员
`dwID`\
用于区分由一个或多个实现的查看器的 ID `GUID` 。

`bstrMenuName`\
将显示在下拉菜单中的文本。

`bstrDescription`\
如果未使用) ，则自定义查看器或类型可视化工具的说明 (必须为 null 值。

`guidLang`\
提供表达式计算器的语言。

`guidVendor`\
提供表达式计算器的供应商。

`bstrMetric`\
用于存储自定义查看器或类型可视化工具的度量值 `CLSID` 。

## <a name="remarks"></a>备注
此结构的列表由对 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) 方法的调用返回， (，并通过扩展 [) 方法进行](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md) 。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)
