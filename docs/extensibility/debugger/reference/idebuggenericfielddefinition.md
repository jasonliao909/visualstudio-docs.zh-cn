---
description: 表示托管代码泛型类型的字段定义。
title: IDebugGenericFieldDefinition |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugGenericFieldDefinition interface
ms.assetid: b5a853b7-221e-4d62-8948-07423089d75d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 2adea2605acb71969f369228d073ba4b13e53a46
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122111003"
---
# <a name="idebuggenericfielddefinition"></a>IDebugGenericFieldDefinition
表示托管代码泛型类型的字段定义。

## <a name="syntax"></a>语法

```
IDebugGenericFieldDefinition : IUnknown
```

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[ConstructInstantiation](../../../extensibility/debugger/reference/idebuggenericfielddefinition-constructinstantiation.md)|给定类型参数的数组，构造一个字段实例。|
|[GetFormalTypeParams](../../../extensibility/debugger/reference/idebuggenericfielddefinition-getformaltypeparams.md)|根据参数的数量检索类型参数。|
|[TypeParamCount](../../../extensibility/debugger/reference/idebuggenericfielddefinition-typeparamcount.md)|检索与泛型字段关联的类型参数的数目。|

## <a name="requirements"></a>要求
 标头： Sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
