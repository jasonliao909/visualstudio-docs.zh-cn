---
description: 打开并验证程序数据库 (.pdb) 文件是否与提供的签名信息匹配，并准备用作调试数据源的 .pdb 文件。
title: IDiaDataSource::loadAndValidateDataFromPdb | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadAndValidateDataFromPdb method
ms.assetid: d66712dd-6c24-4192-919a-cce262066f0e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9a3d09b96f835b84399742a461b404bc4b75ddc0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832334"
---
# <a name="idiadatasourceloadandvalidatedatafrompdb"></a>IDiaDataSource::loadAndValidateDataFromPdb
打开并验证程序数据库 (.pdb) 文件是否与提供的签名信息匹配，并准备用作调试数据源的 .pdb 文件。

## <a name="syntax"></a>语法

```C++
HRESULT loadAndValidateDataFromPdb ( 
   LPCOLESTR pdbPath,
   GUID*     pcsig70,
   DWORD     sig,
   DWORD     age
);
```

#### <a name="parameters"></a>参数
`pdbPath`

[in] .pdb 文件的路径。

`pcsig70`

[in] 要根据 .pdb 文件签名进行验证的 GUID 签名。 只有 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 和更高版本中的 .pdb 文件具有 GUID 签名。

`sig`

[in] 要根据 .pdb 文件签名进行验证的 32 位签名。

`age`

[in] 要验证的年限值。 年限不一定与任何已知的时间值相对应；它用于确定 .pdb 文件是否与相应的 .exe 文件不同步。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK`；否则，返回错误代码。 下表显示了此方法的可能返回值。

|值|说明|
|-----------|-----------------|
|E_PDB_NOT_FOUND|无法打开文件或该文件的格式无效。|
|E_PDB_FORMAT|尝试访问采用过时格式的文件。|
|E_PDB_INVALID_SIG|签名不匹配。|
|E_PDB_INVALID_AGE|年限不匹配。|
|E_INVALIDARG|参数无效。|
|E_UNEXPECTED|数据源已准备好。|

## <a name="remarks"></a>备注
.pdb 文件同时包含签名值和年限值。 这些值复制在与 .pdb 文件匹配的 .exe 或 .dll 文件中。 准备数据源之前，此方法会验证已命名 .pdb 文件的签名和年限值是否与提供的值相匹配。

若要在不进行验证的情况下加载 .pdb 文件，请使用 [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) 方法。

若要获取对数据加载过程的访问权限（通过回调机制），请使用 [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) 方法。

若要直接从内存加载 .pdb 文件，请使用 [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md) 方法。

## <a name="example"></a>示例

```C++
IDiaDataSource* pSource;  // Previously created data source.
DEFINE_GUID(expectedGUIDSignature,0x1234,0x5678,0x01,0x02,0x03,0x04,0x05,0x06,0x07,0x08);
DWORD expectedFileSignature = 0x12345678;
DWORD expectedAge           = 128;

HRESULT hr;
hr = pSource->loadAndValidateDataFromPdb( L"yprog.pdb",
                                          &expectedGUIDSignature,
                                          expectedFileSignature,
                                          expectedAge);
if (FAILED(hr))
{
    // Report an error
}

```

## <a name="see-also"></a>另请参阅
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)
- [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
