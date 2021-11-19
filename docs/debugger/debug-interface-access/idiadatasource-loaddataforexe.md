---
description: 打开并准备与 .exe/.dll 文件关联的调试数据。
title: IDiaDataSource::loadDataForExe | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaDataSource::loadDataForExe method
ms.assetid: d94a1068-f53f-44b5-b6fb-00dec361a7f2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 6e11a6d85e8a33803b7cbf8b912d3db834996753
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832331"
---
# <a name="idiadatasourceloaddataforexe"></a>IDiaDataSource::loadDataForExe
打开并准备与 .exe/.dll 文件关联的调试数据。

## <a name="syntax"></a>语法

```C++
HRESULT loadDataForExe (
   LPCOLESTR executable,
   LPCOLESTR searchPath,
   IUnknown* pCallback
);
```

#### <a name="parameters"></a>参数
可执行文件

[in] .exe 或 .dll 文件的路径。

SearchPath

[in] 用于搜索调试数据的备用路径。

pCallback

[in] 支持调试回调接口的对象的 `IUnknown` 接口，如 [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)、[IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)、[IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md) 和/或 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md) 接口。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK`；否则，返回错误代码。 下表显示了此方法的一些可能的错误代码。

|值|说明|
|-----------|-----------------|
|E_PDB_NOT_FOUND|无法打开文件或该文件的格式无效。|
|E_PDB_FORMAT|尝试访问采用过时格式的文件。|
|E_PDB_INVALID_SIG|签名不匹配。|
|E_PDB_INVALID_AGE|时长不匹配。|
|E_INVALIDARG|参数无效。|
|E_UNEXPECTED|数据源已准备好。|

## <a name="remarks"></a>备注
.exe/.dll 文件的调试头会命名相关的调试数据位置。

如果要从符号服务器加载调试数据，symsrv.dll 必须存在于安装了用户应用程序或 msdia140.dll 的同一目录中，或者必须存在于系统目录中。

此方法会读取调试头，然后搜索并准备调试数据。 搜索的进度可以选择通过回调进行报告和控制。 例如，当 `IDiaDataSource::loadDataForExe` 方法查找并处理调试目录时，将调用 [IDiaLoadCallback::NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)。

当无法通过标准文件 I/O 直接访问文件时，[IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md) 和 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md) 接口允许客户端应用程序提供从可执行文件读取数据的替代方法。

若要在不进行验证的情况下加载 .pdb 文件，请使用 [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md) 方法。

若要根据特定条件验证 .pdb 文件，请使用 [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md) 方法。

若要直接从内存加载 .pdb 文件，请使用 [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md) 方法。

## <a name="example"></a>示例

```C++
class MyCallBack: public IDiaLoadCallback
{
...
};
MyCallBack callback;
...
HRESULT hr = pSource->loadDataForExe( L"myprog.exe", L".\debug", (IUnknown*)&callback);
if (FAILED(hr))
{
    // Report error
}
```

## <a name="see-also"></a>另请参阅
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
- [IDiaLoadCallback::NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaDataSource::loadDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loaddatafrompdb.md)
- [IDiaDataSource::loadAndValidateDataFromPdb](../../debugger/debug-interface-access/idiadatasource-loadandvalidatedatafrompdb.md)
- [IDiaDataSource::loadDataFromIStream](../../debugger/debug-interface-access/idiadatasource-loaddatafromistream.md)
