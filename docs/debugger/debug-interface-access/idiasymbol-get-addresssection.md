---
description: 检索地址位置部分。
title: IDiaSymbol::get_addressSection | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_addressSection method
ms.assetid: fe80d479-3bb5-4f55-9b62-1bd58d0a60ce
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 6e90d81f857aa0088288a1d54db72e3d5de86787
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832574"
---
# <a name="idiasymbolget_addresssection"></a>IDiaSymbol::get_addressSection
检索地址位置部分。 当 [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md) 设置为时使用 `LocIsStatic` 。

## <a name="syntax"></a>语法

```C++
HRESULT get_addressSection ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回地址位置部分。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回 `S_FALSE` 错误代码。

> [!NOTE]
> 返回值意味着该 `S_FALSE` 属性对符号不可用。

## <a name="remarks"></a>备注
 对于位于外部 DLL 中的静态成员，此方法返回的部分可能为0，因为此方法依赖于获取成员的虚拟地址。 仅当使用指定 DLL 的加载地址的非零参数调用了[IDiaSession](../../debugger/debug-interface-access/idiasession.md)接口中的[IDiaSession：:p ut_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)方法时，虚拟地址才有效。

 若要获取地址的偏移量部分，请调用 [IDiaSymbol：： get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md) 方法。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [LocationType 枚举](../../debugger/debug-interface-access/locationtype.md)
