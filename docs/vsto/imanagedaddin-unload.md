---
title: IManagedAddin::Unload
description: 只在托管 VSTO 外接程序卸载之前调用。
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Unload method
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: f877150a747984d0d04f779b16338d04fd55f1ba
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602228"
---
# <a name="imanagedaddinunload"></a>IManagedAddin::Unload
  只在托管 VSTO 外接程序卸载之前调用。

## <a name="syntax"></a>语法

```csharp
HRESULT Unload();
```

## <a name="return-value"></a>返回值
 HRESULT 值，指示方法是否已成功完成。

## <a name="remarks"></a>备注
 当前版本的 Microsoft Office 不调用此方法。 此方法保留供将来使用。

## <a name="see-also"></a>另请参阅
- [IManagedAddin 接口](../vsto/imanagedaddin-interface.md)
- [IManagedAddin::Load](../vsto/imanagedaddin-load.md)
