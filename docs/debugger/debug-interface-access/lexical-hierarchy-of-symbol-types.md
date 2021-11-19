---
description: 下表显示了词汇层次结构中的符号类型。
title: 符号类型的词法层次结构 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- symbols [DIA SDK], type hierarchies
ms.assetid: 912da653-ddfe-45a4-84aa-64281283739a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9c3892267d47cf48fc5fcd8b7e0179478b4c324a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832814"
---
# <a name="lexical-hierarchy-of-symbol-types"></a>符号类型的词法层次结构
下表显示了词汇层次结构中的符号类型。

## <a name="symbol-types"></a>符号类型

|符号类型|说明|
|-----------------|-----------------|
|[批注](../../debugger/debug-interface-access/annotation.md)|指定程序代码中的注释位置。|
|[阻止](../../debugger/debug-interface-access/block.md)|指定函数中的嵌套作用域。|
|`Compiland`|指定 `compiland` 链接到 .exe 文件。|
|[CompilandDetails](../../debugger/debug-interface-access/compilanddetails.md)|指定编译单位数据，这些数据可能需要加载附加的编译单位详细信息，从而导致检索运行时开销。|
|[CompilandEnv](../../debugger/debug-interface-access/compilandenv.md)|指定任何其他环境变量对编译单位的编译非常重要。|
|[自定义（调试接口访问 SDK）](../../debugger/debug-interface-access/custom-debug-interface-access-sdk.md)|指定用户定义的符号。|
|[数据（调试界面访问 SDK）](../../debugger/debug-interface-access/data-debug-interface-access-sdk.md)|指定此类变量作为参数、局部变量、全局变量和类成员。|
|[Exe](../../debugger/debug-interface-access/exe.md)|指定数据的全局范围;对应于整个 .exe 或 .dll 文件。|
|[FuncDebugEnd](../../debugger/debug-interface-access/funcdebugend.md)|指定一个函数，该函数具有一个定义了调试结束点的点。|
|[FuncDebugStart](../../debugger/debug-interface-access/funcdebugstart.md)|指定一个函数，该函数具有定义的点，在该点开始调试。|
|[函数（调试接口访问 SDK）](../../debugger/debug-interface-access/function-debug-interface-access-sdk.md)|指定函数。|
|[标签（调试接口访问 SDK）](../../debugger/debug-interface-access/label-debug-interface-access-sdk.md)|指定程序代码中的位置。|
|[PublicSymbol](../../debugger/debug-interface-access/publicsymbol.md)|指定在生成可执行程序时显示的外部符号。|
|[Thunk](../../debugger/debug-interface-access/thunk.md)|指定 `thunk` 。|
|[UsingNameSpace](../../debugger/debug-interface-access/usingnamespace.md)|指定一个 `namespace` 标识符。|

> [!NOTE]
> 可能还会提供其他符号属性，具体取决于符号类型。 各个符号主题中列出了这些属性。

## <a name="see-also"></a>另请参阅
- [符号类型的类层次结构](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)
- [IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)
- [符号和符号标记](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
