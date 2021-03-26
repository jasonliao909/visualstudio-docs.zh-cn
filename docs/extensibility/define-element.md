---
title: Define 元素 |Microsoft Docs
description: Define 元素定义符号名称和值对。 此符号可以通过条件属性来计算。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Define
- Define element (VSCT XML schema)
ms.assetid: 5aee74e3-de41-4dc6-9618-93e158af56dd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 83a8ee40205cafcaff29399ead4036374f798abf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082265"
---
# <a name="define-element"></a>Define 元素
定义符号名称和值对。 此符号可以通过条件属性来计算。 有关详细信息，请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。 另请参阅 [符号元素](../extensibility/symbols-element.md)。

## <a name="syntax"></a>语法

```
<Define name="Mode" value="Standard" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|name|必需。 符号名称：<br /><br /> name = "Mode"|
|value|必需。 符号的值：<br /><br /> 值 = "标准"|
|天气条件|可选。 有关详细信息，请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义所有元素，这些元素表示 VSPackage 提供给集成开发环境 (IDE) 的命令。 例如，菜单项、菜单、工具栏和组合框。|

## <a name="example"></a>示例

```
<Define name="DEMO_UI"/>
<Define name="MODE" value="Standard"/>
```

## <a name="see-also"></a>另请参阅
- [Visual Studio 命令表 ( .vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
