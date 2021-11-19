---
description: 返回与虚拟地址关联的 PDATA 数据块。
title: IDiaStackWalkHelper::pdataForVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::pdataByVA method
ms.assetid: fafc38fe-74dc-4726-9a51-eebf3a673d7f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: c2267173539401f9b673a6cf760abe9070279970
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831771"
---
# <a name="idiastackwalkhelperpdataforva"></a>IDiaStackWalkHelper::pdataForVA
返回与虚拟地址关联的 PDATA 数据块。

## <a name="syntax"></a>语法

```C++
HRESULT pdataForVA( 
   ULONGLONG  va,
   DWORD      cbData,
   DWORD*     pcbData,
   BYTE*      pbData
);
```

#### <a name="parameters"></a>参数
 `va`

[in] 指定要获取的数据的虚拟地址。

 `cbData`

[in] 要获取的数据的大小（以字节为单位）。

 `pcbData`

[out] 返回获取的数据的实际大小（以字节为单位）。

 `pbData`

[in, out] 使用请求数据填充的缓冲区。 不能为 `NULL`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果指定的地址没有 PDATA，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 编译的 PDATA（名为“.pdata”的部分）包含有关函数异常处理的信息。

 调用方知道要返回多少数据，因此调用方无需询问有多少数据可用。 因此，如果 `pbData` 参数为 `NULL`，则此方法的实现可以返回错误。

## <a name="see-also"></a>另请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
