---
title: 将命令添加到 解决方案资源管理器 工具栏|Microsoft Docs
description: 了解如何将执行命令的按钮添加到 解决方案资源管理器 工具栏Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- toolbars [Visual Studio], adding buttons
- buttons [Visual Studio], adding to Solution Explorer
- Solution Explorer, adding buttons
ms.assetid: f6411557-2f4b-4e9f-b02e-fce12a6ac7e9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b3753f1bce7debe28f33f0c44059b0044d92ef2eadf11ca78215648065450907
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121378278"
---
# <a name="add-a-command-to-the-solution-explorer-toolbar"></a>将命令添加到解决方案资源管理器工具栏
本演练演示如何向工具栏添加 **解决方案资源管理器按钮。**

 工具栏或菜单上的任何命令都称为Visual Studio。 单击按钮时，将执行命令处理程序中的代码。 通常，相关命令组合在一起形成一个组。 菜单或工具栏充当组的容器。 优先级确定组中单个命令在菜单或工具栏上的显示顺序。 可以通过控制按钮的可见性来防止按钮显示在工具栏或菜单上。 .vsct 文件的一部分中列出的 `<VisibilityConstraints>` 命令仅出现在关联的上下文中。 可见性不能应用于组。

 有关菜单、工具栏命令和 *.vsct* 文件详细信息，请参阅命令 [、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

> [!NOTE]
> 使用 *.vsct (.vsct*) 文件而不是命令表配置 (*.)* 文件来定义菜单和命令在 VSPackage 中的显示方式。 有关详细信息，请参阅命令[Visual Studio表 (。Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

## <a name="prerequisites"></a>先决条件
 从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-an-extension-with-a-menu-command"></a>使用菜单命令创建扩展
 创建名为 的 VSIX 项目 `SolutionToolbar` 。 添加名为 **ToolbarButton 的菜单命令项模板**。 若要了解如何执行此操作，请参阅 [使用菜单命令 创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="add-a-button-to-the-solution-explorer-toolbar"></a>向工具栏添加解决方案资源管理器按钮
 本演练的此部分演示如何将按钮添加到 **解决方案资源管理器工具栏。** 单击按钮时，将运行回调方法中的代码。

1. 在 *ToolbarButtonPackage.vsct* 文件中，转到  `<Symbols>` 部分。 节点 `<GuidSymbol>`  包含包模板生成的菜单组和命令。 将 `<IDSymbol>` 元素添加到此节点，以声明将保存命令的组。

    ```xml
    <IDSymbol name="SolutionToolbarGroup" value="0x0190"/>
    ```

2. 在 `<Groups>` 部分的现有组条目之后，定义在上一步中声明的新组。

    ```xml
    <Group guid="guidToolbarButtonPackageCmdSet"
           id="SolutionToolbarGroup" priority="0xF000">
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>
          </Group>
    ```

     将父 GUID：ID 对设置为 并将此组解决方案资源管理器工具栏上，设置高优先级值会将它 `guidSHLMainMenu` `IDM_VS_TOOL_PROJWIN` 放在其他命令组之后。 

3. 在 `<Buttons>` 部分中，更改生成的条目的父 ID 以反映在上一步 `<Button>` 中定义的组。 修改后 `<Button>` 的元素应如下所示：

    ```xml
    <Button guid="guidToolbarButtonPackageCmdSet" id="ToolbarButtonId" priority="0x0100" type="Button">
        <Parent guid="guidToolbarButtonPackageCmdSet" id="SolutionToolbarGroup" />
        <Icon guid="guidImages" id="bmpPicStrikethrough" />
        <Strings>
            <ButtonText>Invoke ToolbarButton</ButtonText>
        </Strings>
    </Button>
    ```

4. 生成项目并启动调试。 这将显示实验实例。

     解决方案资源管理器 **工具栏** 应在现有按钮的右侧显示新的命令按钮。 按钮图标是删除线。

5. 单击新按钮。

     应显示一个对话框，该对话框包含 **消息"SolutionToolbar.ToolbarButton.MenuItemCallback () SolutionToolbar.ToolbarButton.MenuItemCallback"。**

## <a name="control-the-visibility-of-a-button"></a>控制按钮的可见性
 演练的此部分演示如何控制工具栏上按钮的可见性。 将上下文设置为 `<VisibilityConstraints>` *SolutionToolbar.vsct* 文件的 部分中的一个或多个项目，可以限制按钮仅在项目或项目打开时显示。

### <a name="to-display-a-button-when-one-or-more-projects-are-open"></a>打开一个或多个项目时显示按钮

1. 在 `<Buttons>` *ToolbarButtonPackage.vsct* 的 部分中，将两个命令标志添加到 和 标记之间的现有 `<Button>` `<Strings>` `<Icons>` 元素。

   ```xml
   <CommandFlag>DefaultInvisible</CommandFlag>
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

    必须 `DefaultInvisible` `DynamicVisibility` 设置 和 标志，使 节中的条目 `<VisibilityConstraints>` 生效。

2. 创建 `<VisibilityConstraints>` 包含两个条目 `<VisibilityItem>` 的 节。 将新节放在结束标记 `</Commands>` 的正后。

   ```xml
   <VisibilityConstraints>
       <VisibilityItem guid="guidToolbarButtonPackageCmdSet"
             id="ToolbarButtonId"
             context="UICONTEXT_SolutionHasSingleProject" />
       <VisibilityItem guid="guidToolbarButtonPackageCmdSet"
             id="ToolbarButtonId"
             context="UICONTEXT_SolutionHasMultipleProjects" />
   </VisibilityConstraints>
   ```

    每个可见性项都表示显示指定按钮的条件。 若要应用多个条件，必须为同一按钮创建多个条目。

3. 生成项目并启动调试。 这将显示实验实例。

    解决方案资源管理器 **工具栏** 不包含删除线按钮。

4. 打开包含项目的任何解决方案。

    删除线按钮显示在现有按钮右侧工具栏上。

5. 在 **“文件”** 菜单上，单击 **“关闭解决方案”** 。 该按钮从工具栏中消失。

   按钮的可见性由 控制， [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 直到加载 VSPackage。 加载 VSPackage 后，按钮的可见性由 VSPackage 控制。  有关详细信息，请参阅 [MenuCommands 与 OleMenuCommands](/previous-versions/visualstudio/visual-studio-2015/misc/menucommands-vs-olemenucommands?preserve-view=true&view=vs-2015)。

## <a name="see-also"></a>请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)