---
title: 设计 XML 命令表 (。Vsct) Files |Microsoft Docs
description: 了解如何设计 XML 命令表 (.vsct) 文件，该文件描述命令项（包括按钮、组合框、菜单和工具栏）的布局和外观。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, designing
ms.assetid: bb87a322-bac4-4258-92bc-9a876f05d653
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a3dc6aa48ef15e49928c87baeb913e18048a7e9e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122102710"
---
# <a name="design-xml-command-table-vsct-files"></a>设计 XML 命令表 (.vsct) 文件
.vsct (*.vsct*) XML 命令表描述了 VSPackage 的命令项的布局和外观。 命令项包括按钮、组合框、菜单、工具栏和命令项组。 本文介绍 XML 命令表文件、它们如何影响命令项和菜单以及如何创建它们。

## <a name="commands-menus-groups-and-the-vsct-file"></a>命令、菜单、组和 .vsct 文件
 *.vsct* 文件围绕命令、菜单和命令组进行组织。 *.vsct 文件的 XML* 标记表示每个项，以及其他关联的项，例如命令按钮、命令放置和位图。

 通过运行包模板创建新的 VSPackage 时，模板会生成一个 .vsct 文件，该文件包含菜单命令、工具窗口或自定义编辑器所需的元素，具体取决于 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 你的选择。  然后 *，可以修改此 .vsct* 文件以满足特定 VSPackage 的要求。 有关如何修改 *.vsct* 文件的示例，请参阅 [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

 若要创建新的空白 *.vsct* 文件，请参阅 [如何：创建 *.vsct* 文件](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)。 创建后，向文件添加 XML 元素、属性和值，以描述命令项布局。 有关详细的 XML 架构，请参阅 [VSCT XML 架构引用](../../extensibility/vsct-xml-schema-reference.md)。

## <a name="differences-between-ctc-and-vsct-files"></a>.tc 和 .vsct 文件之间的差异
 虽然 *.vsct* 文件中 XML 标记背后的含义与现在弃用 *.提供* 文件格式的标记相同，但它们的实现有所不同：

- 新 **\<extern>** 标记是引用要编译的其他 *.h* 文件的位置，例如工具栏的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 这些文件。

- 虽然 *.vsct* 文件支持 **/include** 语句，就像 *.保存* 文件一样，它还具有新 **\<import>** 元素。 不同之处在于 **，/include** 会引入 *所有* 信息，而 **\<import>** 只引入名称。

- 虽然 *.files* 文件需要用于定义预处理器指令的头文件，但 *.vsct* 文件不需要一个头文件。 相反，将 指令放在符号表中，该表位于 **\<Symbol>** *.vsct* 文件底部的 元素中。

- *.vsct* 文件具有 标记，可让你嵌入你喜欢的任何信息，例如便笺 **\<Annotation>** 甚至图片。

- 值作为属性存储在项上。

- 命令标志可以单独存储或堆叠。  但是，IntelliSense 在堆积命令标志上不起作用。 有关命令标志详细信息，请参阅 [CommandFlag 元素](../../extensibility/command-flag-element.md)。

- 可以指定多种类型，例如拆分下拉列表、组合等。

- GUID 不会验证。

- 每个 UI 元素都有一个字符串，该字符串表示随它一起显示的文本。

- 父级是可选的。 如果省略，则使用 *值 Group Unknown。*

- Icon 参数是可选的。

- 位图部分：此部分与 *.compiler* 文件中相同，只不过现在可以通过 Href 指定文件名，该名称将在编译时由vsct.exe编译器拉取。

- ResID：可以使用旧的位图资源 ID，并且其工作方式仍与 *.files* 文件中相同。

- HRef：一种新方法，可用于指定位图资源的文件名。 它假定使用了所有 ，因此可以省略"已用"部分。 编译器首先搜索文件的本地资源，然后搜索任何网络共享和 **/I** 开关定义的任何资源。

- 键绑定：不再需要指定模拟器。 如果指定一个，编译器将假定编辑器和模拟器相同。

- Keychord：Keychord 已被删除。 新格式为 *Key1、Mod1、Key2、Mod2*。  可以指定字符、十六进制或 VK 常量。

新的编译器 *（vsct.exe* 编译 *.compiler* 和 *.vsct* 文件。 但是 *，ctc.exe* 编译器无法识别或编译 *.vsct* 文件。

可以使用vsct.exe *将现有* *.cto* 文件转换为 *.vsct* 文件。 有关详细信息，请参阅 [如何：从现有 .cto 文件 创建 .vsct 文件](../../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file)。

## <a name="the-vsct-file-elements"></a>.vsct 文件元素
 命令表具有以下层次结构和元素：

- [CommandTable 元素](../../extensibility/commandtable-element.md)：表示与 VSPackage 关联的所有命令、菜单组和菜单。

- [Extern 元素](../../extensibility/extern-element.md)：引用要与 *.vsct* 文件合并的任何外部 .h 文件。

- [Include 元素](../../extensibility/include-element.md)：引用要 (.h) *.vsct* 文件一起编译的任何附加头文件。 *.vsct* 文件可以包含 *.h* 文件，其中包含定义 IDE 或其他 VSPackage 提供的命令、菜单组和菜单的常量。

- [Commands 元素](../../extensibility/commands-element.md)：表示可以执行的所有单个命令。 每个命令具有以下四个子元素：

- [菜单元素](../../extensibility/menus-element.md)：表示 VSPackage 中所有菜单和工具栏。 菜单是命令组的容器。

- [Groups 元素](../../extensibility/groups-element.md)：表示 VSPackage 中的所有组。 组是单个命令的集合。

- [Buttons 元素](../../extensibility/buttons-element.md)：表示 VSPackage 中所有命令按钮和菜单项。 按钮是可与命令关联的可视控件。

- [Bitmaps 元素](../../extensibility/bitmaps-element.md)：表示 VSPackage 中所有按钮的所有位图。 位图是显示在命令按钮旁边或上的图片，具体取决于上下文。

- [CommandPlacements 元素](../../extensibility/commandplacements-element.md)：指示应在 VSPackage 的菜单中放置单个命令的其他位置。

- [VisibilityConstraints 元素](../../extensibility/visibilityconstraints-element.md)：指定命令是一向显示还是仅在特定上下文中显示，例如显示特定对话框或窗口时。 只有指定的上下文处于活动状态时，才显示具有此元素值的菜单和命令。 默认行为是一向显示命令。

- [KeyBindings 元素](../../extensibility/keybindings-element.md)：指定命令的任何键绑定。 也就是说，必须按下一个或多个组合键来执行命令，如 **Ctrl** + **S**。

- [UsedCommands 元素](../../extensibility/usedcommands-element.md)：通知环境，尽管指定的命令由其他代码实现，但当当前 VSPackage 处于活动状态时，它 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 提供命令实现。

- [Symbols 元素](../../extensibility/symbols-element.md)：包含包中所有命令的符号名称和 GUID 标识。

## <a name="vsct-file-design-guidelines"></a>.vsct 文件设计准则
 若要成功设计 *.vsct* 文件，请遵循以下准则。

- 命令只能放置在组中，组只能放置在菜单中，并且菜单只能放置在组中。 实际上，只有菜单显示在 IDE 中，组和命令不会显示。

- 子菜单不能直接分配给菜单，但必须分配给组，而组又分配给菜单。

- 可以使用其定义指令的父字段将命令、子菜单和组分配给一个父组或菜单。

- 仅通过 指令中的父字段组织命令表具有显著限制。 定义 对象的指令只能使用一个父参数。

- 若要重新使用命令、组或子菜单，需要使用新的 指令创建具有其自己的对的对象的新 `GUID:ID` 实例。

- 每个 `GUID:ID` 对必须是唯一的。 重新使用命令（例如，放置在菜单、工具栏或上下文菜单上）由 接口 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 处理。

- 命令和子菜单也可以分配给多个组，并且可以使用 Commands 元素将组分配给 [多个菜单](../../extensibility/commands-element.md)。

## <a name="vsct-file-notes"></a>.vsct 文件说明
 如果在编译 *.vsct* 文件并放在本机附属 DLL 中之后对其进行任何更改，则应该运行 **devenv.exe /setup /nativetupvstemplates**。 这样做会强制重新读取实验注册表中指定的 VSPackage 资源以及描述要重新生成 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的内部数据库。

 在开发过程中，可以在实验性注册表配置单元中创建和注册多个 VSPackage 项目，这可能会导致 IDE 混乱。 若要解决此问题，可以将实验性配置单元重置为默认设置，以删除所有已注册的 VSPackage 及其对 IDE 进行的任何更改。 若要重置实验性配置单元，请使用 CreateExpInstance.exe SDK 随附的 Visual Studio 工具。 可以在：

 *%PROGRAMFILES (x86) %\Visual Studio \\ \<version> SDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe*

 使用命令 **CreateExpInstance /Reset 运行该工具**。 请记住，此工具会从实验性配置单元中删除通常未随 一起安装的所有已注册 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage。

## <a name="see-also"></a>请参阅
- [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)
