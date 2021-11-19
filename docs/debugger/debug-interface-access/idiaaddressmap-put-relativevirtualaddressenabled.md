---
description: 允许客户端启用或禁用相对虚拟地址 (RVA) 的计算与使用。
title: IDiaAddressMap：:p ut_relativeVirtualAddressEnabled |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_relativeVirtualAddressEnabled method
ms.assetid: 767c078e-8ad7-4940-9e00-cae7704aadee
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9cfb2e9b3b77adb5e0b16b896100b5b9eab04596
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832344"
---
# <a name="idiaaddressmapput_relativevirtualaddressenabled"></a>IDiaAddressMap::put_relativeVirtualAddressEnabled
允许客户端启用或禁用相对虚拟地址 (RVA) 的计算与使用。

## <a name="syntax"></a>语法

```C++
HRESULT put_relativeVirtualAddressEnabled ( 
   BOOL NewVal
);
```

#### <a name="parameters"></a>参数
 NewVal

中设置为将 `TRUE` 启用或 `FALSE` 禁用。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 DIA 接口所描述的调试对象的地址，以及可执行文件的映像库的地址可以检索为相对虚拟地址。

 当段最初从 PDB 文件加载时，将启用 Rva。 若要获取 Rva 的当前状态，请调用 [IDiaAddressMap：： get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md) 方法。

 在 `put_relativeVirtualAddress` 成功调用 [IDiaAddressMap：： set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md) 方法后，必须调用方法以启用 rva。

## <a name="see-also"></a>另请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::get_relativeVirtualAddressEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-relativevirtualaddressenabled.md)
- [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)
