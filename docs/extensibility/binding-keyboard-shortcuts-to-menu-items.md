---
title: 将键盘快捷方式绑定到菜单项 |Microsoft Docs
description: 了解如何将 Visual Studio 中的键盘快捷方式映射到 "默认编辑器" 或 "自定义编辑器" 的自定义按钮、菜单项或工具栏命令。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- keyboard command
- keyboards
- command key
- keyboard shortcuts
- menu items
ms.assetid: 19f483b6-4d3e-424e-9d68-dc129c788e47
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 2ea954c65d55a85f15681e2b4bcc8a24fc957ae25ca1db513ee6d700cb1f1d49
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121308452"
---
# <a name="bind-keyboard-shortcuts-to-menu-items"></a>将键盘快捷方式绑定到菜单项
若要将键盘快捷方式绑定到自定义菜单命令，只需将条目添加到包的 *.vsct* 文件。 本主题说明如何将键盘快捷方式映射到自定义按钮、菜单项或工具栏命令，以及如何在默认编辑器中应用键盘映射或将其限制为自定义编辑器。

 若要为现有 Visual Studio 菜单项分配键盘快捷键，请参阅[标识并自定义键盘快捷方式](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)。

## <a name="choose-a-key-combination"></a>选择组合键
 许多键盘快捷方式已在 Visual Studio 中使用。 不应为多个命令分配相同的快捷方式，因为重复的绑定很难检测，也可能导致不可预知的结果。 因此，最好在分配快捷方式之前验证快捷方式的可用性。

### <a name="to-verify-the-availability-of-a-keyboard-shortcut"></a>验证键盘快捷方式的可用性

1. 在 "**工具**  >  **选项**"  >  **环境** 窗口中，选择 "**键盘**"。

2. 请确保将 **"使用新快捷方式"** 设置为 " **全局**"。

3. 在 " **按快捷键** " 框中，键入要使用的键盘快捷方式。

    如果 Visual Studio 中已经使用了该快捷方式，则 **当前使用的快捷方式** 将显示快捷方式当前调用的命令。

4. 尝试不同的键组合，直到找到一个未映射的键组合。

   > [!NOTE]
   > 使用 **Alt** 的键盘快捷方式可打开菜单而不直接执行命令。 因此，当您键入包含 **Alt** 的快捷方式时，"**当前使用者**" 框中的快捷方式可能为空。可以通过关闭 "**选项**" 对话框，然后按下键来验证快捷方式是否未打开菜单。

   下面的过程假定您有一个具有菜单命令的现有 VSPackage。 如果需要执行此操作的帮助，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

### <a name="to-assign-a-keyboard-shortcut-to-a-command"></a>为命令分配键盘快捷方式

1. 打开包的 *.vsct* 文件。

2. `<KeyBindings>`如果不存在，请在后面创建一个空部分 `<Commands>` 。

   > [!WARNING]
   > 有关密钥绑定的详细信息，请参阅 [键绑定](../extensibility/keybinding-element.md)。

    在 `<KeyBindings>` 部分中，创建一个 `<KeyBinding>` 条目。

    将 `guid`  和  `id` 属性设置为要调用的命令的属性。

    将 `mod1` 属性设置为 " **控件**"、" **Alt**" 或 " **移动**"。

    键绑定部分应如下所示：

   ```xml
   <KeyBindings>
       <KeyBinding guid="<name of command set>" id="<name of command id>"
           editor="guidVSStd97" key1="1" mod1="CONTROL"/>
   </KeyBindings>

   ```

   如果键盘快捷方式需要两个以上的键，请设置 `mod2` 和 `key2` 属性。

   在大多数情况下，不应在没有第二个修饰符的情况下使用 **Shift** ，因为按下它已使大多数字母数字键都可键入一个大写字母或符号。

   利用虚拟键代码，你可以访问没有与其关联的字符的特殊键，例如，函数键和 **Backspace** 键。 有关详细信息，请参阅 [虚拟键代码](/windows/desktop/inputdev/virtual-key-codes)。

   若要使命令在 Visual Studio 编辑器中可用，请将 `editor` 属性设置为 `guidVSStd97` 。

   若要使命令仅在自定义编辑器中可用，请将 `editor` 属性设置为 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 创建包含自定义编辑器的 VSPackage 时由包模板生成的自定义编辑器的名称。 若要查找名称值，请在部分中查找 `<Symbols>` `<GuidSymbol>` 属性以 `name` "." 结尾的节点 `editorfactory` 。这是自定义编辑器的名称。

## <a name="example-1"></a>示例 1
 此示例将键盘快捷方式 **Ctrl** + **Alt** + **C** 绑定到名为的包中名为的命令 `cmdidMyCommand` `MyPackage` 。

```
<CommandTable>
. . .
<Commands>
. . .
</Commands>
<KeyBindings>
  <KeyBinding guid="guidMyPackageCmdSet" id="cmdidMyCommand"
      key1="C" mod1="CONTROL" mod2="ALT" editor="guidVSStd97" />
</KeyBindings>
. . .
</CommandTable>
```

## <a name="example-2"></a>示例 2
 此示例将键盘快捷方式 **Ctrl +** 绑定 + 到名为的项目中名为的命令 `cmdidBold` `TestEditor` 。 命令仅在自定义编辑器中可用，在其他编辑器中不可用。

```xml
<KeyBinding guid="guidVSStd97" id="cmdidBold" editor="guidTestEditorEditorFactory" key1="B" mod1="Control" />
```

## <a name="see-also"></a>另请参阅
- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
