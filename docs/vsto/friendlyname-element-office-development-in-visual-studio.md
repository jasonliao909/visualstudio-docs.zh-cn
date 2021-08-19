---
description: vstov4 命名空间的 friendlyName 元素存储已安装程序列表中显示的名称。
title: '&lt;friendlyName &gt; 元素 (Office Visual Studio) '
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
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 887c28cdd81f4f3176dcf29804fa9f6ec4b27123
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083604"
---
# <a name="ltfriendlynamegt-element-office-development-in-visual-studio"></a>&lt;friendlyName &gt; 元素 (Office Visual Studio) 
  `friendlyName` 命名空间的 `vstov4` 元素存储已安装程序列表中出现的名称。

## <a name="syntax"></a>语法

```xml
<friendlyName>
</friendlyName>
```

## <a name="elements-and-attributes"></a>元素和属性
 `friendlyName` 元素位于 `vstov4` 命名空间中。 值出现在计算机中已安装程序列表中和 Microsoft Office 应用程序的 COM VSTO 外接程序对话框中。

 `friendlyName` 元素没有属性或子元素。

## <a name="vsto-add-in-example"></a>VSTO外接程序示例

### <a name="description"></a>说明
 下面的代码示例演示使用 `friendlyName` 部署的应用程序级解决方案的 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]元素。 此代码示例是应用程序清单中为解决方案 提供Office[的一部分](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstov4:friendlyName>
  ContosoOutlookAddIn
</vstov4:friendlyName>
```

## <a name="see-also"></a>请参阅

- [解决方案的应用程序Office清单](../vsto/application-manifests-for-office-solutions.md)
- [解决方案部署Office清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)
