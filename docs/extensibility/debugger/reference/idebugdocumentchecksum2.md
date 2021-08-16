---
description: 表示调试文档的校验和，并启用在组件之间传递校验和。
title: IDebugDocumentChecksum2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentChecksum2 interface
ms.assetid: 6d22fa94-21aa-46cb-b5b5-32a6399ebb20
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 3bcd872ed06fac90d48bc773250fd007d3ed1d21e8b4714876d62e038df2f813
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433991"
---
# <a name="idebugdocumentchecksum2"></a>IDebugDocumentChecksum2
表示调试文档的校验和，并启用在组件之间传递校验和。

## <a name="syntax"></a>语法

```
IDebugDocumentChecksum2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 此接口可以通过公开 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) 接口的任何组件实现。 但是，它主要由调试引擎实现，以便符号文件 (*.pdb) 中嵌入的校验和可以传递回 IDE，并可在查找源时使用。

## <a name="methods"></a>方法
 下表显示了 的方法 `IDebugDocumentChecksum2` 。

|方法|说明|
|------------|-----------------|
|[GetChecksumAndAlgorithmId](../../../extensibility/debugger/reference/idebugdocumentchecksum2-getchecksumandalgorithmid.md)|根据要使用的最大字节数检索文档校验和和算法标识符。|

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
