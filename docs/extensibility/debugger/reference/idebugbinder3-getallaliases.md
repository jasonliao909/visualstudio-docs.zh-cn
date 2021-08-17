---
description: 此方法从程序中检索别名列表。
title: IDebugBinder3：：GetAllAliases |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetAllAliases
helpviewer_keywords:
- IDebugBinder3::GetAllAliases method
ms.assetid: 1f9ab2ee-2ab3-4a61-8b99-95dd7fdf3511
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 72e8b174888e2484a1b065268045a7bf33194957a909fb9ec71dc7c30a716fdd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121293048"
---
# <a name="idebugbinder3getallaliases"></a>IDebugBinder3::GetAllAliases
此方法从程序中检索别名列表。

## <a name="syntax"></a>语法

```cpp
HRESULT GetAllAliases(
   UINT          uRequest,
   IDebugAlias** ppAliases,
   UINT*         puFetched
);
```

```csharp
int GetAllAliases(
   uint          uRequest,
   IDebugAlias[] ppAliases,
   out uint      puFetched
);
```

## <a name="parameters"></a>参数
`uRequest`\
[in]要返回的最大别名数 (指定传入数组的数组 `ppAliases`) 。

`ppAliases`\
[in， out]要用别名填充的数组 (如果此值为 null 且为 0，则返回的别名计数将返回 `uRequest` `puFetched`) 。

`puFetched`\
[out]返回获取的别名数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
