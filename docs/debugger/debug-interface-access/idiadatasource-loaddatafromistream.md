---
description: 准备存储在程序数据库 (.pdb) 文件中通过内存中数据流访问的调试数据。
title: IDiaDataSource：：loadDataFromIStream |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadDataFromIStream method
ms.assetid: 8fe33eea-1457-4b8c-ae19-f1ede5578483
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 005c423df13f2d1b906a229665c79d6ee52627a7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832332"
---
# <a name="idiadatasourceloaddatafromistream"></a>IDiaDataSource::loadDataFromIStream
准备存储在程序数据库 (.pdb) 文件中通过内存中数据流访问的调试数据。

## <a name="syntax"></a>语法

```C++
HRESULT loadDataFromIStream ( 
   IStream* pIStream
);
```

#### <a name="parameters"></a>参数
 pIStream

[in]一 <xref:IStream> 个 对象，该对象表示要使用的数据流。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 下表显示了此方法的可能返回值。

|值|说明|
|-----------|-----------------|
|E_PDB_FORMAT|尝试访问采用过时格式的文件。|
|E_INVALIDARG|参数无效。|
|E_UNEXPECTED|数据源已准备就绪。|

## <a name="remarks"></a>备注
 此方法允许通过 对象从内存中获取可执行文件的调试 <xref:IStream> 数据。

 若要在不进行验证的情况下加载 .pdb 文件，请使用 [IDiaDataSource：：loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) 方法。

 若要根据特定条件验证 .pdb 文件，请使用 [IDiaDataSource：：loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md) 方法。

 若要通过回调机制 (数据加载过程) ，请使用 [IDiaDataSource：：loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)
- [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)
