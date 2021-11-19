---
title: '&lt;Schedules&gt; 元素（引导程序）| Microsoft Docs'
description: Schedules 元素包含一些 Schedule 元素，这些元素定义运行 Command 元素定义的命令的特定时间。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <Schedules> element [bootstrapper]
ms.assetid: 28d094cf-64f5-42b1-bd8a-3697082aab4f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 8f9430dd814ba76f0a8e688d6a198c8715fc4d99
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601001"
---
# <a name="ltschedulesgt-element-bootstrapper"></a>&lt;Schedules&gt; 元素（引导程序）
`Schedules` 元素包含一些 `Schedule` 元素，这些元素定义运行 `Command` 元素定义的命令的特定时间。

## <a name="syntax"></a>语法

```xml
<Schedules>
    <Schedule
        Name
    >
        <BuildList />
        <BeforePackage />
        <AfterPackage />
    </Schedule>
</Schedules>
```

## <a name="elements-and-attributes"></a>元素和属性
 `Schedules` 元素是 `Product` 元素的一个子元素。 每个 `Product` 元素最多只能有一个 `Schedules` 元素。 `Schedules` 元素没有属性。

## <a name="schedule"></a>计划
 `Schedule` 元素是 `Schedules` 元素的一个子元素。 一个 `Schedules` 元素必须至少有一个 `Schedule` 元素。

 `Schedule` 具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Name`|必需。 计划项的名称。 它与 `Command` 元素的 `ScheduleName` 属性对应。 当 `Command` 引用命名计划时，它将仅在 `Schedule` 元素指示的时间执行。 计划也可能与 `FailIf` 和 `BypassIf` 元素相关联，这两个元素将这些条件测试限制为按指定的计划执行。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|

 给定的 `Schedule` 元素可以正好具有以下子元素之一。

## <a name="buildlist"></a>BuildList
 `BuildList` 元素指示安装程序在开始启动应用程序后立即执行命令。

## <a name="beforepackage"></a>BeforePackage
 `BeforePackage` 元素指示安装程序在安装指定包之前执行命令。

## <a name="afterpackage"></a>AfterPackage
 `AfterPackage` 元素指示安装程序在安装指定包之后执行命令。

## <a name="see-also"></a>另请参阅
- [\<Product> 元素](../deployment/product-element-bootstrapper.md)
- [产品和包架构引用](../deployment/product-and-package-schema-reference.md)