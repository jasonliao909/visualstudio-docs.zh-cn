---
title: 菜单&命令
description: 中菜单和命令系统的Visual Studio。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: f475a7369050697726dd8a63963c4bc0fb9519a9
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515860"
---
# <a name="adding-menus--commands-to-visual-studio-extensions"></a>将菜单&命令添加到Visual Studio扩展

本文逐步介绍如何将菜单和命令添加到Visual Studio扩展。 命令通常用作控件周围菜单中的Visual Studio。 若要创建命令，需要执行两个步骤：

1. 定义命令
2. 处理单击/调用

## <a name="define-the-command"></a>定义命令
每个菜单中的每一个按钮都是一个命令。 若要将命令添加到扩展，必须先在 .vsct 文件中定义该命令。 可能如下所示：

```xml
<Buttons>
  <Button guid="MyPackage" id="MyCommand" priority="0x0105" type="Button">
    <Parent guid="VSMainMenu" id="View.DevWindowsGroup.OtherWindows.Group1"/>
    <Icon guid="ImageCatalogGuid" id="StatusInformation" />
    <CommandFlag>IconIsMoniker</CommandFlag>
    <Strings>
      <ButtonText>R&amp;unner Window</ButtonText>
    </Strings>
  </Button>
</Buttons>
```

此按钮放置在父组中，位于"视图 **">"** 其他Windows菜单中，如 `Parent` 元素中指定。

现在可以运行扩展，查看命令是否显示在正确的位置和菜单中。

## <a name="handle-the-clickinvocations"></a>处理单击/调用
定义按钮后，我们需要处理调用按钮时发生的情况。 我们在如下所示的 C# 类中执行此操作：

```csharp
[Command("489ba882-f600-4c8b-89db-eb366a4ee3b3", 0x0100)]
public class MyCommand : BaseCommand<TestCommand>
{
    protected override Task ExecuteAsync(OleMenuCmdEventArgs e)
    {
        // Do something
    }
}
```

请确保从 类的 方法 `Package` 调用 `InitializeAsync` 它。

```csharp
protected override async Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
{
    await this.RegisterCommandsAsync();
 }    
```

命令 Guid 和 ID 必须与 .vsct 文件中元素的 guid/id `Button` 对匹配

## <a name="additional-resources"></a>其他资源

* [Visual Studio 命令表格 (.Vsct) 文件](../../internals/visual-studio-command-table-dot-vsct-files.md)
