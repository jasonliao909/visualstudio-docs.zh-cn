---
title: 将子菜单添加到菜单|Microsoft Docs
description: 了解如何创建子菜单、将其添加到Visual Studio栏，以及如何向子菜单添加新命令。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- context menus
- submenus, cascading
- cascading submenus
- menus, creating cascading submenus
ms.assetid: 692600cb-d052-40e2-bdae-4354ae7c6c84
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6ebd3a4d97d19977b8a97ff7fcb2a545654f4165
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122065184"
---
# <a name="add-a-submenu-to-a-menu"></a>向菜单添加子菜单
本演练基于向菜单栏添加Visual Studio [中的](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)演示，其中显示了如何将子菜单添加到 **TestMenu** 菜单。

 子菜单是显示在另一个菜单中的辅助菜单。 子项可以通过名称后跟的箭头进行标识。 单击名称会导致显示子菜单及其命令。

 本演练在菜单栏上的菜单中创建Visual Studio菜单，并将新命令放在子菜单上。 本演练还实现了新命令。

## <a name="prerequisites"></a>必备条件
 从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="add-a-submenu-to-a-menu"></a>向菜单添加子菜单

1. 按照将菜单[添加到菜单栏中的步骤Visual Studio菜单栏创建](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)项目和菜单项。 本演练中的步骤假定 VSIX 项目的名称为 `TopLevelMenu` 。

2. 打开 *TestCommandPackage.vsct*。 在 部分中，为子menu 添加一个元素，为子menu 组添加一个元素，为命令添加一个元素，所有元素都位于名为 `<Symbols>` `<IDSymbol>` `<GuidSymbol>` "guidTopLevelMenuCmdSet"的节点中。 这是包含顶级菜单 `<IDSymbol>` 元素的同一节点。

    ```xml
    <IDSymbol name="SubMenu" value="0x1100"/>
    <IDSymbol name="SubMenuGroup" value="0x1150"/>
    <IDSymbol name="cmdidTestSubCommand" value="0x0105"/>
    ```

3. 将新创建的子menu 添加到 `<Menus>` 节。

    ```xml
    <Menu guid="guidTestCommandPackageCmdSet" id="SubMenu" priority="0x0100" type="Menu">
        <Parent guid="guidTestCommandPackageCmdSet" id="MyMenuGroup"/>
        <Strings>
            <ButtonText>Sub Menu</ButtonText>
            <CommandName>Sub Menu</CommandName>
        </Strings>
    </Menu>
    ```

     父级的 GUID/ID 对指定在将菜单添加到 Visual Studio[菜单](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)栏中生成的菜单组，它是顶级菜单的子级。

4. 将步骤 2 中定义的菜单组添加到 `<Groups>` 节，并将其添加到子菜单的子菜单。

    ```xml
    <Group guid="guidTestCommandPackageCmdSet" id="SubMenuGroup" priority="0x0000">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>
    ```

5. 向 节 `<Button>` 添加新元素 `<Buttons>` ，以将步骤 2 中创建的命令定义为子菜单项上的项。

    ```xml
    <Button guid="guidTestCommandPackageCmdSet" id="cmdidTestSubCommand" priority="0x0000" type="Button">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenuGroup" />
        <Icon guid="guidImages" id="bmpPic2" />
        <Strings>
           <CommandName>cmdidTestSubCommand</CommandName>
           <ButtonText>Test Sub Command</ButtonText>
        </Strings>
    </Button>
    ```

6. 生成解决方案并启动调试。 应会看到实验实例。

7. 单击 **"TestMenu"** 查看名为"子菜单 **"的新子菜单**。 单击 **"子** 菜单"打开子菜单，并查看新的命令 **"测试子命令"。** 请注意，单击 **"测试子命令"** 不执行任何操作。

## <a name="add-a-command"></a>添加命令

1. 打开 *TestCommand.cs，* 在现有的命令 ID 后添加以下命令 ID。

    ```csharp
    public const int cmdidTestSubCmd = 0x0105;
    ```

2. 添加子命令。 查找命令构造函数。 在调用 方法之后添加以下 `AddCommand` 行。

    ```csharp
    CommandID subCommandID = new CommandID(CommandSet, cmdidTestSubCmd);
    MenuCommand subItem = new MenuCommand(new EventHandler(SubItemCallback), subCommandID);
    commandService.AddCommand(subItem);
    ```

    `SubItemCallback`稍后将定义命令处理程序。 构造函数现在应如下所示：

    ```csharp
    private TestCommand(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException("package");
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            var menuCommandID = new CommandID(CommandSet, CommandId);
            var menuItem = new MenuCommand(this.MenuItemCallback, menuCommandID);
            commandService.AddCommand(menuItem);

            CommandID subCommandID = new CommandID(CommandSet, cmdidTestSubCmd);
            MenuCommand subItem = new MenuCommand(new EventHandler(SubItemCallback), subCommandID);
            commandService.AddCommand(subItem);
        }
    }
    ```

3. 添加 `SubItemCallback()`。 这是在单击子菜单中的新命令时调用的方法。

    ```csharp
    private void SubItemCallback(object sender, EventArgs e)
    {
        ThreadHelper.ThrowIfNotOnUIThread();
        IVsUIShell uiShell = this.package.GetService<SVsUIShell, IVsUIShell>();
        Guid clsid = Guid.Empty;
        int result;
        uiShell.ShowMessageBox(
            0,
            ref clsid,
            "TestCommand",
            string.Format(CultureInfo.CurrentCulture,
            "Inside TestCommand.SubItemCallback()",
            this.ToString()),
            string.Empty,
            0,
            OLEMSGBUTTON.OLEMSGBUTTON_OK,
            OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,
            OLEMSGICON.OLEMSGICON_INFO,
            0,
            out result);
    }
    ```

4. 生成项目并启动调试。 应显示实验实例。

5. 在 **"TestMenu"菜单** 上，单击"**子菜单"，** 然后单击"**测试子命令"。** 应会出现一个消息框并显示文本"TestCommand.SubItemCallback () "。

## <a name="see-also"></a>请参阅

- [将菜单添加到菜单Visual Studio栏](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
