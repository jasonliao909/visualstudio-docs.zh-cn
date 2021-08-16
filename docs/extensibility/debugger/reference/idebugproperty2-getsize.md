---
description: 获取属性值的大小（以字节为单位）。
title: IDebugProperty2：： GetSize |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetSize
helpviewer_keywords:
- IDebugProperty2::GetSize
ms.assetid: 0deb8ec5-d6fb-4622-bb14-0c46b9459cc6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 17a1ec60b6f1a60980292b4a82cb218d4ad69b15d504f9d377334369ee663c01
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338691"
---
# <a name="idebugproperty2getsize"></a>IDebugProperty2::GetSize
获取属性值的大小（以字节为单位）。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSize ( 
   DWORD* pdwSize
);
```

```csharp
int GetSize ( 
   out uint pdwSize
);
```

## <a name="parameters"></a>参数
`pdwSize`\
弄返回属性值的大小（以字节为单位）。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `S_GETSIZE_NO_SIZE`如果属性没有大小，则返回。

## <a name="see-also"></a>另请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
