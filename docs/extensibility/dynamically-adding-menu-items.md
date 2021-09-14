---
title: 动态添加菜单项|Microsoft Docs
description: 了解如何在运行时使用 DynamicItemStart 命令标志添加菜单项。 本文演示如何在解决方案中设置启动Visual Studio项目。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- DYNAMICITEMSTART
- menu items, adding dynamically
- menus, adding dynamic items
ms.assetid: d281e9c9-b289-4d64-8d0a-094bac6c333c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: e7875b939748ff5140d65a1b17ffe30c6ecfac88
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665354"
---
# <a name="dynamically-add-menu-items"></a>动态添加菜单项
可以通过在 Visual Studio 命令表 `DynamicItemStart` (*.vsct*) 文件中指定占位符按钮定义上的命令标志，然后在代码中定义 () )  (以显示和处理命令的菜单项数，来添加菜单项。 加载 VSPackage 时，占位符将替换为动态菜单项。

 Visual Studio使用"最近使用的 **(** MRU) "列表中的动态列表（显示最近打开的文档的名称）和 **Windows** 列表（显示当前打开的窗口的名称）。   `DynamicItemStart`命令定义上的 标志指定命令是占位符，直到 VSPackage 打开。 打开 VSPackage 时，占位符将替换为 0 个或多个命令，这些命令会运行时创建并添加到动态列表中。 在 VSPackage 打开之前，可能无法在菜单上看到动态列表出现的位置。  若要填充动态列表，Visual Studio VSPackage 查找 ID 为 的命令，该命令的第一个字符与占位符的 ID 相同。 当Visual Studio找到匹配的命令时，它会将命令的名称添加到动态列表中。 然后，它会递增 ID 并查找要添加到动态列表中的另一个匹配命令，直到没有更多的动态命令。

 本演练演示如何使用 Visual Studio 工具栏上的 命令在 解决方案资源管理器 解决方案 **中设置** 启动项目。 它使用菜单控制器，该控制器具有活动解决方案中项目的动态下拉列表。 若要在未打开解决方案或打开的解决方案只有一个项目时显示此命令，只有在解决方案有多个项目时，才加载 VSPackage。

 有关 *.vsct* 文件的信息，请参阅 Visual Studio [命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

## <a name="create-an-extension-with-a-menu-command"></a>使用菜单命令创建扩展

1. 创建名为 的 VSIX 项目 `DynamicMenuItems` 。

2. 项目打开时，添加自定义命令项模板，将其命名为 **DynamicMenu**。 有关详细信息，请参阅 [使用菜单命令 创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="setting-up-the-elements-in-the-vsct-file"></a>设置 *.vsct 文件中* 的元素
 若要在工具栏上创建包含动态菜单项的菜单控制器，请指定以下元素：

- 两个命令组，一个包含菜单控制器，另一个包含下拉列表中的菜单项

- 一个类型的菜单元素 `MenuController`

- 两个按钮，一个充当菜单项的占位符，另一个按钮在工具栏上提供图标和工具提示。

1. 在 *DynamicMenuPackage.vsct* 中，定义命令"ID"。 转到"符号"部分，替换 **guidDynamicMenuPackageCmdSet** GuidSymbol 块中的 IDSymbol 元素。 需要为两个组（菜单控制器、占位符命令和定位点命令）定义 IDSymbol 元素。

    ```xml
    <GuidSymbol name="guidDynamicMenuPackageCmdSet" value="{ your GUID here }">
        <IDSymbol name="MyToolbarItemGroup" value="0x1020" />
        <IDSymbol name="MyMenuControllerGroup" value="0x1025" />
        <IDSymbol name="MyMenuController" value ="0x1030"/>
        <IDSymbol name="cmdidMyAnchorCommand" value="0x0103" />
        <!-- NOTE: The following command expands at run time to some number of ids.
         Try not to place command ids after it (e.g. 0x0105, 0x0106).
         If you must add a command id after it, make the gap very large (e.g. 0x200) -->
        <IDSymbol name="cmdidMyDynamicStartCommand" value="0x0104" />
    </GuidSymbol>
    ```

2. 在"组"部分中，删除现有组并添加刚刚定义的两个组：

    ```xml
    <Groups>
        <!-- The group that adds the MenuController on the Solution Explorer toolbar.
             The 0x4000 priority adds this group after the group that contains the
             Preview Selected Items button, which is normally at the far right of the toolbar. -->
        <Group guid="guidDynamicMenuPackageCmdSet" id="MyToolbarItemGroup" priority="0x4000" >
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN" />
        </Group>
        <!-- The group for the items on the MenuController drop-down. It is added to the MenuController submenu. -->
        <Group guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" priority="0x4000" >
            <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" />
        </Group>
    </Groups>
    ```

     添加 MenuController。 设置 DynamicVisibility 命令标志，因为它并不总是可见。 不显示 ButtonText。

    ```xml
    <Menus>
        <!-- The MenuController to display on the Solution Explorer toolbar.
             Place it in the ToolbarItemGroup.-->
        <Menu guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" priority="0x1000" type="MenuController">
            <Parent guid="guidDynamicMenuPackageCmdSet" id="MyToolbarItemGroup" />
            <CommandFlag>DynamicVisibility</CommandFlag>
            <Strings>
               <ButtonText></ButtonText>
           </Strings>
        </Menu>
    </Menus>
    ```

3. 添加两个按钮，一个按钮作为动态菜单项的占位符，另一个作为 MenuController 的定位点。

     占位符按钮的父级是 **MyMenuControllerGroup**。 将 DynamicItemStart、DynamicVisibility 和 TextChanges 命令标志添加到占位符按钮。 不显示 ButtonText。

     定位点按钮保存图标和工具提示文本。 定位点按钮的父级也是 **MyMenuControllerGroup**。 添加 NoShowOnMenuController 命令标志，以确保按钮实际上不会出现在菜单控制器下拉列表中，并添加 FixMenuController 命令标志，使其成为永久定位点。

    ```xml
    <!-- The placeholder for the dynamic items that expand to N items at run time. -->
    <Buttons>
        <Button guid="guidDynamicMenuPackageCmdSet" id="cmdidMyDynamicStartCommand" priority="0x1000" >
          <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" />
          <CommandFlag>DynamicItemStart</CommandFlag>
          <CommandFlag>DynamicVisibility</CommandFlag>
          <CommandFlag>TextChanges</CommandFlag>
          <!-- This text does not appear. -->
          <Strings>
            <ButtonText>Project</ButtonText>
          </Strings>
        </Button>

        <!-- The anchor item to supply the icon/tooltip for the MenuController -->
        <Button guid="guidDynamicMenuPackageCmdSet" id="cmdidMyAnchorCommand" priority="0x0000" >
          <Parent guid="guidDynamicMenuPackageCmdSet" id="MyMenuControllerGroup" />
          <!-- This is the icon that appears on the Solution Explorer toolbar. -->
          <Icon guid="guidImages" id="bmpPicArrows"/>
          <!-- Do not show on the menu controller's drop down list-->
          <CommandFlag>NoShowOnMenuController</CommandFlag>
          <!-- Become the permanent anchor item for the menu controller -->
          <CommandFlag>FixMenuController</CommandFlag>
          <!-- The text that appears in the tooltip.-->
          <Strings>
            <ButtonText>Set Startup Project</ButtonText>
          </Strings>
        </Button>
    </Buttons>
    ```

4. 将图标添加到"资源" (中的项目) ，然后在 *.vsct* 文件中添加对它的引用。 本演练使用项目模板中包含的箭头图标。

5. 在"命令"部分外部的"符号"部分之前添加 VisibilityConstraints 部分。  (如果在 Symbols.) 之后添加，则可能会收到警告。本部分确保菜单控制器仅在加载包含多个项目的解决方案时显示。

    ```xml
    <VisibilityConstraints>
         <!--Make the MenuController show up only when there is a solution with more than one project loaded-->
        <VisibilityItem guid="guidDynamicMenuPackageCmdSet" id="MyMenuController" context="UICONTEXT_SolutionHasMultipleProjects"/>
    </VisibilityConstraints>
    ```

## <a name="implement-the-dynamic-menu-command"></a>实现动态菜单命令
 创建继承自 的动态菜单命令类 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 。 在此实现中，构造函数指定用于匹配命令的谓词。 必须重写 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A> 方法以使用此谓词设置 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A> 属性，该属性标识要调用的命令。

1. 创建名为 *DynamicItemMenuCommand.cs* 的新 C# 类文件，并添加从 继承的名为 **DynamicItemMenuCommand** 的类 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> ：

    ```csharp
    class DynamicItemMenuCommand : OleMenuCommand
    {

    }

    ```

2. 添加以下 using 指令：

    ```csharp
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.Shell.Interop;
    using System.ComponentModel.Design;
    ```

3. 添加专用字段以存储匹配谓词：

    ```csharp
    private Predicate<int> matches;

    ```

4. 添加从构造函数继承的 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand> 构造函数，并指定命令处理程序和 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> 处理程序。 添加用于匹配命令的谓词：

    ```csharp
    public DynamicItemMenuCommand(CommandID rootId, Predicate<int> matches, EventHandler invokeHandler, EventHandler beforeQueryStatusHandler)
        : base(invokeHandler, null /*changeHandler*/, beforeQueryStatusHandler, rootId)
    {
        if (matches == null)
        {
            throw new ArgumentNullException("matches");
        }

        this.matches = matches;
    }
    ```

5. 重写 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.DynamicItemMatch%2A> 方法，以便调用匹配谓词并设置 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.MatchedCommandId%2A> 属性：

    ```csharp
    public override bool DynamicItemMatch(int cmdId)
    {
        // Call the supplied predicate to test whether the given cmdId is a match.
        // If it is, store the command id in MatchedCommandid
        // for use by any BeforeQueryStatus handlers, and then return that it is a match.
        // Otherwise clear any previously stored matched cmdId and return that it is not a match.
        if (this.matches(cmdId))
        {
            this.MatchedCommandId = cmdId;
            return true;
        }

        this.MatchedCommandId = 0;
        return false;
    }
    ```

## <a name="add-the-command"></a>添加 命令
 DynamicMenu 构造函数用于设置菜单命令，包括动态菜单和菜单项。

1. 在 *DynamicMenuPackage.cs* 中，添加命令集的 GUID 和命令 ID：

    ```csharp
    public const string guidDynamicMenuPackageCmdSet = "00000000-0000-0000-0000-00000000";  // get the GUID from the .vsct file
    public const uint cmdidMyCommand = 0x104;
    ```

2. 在 *DynamicMenu.cs* 文件中，添加以下 using 指令：

    ```csharp
    using EnvDTE;
    using EnvDTE80;
    using System.ComponentModel.Design;
    ```

3. 在 类 `DynamicMenu` 中，添加私有字段 **dte2**。

    ```csharp
    private DTE2 dte2;
    ```

4. 添加专用 rootItemId 字段：

    ```csharp
    private int rootItemId = 0;
    ```

5. 在 DynamicMenu 构造函数中，添加菜单命令。 下一部分将定义命令处理程序、 `BeforeQueryStatus` 事件处理程序和匹配谓词。

    ```csharp
    private DynamicMenu(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException(nameof(package));
        }

        this.package = package;

        OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;
        if (commandService != null)
        {
            // Add the DynamicItemMenuCommand for the expansion of the root item into N items at run time.
            CommandID dynamicItemRootId = new CommandID(new Guid(DynamicMenuPackageGuids.guidDynamicMenuPackageCmdSet), (int)DynamicMenuPackageGuids.cmdidMyCommand);
            DynamicItemMenuCommand dynamicMenuCommand = new DynamicItemMenuCommand(dynamicItemRootId,
                IsValidDynamicItem,
                OnInvokedDynamicItem,
                OnBeforeQueryStatusDynamicItem);
                commandService.AddCommand(dynamicMenuCommand);
                }

        dte2 = (DTE2)this.ServiceProvider.GetService(typeof(DTE));
    }
    ```

## <a name="implement-the-handlers"></a>实现处理程序
 若要在菜单控制器上实现动态菜单项，必须在单击动态项时处理 命令。 还必须实现用于设置菜单项状态的逻辑。 将处理程序添加到 `DynamicMenu` 类。

1. 若要实现 Set **Startup Project** 命令，请添加 **OnInvokedDynamicItem** 事件处理程序。 它查找其名称与已调用命令的文本相同的项目，并设置其属性中的绝对路径，将该项目设置为启动 <xref:EnvDTE.SolutionBuild.StartupProjects%2A> 项目。

    ```csharp
    private void OnInvokedDynamicItem(object sender, EventArgs args)
    {
        DynamicItemMenuCommand invokedCommand = (DynamicItemMenuCommand)sender;
        // If the command is already checked, we don't need to do anything
        if (invokedCommand.Checked)
            return;

        // Find the project that corresponds to the command text and set it as the startup project
        var projects = dte2.Solution.Projects;
        foreach (Project proj in projects)
        {
            if (invokedCommand.Text.Equals(proj.Name))
            {
                dte2.Solution.SolutionBuild.StartupProjects = proj.FullName;
                return;
            }
        }
    }
    ```

2. 添加 `OnBeforeQueryStatusDynamicItem` 事件处理程序。 这是在事件之前调用的 `QueryStatus` 处理程序。 它确定菜单项是否是"实际"项，即不是占位符项，以及是否已选中该项 (这意味着项目已设置为启动项目) 。

    ```csharp
    private void OnBeforeQueryStatusDynamicItem(object sender, EventArgs args)
    {
        DynamicItemMenuCommand matchedCommand = (DynamicItemMenuCommand)sender;
        matchedCommand.Enabled = true;
        matchedCommand.Visible = true;

        // Find out whether the command ID is 0, which is the ID of the root item.
        // If it is the root item, it matches the constructed DynamicItemMenuCommand,
         // and IsValidDynamicItem won't be called.
        bool isRootItem = (matchedCommand.MatchedCommandId == 0);

        // The index is set to 1 rather than 0 because the Solution.Projects collection is 1-based.
        int indexForDisplay = (isRootItem ? 1 : (matchedCommand.MatchedCommandId - (int) DynamicMenuPackageGuids.cmdidMyCommand) + 1);

        matchedCommand.Text = dte2.Solution.Projects.Item(indexForDisplay).Name;

        Array startupProjects = (Array)dte2.Solution.SolutionBuild.StartupProjects;
        string startupProject = System.IO.Path.GetFileNameWithoutExtension((string)startupProjects.GetValue(0));

        // Check the command if it isn't checked already selected
        matchedCommand.Checked = (matchedCommand.Text == startupProject);

        // Clear the ID because we are done with this item.
        matchedCommand.MatchedCommandId = 0;
    }
    ```

## <a name="implement-the-command-id-match-predicate"></a>实现命令 ID 匹配谓词

现在实现匹配谓词。 我们需要确定两点：首先，命令 ID 是否有效 (它是否大于或等于声明的命令 ID) ;第二，它是否指定了可能的项目 (它小于解决方案) 中的项目数。

```csharp
private bool IsValidDynamicItem(int commandId)
{
    // The match is valid if the command ID is >= the id of our root dynamic start item
    // and the command ID minus the ID of our root dynamic start item
    // is less than or equal to the number of projects in the solution.
    return (commandId >= (int)DynamicMenuPackageGuids.cmdidMyCommand) && ((commandId - (int)DynamicMenuPackageGuids.cmdidMyCommand) < dte2.Solution.Projects.Count);
}
```

## <a name="set-the-vspackage-to-load-only-when-a-solution-has-multiple-projects"></a>将 VSPackage 设置为仅在解决方案具有多个项目时加载
 由于 **"Project** 启动"命令没有意义，除非活动解决方案具有多个项目，因此可以将 VSPackage 设置为仅在这种情况下自动加载。 与 <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> UI 上下文 一起使用 <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids.SolutionHasMultipleProjects> 。 在 *DynamicMenuPackage.cs* 文件中，将以下属性添加到 DynamicMenuPackage 类：

```csharp
[PackageRegistration(UseManagedResourcesOnly = true)]
[InstalledProductRegistration("#110", "#112", "1.0", IconResourceID = 400)]
[ProvideMenuResource("Menus.ctmenu", 1)]
[ProvideAutoLoad(UIContextGuids.SolutionHasMultipleProjects)]
[Guid(DynamicMenuPackage.PackageGuidString)]
public sealed class DynamicMenuItemsPackage : Package
{}
```

## <a name="test-the-set-startup-project-command"></a>测试 set startup project 命令
 现在，可以测试代码。

1. 生成项目并启动调试。 应显示实验实例。

2. 在实验实例中，打开具有多个项目的解决方案。

     应在工具栏上看到箭头 **解决方案资源管理器** 图标。 展开它时，应显示表示解决方案中不同项目的菜单项。

3. 检查其中一个项目时，它将成为启动项目。

4. 关闭解决方案或打开只有一个项目的解决方案时，工具栏图标应消失。

## <a name="see-also"></a>另请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
- [VSPackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
