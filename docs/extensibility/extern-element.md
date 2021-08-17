---
title: Extern 元素|Microsoft Docs
description: Extern 元素引用任何外部标头 (.h) 文件，以在编译时与 .vsct 文件合并。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- Extern
helpviewer_keywords:
- VSCT XML schema elements, Extern
- Extern element (VSCT XML schema)
ms.assetid: db6c3ddd-a1ba-450a-897a-bb568a5377fc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 22f10cb94421d891f62bc5e57769e740e25dc05089c7dd442a145ebd1077b060
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401786"
---
# <a name="extern-element"></a>Extern 元素
Extern 元素引用 *.h* (的任何) 标头，以在编译时与 *.vsct* 文件合并。 要合并的文件必须位于给定给 VSCT 编译器的 Include 路径上，或由 Include 元素 [引用](../extensibility/include-element.md)。 这些文件可能是其他 *.vsct* 文件或 C++ 头文件。

 头文件中的定义必须格式为"#define [Symbol] [Value]"，如果该值以前已定义，则该值可能是另一个符号。 定义可用于命令项的条件语句。 将放弃实际未使用的任何符号。

 CommandTable 元素 Extern 元素

## <a name="syntax"></a>语法

```xml
<Extern href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|href|必需。 头文件的路径：<br /><br /> href="stdidcmd.h"|
|条件|可选。 请参阅 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|
|语言|可选。 命令表中所有 [\<Strings>](../extensibility/strings-element.md) 元素的默认语言：<br /><br /> language="en-us"|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|无。|无。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示 VSPackage 向 IDE 提供的命令（即菜单项、菜单、工具栏和组合框）的所有元素。|

## <a name="example"></a>示例

```xml
<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-
  18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <Extern href="C:\VSCore\vscommon\inc\vsshlids.h"/>
    ...
  <Commands package="guidMyPackage">
</CommandTable>
```

## <a name="see-also"></a>请参阅
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSPackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
