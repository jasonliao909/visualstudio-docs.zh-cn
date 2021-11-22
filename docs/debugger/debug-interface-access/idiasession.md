---
description: 为调试符号提供查询上下文。
title: IDiaSession | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession interface
ms.assetid: 69dab9bf-2c68-4f70-9678-3b50fba3e6fa
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 97a1491b524311f8e48a1e59123e2648efa8d6c1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831860"
---
# <a name="idiasession"></a>IDiaSession
为调试符号提供查询上下文。

## <a name="syntax"></a>语法

```
IDiaSession : IUnknown
```

## <a name="methods"></a>方法
下表显示了 `IDiaSession` 方法。

|方法|说明|
|------------|-----------------|
|[IDiaSession::get_loadAddress](../../debugger/debug-interface-access/idiasession-get-loadaddress.md)|检索可执行文件的加载地址，该地址与此符号存储区中的符号对应。 此值与传递给 `put_loadAddress` 方法的值相同。|
|[IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md)|设置可执行文件的加载地址，该地址与此符号存储区中的符号对应。 注意：在获取 `IDiaSession` 和开始使用对象之前调用该方法非常重要。|
|[IDiaSession::get_globalScope](../../debugger/debug-interface-access/idiasession-get-globalscope.md)|检索对全局范围的引用。|
|[IDiaSession::getEnumTables](../../debugger/debug-interface-access/idiasession-getenumtables.md)|检索符号存储区中包含的所有表的枚举器。|
|[IDiaSession::getSymbolsByAddr](../../debugger/debug-interface-access/idiasession-getsymbolsbyaddr.md)|检索静态位置的所有命名符号的枚举器。|
|[IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)|检索名称和符号类型都匹配的特定父标识符的所有子级。|
|[IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)|检索包含或最接近指定地址的指定符号类型。|
|[IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)|检索包含或最接近指定相对虚拟地址 (RVA) 的指定符号类型。|
|[IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)|检索包含或最接近指定虚拟地址 (VA) 的指定符号类型。|
|[IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)|检索包含指定元数据令牌的符号。|
|[IDiaSession::symsAreEquiv](../../debugger/debug-interface-access/idiasession-symsareequiv.md)|检查两个符号是否相等。|
|[IDiaSession::symbolById](../../debugger/debug-interface-access/idiasession-symbolbyid.md)|按其唯一标识符检索符号。|
|[IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)|检索包含或最接近指定相对虚拟地址和偏移的指定符号类型。|
|[IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)|检索包含或最接近指定虚拟地址和偏移量的指定符号类型。|
|[IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)|按编译单位和名称检索源文件。|
|[IDiaSession::findFileById](../../debugger/debug-interface-access/idiasession-findfilebyid.md)|按源文件标识符检索源文件。|
|[IDiaSession::findLines](../../debugger/debug-interface-access/idiasession-findlines.md)|检索指定编译单位和源文件标识符中的行号。|
|[IDiaSession::findLinesByAddr](../../debugger/debug-interface-access/idiasession-findlinesbyaddr.md)|检索包含指定地址的指定编译单位中的行。|
|[IDiaSession::findLinesByRVA](../../debugger/debug-interface-access/idiasession-findlinesbyrva.md)|检索包含指定相对虚拟地址的指定编译单位中的行。|
|[IDiaSession::findLinesByVA](../../debugger/debug-interface-access/idiasession-findlinesbyva.md)|查找包含在指定的地址范围内的行的行号信息。|
|[IDiaSession::findLinesByLinenum](../../debugger/debug-interface-access/idiasession-findlinesbylinenum.md)|按源文件和行号检索指定的编译单位中的行。|
|[IDiaSession::findInjectedSource](../../debugger/debug-interface-access/idiasession-findinjectedsource.md)|检索源，该列表已由属性提供程序或编译过程的其他组件放入符号存储区中。|
|[IDiaSession::getEnumDebugStreams](../../debugger/debug-interface-access/idiasession-getenumdebugstreams.md)|检索调试数据流的枚举序列。|
|[IDiaSession::findInlineFramesByAddr](../../debugger/debug-interface-access/idiasession-findinlineframesbyaddr.md)|检索允许客户端在给定地址中遍历所有内联帧的枚举。|
|[IDiaSession::findInlineFramesByRVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyrva.md)|检索允许客户端在指定相对虚拟地址 (RVA) 中循环访问所有内联帧的枚举。|
|[IDiaSession::findInlineFramesByVA](../../debugger/debug-interface-access/idiasession-findinlineframesbyva.md)|检索允许客户端在指定虚拟地址 (VA) 中循环访问所有内联帧的枚举。|
|[IDiaSession::findInlineeLines](../../debugger/debug-interface-access/idiasession-findinlineelines.md)|检索一个枚举，该枚举允许客户端遍历由指定的父符号直接或间接内联的所有函数的行号信息。|
|[IDiaSession::findInlineeLinesByAddr](../../debugger/debug-interface-access/idiasession-findinlineelinesbyaddr.md)|检索一个枚举，该枚举允许客户端遍历由指定的父符号直接或间接内联并包含在指定地址范围中的所有函数的行号信息。|
|[IDiaSession::findInlineeLinesByRVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyrva.md)|检索一个枚举，该枚举允许客户端遍历由指定的父符号直接或间接内联并包含在指定相对虚拟地址 (RVA) 中的所有函数的行号信息。|
|[IDiaSession::findInlineeLinesByVA](../../debugger/debug-interface-access/idiasession-findinlineelinesbyva.md)|检索一个枚举，该枚举允许客户端遍历由指定的父符号直接或间接内联并包含在指定虚拟地址 (VA) 中的所有函数的行号信息。|
|[IDiaSession::findInlineeLinesByLinenum](../../debugger/debug-interface-access/idiasession-findinlineelinesbylinenum.md)|检索一个枚举，该枚举允许客户端遍历指定源文件和行号中直接或间接内联到此符号中的所有函数的行号信息。|
|[IDiaSession::findInlineesByName](../../debugger/debug-interface-access/idiasession-findinlineesbyname.md)|检索一个枚举，该枚举允许客户端遍历与指定名称匹配的所有内联函数的行号信息。|
|[IDiaSession::findSymbolsForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsforacceleratorpointertag.md)|返回指定的标记值在父级 Accelerator 存根函数中对应的变量的符号枚举。|
|[IDiaSession::findSymbolsByRVAForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasession-findsymbolsbyrvaforacceleratorpointertag.md)|给定相应的标记值后，此方法将在指定的相对虚拟地址返回指定父级 Accelerator 存根函数中包含的符号的枚举。|
|[IDiaSession::findAcceleratorInlineesByName](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbyname.md)|返回与指定的内联函数名称对应的内联框架的符号枚举。|
|[IDiaSession::findAcceleratorInlineesByLinenum](../../debugger/debug-interface-access/idiasession-findacceleratorinlineesbylinenum.md)|返回与指定源位置对应的内联框架的符号枚举。|

## <a name="remarks"></a>备注
创建 `IDiaSession` 对象后调用 [IDiaSession::put_loadAddress](../../debugger/debug-interface-access/idiasession-put-loadaddress.md) 方法非常关键 — 传递给 `put_loadAddress` 方法的值必须为非零 — 对于符号的任意虚拟地址 (VA) 属性可访问。 加载地址来自加载正在调试的可执行文件的任何程序。 例如，可以调用 Win32 函数 `GetModuleInformation` 以检索可执行文件的加载地址（为可执行文件提供句柄）。

## <a name="example"></a>示例
该示例介绍如何获取 `IDiaSession` 接口作为 DIA SDK 常规初始化的一部分。

```C++
CComPtr<IDiaDataSource> pSource;
ComPtr<IDiaSession> psession;

void InitializeDIA(const char *szFilename)
{
    HRESULT hr = CoCreateInstance( CLSID_DiaSource,
                                   NULL,
                                   CLSCTX_INPROC_SERVER,
                                   __uuidof( IDiaDataSource ),
                                  (void **) &pSource);
    if (FAILED(hr))
    {
        Fatal("Could not CoCreate CLSID_DiaSource. Register msdia80.dll." );
    }
    wchar_t wszFilename[ _MAX_PATH ];
    mbstowcs( wszFilename,
              szFilename,
              sizeof( wszFilename )/sizeof( wszFilename[0] ) );
    if ( FAILED( pSource->loadDataFromPdb( wszFilename ) ) )
    {
        if ( FAILED( pSource->loadDataForExe( wszFilename, NULL, NULL ) ) )
        {
            Fatal( "loadDataFromPdb/Exe" );
        }
    }
    if ( FAILED( pSource->openSession( &psession ) ) )
    {
        Fatal( "openSession" );
    }
}
```

## <a name="requirements"></a>要求
标头：Dia2.h

库：diaguids.lib

DLL：msdia80.dll

## <a name="see-also"></a>另请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [概述](../../debugger/debug-interface-access/overview-debug-interface-access-sdk.md)
- [Exe](../../debugger/debug-interface-access/exe.md)
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)
- [IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)
- [IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)
- [查询 .Pdb 文件](../../debugger/debug-interface-access/querying-the-dot-pdb-file.md)
