---
title: '&lt;&gt;Visual Studio 中 Office 开发 (说明元素) '
description: 了解 "vstov4" 命名空间的 description 元素存储 "COM 外接程序" 对话框中显示的 Office 解决方案的描述。
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
ms.openlocfilehash: 8c20ccff5941fc03bec7aac314f680912b45da7d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122038053"
---
# <a name="ltdescriptiongt-element-office-development-in-visual-studio"></a>&lt;&gt;Visual Studio 中 Office 开发 (说明元素) 
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
 下面的代码示例演示使用 `description` 部署的应用程序级解决方案的 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]元素。 此代码示例是[Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

### <a name="code"></a>代码

```xml
<vstov4:description>
  ContosoOutlookAddIn - Outlook add-in
  created with Visual Studio Tools for Office
</vstov4:description>
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)