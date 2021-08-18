---
title: 将工具栏添加到工具窗口|Microsoft Docs
description: 了解如何在 IDE Visual Studio 集成开发环境中将包含绑定到命令的按钮的工具栏 (工具) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tool windows, adding toolbars
- toolbars [Visual Studio], adding to tool windows
ms.assetid: 172f64b3-87f8-4292-9c1c-65bffa2b0970
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6a2c93459dd588a1a04be098cf675aa4c58b8d37
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122051360"
---
# <a name="add-a-toolbar-to-a-tool-window"></a>向工具窗口添加工具栏
本演练演示如何向工具窗口添加工具栏。

 工具栏是一个水平或垂直条带，其中包含绑定到命令的按钮。 工具窗口中工具栏的长度始终与工具窗口的宽度或高度相同，具体取决于工具栏停靠的位置。

 与 IDE 中的工具栏不同，工具窗口中的工具栏必须停靠，并且不能移动或自定义。 如果 VSPackage 是使用统一代码编写的，则工具栏可以停靠在任何边缘上。

 若要详细了解如何添加工具栏，请参阅 [添加工具栏](../extensibility/adding-a-toolbar.md)。

## <a name="prerequisites"></a>必备条件
 从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-toolbar-for-a-tool-window"></a>为工具窗口创建工具栏

1. 创建一个名为 的 VSIX `TWToolbar` 项目，该项目包含名为 **TWTestCommand** 的菜单命令和名为 **TestToolWindow 的工具窗口**。 有关详细信息，请参阅[使用菜单命令创建扩展和](../extensibility/creating-an-extension-with-a-menu-command.md)[使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。 在添加工具窗口模板之前，需要添加命令项模板。

2. 在 *TWTestCommandPackage.vsct* 中，查找"符号"部分。 在名为 guidTWTestCommandPackageCmdSet 的 GuidSymbol 节点中，声明工具栏和工具栏组，如下所示。

    ```xml
    <IDSymbol name="TWToolbar" value="0x1000" />
    <IDSymbol name="TWToolbarGroup" value="0x1050" />
    ```

3. 在部分顶部 `Commands` ，创建一个 `Menus` 节。 添加 `Menu` 元素以定义工具栏。

    ```xml
    <Menus>
        <Menu guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" type="ToolWindowToolbar">
            <CommandFlag>DefaultDocked</CommandFlag>
            <Strings>
                <ButtonText>Test Toolbar</ButtonText>
                <CommandName>Test Toolbar</CommandName>
            </Strings>
        </Menu>
    </Menus>
    ```

     工具栏不能像子菜单一样嵌套。 因此，不必分配父级。 此外，不必设置优先级，因为用户可以移动工具栏。 通常，工具栏的初始位置以编程方式定义，但用户的后续更改将持久保存。

4. 在"组"部分中，定义一个组以包含工具栏的命令。

    ```xml

    <Group guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" priority="0x0000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbar" />
    </Group>
    ```

5. 在"按钮"部分中，将现有 Button 元素的父级更改为工具栏组，以便显示工具栏。

    ```xml
    <Button guid="guidTWTestCommandPackageCmdSet" id="TWTestCommandId" priority="0x0100" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke TWTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     默认情况下，如果工具栏没有命令，则不显示。

     由于新工具栏不会自动添加到工具窗口，因此必须显式添加工具栏。 下一节中将对此进行讨论。

## <a name="add-the-toolbar-to-the-tool-window"></a>将工具栏添加到工具窗口

1. 在 *TWTestCommandPackageGuids.cs* 中添加以下行。

    ```csharp
    public const string guidTWTestCommandPackageCmdSet = "00000000-0000-0000-0000-0000";  // get the GUID from the .vsct file
    public const int TWToolbar = 0x1000;
    ```

2. 在 *TestToolWindow.cs 中添加* 以下 using 语句。

    ```csharp
    using System.ComponentModel.Design;
    ```

3. 在 TestToolWindow 构造函数中添加以下行。

    ```csharp
    this.ToolBar = new CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), TWTestCommandPackageGuids.TWToolbar);
    ```

## <a name="test-the-toolbar-in-the-tool-window"></a>在工具窗口中测试工具栏

1. 生成项目并启动调试。 应Visual Studio实验实例。

2. 在"**视图/其他Windows** 菜单上，单击"**测试工具""窗口**"以显示工具窗口。

     此时会看到一个 (，它看起来像工具窗口左上方) 标题正下方的默认图标。

3. 在工具栏上，单击图标以显示消息 **TWTestCommandPackage Inside TWToolbar.TWTestCommand.MenuItemCallback () 。**

## <a name="see-also"></a>请参阅
- [添加工具栏](../extensibility/adding-a-toolbar.md)
