---
title: '&lt;customHostSpecified &gt; 元素 (Office开发Visual Studio) '
description: 了解 customHostSpecified 元素如何指示此解决方案不是独立应用程序。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <customHostSpecified> element
- <customHostSpecified> element
- customHostSpecified element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 9c2e9595b3ff10c1769aa1546637fd6743b27358
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122148319"
---
# <a name="ltcustomhostspecifiedgt-element-office-development-in-visual-studio"></a>&lt;customHostSpecified &gt; 元素 (Office开发Visual Studio) 
  `customHostSpecified`元素指示此解决方案不是独立应用程序。 Office解决方案包含托管在应用程序内部Microsoft Office组件。

## <a name="syntax"></a>语法

```xml
<customHostSpecified />
```

## <a name="elements-and-attributes"></a>元素和属性
 `customHostSpecified`元素是解决方案Office项。 此元素位于 命名空间中，并指定此部署包含一个组件，该组件将部署在自定义主机内部， `co.v1` 而不是独立应用程序。

 此元素是应用程序清单中第 `<entrypoint>` 一个元素的子元素。 该元素中不能有其他子 `<entrypoint>` 元素， [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 否则将在安装过程中引发验证错误。

 此元素没有属性，也没有子元素。

## <a name="example"></a>示例
 下面的代码示例演示了解决方案 `customHostSpecified` 的应用程序清单中的 Office 元素。 此代码示例是应用程序清单中为解决方案 提供Office[的一部分](../vsto/application-manifests-for-office-solutions.md)。

```xml
<entryPoint>
    <co.v1:customHostSpecified />
</entryPoint>
```

## <a name="see-also"></a>请参阅

- [解决方案的应用程序Office清单](../vsto/application-manifests-for-office-solutions.md)
- [解决方案部署Office清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)