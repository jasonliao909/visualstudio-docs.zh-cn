---
description: 指定是否应当使用地址映射来转换符号地址。
title: IDiaAddressMap::put_addressMapEnabled | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_addressMapEnabled method
ms.assetid: 0f205337-4e59-4383-8059-7b1d207d6dcd
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: f4c3a08361942df789c7e6bbd055464d69d056fd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832348"
---
# <a name="idiaaddressmapput_addressmapenabled"></a>IDiaAddressMap::put_addressMapEnabled
指定是否应当使用地址映射来转换符号地址。

## <a name="syntax"></a>语法

```C++
HRESULT put_addressMapEnabled ( 
   BOOL NewVal
);
```

#### <a name="parameters"></a>参数
 NewVal

[in]设置为 `TRUE` 可启用符号转换，或 `FALSE` 设置为 禁用。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 可执行后处理器有时会更新可执行文件。 DIA 包含支持将符号转换到新布局的机制。

 加载 PDB 文件时，将启用存储在该文件中的地址映射。 但是，有时客户端应用程序可能需要通过调用 [IDiaAddressMap：：set_addressMap 方法提供自己的地址](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) 映射。 如果 `set_addressMap` 方法成功，客户端应用程序必须使用 的参数调用 方法 `put_addressMapEnabled` `NewVal` `TRUE` ，以启用该地址映射的使用。

 可以通过调用 [IDiaAddressMap：：get_addressMapEnabled 方法来检索正在启用的地址映射的当前](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md) 状态。

## <a name="see-also"></a>另请参阅
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
- [IDiaAddressMap::get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md)
