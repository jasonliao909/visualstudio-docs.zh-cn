---
description: 检索上次加载错误的文件名。
title: IDiaDataSource::get_lastError | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::get_lastError method
ms.assetid: cf08850b-8b75-4e8c-90bd-bd0214756f99
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 1a15333df3c4c994f752ff7bd93978a7b7e34ffb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832335"
---
# <a name="idiadatasourceget_lasterror"></a>IDiaDataSource::get_lastError
检索上次加载错误的文件名。

## <a name="syntax"></a>语法

```C++
HRESULT get_lastError (
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 pRetVal

[out] 返回包含与上次加载错误关联的 .pdb 文件名的字符串。

## <a name="return-value"></a>返回值
 返回由加载操作引起的上一个错误代码。 如果 `pRetVal` 参数为 `NULL`，则返回 `E_INVALIDARG`。

## <a name="example"></a>示例

```C++
BSTR    fileName;
HRESULT errorCode = pSource->get_lastError( &fileName );
```

## <a name="see-also"></a>另请参阅
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
