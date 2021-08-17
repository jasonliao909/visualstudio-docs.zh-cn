---
title: 将最近使用的列表添加到子|Microsoft Docs
description: 了解如何将包含最近使用的菜单命令的动态列表添加到 IDE Visual Studio 集成开发 (子菜单中) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- MRU lists
- menus, creating MRU list
- most recently used
ms.assetid: 27d4bbcf-99b1-498f-8b66-40002e3db0f8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 71c649d9eeb66b67cde133bef6a525427c618209
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122035327"
---
# <a name="add-a-most-recently-used-list-to-a-submenu"></a>将最近使用的列表添加到子项
本演练基于将子菜单添加到菜单中的演示，[](../extensibility/adding-a-submenu-to-a-menu.md)并演示如何向子菜单添加动态列表。 动态列表构成了创建 MRU (最近) 的基础。

动态菜单列表以菜单上的占位符开头。 每次显示菜单时，Visual Studio集成开发环境 (IDE) 向 VSPackage 询问应显示在占位符上的所有命令。 动态列表可以出现在菜单上的任意位置。 但是，动态列表通常自行在子菜单或菜单底部存储和显示。 使用这些设计模式，可以启用命令的动态列表以展开和收缩，而不会影响菜单上其他命令的位置。 在此演练中，动态 MRU 列表显示在现有子菜单的底部，与子菜单的其余部分之间用一行分隔。

从技术上说，动态列表也可以应用于工具栏。 但是，我们禁止使用，因为工具栏应保持不变，除非用户执行特定步骤来更改它。

本演练创建包含四个项的 MRU 列表，这些项每次选择其中一个项时都会更改其顺序 (所选项移动到列表顶部) 。

有关菜单和 *.vsct 文件的信息* ，请参阅 [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

## <a name="prerequisites"></a>先决条件
要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

## <a name="create-an-extension"></a>创建一个扩展

- 按照将子 [菜单添加到菜单中](../extensibility/adding-a-submenu-to-a-menu.md) 的过程创建在下列过程中修改的子菜单。

  本演练中的过程假定 VSPackage 的名称为 ，这是在将菜单添加到菜单栏 `TestCommand` [中使用的Visual Studio的名称](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)。

## <a name="create-a-dynamic-item-list-command"></a>创建动态项列表命令

1. 打开 *TestCommandPackage.vsct*。

2. 在 部分 `Symbols` ，在名为 `GuidSymbol` guidTestCommandPackageCmdSet 的节点中，为组和 命令添加 符号 `MRUListGroup` `cmdidMRUList` ，如下所示。

    ```xml
    <IDSymbol name="MRUListGroup" value="0x1200"/>
    <IDSymbol name="cmdidMRUList" value="0x0200"/>
    ```

3. 在 `Groups` 节中，将声明的组添加到现有组条目之后。

    ```xml
    <Group guid="guidTestCommandPackageCmdSet" id="MRUListGroup"
            priority="0x0100">
        <Parent guid="guidTestCommandPackageCmdSet" id="SubMenu"/>
    </Group>
    ```

4. 在 `Buttons` 节中，添加一个节点来表示新声明的命令（在现有的按钮条目之后）。

    ```xml
    <Button guid="guidTestCommandPackageCmdSet" id="cmdidMRUList"
        type="Button" priority="0x0100">
        <Parent guid="guidTestCommandPackageCmdSet" id="MRUListGroup" />
        <CommandFlag>DynamicItemStart</CommandFlag>
        <Strings>
            <CommandName>cmdidMRUList</CommandName>
            <ButtonText>MRU Placeholder</ButtonText>
        </Strings>
    </Button>
    ```

    `DynamicItemStart`标志允许动态生成命令。

5. 生成项目并开始调试以测试新命令的显示。

    在 **"TestMenu"** 菜单上，单击新的子菜单"子 **菜单**"以显示新命令 **MRU 占位符**。 下一个过程中实现命令的动态 MRU 列表后，每次打开子菜单时，此命令标签都将替换为该列表。

## <a name="filling-the-mru-list"></a>填写 MRU 列表

1. 在 *TestCommandPackageGuids.cs* 中，在类定义中的现有命令 ID 之后添加 `TestCommandPackageGuids` 以下行。

    ```csharp
    public const string guidTestCommandPackageCmdSet = "00000000-0000-0000-0000-00000000"; // get the GUID from the .vsct file
    public const uint cmdidMRUList = 0x200;
    ```

2. 在 *TestCommand.cs 中添加* 以下 using 语句。

    ```csharp
    using System.Collections;
    ```

3. 最后一个 AddCommand 调用后，在 TestCommand 构造函数中添加以下代码。 `InitMRUMenu`稍后将定义

    ```csharp
    this.InitMRUMenu(commandService);
    ```

4. 在 TestCommand 类中添加以下代码。 此代码初始化表示 MRU 列表中要显示的项的字符串列表。

    ```csharp
    private int numMRUItems = 4;
    private int baseMRUID = (int)TestCommandPackageGuids.cmdidMRUList;
    private ArrayList mruList;

    private void InitializeMRUList()
    {
        if (null == this.mruList)
        {
            this.mruList = new ArrayList();
            if (null != this.mruList)
            {
                for (int i = 0; i < this.numMRUItems; i++)
                {
                    this.mruList.Add(string.Format(CultureInfo.CurrentCulture,
                        "Item {0}", i + 1));
                }
            }
        }
    }
    ```

5. 在 `InitializeMRUList` 方法之后，添加 `InitMRUMenu` 方法。 这会初始化 MRU 列表菜单命令。

    ```csharp
    private void InitMRUMenu(OleMenuCommandService mcs)
    {
        InitializeMRUList();
        for (int i = 0; i < this.numMRUItems; i++)
        {
            var cmdID = new CommandID(
                new Guid(TestCommandPackageGuids.guidTestCommandPackageCmdSet), this.baseMRUID + i);
            var mc = new OleMenuCommand(
                new EventHandler(OnMRUExec), cmdID);
            mc.BeforeQueryStatus += new EventHandler(OnMRUQueryStatus);
            mcs.AddCommand(mc);
        }
    }
    ```

    必须为 MRU 列表中的每个可能项创建菜单命令对象。 IDE 为 `OnMRUQueryStatus` MRU 列表中的每个项调用 方法，直到没有更多项。 在托管代码中，IDE 知道没有更多项的唯一方法就是先创建所有可能的项。 如果需要，可以在创建菜单命令后使用 将其他项标记为不可见 `mc.Visible = false;` 。 然后，可以在 方法中使用这些项，使 `mc.Visible = true;` 这些项在以后 `OnMRUQueryStatus` 可见。

6. 在 `InitMRUMenu` 方法之后，添加以下 `OnMRUQueryStatus` 方法。 这是设置每个 MRU 项的文本的处理程序。

    ```csharp
    private void OnMRUQueryStatus(object sender, EventArgs e)
    {
        OleMenuCommand menuCommand = sender as OleMenuCommand;
        if (null != menuCommand)
        {
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)
            {
                menuCommand.Text = this.mruList[MRUItemIndex] as string;
            }
        }
    }
    ```

7. 在 `OnMRUQueryStatus` 方法之后，添加以下 `OnMRUExec` 方法。 这是用于选择 MRU 项的处理程序。 此方法将所选项移动到列表顶部，然后在消息框中显示所选项。

    ```csharp
    private void OnMRUExec(object sender, EventArgs e)
    {
        var menuCommand = sender as OleMenuCommand;
        if (null != menuCommand)
        {
            int MRUItemIndex = menuCommand.CommandID.ID - this.baseMRUID;
            if (MRUItemIndex >= 0 && MRUItemIndex < this.mruList.Count)
            {
                string selection = this.mruList[MRUItemIndex] as string;
                for (int i = MRUItemIndex; i > 0; i--)
                {
                    this.mruList[i] = this.mruList[i - 1];
                }
                this.mruList[0] = selection;
                System.Windows.Forms.MessageBox.Show(
                    string.Format(CultureInfo.CurrentCulture,
                                  "Selected {0}", selection));
            }
        }
    }
    ```

## <a name="testing-the-mru-list"></a>测试 MRU 列表

1. 生成项目并启动调试。

2. 在 **"TestMenu"菜单** 上，单击 **"调用 TestCommand"。** 执行此操作会显示一个消息框，指示已选择该命令。

    > [!NOTE]
    > 必须执行此步骤才能强制 VSPackage 加载并正确显示 MRU 列表。 如果跳过此步骤，则不显示 MRU 列表。

3. 在"测试 **菜单"菜单** 上，单击"**子菜单"。** 子菜单的末尾（分隔符下方）显示四个项的列表。 单击"**项目 3"时**，应会出现一个消息框并显示文本 **"选定项 3"。**  (如果未显示四个项的列表，请确保已按照前面步骤中的说明) 

4. 再次打开子menu。 请注意 **，项 3** 现在位于列表顶部，其他项已向下推送一个位置。 再次单击"项 **3"，** 请注意，消息框仍显示"选定项 **3"，** 这表示文本已与命令标签一起正确移动到新位置。

## <a name="see-also"></a>请参阅
- [动态添加菜单项](../extensibility/dynamically-adding-menu-items.md)
