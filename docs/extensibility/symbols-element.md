---
title: Symbols 元素|Microsoft Docs
description: Symbols 元素定义其他 VSCT 元素使用的 GUID 和 ID。 本文包含一个示例。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Symbols element (VSCT XML schema)
- VSCT XML schema elements, Symbols
ms.assetid: 1cda43d8-42a5-4b1b-a3c8-cf0401c3202f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b593f353714f2fbb6f5b726fa2bbc0da449043ea
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901729"
---
# <a name="symbols-element"></a>Symbols 元素
定义其他 VSCT 元素使用的 GUID 和 ID。 对于非托管代码，此信息通常来自 [Extern 元素 指定的头文件](../extensibility/extern-element.md)。 托管代码使用 Symbols 元素的子元素来定义此信息。

 如果从现有 .cto 文件创建 .vsct 文件，符号将生成为 Symbols 元素的子元素。 有关详细信息，请参阅 [如何：创建 。现有 中的 Vsct 文件。Cto 文件](../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file)。

 Symbols 元素不应与 [Define 元素](../extensibility/define-element.md)混淆，该元素定义供预处理器使用的名称/值对。

## <a name="syntax"></a>语法

```
<Symbols>
  <GuidSymbol>... </GuidSymbol>
  <GuidSymbol>... </GuidSymbol>
</Symbols>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|描述|
|---------------|-----------------|
|无||

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|GuidSymbol|定义 GUID 符号。 GuidSymbol 具有两个必需属性：名称和值。 名称是符号的名称，值是作为字符串的 GUID 值。<br /><br /> 例如：\<GuidSymbol name="guidVsPackage1Pkg"   value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />|
|IDSymbol|定义符号。 IDSymbol 具有两个必需属性：名称和值。 名称是符号的名称，值是字符串形式符号的值。<br /><br /> 例如：\<IDSymbol name="MyMenuGroup" value="0x1020" />|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|.vsct 文件的根元素。|

## <a name="example"></a>示例

```
<Symbols>
  <GuidSymbol name="guidVsPackage1Pkg" value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />
  <GuidSymbol name="guidVsPackage1CmdSet" value="{cb9dfd7f-2fcc-4a3e-aae8-f7fe30b1cfac}">
    <IDSymbol name="MyMenuGroup" value="0x1020" />
    <IDSymbol name="cmdidMyCommand" value="0x0100" />
    <IDSymbol name="cmdidMyTool" value="0x0101" />
  </GuidSymbol>
</Symbols>
```

## <a name="see-also"></a>另请参阅
- [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
