---
description: 设置搜索调试符号的路径。
title: IDebugEngine3：：SetSymbolPath |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetSymbolPath
helpviewer_keywords:
- IDebugEngine3::SetSymbolPath
ms.assetid: 47b48f84-8a96-401f-84df-0baa8a96d26e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 73e7d4cb8ed36546e60326bc0935817d9b647adb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664835"
---
# <a name="idebugengine3setsymbolpath"></a>IDebugEngine3::SetSymbolPath
设置搜索调试符号的路径。

## <a name="syntax"></a>语法

```cpp
HRESULT SetSymbolPath (
   LPOLESTR            szSymbolSearchPath,
   LPOLESTR            szSymbolCachePath,
   LOAD_SYMBOLS_FLAGS  Flags
);
```

```csharp
int SetSymbolPath(
   string                    szSymbolSearchPath,
   string                    szSymbolCachePath,
   enum_LOAD_SYMBOLS_FLAGS   Flags
);
```

## <a name="parameters"></a>parameters

`szSymbolSearchPath`\
[in]包含符号搜索路径或路径的字符串。 有关详细信息，请参阅"备注"。 不能为 null。

`szSymbolCachePath`\
[in]包含可在其中缓存符号的本地路径的字符串。 不能为 null。

`Flags`\
[in]未使用;始终设置为 0。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则返回错误代码。

## <a name="remarks"></a>备注
 字符串是一个或多个路径的列表，用分号分隔， `szSymbolSearchPath` 用于搜索符号。 这些路径可以是本地路径、UNC 样式路径或 URL。 这些路径也可以混合使用不同类型的路径。 如果路径是 UNC (例如 \\ \Symserver\Symbols) ，则调试引擎应确定该路径是否指向符号服务器，并且应该能够从该服务器加载符号，将其缓存在 指定的路径中 `szSymbolCachePath` 。

 符号路径还可以包含一个或多个缓存位置。 缓存按优先级顺序列出，优先级最高的缓存优先，用 * 符号分隔。 例如：

```
\\symbols\symbols;\\someotherserver\symbols;c:\symbols\httpsymbols*https://msdl.microsoft.com
```

 [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)方法执行符号的实际加载。

## <a name="see-also"></a>另请参阅
- [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
