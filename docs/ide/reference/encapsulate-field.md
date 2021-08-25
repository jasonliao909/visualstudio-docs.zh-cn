---
title: 将字段重构为属性
description: 了解如何使用“快速操作和重构”菜单将字段转换为属性。
ms.custom: SEO-VS-2020
ms.date: 01/26/2018
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
f1_keywords:
- vs.csharp.refactoring.encapsulatefield
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 3c60840fcbf0953c308bec174c49058e7f94163e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122062337"
---
# <a name="encapsulate-a-field-refactoring"></a>“封装字段”重构

此重构适用于：

- C#

- Visual Basic

功能：将字段转换为属性，并将该字段的所有用法更新为使用新创建的属性。

时机：想要将字段移到属性中，并更新对此字段的所有引用时。

原因：想要为其他类提供字段的访问权限，但不想要这些字段拥有直接访问权限。  例如，通过将字段包装在属性中，可编写代码来验证正在分配的值。

## <a name="how-to"></a>操作说明

1. 突出显示要封装的字段的名称，或将文本光标置于其中：

   - C#：

       ![突出显示的代码 - C#](media/encapsulate-highlight-cs.png)

   - Visual Basic：

       ![突出显示的代码 - Visual Basic](media/encapsulate-highlight-vb.png)

2. 接下来，执行以下操作之一：

   - **键盘**
      - 按“Ctrl+R”，然后按“Ctrl+E”。  （请注意，键盘快捷方式可能因所选的配置文件而有所不同。）
      - 按“Ctrl”+ **。** 触发“快速操作和重构”菜单，然后从“预览”弹出窗口选择任意一个“封装字段”项。
   - **鼠标**
      - 选择“编辑 > 重构> 封装字段”。
      - 右键单击代码，选择“快速操作和重构”菜单，然后从“预览”弹出窗口选择任意一个“封装字段”项。

   选择 | 说明
   --------- | -----------
   封装字段 (并使用属性) | 使用属性封装字段，并将此字段的所有用法更新为使用所生成的属性
   封装字段 (但仍使用字段) | 使用属性封装字段，但将此字段的所有用法保留不变

   选择后，即会创建属性并更新对字段的引用。

   > [!TIP]
   > 提交前，使用弹出窗口中的“预览更改”链接[查看最后的结果](../../ide/preview-changes.md)。

   - C#：

      ![“封装属性”的结果 - C#](media/encapsulate-result-cs.png)

   - Visual Basic：

      ![“封装属性”的结果 - Visual Basic](media/encapsulate-result-vb.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)
