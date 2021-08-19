---
title: 创建可重用的按钮组|Microsoft Docs
description: 了解如何创建命令组，这是一系列命令，这些命令一起显示在菜单或工具栏上。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- button groups, creating in VSPackages
- VSPackages, creating reusable button groups
- buttons, creating reusable groups
ms.assetid: 0c561617-fb86-476d-8bd1-c6e5e7464c65
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 5ef9e4c78fcd4bfe22ba6bcffcb2fe41d1a7dda2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122057988"
---
# <a name="create-reusable-groups-of-buttons"></a>创建可重用的按钮组
命令组是始终显示在菜单或工具栏上的命令的集合。 可以通过将任何命令组分配到 *.vsct* 文件的 CommandPlacements 节中的不同父菜单来重新使用它。

 命令组通常包含按钮，但它们也可以包含其他菜单或组合框。

## <a name="to-create-a-reusable-group-of-buttons"></a>创建可重用的按钮组

1. 创建名为 的 VSIX 项目 `ReusableButtons` 。 有关详细信息，请参阅 [使用菜单命令 创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 项目打开时，添加名为 **ReusableCommand 的自定义命令项模板**。 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 在"**添加新项"对话框中**，转到 **"Visual C#**  >  **扩展性"，** 然后选择"**自定义命令"。** 在 **窗口底部的** "名称"字段中，将命令文件名更改为 *ReusableCommand.cs*。

3. 在 *.vsct 文件中* ，转到"符号"部分，找到包含项目的组和命令的 GuidSymbol 元素。 它应命名为 guidReusableCommandPackageCmdSet。

4. 为要添加到组的每个按钮添加 IDSymbol，如以下示例所示。

    ```xml
    <GuidSymbol name="guidReusableCommandPackageCmdSet" value="{7f383b2a-c6b9-4c1d-b4b8-a26dc5b60ca1}">
        <IDSymbol name="MyMenuGroup" value="0x1020" />
        <IDSymbol name="ReusableCommandId" value="0x0100" />
        <IDSymbol name="SecondReusableCommandId" value="0x0200" />
    </GuidSymbol>
    ```

     默认情况下，命令项模板会创建一个名为 **MyMenuGroup** 的组和一个按钮，该按钮具有你提供的名称，以及每个组的 IDSymbol 条目。

5. 在"组"部分中，创建一个 Group 元素，该元素的 GUID 和 ID 属性与"符号"部分中给定的属性相同。 也可使用现有组，或使用命令模板提供的条目，如以下示例所示。 此组显示在"工具 **"菜单** 上

    ```xml
    <Groups>
        <Group guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
              <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS"/>
        </Group>
    </Groups>
    ```

## <a name="to-create-a-group-of-buttons-for-reuse"></a>创建一组按钮以便重复使用

1. 可以通过在命令或菜单的定义中将组用作父级，或者通过使用 CommandPlacements 节将命令或菜单放入组中，将命令或菜单放入组中。

     在"按钮"部分中，定义一个按钮，该按钮将组作为其父级，或使用包模板提供的按钮，如以下示例所示。

    ```xml
    <Button guid="guidReusableCommandPackageCmdSet" id="ReusableCommandId" priority="0x0100" type="Button">
        <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ReusableCommand</ButtonText>
        </Strings>
    </Button>
    ```

2. 如果按钮必须出现在多个组中，请在此"CommandPlacements"部分中创建一个条目，该条目必须放置在"命令"部分之后。 将 CommandPlacement 元素的 GUID 和 ID 属性设置为与要定位的按钮的 GUID 和 ID 属性匹配，然后将其 Parent 元素的 GUID 和 ID 设置为目标组的 GUID 和 ID，如以下示例所示。

    ```xml
    <CommandPlacements>
        <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="SecondReusableCommandId" priority="0x105">
          <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        </CommandPlacement>
    </CommandPlacements>
    ```

    > [!NOTE]
    > "优先级"字段的值确定命令在新建命令组中的位置。 CommandPlacement 元素中设置的优先级将替代项定义中设置的优先级。 优先级值较低的命令显示在优先级值较高的命令之前。 允许重复的优先级值，但无法保证具有相同优先级值的命令的相对位置，因为 **devenv /setup** 命令从注册表创建最终接口的顺序可能不一致。

## <a name="to-put-a-reusable-group-of-buttons-on-a-menu"></a>将可重用的一组按钮放在菜单上

1. 在 节中创建 `CommandPlacements` 一个条目。 将元素的 GUID 和 ID 设置为组的 GUID 和 ID，将父 GUID 和 ID 设置为 `CommandPlacement` 目标位置的 GUID 和 ID。

    CommandPlacements 部分应放在"命令"部分之后：

   ```xml
   <CommandTable>
   ...
     <Commands>... </Commands>
     <CommandPlacements>... </CommandPlacements>
   ...
   </CommandTable>
   ```

    命令组可以包括在多个菜单上。 父菜单可以是你创建的菜单，可以是由 (提供的菜单（如 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] *ShellCmdDef.vsct* 或 *SharedCmdDef.vsct*) 中所述），或者是在另一个 VSPackage 中定义的菜单。 只要父菜单最终连接到 VSPackage 显示的快捷菜单或快捷菜单，父菜单的数量就不受限制 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

    以下示例将组放在其他解决方案资源管理器工具栏的右侧。

   ```xml
   <CommandPlacements>
       <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0xF00">
         <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>
       </CommandPlacement>
   </CommandPlacements>
   ```

   ```xml
   <CommandPlacements>
     <CommandPlacement guid="guidButtonGroupCmdSet" id="MyMenuGroup"
         priority="0x605">
       <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS" />
     </CommandPlacement>
   </CommandPlacements>

   ```
