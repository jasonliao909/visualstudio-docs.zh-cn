---
description: 允许表达式计算 (企业版) 在调试器的输出窗口中显示消息。
title: IDebugIDECallback |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugIDECallback interface
ms.assetid: 8d31adc0-1c44-4658-8d4f-f4b73e35f4a6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: e2bc49d54ce5bdce90e47f51e940d0a7c47d78d7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122064130"
---
# <a name="idebugidecallback"></a>IDebugIDECallback
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 允许表达式计算 (企业版) 在调试器的输出窗口中显示消息。

## <a name="syntax"></a>语法

```
IDebugIDECallback : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 此回调由托管调试引擎实现。

## <a name="notes-for-callers"></a>调用方说明
 表达式计算程序可以使用它向调试器的输出窗口发送输出。

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[DisplayMessage](../../../extensibility/debugger/reference/idebugidecallback-displaymessage.md)|将指定的消息字符串发送到调试器的输出窗口。|

## <a name="requirements"></a>要求
 标头：Ee.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
