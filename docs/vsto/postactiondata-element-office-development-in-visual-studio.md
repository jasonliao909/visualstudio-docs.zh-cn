---
title: '&lt;postActionData &gt; 元素 (Office开发) '
description: vstav3 命名空间的 postActionData 元素指定与安装解决方案后运行的任何部署Office关联的数据。
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- <postActionData> element
- application manifests [Office development in Visual Studio], <postActionData> element
- postActionData element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 4196c3061372d46a2fad4c2b46ff8c1fe4ee2b39
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122025883"
---
# <a name="ltpostactiondatagt-element-office-development"></a>&lt;postActionData &gt; 元素 (Office开发) 
  `postActionData` 命名空间的 `vstav3` 元素指定与任何部署后操作关联的数据，这些操作在 Office 解决方案安装后运行。

## <a name="syntax"></a>语法

```xml
<postActionData>
</postActionData>
```

## <a name="elements-and-attributes"></a>元素和属性
 `postActionData` 元素是可选的且位于 `vstav3` 命名空间中。 每个部署后操作的应用程序清单中只定义了一个 `postActionData` 元素。

 `postActions` 元素没有属性。

 `postActions` 无子元素。

## <a name="post-deployment-action-example"></a>部署后操作示例

### <a name="description"></a>说明
 下面的代码示例演示 Office 解决方案的应用程序清单中的 `postAction` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例是应用程序清单中为解决方案 提供Office[的一部分](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstav3:postActionData>
  data in any format
</vstav3:postActionData>
```

## <a name="see-also"></a>请参阅

- [解决方案的应用程序Office清单](../vsto/application-manifests-for-office-solutions.md)
- [解决方案部署Office清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)
