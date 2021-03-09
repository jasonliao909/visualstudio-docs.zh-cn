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
ms.workload:
- office
ms.openlocfilehash: e45fd9e6385388b9c6bc32098cf59799618d511b
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2021
ms.locfileid: "102469705"
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
