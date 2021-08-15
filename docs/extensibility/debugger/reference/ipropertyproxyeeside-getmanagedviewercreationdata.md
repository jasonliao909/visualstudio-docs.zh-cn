---
description: 检索有关此属性类型的查看器的信息，以便实例化该查看器。
title: IPropertyProxyEESide：： GetManagedViewerCreationData |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::GetManagedViewerCreationData
helpviewer_keywords:
- IPropertyProxyEESide::GetManagedViewerCreationData
ms.assetid: c4eb4d60-8816-4d52-bc8d-dffd4f066499
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3044abff780c0b7798c7c311cf32199166230c0315a12dfc6caf47ca23cc9da4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121321384"
---
# <a name="ipropertyproxyeesidegetmanagedviewercreationdata"></a>IPropertyProxyEESide::GetManagedViewerCreationData
检索有关此属性类型的查看器的信息，以便实例化该查看器。

## <a name="syntax"></a>语法

```cpp
HRESULT GetManagedViewerCreationData(
   BSTR*                  assemName,
   IEEDataStorage**       assemBytes,
   IEEDataStorage**       assemPdb,
   BSTR*                  className,
   ASSEMBLYLOCRESOLUTION* alr,
   BOOL*                  replacementOk
);
```

```csharp
int GetManagedViewerCreationData(
   out string                     assemName,
   out IEEDataStorage             assemBytes,
   out IEEDataStorage             assemPdb,
   out string                     className,
   out enum_ASSEMBLYLOCRESOLUTION alr,
   out int                        replacementOk
);
```

## <a name="parameters"></a>参数
`assemName`\
弄返回包含此对象的程序集的名称。

`assemBytes`\
弄返回一个 [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) 对象，该对象包含此对象的程序集字节 (如果没有可用字节) ，则此值为 null 值。

`assemPdb`\
弄返回一个 `IEEDataStorage` 对象，该对象包含此对象的符号存储区信息 (如果没有符号存储区) 可用，则此值为 null 值。

`className`\
弄返回包含此对象的类名。

`alr`\
弄返回 [ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md) 枚举中的一个值，该值指示程序集的位置。

`replacementOk`\
弄 `TRUE` 如果可以更改此对象的值，则返回非零 () ; `FALSE` 如果对象是只读的，则返回零 () 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 类型可视化工具使用此方法实例化托管查看器。

## <a name="see-also"></a>另请参阅
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
