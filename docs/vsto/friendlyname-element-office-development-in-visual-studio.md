---
description: Vstov4 命名空间的 friendlyName 元素存储已安装程序列表中显示的名称。
title: '&lt;&gt; (Visual Studio 中的 Office 开发) 的 friendlyName 元素'
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <friendlyName> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: adcf46a2c232176026181283549c0c59fc713603
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223441"
---
# <a name="ltfriendlynamegt-element-office-development-in-visual-studio"></a>&lt;&gt; (Visual Studio 中的 Office 开发) 的 friendlyName 元素
  `friendlyName` 命名空间的 `vstov4` 元素存储已安装程序列表中出现的名称。

## <a name="syntax"></a>语法

```xml
<friendlyName>
</friendlyName>
```

## <a name="elements-and-attributes"></a>元素和属性
 `friendlyName` 元素位于 `vstov4` 命名空间中。 值出现在计算机中已安装程序列表中和 Microsoft Office 应用程序的 COM VSTO 外接程序对话框中。

 `friendlyName` 元素没有属性或子元素。

## <a name="vsto-add-in-example"></a>VSTO 外接程序示例

### <a name="description"></a>描述
 下面的代码示例演示使用 `friendlyName` 部署的应用程序级解决方案的 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]元素。 此代码示例是 [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)中提供的一个更大示例的一部分。

### <a name="code"></a>代码

```xml
<vstov4:friendlyName>
  ContosoOutlookAddIn
</vstov4:friendlyName>
```

## <a name="see-also"></a>请参阅

- [Office 解决方案的应用程序清单](../vsto/application-manifests-for-office-solutions.md)
- [Office 解决方案的部署清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
