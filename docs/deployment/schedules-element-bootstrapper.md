---
title: '&lt;Schedules &gt; 元素 (引导程序) |Microsoft Docs'
description: Schedules 元素包含 Schedule 元素，这些元素定义运行 Command 元素定义的命令的特定时间。
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
ms.openlocfilehash: 7b7ca1fb76480738240f2c6a1240e1f243ef534c37fe8f1dd3e9dba4c5b5da10
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121435317"
---
# <a name="ltschedulesgt-element-bootstrapper"></a>&lt;Schedules &gt; 元素 (引导程序) 
`Schedules`元素包含 `Schedule` 元素，这些元素定义应运行元素定义的命令 `Command` 的特定时间。

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
 `Schedules`元素是 元素的 `Product` 子元素。 每个 `Product` 元素可能最多包含一 `Schedules` 个元素。 `Schedules` 元素没有属性。

## <a name="schedule"></a>计划
 `Schedule`元素是 元素的 `Schedules` 子元素。 元素 `Schedules` 必须至少有一 `Schedule` 个元素。

 `Schedule` 具有以下属性。

|属性|说明|
|---------------|-----------------|
|`Name`|必需。 计划项的名称。 这对应于 `ScheduleName` 元素的 `Command` 属性。 当 `Command` 引用命名计划时，它仅在该元素指示的时间 `Schedule` 执行。 计划还可以与 和 元素相关联，这两个元素 `FailIf` `BypassIf` 限制这些条件测试按指定计划执行。 有关详细信息，请参阅 [\<Commands> 元素](../deployment/commands-element-bootstrapper.md)。|

 给定 `Schedule` 元素可能正好具有以下子元素之一。

## <a name="buildlist"></a>BuildList
 `BuildList`元素指示安装程序在启动应用程序后立即执行命令。

## <a name="beforepackage"></a>BeforePackage
 `BeforePackage`元素指示安装程序在安装指定包之前执行命令。

## <a name="afterpackage"></a>AfterPackage
 `AfterPackage`元素指示安装程序在安装指定包后执行命令。

## <a name="see-also"></a>请参阅
- [\<Product> 元素](../deployment/product-element-bootstrapper.md)
- [产品和包架构参考](../deployment/product-and-package-schema-reference.md)