---
description: 表示托管数组对象，并允许表达式 (企业版) 确定数组 (下限) 基索引。
title: IDebugArrayObject2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugArrayObject2 interface
ms.assetid: be6e504d-4ab3-4141-a61b-0953ee0e038e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 834525917e33ebb7f7fabedbfbd610a9a105f600
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119953"
---
# <a name="idebugarrayobject2"></a>IDebugArrayObject2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示托管数组对象，并允许表达式 (企业版) 确定数组 (下限) 基索引。

## <a name="syntax"></a>语法

```
IDebugArrayObject2 : IDebugArrayObject
```

## <a name="notes-for-implementers"></a>实现者说明
 这由 DE (托管调试引擎) 。

## <a name="methods"></a>方法
 除了 [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md) 接口上的方法外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetBaseIndices](../../../extensibility/debugger/reference/idebugarrayobject2-getbaseindices.md)|根据数组中的 (，) 检索每个索引的下限和基索引。|
|[HasBaseIndices](../../../extensibility/debugger/reference/idebugarrayobject2-hasbaseindices.md)|确定数组的基索引是否 (下限) 定义。|

## <a name="remarks"></a>备注
 表达式计算程序使用此接口来表示分析树中的托管数组。

## <a name="requirements"></a>要求
 标头：Ee.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
