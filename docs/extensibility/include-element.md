---
title: Include 元素 |Microsoft Docs
description: Include 元素指定一个文件，该文件可位于提供的包含路径上，用于插入当前文件。
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
ms.openlocfilehash: adec3a58853768a6ca4225fde58870ac66f73242
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122159303"
---
# <a name="include-element"></a>Include 元素
Include 元素指定一个文件，该文件可位于提供的包含路径上，用于插入当前文件。  所有定义的符号和类型将成为编译结果的一部分。

## <a name="syntax"></a>语法

```csharp
<Include href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|href|必需。 标头文件的路径：<br /><br /> href = "stdidcmd"|
|条件|可选。 请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|无。|无。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义所有元素，这些元素表示 VSPackage 提供给 IDE 的命令（即菜单项、菜单、工具栏和组合框）。|

## <a name="example"></a>示例

```
<Include href="PackagePlacements.vsct"/>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表 ( .vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
