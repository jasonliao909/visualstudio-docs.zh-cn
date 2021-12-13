---
title: IManagedAddin::Load
description: 在加载托管 VSTO 外接程序时调用。
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords: ''
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 6315d434f83974365059f7d828b6aa04a40960f6
ms.sourcegitcommit: 0f2af2f1a8cf0a481fd8f673accf3aebf2e262c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2021
ms.locfileid: "134713637"
---
# <a name="imanagedaddinload"></a>IManagedAddin::Load
  在加载托管 VSTO 外接程序时调用。

## <a name="syntax"></a>语法

```csharp
HRESULT Load([in] BSTR bstrManifestURL,
             [in] IDispatch *pdispApplication);
```

### <a name="parameters"></a>parameters

|参数|说明|
|---------------|-----------------|
|*bstrManifestURL*|VSTO 外接程序清单的完整路径。|
|*pdispApplication*|指向 IDispatch 的指针，该指针表示正在加载 VSTO 外接程序的主机应用程序。|

## <a name="return-value"></a>返回值
 HRESULT 值，指示方法是否已成功完成。

## <a name="remarks"></a>备注
 清单是一个文件（通常是 XML 文件），提供用于帮助加载 VSTO 外接程序的信息。 例如，加载 VSTO 外接程序时，清单可以指定 VSTO 外接程序程序集的位置以及要实例化的入口点类。

 *bstrManifestURL* 参数包含 `Manifest` VSTO 外接程序 **HKEY_CURRENT_USER\Software\Microsoft\Office\\ _\<application name>_ \Addins \\ _\<add-in ID>_** 注册表项下的项的值。 有关详细信息，请参阅 [IManagedAddin 接口](../vsto/imanagedaddin-interface.md)。

 实现 [IManagedAddIn::Load](../vsto/imanagedaddin-load.md) 方法以执行各项任务，例如为正在加载的 VSTO 外接程序配置应用程序域和安全策略。

## <a name="see-also"></a>另请参阅
- [IManagedAddin Interface](../vsto/imanagedaddin-interface.md)
- [IManagedAddin::Unload](../vsto/imanagedaddin-unload.md)
