---
title: 更改菜单命令的文本 |Microsoft Docs
description: 查看此代码示例，了解如何通过使用 IMenuCommandService 服务来更改菜单命令的文本标签。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- menus, changing text
- text, menus
- commands, changing text
ms.assetid: 5cb676a0-c6e2-47e5-bd2b-133dc8842e46
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 637fb644d5112ab6b6aceefed15093d31a3ca9cd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122043786"
---
# <a name="change-the-text-of-a-menu-command"></a>更改菜单命令的文本
以下步骤演示如何使用服务更改菜单命令的文本标签 <xref:System.ComponentModel.Design.IMenuCommandService> 。

## <a name="changing-a-menu-command-label-with-the-imenucommandservice"></a>使用 IMenuCommandService 更改菜单命令标签

1. `MenuText`使用名为 **ChangeMenuText** 的菜单命令创建一个名为的 VSIX 项目。 有关详细信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 在 *.vsct* 文件中，将标志添加 `TextChanges` 到菜单命令中，如下面的示例中所示。

    ```xml
    <Button guid="guidChangeMenuTextPackageCmdSet" id="ChangeMenuTextId" priority="0x0100" type="Button">
        <Parent guid="guidChangeMenuTextPackageCmdSet" id="MyMenuGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <CommandFlag>TextChanges</CommandFlag>
        <Strings>
            <ButtonText>Invoke ChangeMenuText</ButtonText>
        </Strings>
    </Button>
    ```

3. 在 *ChangeMenuText* 文件中，创建一个将在显示菜单命令之前调用的事件处理程序。

    ```csharp
    private void OnBeforeQueryStatus(object sender, EventArgs e)
    {
        var myCommand = sender as OleMenuCommand;
        if (null != myCommand)
        {
            myCommand.Text = "New Text";
        }
    }
    ```

    还可以通过更改 <xref:System.ComponentModel.Design.MenuCommand.Visible%2A> 对象的、和属性来更新此方法中的菜单命令的状态 <xref:System.ComponentModel.Design.MenuCommand.Checked%2A> <xref:System.ComponentModel.Design.MenuCommand.Enabled%2A> <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 。

4. 在 ChangeMenuText 构造函数中，将原始命令初始化和位置代码替换为创建 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> (而不是 `MenuCommand` 表示菜单命令的) 的代码， <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> 并添加事件处理程序，并为菜单命令服务提供菜单命令。

    如下所示：

    ```csharp
    private ChangeMenuText(AsyncPackage package, OleMenuCommandService commandService)
    {
        this.package = package ?? throw new ArgumentNullException(nameof(package));
        commandService = commandService ?? throw new ArgumentNullException(nameof(commandService));
        
        var menuCommandID = new CommandID(CommandSet, CommandId);
        var menuItem = new OleMenuCommand(this.Excute, menuCommandID);
        menuItem.BeforeQueryStatus += new EventHandler(OnBeforeQueryStatus);
        commandService.AddCommand(menuItem);
    }
    ```

5. 生成项目并启动调试。 将显示 Visual Studio 的实验实例。

6. 在 " **工具** " 菜单中，应会看到名为 " **调用 ChangeMenuText**" 的命令。

7. 单击该命令。 应该会看到消息框，指出已调用 **MenuItemCallback** 。 关闭消息框时，应会看到 "工具" 菜单上的命令名称现在为 " **新文本**"。
