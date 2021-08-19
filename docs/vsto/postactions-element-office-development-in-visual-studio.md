---
title: '&lt;postActions &gt; 元素 (Office开发) '
description: vstav3 命名空间的 postActions 元素包含描述部署后操作的所有 postAction 元素，这些操作在安装Office后运行。
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio], <postActions> element
- postActions element
- <postActions> element
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 9051d2a4947057eed815b234880702c198426949
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122147773"
---
# <a name="ltpostactionsgt-element-office-development"></a>&lt;postActions &gt; 元素 (Office开发) 
  `postActions` 命名空间的 `vstav3` 元素包含描述部署后操作（在安装 Office 解决方案后运行）的 `postAction` 所有元素。

## <a name="syntax"></a>语法

```xml
<postActions>
  <postAction>
    <entryPoint>
    </entryPoint>
    <postActionData>
    </postActionData>
  </postAction>
</postActions>
```

## <a name="elements-and-attributes"></a>元素和属性
 `postActions` 元素是可选的，它位于 `vstav3` 命名空间中。 在应用程序清单中定义的 `postActions` 元素只有一个。

 `postActions` 元素没有属性。

 `postActions` 具有以下元素。

### <a name="postaction"></a>postAction
 可选。 命名空间中 元素的角色在&#60;postAction&#62; `postAction` 元素&#40;Office `vstav3` [定义](../vsto/postaction-element-office-development-in-visual-studio.md)Visual Studio&#41;。

## <a name="post-deployment-action-example"></a>部署后操作示例

### <a name="description"></a>说明
 下面的代码示例演示 Office 解决方案的应用程序清单中的 `postActions` 元素，该解决方案是使用 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)]部署的。 此代码示例是应用程序清单中为解决方案 提供Office[的一部分](../vsto/application-manifests-for-office-solutions.md)。

### <a name="code"></a>代码

```xml
<vstav3:postActions>
  <vstav3:postAction>
    <vstav3:entryPoint
      class="PostDeploymentAction.PostDeploymentActionSample">
      <assemblyIdentity
        name="PostDeploymentAction"
        version="1.0.0.0"
        language="neutral"
        processorArchitecture="msil" />
    </vstav3:entryPoint>
    <vstav3:postActionData>
    </vstav3:postActionData>
  </vstav3:postAction>
</vstav3:postActions>
```

## <a name="see-also"></a>请参阅

- [解决方案的应用程序Office清单](../vsto/application-manifests-for-office-solutions.md)
- [解决方案部署Office清单](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce应用程序清单](../deployment/clickonce-application-manifest.md)
