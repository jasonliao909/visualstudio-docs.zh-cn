---
description: 启用 Visual Studio UI 以显示 "附加到进程" 对话框的 "传输信息" 部分中的文本。
title: IDebugPortSupplierDescription2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortSupplierDescription2 interface
ms.assetid: dd19b9d6-0703-44b3-9498-cedffa0ce5b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dba3cd07bb84843ff4d2531cdde63ab9e671f961
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071917"
---
# <a name="idebugportsupplierdescription2"></a>IDebugPortSupplierDescription2
允许 UI 在 " [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] **附加到进程**" 对话框的 "**传输信息**" 部分中显示文本。

## <a name="syntax"></a>语法

```
IDebugPortSupplierDescription2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 此接口由端口供应商实现。

## <a name="methods"></a>方法
 下表显示的方法 `IDebugPortSupplierDescription2` 。

|方法|说明|
|------------|-----------------|
|[GetDescription](../../../extensibility/debugger/reference/idebugportsupplierdescription2-getdescription.md)|检索端口提供程序的说明和说明元数据。|

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
