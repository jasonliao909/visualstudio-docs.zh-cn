---
title: IDebugDocumentChecksum2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentChecksum2 interface
ms.assetid: 6d22fa94-21aa-46cb-b5b5-32a6399ebb20
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ca8a33626ad68dcac690ca288d4bc375679a4e3e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99880770"
---
# <a name="idebugdocumentchecksum2"></a>IDebugDocumentChecksum2
表示调试文档的校验和，并允许传递组件之间的校验和。

## <a name="syntax"></a>语法

```
IDebugDocumentChecksum2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 此接口可由公开 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) 接口的任何组件实现。 不过，它主要由调试引擎实现，以便在符号文件中嵌入的校验和 ( * .pdb) 可以传递回 IDE 并在查找源时使用。

## <a name="methods"></a>方法
 下表显示的方法 `IDebugDocumentChecksum2` 。

|方法|说明|
|------------|-----------------|
|[GetChecksumAndAlgorithmId](../../../extensibility/debugger/reference/idebugdocumentchecksum2-getchecksumandalgorithmid.md)|在给定要使用的最大字节数的情况中，检索文档校验和和算法标识符。|

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
