---
title: 拉取成员
description: 了解如何使用“快速操作和重构”菜单将成员拉取到基类型。
ms.custom: SEO-VS-2020
ms.date: 02/13/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 9abfe9498d1b6bda0c9423566172395d0aca5096
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640672"
---
# <a name="pull-members-up"></a>拉取成员

此重构适用于：

- C#

- Visual Basic

**功能：** 可以将成员拉取到基类型。

**使用时机：** 已实现接口，并且要将成员移到基类型。

操作原因：拉取成员使接口的其他实现也可以继承这些成员。

## <a name="how-to"></a>操作说明

1. 请将光标放在已实现接口的任何成员中。
2. 按“Ctrl”+ **。** 触发“快速操作和重构”  菜单。

   ![拉取成员](media/pull-members-up.png)

2. 选择“将成员拉取到基类型”。

3. 在对话框中，选择要添加到所选接口的成员。

   ![拉取成员](media/pull-members-up-dialog.png)

4. 选择 **“确定”** 。 所选成员将拉取到接口。

   ![拉取成员完成](media/pull-members-up-completed.png)

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
