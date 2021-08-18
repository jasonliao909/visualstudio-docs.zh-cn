---
description: vstov4 命名空间的文档元素存储文档级自定义项的自定义特定信息。
title: '&lt;document &gt; 元素 (Office开发Visual Studio) '
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document element
- application manifests [Office development in Visual Studio], <document> element
- <document> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 66ef774db63c01a1b622c6ea937bd29444bc3d71
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122148293"
---
# <a name="ltdocumentgt-element-office-development-in-visual-studio"></a>&lt;document &gt; 元素 (Office开发Visual Studio) 
  `document`命名空间的 `vstov4` 元素存储文档级自定义项的自定义特定信息。

## <a name="syntax"></a>语法

```xml
<document solutionId />
```

## <a name="elements-and-attributes"></a>元素和属性
 仅文档级自定义项是必需的。 `document` 元素位于 `vstov4` 命名空间中。 `document` 元素具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`solutionId`|必需。 运行时用于唯Visual Studio Tools for Office文档级解决方案的 GUID。 此值存储为自定义_AssemblyLocation属性。 有关详细信息，请参阅自定义 [文档属性概述](../vsto/custom-document-properties-overview.md)。|

 `document` 无子元素。

## <a name="document-level-customization-example"></a>文档级自定义示例

### <a name="description"></a>说明
 下面的代码示例演示使用 部署的文档 `document` Office解决方案中的 元素 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 。 此代码示例是应用程序清单中为解决方案 提供Office[的一部分](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstov4:document
  solutionId="73e" />
```

## <a name="see-also"></a>请参阅

- [解决方案的应用程序Office清单](../vsto/application-manifests-for-office-solutions.md)
- [解决方案部署Office清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)
