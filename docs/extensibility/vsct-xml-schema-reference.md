---
title: VSCT XML 架构参考|Microsoft Docs
description: VSCT XML 架构参考文章介绍了命令表编译器架构元素，其中每个元素都有允许的子元素和属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Visual Studio command table configuration files (VSCT), XML schema
- VSCT XML schema elements
ms.assetid: 49e7efae-e713-4762-a824-96fdaf92cdc9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6f6564d563894dfb48d0fea1a008ffffb65ba280
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122028405"
---
# <a name="vsct-xml-schema-reference"></a>VSCT XML 架构参考
提供命令表编译器架构元素的表，其中每个元素都有允许的子元素和属性。

 基于 XML 的命令表配置 (.vsct) 文件定义 VSPackage 向集成开发环境提供的命令元素 (IDE) 。 这些元素包括菜单项、菜单、工具栏和组合框。

> [!NOTE]
> VSCT 编译器可以在 .vsct 文件上运行预处理器。 由于这通常是 C++ 预处理器，因此可以定义包含 和 宏，这些宏的语法与 C++ 文件中使用的语法相同。 "新建包"向导为 VSPackage 项目创建的 .vsct **Project** 提供了此类示例。

## <a name="optional-elements"></a>可选元素
 某些 VSCT 元素是可选的。 如果 `Parent` 未指定参数，则Group_Undefined：0将隐含 。 如果 `Icon` 未指定参数，则隐含 guidOfficeIcon：msotcidNoIcon。 定义快捷键时，通常未使用的仿真是可选的。

 通过指定参数中位图条的位置，可以在编译时嵌入位 `href` 图项。 位图条是在合并期间复制的，而不是从 DLL 的资源中提取的。 提供 `href` 参数时，参数变为可选，并且位图条中所有槽 `usedList` 都被视为已使用。

 必须使用符号名称定义所有 GUID 和 ID 值。 这些名称可以在头文件或 VSCT 节中 \<Symbols> 定义。 符号名称必须是局部的、通过元素包含 \<Include> 的或由元素 \<Extern> 引用的。 如果符号名称遵循符号值的简单模式，则从元素中指定的标头#define \<Extern> 名称。 只要之前定义了该符号，该值就可能是另一个符号。 GUID 定义必须遵循 OLE 或 C++ 格式。 ID 值可以是十进制数字或前面带有 0x 的十六进制数字，如以下行所示：

- {6D484634-E53D-4a2c-ADCB-55145C9362C8}

- { 0x6d484634， 0xe53d， 0x4a2c， { 0xad， 0xcb， 0x55， 0x14， 0x5c， 0x93， 0x62， 0xc8 } }

  可能使用 XML 注释，但 GUI 和 GUI (的) 可能会丢弃它们。 无论格式 \<Annotation> 如何，都保证维护元素的内容。

## <a name="schema-hierarchy"></a>架构层次结构
 .vsct 文件具有以下主要元素。

- [CommandTable 元素](../extensibility/commandtable-element.md)

- [Extern 元素](../extensibility/extern-element.md)

- [Include 元素](../extensibility/include-element.md)

- [定义元素](../extensibility/define-element.md)

- [Commands 元素](../extensibility/commands-element.md)

- [CommandPlacements 元素](../extensibility/commandplacements-element.md)

- [VisibilityConstraints 元素](../extensibility/visibilityconstraints-element.md)

- [KeyBindings 元素](../extensibility/keybindings-element.md)

- [UsedCommands 元素](../extensibility/usedcommands-element.md)

- [父元素](../extensibility/parent-element.md)

- [Icon 元素](../extensibility/icon-element.md)

- [Strings 元素](../extensibility/strings-element.md)

- [Command Flag 元素](../extensibility/command-flag-element.md)

- [Symbols 元素](../extensibility/symbols-element.md)

- [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)

## <a name="see-also"></a>请参阅
- [VSPackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [VSPackages 中的命令路由](../extensibility/internals/command-routing-in-vspackages.md)
