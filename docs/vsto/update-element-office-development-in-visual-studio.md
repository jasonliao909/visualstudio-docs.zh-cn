---
title: '&lt;update &gt; 元素 (Office开发Visual Studio) '
description: update 元素指定解决方案检查更新的时间间隔。
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- update element
- <update> element
- application manifests [Office development in Visual Studio], <update> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 35f082a176c958ea40539fac594f1119405de819b7ab054f4c51010aff2044a3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121365921"
---
# <a name="ltupdategt-element-office-development-in-visual-studio"></a>&lt;update &gt; 元素 (Office开发Visual Studio) 
  `update`元素指定解决方案检查更新的时间间隔。

## <a name="syntax"></a>语法

```xml
<update
  enabled>
  <expiration
    maximumAge
    unit
  />
</update>
```

## <a name="elements-and-attributes"></a>元素和属性
 `update` 元素是必需的，它位于 `vstav3` 命名空间中。

 `update` 元素具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`enabled`|必需。 将 enabled 设置为以下值之一：<br /><br /> -   若要检查更新，为 **true。**<br />-   **false** 可阻止检查更新。|

 `update` 元素具有以下子元素。

### <a name="expiration"></a>expiration
 `expiration` 元素是必需的，它位于 `vstav3` 命名空间中。 此元素指定解决方案检查更新的时间间隔。

 `expiration` 元素具有以下属性。

|Attribute|说明|
|---------------|-----------------|
|`maximumAge`| 必需。 将此 设置为整数。|
|`unit`|必需。 将 `unit` 设置为以下值之一：<br /><br /> -   **小时**<br />-   **天**<br />-   **星期**|

## <a name="example-of-always-checking-for-updates"></a>始终检查更新的示例

### <a name="description"></a>说明
 下面的代码示例演示一个元素，该元素 `update` 设置为始终检查解决方案中的Office。

### <a name="code"></a>代码

```xml
<vstav3:update enabled="true" />
```

## <a name="example-of-setting-a-default-update-interval"></a>设置默认更新间隔的示例

### <a name="description"></a>说明
 下面的代码示例演示了 `update` 应用程序清单中用于解决方案Office元素。 此代码示例是应用程序清单中为解决方案 提供Office[的一部分](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstav3:update enabled="true">
    <vstav3:expiration maximumAge="7" unit="days" />
</vstav3:update>
```

## <a name="see-also"></a>另请参阅

- [使用 Office 部署 ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [解决方案的应用程序Office清单](../vsto/application-manifests-for-office-solutions.md)
- [解决方案部署Office清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)
