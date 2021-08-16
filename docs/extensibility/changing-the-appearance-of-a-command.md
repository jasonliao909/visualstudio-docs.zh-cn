---
title: 更改命令命令|Microsoft Docs
description: 了解如何提供更改命令外观的反馈，例如使命令可用/不可用、隐藏/显示或已选中/未选中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- commands, changing appearance
- menu commands, changing appearance
- menus, changing command appearance
ms.assetid: da2474fa-f92d-4e9e-b8bf-67c61bf249c2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6344d5d58856c420807e80020d80f0067d0f973c566b3e613782e5fa0b85ef11
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121452623"
---
# <a name="change-the-appearance-of-a-command"></a>更改命令的外观
可以通过更改命令的外观来为用户提供反馈。 例如，你可能希望命令在不可用时看起来不同。 可以使命令可用或不可用，隐藏或显示它们，或在菜单上选中或取消选中它们。

若要更改命令的外观，请执行以下操作之一：

- 在命令表文件的命令定义中指定相应的标志。

- 使用 <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> 服务。

- 实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口并修改原始命令对象。

  以下步骤显示如何使用 MPF 中的托管包框架查找和更新命令 (的外观) 。

### <a name="to-change-the-appearance-of-a-menu-command"></a>更改菜单命令的外观

1. 按照更改菜单 [命令的文本中的说明创建](../extensibility/changing-the-text-of-a-menu-command.md) 名为 的菜单项 `New Text` 。

2. 在 *ChangeMenuText.cs* 文件中，添加以下 using 语句：

    ```csharp
    using System.Security.Permissions;
    ```

3. 在 *ChangeMenuTextPackageGuids.cs* 文件中，添加以下行：

    ```csharp
    public const string guidChangeMenuTextPackageCmdSet= "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file
    ```

4. 在 *ChangeMenuText.cs* 文件中，将 ShowMessageBox 方法中的代码替换为以下内容：

    ```csharp
    private void Execute(object sender, EventArgs e)
    {
        ThreadHelper.ThrowIfNotOnUIThread();
        var command = sender as OleMenuCommand;
        if (command.Text == "New Text")
            ChangeMyCommand(command.CommandID.ID, false);
    }
    ```

5. 从 对象获取要更新的命令 <xref:Microsoft.VisualStudio.Shell.OleMenuCommandService> ，然后在命令对象上设置相应的属性。 例如，以下方法使 VSPackage 命令集的指定命令可用或不可用。 以下代码使名为 的菜单项 `New Text` 在单击后不可用。

    ```csharp
    public bool ChangeMyCommand(int cmdID, bool enableCmd)
    {
        bool cmdUpdated = false;
        var mcs = this.package.GetService<IMenuCommandService, OleMenuCommandService>();
        var newCmdID = new CommandID(new Guid(ChangeMenuTextPackageGuids.guidChangeMenuTextPackageCmdSet), cmdID);
        MenuCommand mc = mcs.FindCommand(newCmdID);
        if (mc != null)
        {
            mc.Enabled = enableCmd;
            cmdUpdated = true;
        }
        return cmdUpdated;
    }
    ```

6. 生成项目并启动调试。 应显示 Visual Studio实例。

7. 在" **工具"** 菜单上，单击 **"调用 ChangeMenuText"** 命令。 此时，命令名称为 **Invoke ChangeMenuText**，因此命令处理程序不会调用 **ChangeMyCommand () 。**

8. 在"**工具"** 菜单上，现在应会看到"**新建文本"。** 单击"**新建文本"。** 命令现在应灰显。

## <a name="see-also"></a>另请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
- [VSPackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
- [Visual Studio命令表 (。Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
