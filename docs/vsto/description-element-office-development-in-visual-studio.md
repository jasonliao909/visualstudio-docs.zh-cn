---
title: '&lt;description &gt; 元素 (Office开发Visual Studio) '
description: 了解 vstov4 命名空间的 description 元素存储 COM Office对话框中显示的解决方案的说明。
titleSuffix: ''
ms.custom: secdec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- description element
- <description> element
- application manifests [Office development in Visual Studio], <description> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 24377ea58285a87372a590b267ad3301e5bd4d284879cfb44337e0beaaa3cb2c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121268399"
---
# <a name="ltdescriptiongt-element-office-development-in-visual-studio"></a>&lt;description &gt; 元素 (Office开发Visual Studio) 
  `description` 命名空间的 `vstov4` 元素会存储在 Microsoft Office 应用程序的 COM 加载项对话框中显示的 Office 解决方案说明。

## <a name="syntax"></a>语法

```xml
<description>
</description>
```

## <a name="elements-and-attributes"></a>元素和属性
 可选。 `description` 元素位于 `vstov4` 命名空间中。 它包含在 Microsoft Office 应用程序中的 COM 加载项对话框中显示的加载项说明。

 `description` 元素没有属性或元素。

## <a name="vsto-add-in-example"></a>VSTO外接程序示例

### <a name="description"></a>说明
 下面的代码示例演示使用 `description` 部署的应用程序级解决方案的 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]元素。 此代码示例是应用程序清单中为解决方案 提供Office[的一部分](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstov4:description>
  ContosoOutlookAddIn - Outlook add-in
  created with Visual Studio Tools for Office
</vstov4:description>
```

## <a name="see-also"></a>另请参阅

- [解决方案的应用程序Office清单](../vsto/application-manifests-for-office-solutions.md)
- [解决方案部署Office清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)