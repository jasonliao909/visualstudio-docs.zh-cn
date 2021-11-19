---
description: 打开并准备程序数据库 (.pdb) 文件作为调试数据源。
title: IDiaDataSource::loadDataFromPdb | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadDataFromPdb method
ms.assetid: 02159073-8144-47f8-a0b0-aa0edcb92b5b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 957cee1c9694f31f0fecd2123d7b4d7fdf104df5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832329"
---
# <a name="idiadatasourceloaddatafrompdb"></a>IDiaDataSource::loadDataFromPdb
打开并准备程序数据库 (.pdb) 文件作为调试数据源。

## <a name="syntax"></a>语法

```C++
HRESULT loadDataFromPdb (
   LPCOLESTR pdbPath
);
```

#### <a name="parameters"></a>参数
pdbPath

[in] .pdb 文件的路径。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK`；否则，返回错误代码。 下表显示了此方法的可能返回值。

|值|说明|
|-----------|-----------------|
|E_PDB_NOT_FOUND|无法打开文件或确定该文件的格式无效。|
|E_PDB_FORMAT|尝试访问采用过时格式的文件。|
|E_INVALIDARG|参数无效。|
|E_UNEXPECTED|数据源已准备好。|

## <a name="remarks"></a>备注
此方法直接从 .pdb 文件加载调试数据。

若要根据特定条件验证 .pdb 文件，请使用 [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md) 方法。

若要获取对数据加载过程的访问权限（通过回调机制），请使用 [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) 方法。

若要直接从内存加载 .pdb 文件，请使用 [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md) 方法。

## <a name="example"></a>示例

```C++
HRESULT hr = pSource->loadDataFromPdb( L"myprog.pdb" );
if (FAILED(hr))
{
    // report error
}
```

## <a name="see-also"></a>另请参阅
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)
- [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
