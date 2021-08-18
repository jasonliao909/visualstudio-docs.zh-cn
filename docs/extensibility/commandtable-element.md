---
title: CommandTable 元素|Microsoft Docs
description: CommandTable 是 .vsct 文件的根元素，它定义 VSPackage 向 IDE 提供的命令的布局和类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CommandTable
helpviewer_keywords:
- CommandTable element (VSCT XML schema)
- VSCT XML schema elements, CommandTable
ms.assetid: 15c38159-660a-4ef4-9643-aa6fcfca82a9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: fe604d47cc6fcf1382bb58dd53cc8cde40cab4f7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122051256"
---
# <a name="commandtable-element"></a>CommandTable 元素
CommandTable 是 *.vsct* 文件的根元素。 此文件定义 VSPackage 向 IDE 提供的命令的实际布局和类型。 命令可能包括菜单项、菜单、工具栏和组合框。 有关详细信息，请参阅命令[Visual Studio表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

## <a name="syntax"></a>语法

```xml
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema" >
  <Extern>... </Extern>
  <Include>... </Include>
  <Define>... </Define>
  <Commands>... </Commands>
  <CommandPlacements>... </CommandPlacements>
  <VisibilityConstraints>... </VisibilityConstraints>
  <KeyBindings>... </KeyBindings>
  <UsedCommands... </UsedCommands>
  <Symbols>... </Symbols>
</CommandTable>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

| 属性 | 说明 |
|-----------| - |
| xmlns | 必需。 XML 命名空间：<br /><br /> `xmlns=http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable`<br /><br /> xmlns：xs=" <http://www.w3.org/2001/XMLSchema> " |
| 语言 | 可选。 语言属性可用于指定命令表中所有 \<Strings> 元素的默认语言。  如果未指定语言，则使用当前进程的语言：<br /><br /> language="en-us" |

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[Extern 元素](../extensibility/extern-element.md)|可选。 包含编译器的预处理器指令。|
|[Include 元素](../extensibility/include-element.md)|可选。 包含要包含在编译中的任何文件的路径。|
|[定义元素](../extensibility/define-element.md)|可选。 根据符号的名称和值定义符号。|
|[Commands 元素](../extensibility/commands-element.md)|可选。 定义包含所有其他元素的 VSPackage 的所有命令的父元素。|
|[CommandPlacements 元素](../extensibility/commandplacements-element.md)|可选。 定义命令栏上命令的放置位置。|
|[VisibilityConstraints 元素](../extensibility/visibilityconstraints-element.md)|可选。 确定命令和工具栏的静态可见性。|
|[KeyBindings 元素](../extensibility/keybindings-element.md)|可选。 指定命令的快捷键组合（如果有）。|
|[UsedCommands 元素](../extensibility/usedcommands-element.md)|可选。 允许 VSPackage 选择性地实现自己的功能版本，该功能最初由其他 VSPackage 支持。|
|[Symbols 元素](https://www.microsoft.com/download/details.aspx?id=55984)|可选。 包含编译器的任何符号数据（GUID、标识等）。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|无||

## <a name="see-also"></a>请参阅
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
