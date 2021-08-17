---
description: 获取 属性的扩展信息。
title: IDebugProperty2：：GetExtendedInfo |Microsoft Docs
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
ms.openlocfilehash: 97649d53ce7f5b0e44d084003de165207d6fcebe
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122071306"
---
# <a name="idebugproperty2getextendedinfo"></a>IDebugProperty2::GetExtendedInfo
获取 属性的扩展信息。

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
[in]GUID，确定要检索的扩展信息的类型。 有关详细信息，请参阅“备注”。

`pExtendedInfo`\
[out]返回 (C#) 的 C++ (或对象) 可用于检索 `VARIANT` 扩展属性信息。 例如，此参数可能返回一个 `IUnknown` 接口，该接口可以查询 [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md) 接口。 有关详细信息，请参阅“备注”。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 如果没有 `S_GETEXTENDEDINFO_NO_EXTENDEDINFO` 要检索的扩展信息，则返回 。

## <a name="remarks"></a>备注
 存在此方法的目的是检索信息，而该信息本身无法通过调用 [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) 方法进行检索。

 此方法通常可识别以下 GUID， (为 C# 指定 GUID 值，因为名称在任何程序集中) 。 可创建其他 GUID 供内部使用。

|名称|GUID|描述|
|----------|----------|-----------------|
|guidDocument|{3f98de84-fee9-11d0-b47f-00a0244a1dd2}|返回 `IUnknown` 文档的接口。 通常 [，IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md) 接口可以从此接口 `IUnknown` 获取。|
|guidCodeContext|{e2fc65e-56ce-11d1-b528-00aax004a8797}|返回 `IUnknown` 文档上下文的接口。 通常 [，IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) 接口可以从此接口 `IUnknown` 获取。|
|guidCustomViewerSupported|{d9c9da31-ffbe-4eeb-9186-23121e3c088c}|返回一个字符串，该字符串包含通常由表达式计算程序实现的自定义查看器的 CLSID。|
|guidExtendedInfoSlot|{6df235ad-82c6-4292-9c97-7389770bc42f}|如果此属性表示托管代码本地地址，则返回表示所需槽号的 32 位数字。|
|guidExtendedInfoSignature|{b5fb6d46-f805-417f-96a3-8ba737073ffd}|返回一个字符串，该字符串包含与属性对象关联的变量的签名。|

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
