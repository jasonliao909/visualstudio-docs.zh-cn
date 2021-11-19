---
description: 检索校验和字节。
title: IDiaSourceFile::get_checksum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_checksum method
ms.assetid: aad63a7e-4e22-44e4-8a5b-81b5174ced1e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 6c816fd0e44ee4870bbc656aa48621b175908692
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831854"
---
# <a name="idiasourcefileget_checksum"></a>IDiaSourceFile::get_checksum
检索校验和字节。

## <a name="syntax"></a>语法

```C++
HRESULT get_checksum ( 
   DWORD  cbData,
   DWORD* pcbData,
   BYTE   data[]
);
```

#### <a name="parameters"></a>参数
 `cbData`

中数据缓冲区的大小（以字节为单位）。

 `pcbData`

弄返回校验和字节数。 此参数不能为 `NULL`。

 `data`

[in，out]用校验和字节填充的缓冲区。 如果此参数为 `NULL` ，则 `pcbData` 返回所需的字节数。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 若要确定用于生成校验和字节的校验和算法类型，请调用 [IDiaSourceFile：： get_checksumType](../../debugger/debug-interface-access/idiasourcefile-get-checksumtype.md) 方法。

 校验和通常是从源文件的映像生成的，因此，源文件中的更改会反映在校验和字节的更改中。 如果校验和字节与从文件的加载映像生成的校验和不匹配，则该文件应视为已损坏或已被篡改。

 典型校验和的大小绝不会超过32个字节，但不会假定为校验和的最大大小。 将 `data` 参数设置为 `NULL` ，以获取检索校验和所需的字节数。 然后，分配适当大小的缓冲区，并使用新缓冲区再次调用此方法。

## <a name="see-also"></a>另请参阅
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSourceFile::get_checksumType](../../debugger/debug-interface-access/idiasourcefile-get-checksumtype.md)
