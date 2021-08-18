---
title: Include 元素|Microsoft Docs
description: Include 元素指定一个文件，该文件可以位于提供的 include 路径上，以插入到当前文件中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- Include
helpviewer_keywords:
- Include element (VSCT XML schema)
- VSCT XML schema elements, Include
ms.assetid: c923dfe6-084a-4105-aec1-f0a3f8399c54
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: d6e8579bbe71e1229f553a4618eae30588b1e15e7d8182716b25c0011fe17845
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359827"
---
# <a name="include-element"></a>Include 元素
Include 元素指定一个文件，该文件可以位于提供的 include 路径上，以插入到当前文件中。  定义的所有符号和类型将成为编译结果的一部分。

## <a name="syntax"></a>语法

```csharp
<Include href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|href|必需。 头文件的路径：<br /><br /> href="stdidcmd.h"|
|条件|可选。 请参阅 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|无。|无。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示 VSPackage 向 IDE 提供的命令（即菜单项、菜单、工具栏和组合框）的所有元素。|

## <a name="example"></a>示例

```
<Include href="PackagePlacements.vsct"/>
```

## <a name="see-also"></a>请参阅
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
