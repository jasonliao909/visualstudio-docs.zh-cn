---
description: 表示变量的数值别名，使表达式 (企业版) 获取别名的应用程序域。
title: IDebugAlias2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugAlias2 interface
ms.assetid: 5252dcbb-8bfe-4d8a-a8e5-b022b194df19
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: ae66d69153a539c42000914c9df1c275aa3a431c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122072871"
---
# <a name="idebugalias2"></a>IDebugAlias2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示变量的数值别名，使表达式 (企业版) 获取别名的应用程序域。

## <a name="syntax"></a>语法

```
IDebugAlias2 : IDebugAlias
```

## <a name="notes-for-implementers"></a>实现者说明
 此接口由托管调试引擎在 DE (实现) 。

## <a name="methods"></a>方法
 除了 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) 接口上的方法外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetAppDomainId](../../../extensibility/debugger/reference/idebugalias2-getappdomainid.md)|检索应用程序域的标识符。|

## <a name="remarks"></a>备注
 别名是字符串形式的十进制数，后跟 # 字符，例如 1001#。

## <a name="requirements"></a>要求
 标头：Ee.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
