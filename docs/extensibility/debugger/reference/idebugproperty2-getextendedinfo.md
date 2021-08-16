---
description: 获取属性的扩展信息。
title: IDebugProperty2：： GetExtendedInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetExtendedInfo
helpviewer_keywords:
- IDebugProperty2::GetExtendedInfo
ms.assetid: 0c9c0b2b-7540-4424-adb5-fce7aa37a026
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 996e470d3ee61efde790d95adc367d9b1b86688c4df64cefae9384e0a657d050
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121449048"
---
# <a name="idebugproperty2getextendedinfo"></a>IDebugProperty2::GetExtendedInfo
获取属性的扩展信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetExtendedInfo ( 
   REFGUID* guidExtendedInfo,
   VARIANT* pExtendedInfo
);
```

```csharp
int GetExtendedInfo ( 
   ref Guid guidExtendedInfo,
   out object pExtendedInfo
);
```

## <a name="parameters"></a>参数
`guidExtendedInfo`\
中确定要检索的扩展信息的类型的 GUID。 有关详细信息，请参阅“备注”。

`pExtendedInfo`\
弄返回 `VARIANT` (c + +) 或对象 (c # ) ，该对象可用于检索扩展属性信息。 例如，此参数可能会返回一个 `IUnknown` 接口，该接口可用于查询 [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md) 接口。 有关详细信息，请参阅“备注”。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `S_GETEXTENDEDINFO_NO_EXTENDEDINFO`如果没有要检索的扩展信息，则返回。

## <a name="remarks"></a>备注
 此方法的目的在于检索不会通过调用 [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 方法来检索的信息。

 此方法通常会识别以下 Guid (为 c # 指定了 GUID 值，因为该名称在任何程序集) 中都不可用。 可以创建其他 Guid 供内部使用。

|名称|GUID|描述|
|----------|----------|-----------------|
|guidDocument|{3f98de84-fee9-11d0-b47f-00a0244a1dd2}|返回 `IUnknown` 文档的接口。 通常，可从此接口获取 [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md) 接口 `IUnknown` 。|
|guidCodeContext|{e2fc65e-56ce-11d1-b528-00aax004a8797}|返回 `IUnknown` 文档上下文的接口。 通常，可从此接口获取 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) 接口 `IUnknown` 。|
|guidCustomViewerSupported|{d9c9da31-ffbe-4eeb-9186-23121e3c088c}|返回一个字符串，该字符串包含自定义查看器的 CLSID，通常由表达式计算器实现。|
|guidExtendedInfoSlot|{6df235ad-82c6-4292-9c97-7389770bc42f}|如果此属性表示托管代码本地地址，则返回一个表示所需槽号的32位数字。|
|guidExtendedInfoSignature|{b5fb6d46-f805-417f-96a3-8ba737073ffd}|返回一个字符串，该字符串包含与属性对象关联的变量的签名。|

## <a name="see-also"></a>另请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
