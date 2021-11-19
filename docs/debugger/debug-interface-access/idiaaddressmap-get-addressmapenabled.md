---
description: 指示是否已为特定会话建立地址映射。
title: IDiaAddressMap::get_addressMapEnabled | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::get_addressMapEnabled method
ms.assetid: 6183dc5e-befa-4e5a-ae5a-f4aa24f3ed9e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 592beea4cd85ad14b878886e0cbd8c94ad4d88eb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832353"
---
# <a name="idiaaddressmapget_addressmapenabled"></a>IDiaAddressMap::get_addressMapEnabled
指示是否已为特定会话建立地址映射。

## <a name="syntax"></a>语法

```C++
HRESULT get_addressMapEnabled ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 pRetVal

弄 `TRUE` 如果已启用地址映射，则返回。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 可执行的后处理器有时会更新可执行文件。 DIA 包含一种机制，用于支持将符号转换为新的布局。

 客户端应用程序可以通过从[IDiaSession](../../debugger/debug-interface-access/idiasession.md)接口获取[IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)接口并调用[IDiaAddressMap：： Set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)方法，然后调用[IDiaAddressMap：:p ut_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)方法来设置特定会话的地址映射。 `get_addressMapEnabled`方法返回调用方法的结果 `put_addressMapEnabled` 。

## <a name="see-also"></a>另请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
- [IDiaAddressMap::put_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)
