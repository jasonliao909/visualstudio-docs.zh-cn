---
title: '&lt;&gt;Visual Studio 中的 v 元素 (Office 开发) '
titleSuffix: ''
description: Vstav3 命名空间的 v 元素包含特定 Office 解决方案的受支持的 Visual Studio Tools for Office 运行时版本。
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <vstoRuntime> element
- <vstoRuntime> element
- vstoRuntime element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7c856836bd2ba107a2fa6c3017c5ecb2694fcf6b
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2021
ms.locfileid: "102468567"
---
# <a name="ltvstoruntimegt-element-office-development-in-visual-studio"></a>&lt;&gt;Visual Studio 中的 v 元素 (Office 开发) 
  `vstoRuntime` 命名空间的 `vstav3` 元素包含针对特定 Office 解决方案的受支持的 Visual Studio Tools for Office Runtime 版本。

## <a name="syntax"></a>语法

```xml
<vstoRuntime
    release
    version
    supportUrl />
```

## <a name="elements-and-attributes"></a>元素和属性
 `vstoRuntime` 元素是必需的，它位于 `vstav3` 命名空间中。 如果 Office 解决方案支持两个版本的 Visual Studio Tools for Office Runtime，则应用程序清单中存在两个 `vstoRuntime` 元素。

 `vstoRuntime` 元素具有以下属性。

|属性|说明|
|---------------|-----------------|
|`release`|必需。 Visual Studio Tools for Office Runtime 的发布版本。|
|`version`|必需。 Visual Studio Tools for Office Runtime 的版本号。|
|`supportUrl`|可选。 指向 Visual Studio Tools for Office Runtime 安装位置的链接。|

 `vstoRuntime` 不包含任何元素。

## <a name="example"></a>示例：
 下面的代码示例演示 Office 解决方案的应用程序清单中的 `vstoRuntime` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例是 [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

```xml
<vstav3:vstoRuntime
    release="VSTOR40Beta1"
    version="10.0.20303"
    supportUrl="http://www.microsoft.com" />
```

## <a name="see-also"></a>另请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
