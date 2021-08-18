---
description: 使Visual Studio UI 能够在"附加到进程"对话框的"传输信息"部分内显示文本。
title: IDebugPortSupplierDescription2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierDescription2 interface
ms.assetid: dd19b9d6-0703-44b3-9498-cedffa0ce5b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: a8724b75e4360e8b7e4b097fa00f5f3ed112e735
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126786"
---
# <a name="idebugportsupplierdescription2"></a>IDebugPortSupplierDescription2
使 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] UI 能够在"附加到进程"对话框的"传输信息"**部分内显示** 文本。

## <a name="syntax"></a>语法

```
IDebugPortSupplierDescription2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 此接口由端口供应商实现。

## <a name="methods"></a>方法
 下表显示了 的方法 `IDebugPortSupplierDescription2` 。

|方法|说明|
|------------|-----------------|
|[GetDescription](../../../extensibility/debugger/reference/idebugportsupplierdescription2-getdescription.md)|检索端口供应商的说明和说明元数据。|

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
