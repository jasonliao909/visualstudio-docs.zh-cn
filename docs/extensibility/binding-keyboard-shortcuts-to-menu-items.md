---
title: 将键盘快捷方式绑定到菜单项|Microsoft Docs
description: 了解如何将键盘快捷方式映射到Visual Studio编辑器或自定义编辑器的自定义按钮、菜单项或工具栏命令。
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
ms.workload:
- vssdk
ms.openlocfilehash: 6a9591a7412b0bcaf506483a16a6660790df5f40
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900429"
---
# <a name="bind-keyboard-shortcuts-to-menu-items"></a>将键盘快捷方式绑定到菜单项
若要将键盘快捷方式绑定到自定义菜单命令，只需将条目添加到包 *的 .vsct* 文件即可。 本主题说明如何将键盘快捷方式映射到自定义按钮、菜单项或工具栏命令，以及如何在默认编辑器中应用键盘映射或将键盘映射限制为自定义编辑器。

 若要将键盘快捷方式分配给现有Visual Studio，请参阅 [标识和自定义键盘快捷方式](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)。

## <a name="choose-a-key-combination"></a>选择组合键
 许多键盘快捷方式已用于Visual Studio。 不应将相同的快捷方式分配给多个命令，因为难以检测重复绑定，并且还可能导致不可预知的结果。 因此，建议在分配快捷方式之前验证快捷方式的可用性。

### <a name="to-verify-the-availability-of-a-keyboard-shortcut"></a>验证键盘快捷方式的可用性

1. 在"**工具**  >  **选项**  >  **环境"窗口中**，选择"键盘 **"。**

2. 确保"**在 中使用新快捷方式**"设置为"全局 **"。**

3. 在 **"按快捷键"** 框中，键入想要使用的键盘快捷方式。

    如果快捷方式已在 Visual Studio，则"当前使用的快捷方式"框将显示快捷方式当前调用的命令。

4. 尝试不同的键组合，直到找到未映射的键。

   > [!NOTE]
   > 使用 Alt 的 **键盘** 快捷方式可能会打开菜单，而不是直接执行命令。 因此，**键入包含** Alt 的快捷方式时，框当前使用的快捷方式可能 **为空**。可以通过关闭"选项"对话框，然后按键来验证快捷方式是否未打开菜单。

   以下过程假定你有一个包含菜单命令的现有 VSPackage。 如果需要帮助，请看一下使用菜单命令 [创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

### <a name="to-assign-a-keyboard-shortcut-to-a-command"></a>为命令分配键盘快捷方式

1. 打开 *包的 .vsct* 文件。

2. 在 之后 `<KeyBindings>` 创建一个 `<Commands>` 空部分（如果不存在）。

   > [!WARNING]
   > 有关键绑定详细信息，请参阅 [Keybinding](../extensibility/keybinding-element.md)。

    在 `<KeyBindings>` 部分中，创建 `<KeyBinding>` 一个条目。

    将 `guid`  和  `id` 属性设置为要调用的命令的属性。

    将 属性 `mod1` 设置为 **Control、Alt** 或 **Shift**。 

    KeyBindings 部分应如下所示：

   ```xml
   <KeyBindings>
       <KeyBinding guid="<name of command set>" id="<name of command id>"
           editor="guidVSStd97" key1="1" mod1="CONTROL"/>
   </KeyBindings>

   ```

   如果键盘快捷方式需要两个以上键，请设置 `mod2` 和 `key2` 属性。

   在大多数情况下，不应在没有第二个修饰符的情况下使用 **Shift，** 因为按它已会导致大多数字母数字键键入大写字母或符号。

   虚拟密钥代码允许访问没有与之关联的字符的特殊键，例如函数键和 **Backspace** 键。 有关详细信息，请参阅 [虚拟密钥代码](/windows/desktop/inputdev/virtual-key-codes)。

   若要使命令在编辑器中Visual Studio，将 `editor` 属性设置为 `guidVSStd97` 。

   若要使命令仅在自定义编辑器中可用，将 属性设置为创建包含自定义编辑器的 VSPackage 时包模板生成的自定义 `editor` [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 编辑器的名称。 若要查找名称值，请查找属性以"."结尾 `<Symbols>` `<GuidSymbol>` `name` 的节点 `editorfactory` 的 部分。这是自定义编辑器的名称。

## <a name="example-1"></a>示例 1
 此示例将键盘快捷方式 **Ctrl** Alt C 绑定到名为 的包 +  +  `cmdidMyCommand` 中名为 的命令 `MyPackage` 。

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
 此示例将键盘快捷方式 **Ctrl** B 绑定到名为 的项目中 +  `cmdidBold` 名为 的命令 `TestEditor` 。 命令仅在自定义编辑器中可用，在其他编辑器中不可用。

```xml
<KeyBinding guid="guidVSStd97" id="cmdidBold" editor="guidTestEditorEditorFactory" key1="B" mod1="Control" />
```

## <a name="see-also"></a>另请参阅
- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
