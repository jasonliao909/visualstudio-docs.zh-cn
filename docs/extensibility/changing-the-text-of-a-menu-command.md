---
title: 更改菜单命令文本|Microsoft Docs
description: 查看此代码示例，了解如何使用 IMenuCommandService 服务更改菜单命令的文本标签。
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
ms.openlocfilehash: 3c7396b54147d185b98af99c9ab8d87c464eff69eaf59a29e86b5962f8daf753
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121308306"
---
# <a name="change-the-text-of-a-menu-command"></a>更改菜单命令的文本
以下步骤显示如何使用 服务更改菜单命令的文本 <xref:System.ComponentModel.Design.IMenuCommandService> 标签。

## <a name="changing-a-menu-command-label-with-the-imenucommandservice"></a>使用 IMenuCommandService 更改菜单命令标签

1. 使用名为 `MenuText` **ChangeMenuText** 的菜单命令创建名为 的 VSIX 项目。 有关详细信息，请参阅 [使用菜单命令 创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 在 *.vsct 文件中* ，将 标志添加到 `TextChanges` 菜单命令，如以下示例所示。

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

3. 在 *ChangeMenuText.cs* 文件中，创建将在显示菜单命令之前调用的事件处理程序。

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

    还可以在此方法中通过更改 对象的 、 和 属性来 <xref:System.ComponentModel.Design.MenuCommand.Visible%2A> <xref:System.ComponentModel.Design.MenuCommand.Checked%2A> <xref:System.ComponentModel.Design.MenuCommand.Enabled%2A> 更新菜单命令 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 的状态。

4. 在 ChangeMenuText 构造函数中，将原始命令初始化和放置代码替换为创建 (而不是表示菜单命令的) 的代码，添加事件处理程序，并将菜单命令授予菜单命令服务。 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> `MenuCommand` <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>

    它应如下所示：

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

5. 生成项目并启动调试。 将显示该实例Visual Studio实例。

6. 在" **工具"** 菜单上，应会看到名为 **"调用 ChangeMenuText"的命令**。

7. 单击 命令。 应会看到消息框，指出已调用 **MenuItemCallback。** 关闭消息框时，应会看到"工具"菜单上的命令名称现在为"**新建文本"。**
