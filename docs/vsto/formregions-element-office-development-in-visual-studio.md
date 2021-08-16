---
description: vstov4 命名空间的 formRegions 元素包含Microsoft Office Outlook外接程序关联的VSTO区域。
title: '&lt;formRegions &gt; 元素 (Office开发Visual Studio) '
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formRegions element
- <formRegions> element
- application manifests [Office development in Visual Studio], <formRegions> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: e1a4439f5c1dab78ce32c553a4bee98db6fa7da4f072152c3a046ba819222128
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121440859"
---
# <a name="ltformregionsgt-element-office-development-in-visual-studio"></a>&lt;formRegions &gt; 元素 (Office开发Visual Studio) 
  `formRegions`命名空间的 `vstov4` 元素包含Microsoft Office Outlook外接程序关联的窗体VSTO区域。

## <a name="syntax"></a>语法

```xml
<formRegions>
  <formRegion>
  </formRegion>
</formRegions>
```

## <a name="elements-and-attributes"></a>元素和属性
 `formRegions` 命名空间的 `vstov4` 元素包含 Outlook VSTO 外接程序的所有 `formRegion` 元素。 只有包括窗体区域的 Outlook VSTO 外接程序才需要该元素。

 在应用程序清单中定义的 `formRegions` 元素可能只有一个。

 `formRegions` 元素没有属性。

 `formRegions` 元素具有以下元素。

### <a name="formregion"></a>formRegion
 为包含窗体区域的 Outlook VSTO 外接程序所需。 元素 `formRegion` 在&#60;[formRegion&#62; &#40;Office中Visual Studio&#41;。 ](../vsto/formregion-element-office-development-in-visual-studio.md)

## <a name="vsto-add-in-example"></a>VSTO外接程序示例

### <a name="description"></a>说明
 下面的代码示例演示应用程序级 Office 解决方案的应用程序清单中的 `formRegions` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例是应用程序清单中为解决方案 提供Office[的一部分](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstov4:formRegions>
  <vstov4:formRegion
      name="OutlookAddIn1.FormRegion1">
    <vstov4:messageClass name="IPM.Note" />
    <vstov4:messageClass name="IPM.Contact" />
    <vstov4:messageClass name="IPM.Appointment" />
  </vstov4:formRegion>
</vstov4:formRegions>
```

## <a name="see-also"></a>另请参阅

- [解决方案的应用程序Office清单](../vsto/application-manifests-for-office-solutions.md)
- [解决方案部署Office清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)
