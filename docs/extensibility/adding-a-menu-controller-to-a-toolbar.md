---
title: 将菜单控制器添加到工具栏|Microsoft Docs
description: 了解如何创建菜单控制器，并将其添加到 Visual Studio 工具窗口工具栏，然后实现菜单控制器命令并测试它。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- toolbars [Visual Studio], adding menu controllers
- menus, adding menu controllers to toolbars
- menu controllers, adding to toolbars
ms.assetid: 6af9b0b4-037f-404c-bb40-aaa1970768ea
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 439b9475c92eb78e7deed63c3718d73dd9f81a4d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122111991"
---
# <a name="add-a-menu-controller-to-a-toolbar"></a>将菜单控制器添加到工具栏
本演练基于向工具窗口添加工具栏[](../extensibility/adding-a-toolbar-to-a-tool-window.md)演练生成，并演示如何将菜单控制器添加到工具窗口工具栏。 此处显示的步骤也可以应用于在添加工具栏演练中创建的工具栏。 [](../extensibility/adding-a-toolbar.md)

菜单控制器是拆分控件。 菜单控制器的左侧显示最后使用的命令，可以通过单击它来运行该命令。 菜单控制器的右侧是一个箭头，单击该箭头会打开其他命令的列表。 单击列表中的命令时，该命令将运行，并替换菜单控制器左侧的命令。 这样，菜单控制器的运行方式就像命令按钮一样，始终显示列表中最后使用的命令。

菜单控制器可以显示在菜单上，但它们通常用于工具栏。

## <a name="prerequisites"></a>必备条件
从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-a-menu-controller"></a>创建菜单控制器

1. 按照向工具 [窗口添加工具栏中所述的过程](../extensibility/adding-a-toolbar-to-a-tool-window.md) 创建具有工具栏的工具窗口。

2. 在 *TWTestCommandPackage.vsct* 中，转到"符号"部分。 在名为 **guidTWTestCommandPackageCmdSet** 的 GuidSymbol 元素中，声明菜单控制器、菜单控制器组和三个菜单项。

    ```xml
    <IDSymbol name="TestMenuController" value="0x1300" /><IDSymbol name="TestMenuControllerGroup" value="0x1060" /><IDSymbol name="cmdidMCItem1" value="0x0130" /><IDSymbol name="cmdidMCItem2" value="0x0131" /><IDSymbol name="cmdidMCItem3" value="0x0132" />
    ```

3. 在"菜单"部分中，最后一个菜单项之后，将菜单控制器定义为菜单。

    ```xml
    <Menu guid="guidTWTestCommandPackageCmdSet" id="TestMenuController" priority="0x0100" type="MenuController">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TWToolbarGroup" />
        <CommandFlag>IconAndText</CommandFlag>
        <CommandFlag>TextChanges</CommandFlag>
        <CommandFlag>TextIsAnchorCommand</CommandFlag>
        <Strings>
            <ButtonText>Test Menu Controller</ButtonText>
            <CommandName>Test Menu Controller</CommandName>
        </Strings>
    </Menu>
    ```

    必须 `TextChanges` `TextIsAnchorCommand` 包含 和 标志，使菜单控制器能够反映上次选择的命令。

4. 在"组"部分的最后一个组条目之后，添加菜单控制器组。

    ```xml
    <Group guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" priority="0x000">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuController" />
    </Group>
    ```

    将菜单控制器设置为父级后，放置在此组的任何命令都将显示在菜单控制器中。 `priority`省略 属性，该属性将设置为默认值 0，因为它是菜单控制器上的唯一组。

5. 在"按钮"部分中，最后一个按钮条目后，为每个菜单项添加 Button 元素。

    ```xml
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem1" priority="0x0000" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 1</ButtonText>
            <CommandName>MC Item 1</CommandName>
        </Strings>
    </Button>
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem2" priority="0x0100" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPic2" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 2</ButtonText>
            <CommandName>MC Item 2</CommandName>
        </Strings>
    </Button>
    <Button guid="guidTWTestCommandPackageCmdSet" id="cmdidMCItem3" priority="0x0200" type="Button">
        <Parent guid="guidTWTestCommandPackageCmdSet" id="TestMenuControllerGroup" />
        <Icon guid="guidImages" id="bmpPicSearch" />
        <CommandFlag>IconAndText</CommandFlag>
        <Strings>
            <ButtonText>MC Item 3</ButtonText>
            <CommandName>MC Item 3</CommandName>
        </Strings>
    </Button>
    ```

6. 此时，你可以查看菜单控制器。 生成项目并启动调试。 应会看到实验实例。

   1. 在"**视图/其他Windows"** 菜单上，打开"**测试工具""Window"。**

   2. 菜单控制器将显示在工具窗口的工具栏上。

   3. 单击菜单控制器右侧箭头以查看三个可能的命令。

      请注意，单击命令时，菜单控制器的标题将更改以显示该命令。 下一部分将添加用于激活这些命令的代码。

## <a name="implement-the-menu-controller-commands"></a>实现菜单控制器命令

1. 在 *TWTestCommandPackageGuids.cs* 中，将三个菜单项的命令 ID 添加到现有命令 ID 之后。

    ```csharp
    public const int cmdidMCItem1 = 0x130;
    public const int cmdidMCItem2 = 0x131;
    public const int cmdidMCItem3 = 0x132;
    ```

2. 在 *TWTestCommand.cs* 中，在 类的顶部添加以下 `TWTestCommand` 代码。

    ```csharp
    private int currentMCCommand; // The currently selected menu controller command
    ```

3. 在 TWTestCommand 构造函数中，最后一次调用 方法后，添加代码以通过相同的处理程序路由每个 `AddCommand` 命令的事件。

    ```csharp
    for (int i = TWTestCommandPackageGuids.cmdidMCItem1; i <=
        TWTestCommandPackageGuids.cmdidMCItem3; i++)
    {
        CommandID cmdID = new
        CommandID(new Guid(TWTestCommandPackageGuids.guidTWTestCommandPackageCmdSet), i);
        OleMenuCommand mc = new OleMenuCommand(new
          EventHandler(OnMCItemClicked), cmdID);
        mc.BeforeQueryStatus += new EventHandler(OnMCItemQueryStatus);
        commandService.AddCommand(mc);
        // The first item is, by default, checked. 
        if (TWTestCommandPackageGuids.cmdidMCItem1 == i)
        {
            mc.Checked = true;
            this.currentMCCommand = i;
        }
    }
    ```

4. 将事件处理程序添加到 **TWTestCommand** 类，以将所选命令标记为已选中。

    ```csharp
    private void OnMCItemQueryStatus(object sender, EventArgs e)
    {
        OleMenuCommand mc = sender as OleMenuCommand;
        if (null != mc)
        {
            mc.Checked = (mc.CommandID.ID == this.currentMCCommand);
        }
    }
    ```

5. 添加一个事件处理程序，当用户在菜单控制器上选择命令时显示 MessageBox：

    ```csharp
    private void OnMCItemClicked(object sender, EventArgs e)
    {
        OleMenuCommand mc = sender as OleMenuCommand;
        if (null != mc)
        {
            string selection;
            switch (mc.CommandID.ID)
            {
                case c.cmdidMCItem1:
                    selection = "Menu controller Item 1";
                    break;

                case TWTestCommandPackageGuids.cmdidMCItem2:
                    selection = "Menu controller Item 2";
                    break;

                case TWTestCommandPackageGuids.cmdidMCItem3:
                    selection = "Menu controller Item 3";
                    break;

                default:
                    selection = "Unknown command";
                    break;
            }
            this.currentMCCommand = mc.CommandID.ID;

            IVsUIShell uiShell =
              (IVsUIShell) ServiceProvider.GetService(typeof(SVsUIShell));
            Guid clsid = Guid.Empty;
            int result;
            uiShell.ShowMessageBox(
                    0,
                    ref clsid,
                    "Test Tool Window Toolbar Package",
                    string.Format(CultureInfo.CurrentCulture,
                                 "You selected {0}", selection),
                    string.Empty,
                    0,
                    OLEMSGBUTTON.OLEMSGBUTTON_OK,
                    OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST,
                    OLEMSGICON.OLEMSGICON_INFO,
                    0,
                    out result);
        }
    }
    ```

## <a name="testing-the-menu-controller"></a>测试菜单控制器

1. 生成项目并启动调试。 应会看到实验实例。

2. 在"**视图"/"其他"菜单****上打开"测试工具Windows** 窗口。

    菜单控制器将显示在工具窗口的工具栏中，并显示 MC **项 1。**

3. 单击箭头左侧的菜单控制器按钮。

    应会看到三个项，其中第一个项已选中，其图标周围有一个突出显示框。 单击 **"MC 项目 3"。**

    将出现一个对话框，显示消息"**你选择了菜单控制器项 3"。** 请注意，该消息对应于菜单控制器按钮上的文本。 菜单控制器按钮现在显示 **MC 项 3。**

## <a name="see-also"></a>请参阅
- [向工具窗口添加工具栏](../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [添加工具栏](../extensibility/adding-a-toolbar.md)
