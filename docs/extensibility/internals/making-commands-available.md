---
title: 使命令可用|Microsoft Docs
description: 了解如何使用延迟加载、上下文和可见性来控制在 VSPackages Visual Studio IDE 中添加的命令的可用性。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- best practices, menu and toolbar commands
- toolbars [Visual Studio], best practices
- menu commands, best practices
ms.assetid: 3ffc4312-c6db-4759-a946-a4bb85f4a17a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c92d9b34c669f5de4df8b9bd42cfb9e9e53996e2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600720"
---
# <a name="making-commands-available"></a>使命令可用

将多个 VSPackage 添加到 Visual Studio 时，UI (用户界面) 可能会过度使用命令。 你可以对包进行编程以帮助减少此问题，如下所示：

- 对包进行编程，以便仅在用户需要它时加载它。

- 对包进行编程，以便仅在 IDE 中集成开发环境的当前状态上下文中可能需要这些命令时显示 (命令) 。

## <a name="delayed-loading"></a>延迟加载

启用延迟加载的典型方法就是设计 VSPackage，以便其命令显示在 UI 中，但在用户单击其中一个命令之前不会加载包本身。 为此，在 .vsct 文件中，创建没有命令标志的命令。

以下示例显示 .vsct 文件中菜单命令的定义。 这是在选择模板中的"菜单命令"选项Visual Studio包模板生成的命令。 

```xml
<Button guid="guidTopLevelMenuCmdSet" id="cmdidTestCommand" priority="0x0100" type="Button">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <Strings>
    <CommandName>cmdidTestCommand</CommandName>
    <ButtonText>Test Command</ButtonText>
  </Strings>
</Button>
```

在示例中，如果父组 是顶级菜单（如"工具"菜单）的子级，则该命令将在该菜单上可见，但在用户单击命令之前，不会加载执行命令的包。 `MyMenuGroup`  但是，通过编程命令来实现 接口，可以在首次展开包含命令的菜单时加载 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 包。

请注意，延迟加载还可以提高启动性能。

## <a name="current-context-and-the-visibility-of-commands"></a>当前上下文和命令的可见性

可以将 VSPackage 命令编程为可见或隐藏，具体取决于 VSPackage 数据的当前状态或当前相关的操作。 可以启用 VSPackage 来设置其命令的状态（通常通过使用 接口中的 方法的实现），但这需要先加载 <xref:EnvDTE.IDTCommandTarget.QueryStatus%2A> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> VSPackage，然后才能执行代码。 相反，我们建议启用 IDE 来管理命令的可见性，而无需加载包。 为此，在 .vsct 文件中，将命令与一个或多个特殊 UI 上下文关联。 这些 UI 上下文由称为命令上下文 GUID 的 *GUID 标识*。

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 监视用户操作（如加载项目或从编辑到生成）导致的更改。 发生更改时，将自动修改 IDE 的外观。 下表显示了监视的 IDE 更改的四个主要 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 上下文。

| 上下文类型 | 说明 |
|-------------------------| - |
| 活动Project类型 | 对于大多数项目类型，此值与实现项目的 `GUID` VSPackage 的 GUID 相同。 但是 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] ，项目使用 Project Type `GUID` 作为值。 |
| 活动窗口 | 通常，这是最后一个为键绑定建立当前 UI 上下文的活动文档窗口。 但是，它也可能是一个工具窗口，该工具窗口具有类似于内部 Web 浏览器的键绑定表。 对于 HTML 编辑器等多选项卡文档窗口，每个选项卡具有不同的命令上下文 `GUID` 。 |
| 活动语言服务 | 与文本编辑器中当前显示的文件关联的语言服务。 |
| 活动工具窗口 | 打开且具有焦点的工具窗口。 |

第五个主要上下文区域是 IDE 的 UI 状态。 UI 上下文由活动命令上下文 `GUID` 标识，如下所示：

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Dragging_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.FullScreenMode_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.DesignMode_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.NoSolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.CodeWindow_guid>

这些 GUID 将标记为活动或不活动，具体取决于 IDE 的当前状态。 多个 UI 上下文可以同时处于活动状态。

### <a name="hide-and-display-commands-based-on-context"></a>根据上下文隐藏和显示命令

可以在 IDE 中显示或隐藏包命令，而无需加载包本身。 为此，请通过使用 、 和 命令标志，将一个或多个 VisibilityItem 元素添加到 `DefaultDisabled` `DefaultInvisible` `DynamicVisibility` [VisibilityConstraints](../../extensibility/visibilityconstraints-element.md) [](../../extensibility/visibilityitem-element.md)节，在包的 .vsct 文件中定义 命令。 当指定的命令上下文变为活动状态时， `GUID` 将显示该命令而不加载包。

### <a name="custom-context-guids"></a>自定义上下文 GUID

如果尚未定义相应的命令上下文 GUID，可以在 VSPackage 中定义一个，然后根据控制命令可见性的要求将其编程为活动或非活动。 使用 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> 服务可以：

- 通过调用 (注册上下文 GUID <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A>) 。

- 通过调用 方法 (`GUID` 获取上下文 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>) 。

- 通过 `GUID` 调用 方法 (启用和关闭 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A> 上下文) 。

    > [!CAUTION]
    > 请确保 VSPackage 不会影响任何现有上下文 GUID 的状态，因为其他 VSPackage 可能依赖于它们。

## <a name="example"></a>示例

下面的示例 VSPackage 命令演示了在不加载 VSPackage 的情况下由命令上下文管理的命令的动态可见性。

命令设置为在解决方案存在时启用并显示;也就是说，每当以下命令上下文 GUID 之一处于活动状态时：

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

请注意，在示例中，每个命令标志都是单独的 [命令标志](../../extensibility/command-flag-element.md) 元素。

```xml
<Button guid="guidDynamicVisibilityCmdSet" id="cmdidMyCommand"
        priority="0x0100" type="Button">
  <Parent guid="guidDynamicVisibilityCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <CommandFlag>DefaultDisabled</CommandFlag>
  <CommandFlag>DefaultInvisible</CommandFlag>
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <CommandName>cmdidMyCommand</CommandName>
    <ButtonText>My Command name</ButtonText>
  </Strings>
</Button>
```

另请注意，每个 UI 上下文都必须在单独的 元素中 `VisibilityItem` 提供，如下所示。

```xml
<VisibilityConstraints>
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                  id="cmdidMyCommand" context="UICONTEXT_EmptySolution" />
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                      id="cmdidMyCommand" context="UICONTEXT_SolutionHasSingleProject" />
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                  id="cmdidMyCommand" context="UICONTEXT_SolutionHasMultipleProjects" />
</VisibilityConstraints>
```

## <a name="see-also"></a>另请参阅

- [将命令添加到解决方案资源管理器工具栏](../../extensibility/adding-a-command-to-the-solution-explorer-toolbar.md)
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [VSPackage 中的命令传送](../../extensibility/internals/command-routing-in-vspackages.md)
- [动态添加菜单项](../../extensibility/dynamically-adding-menu-items.md)
