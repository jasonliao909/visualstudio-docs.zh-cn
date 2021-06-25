---
title: 定义元素|Microsoft Docs
description: Define 元素定义符号名称和值对。 此符号可以通过条件属性计算。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Define
- Define element (VSCT XML schema)
ms.assetid: 5aee74e3-de41-4dc6-9618-93e158af56dd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 409621410db727f933e41bae894f125dc877b4c2
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898040"
---
# <a name="define-element"></a>定义元素
定义符号名称和值对。 此符号可以通过条件属性计算。 有关详细信息，请参阅 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。 另请参阅 [Symbols 元素](../extensibility/symbols-element.md)。

## <a name="syntax"></a>语法

```
<Define name="Mode" value="Standard" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|name|必需。 符号的名称：<br /><br /> name="Mode"|
|值|必需。 符号的值：<br /><br /> value="Standard"|
|条件|可选。 有关详细信息，请参阅 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示 VSPackage 向集成开发环境提供的命令的所有元素 (IDE) 。 例如，菜单项、菜单、工具栏和组合框。|

## <a name="example"></a>示例

```
<Define name="DEMO_UI"/>
<Define name="MODE" value="Standard"/>
```

## <a name="see-also"></a>另请参阅
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
