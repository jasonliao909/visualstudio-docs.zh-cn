---
title: 符号提供程序接口|Microsoft Docs
description: 本文链接到适用于 Visual Studio SDK 的符号处理接口的说明，这些接口在中断模式下评估调用堆栈中的变量。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- interfaces, symbol handler
- symbol handler, interfaces
- symbol handler, evaluating variables
ms.assetid: 4201f10e-c9f7-4b38-bb45-40fe0082d5bf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: c686b87346487d452a166d41b94a4a8b17d3e82d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122117964"
---
# <a name="symbol-provider-interfaces"></a>符号提供程序接口
下面是 的符号处理接口 [!INCLUDE[vsipsdk](../../../extensibility/includes/vsipsdk_md.md)] 。

## <a name="discussion"></a>讨论 (Discussion)
 这些接口用于在中断模式期间计算调用堆栈中的变量。 它们仅针对 SP (公共语言运行时) 。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)|SP|表示项的地址。|
|[IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md)|SP|表示项的地址，提供对进程 ID 的访问权限。|
|[IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)|SP|表示数组符号或数组类型。|
|[IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)|SP|表示类符号或类类型。|
|[IDebugComPlusSymbolProvider](../../../extensibility/debugger/reference/idebugcomplussymbolprovider.md)|SP|表示具有特定于托管代码的方法的 COM+ 符号提供程序。|
|[IDebugComPlusSymbolProvider2](../../../extensibility/debugger/reference/idebugcomplussymbolprovider2.md)|SP|表示 COM+ 符号提供程序，其方法特定于托管代码并扩展了 **IDebugComPlusSymbolProvider**。|
|[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)|SP|表示一个符号或类型，该符号或类型是其他符号或类型的容器。|
|[IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)|SP|表示可附加到符号的自定义属性。|
|[IDebugCustomAttributeQuery](../../../extensibility/debugger/reference/idebugcustomattributequery.md)|SP|表示对方法或类型上的自定义属性的查询。|
|[IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)|SP|提供对符号上的自定义属性的访问。|
|[IDebugDynamicField](../../../extensibility/debugger/reference/idebugdynamicfield.md)|SP|可在运行时确定的任何类型的基接口。|
|[IDebugDynamicFieldCOMPlus](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus.md)|SP|表示 [IDebugBinder 对象的动态](../../../extensibility/debugger/reference/idebugbinder.md) 字段。|
|[IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)|SP|表示枚举类型。|
|[IDebugExtendedField](../../../extensibility/debugger/reference/idebugextendedfield.md)|Sp|扩展可用字段的类型以支持托管代码泛型。|
|[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)|SP|所有字段的基类;表示符号或类型的说明。|
|[IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)|SP|表示托管代码泛型类型的字段的定义。|
|[IDebugGenericFieldInstance](../../../extensibility/debugger/reference/idebuggenericfieldinstance.md)|SP|表示托管代码泛型类型的字段的实例。|
|[IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)|SP|表示托管代码泛型类型的参数。|
|[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)|SP|表示方法。|
|[IDebugModOpt](../../../extensibility/debugger/reference/idebugmodopt.md)|SP|表示调试可选修饰符。|
|[IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)|SP|表示指针。|
|[IDebugPrimitiveTypeField](../../../extensibility/debugger/reference/idebugprimitivetypefield.md)|SP|表示来自 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口的基元类型枚举值。|
|[IDebugPropertyField](../../../extensibility/debugger/reference/idebugpropertyfield.md)|SP|表示可获取或设置的托管代码类的属性。|
|[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)|SP|表示提供符号和类型的符号提供程序。|
|[IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)|SP|表示直接访问元数据和核心符号接口的符号提供程序。|
|[IDebugTypeFieldBuilder](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md)|SP|表示创建表示类型的字段的能力。|
|[IDebugTypeFieldBuilder2](../../../extensibility/debugger/reference/idebugtypefieldbuilder2.md)|SP|扩展 **IDebugTypeFieldBuilder，** 以创建数组类型。|
|[IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)|SP|表示 [IDebugAddress 对象](../../../extensibility/debugger/reference/idebugaddress.md) 的集合。|
|[IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)|SP|表示 [IDebugCustomAttribute 对象](../../../extensibility/debugger/reference/idebugcustomattribute.md) 的集合。|
|[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)|SP|表示 [IDebugField 对象](../../../extensibility/debugger/reference/idebugfield.md) 的集合。|

## <a name="see-also"></a>请参阅
- [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
