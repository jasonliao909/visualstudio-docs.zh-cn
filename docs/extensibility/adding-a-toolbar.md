---
title: 添加工具栏|Microsoft Docs
description: 了解如何添加一个工具栏，其中包含绑定到 IDE Visual Studio集成开发环境的命令 (按钮) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- toolbars [Visual Studio], adding to IDE
- IDE, adding toolbars
ms.assetid: 17302c25-6f59-4e97-8c85-54f95336a07f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ca32c96358982352d1570f916799409fbf8090a270424beaf5e1651a54d66a5d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434966"
---
# <a name="add-a-toolbar"></a>添加工具栏
本演练演示如何向 IDE Visual Studio工具栏。

 工具栏是一个水平或垂直条带，其中包含绑定到命令的按钮。 IDE 中的工具栏可以重新定位、停靠在主 IDE 窗口的任何一侧，或者位于其他窗口的前面，具体取决于其实现。

 此外，用户可以使用"自定义"对话框将命令添加到工具栏 **或删除它们。** 通常，VSPackage 中的工具栏是用户可自定义的。 IDE 处理所有自定义项，VSPackage 响应命令。 VSPackage 无需知道命令的物理位置。

 有关菜单详细信息，请参阅 [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

## <a name="prerequisites"></a>先决条件
 从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-an-extension-with-a-toolbar"></a>使用工具栏创建扩展
 创建名为 的 VSIX 项目 `IDEToolbar` 。 添加名为 **ToolbarTestCommand 的菜单命令项模板**。 若要了解如何执行此操作，请参阅 [使用菜单命令 创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="create-a-toolbar-for-the-ide"></a>为 IDE 创建工具栏

1. 在 *ToolbarTestCommandPackage.vsct* 中，查找"符号"部分。 在名为 guidToolbarTestCommandPackageCmdSet 的 GuidSymbol 元素中，添加工具栏和工具栏组的声明，如下所示。

    ```xml
    <IDSymbol name="Toolbar" value="0x1000" />
    <IDSymbol name="ToolbarGroup" value="0x1050" />

    ```

2. 在"命令"部分的顶部，创建"菜单"部分。 将 Menu 元素添加到"菜单"部分以定义工具栏。

    ```xml
    <Menus>
        <Menu guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"
            type="Toolbar" >
            <CommandFlag>DefaultDocked</CommandFlag>
            <Strings>
                <ButtonText>Test Toolbar</ButtonText>
                <CommandName>Test Toolbar</CommandName>
            </Strings>
          </Menu>
    </Menus>
    ```

     工具栏不能像子菜单一样嵌套。 因此，不需要分配父组。 此外，不需要设置优先级，因为用户可以移动工具栏。 通常，工具栏的初始位置以编程方式定义，但用户的后续更改将持久保存。

3. 在" [组](../extensibility/groups-element.md) "部分的现有组条目之后，定义 [一个 Group](../extensibility/group-element.md) 元素以包含工具栏的命令。

    ```xml
    <Group guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup"
          priority="0x0000">
      <Parent guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"/>
    </Group>
    ```

4. 使按钮显示在工具栏上。 在"按钮"部分中，将"按钮"中的"父"块替换为工具栏。 生成的 Button 块应如下所示：

    ```xml
    <Button guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarTestCommandId" priority="0x0100" type="Button">
        <Parent guid= "guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup" />
                <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ToolbarTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     默认情况下，如果工具栏没有命令，则不显示。

5. 生成项目并启动调试。 应显示实验实例。

6. 右键单击Visual Studio栏，获取工具栏列表。 选择"**测试工具栏"。**

7. 现在，工具栏应会显示为"在文件中查找"图标右边的图标。 单击图标时，应会看到一个消息框，显示 **"ToolbarTestCommandPackage"。在 IDEToolbar.ToolbarTestCommand.MenuItemCallback ()**。

## <a name="see-also"></a>另请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
