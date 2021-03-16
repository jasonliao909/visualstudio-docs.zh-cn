---
title: 提取基类
description: 此重构将选定类中的成员提取到新基类。
ms.date: 11/03/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 9d7a21bbd3e51ee6a6776ca728a545cbbb731cab
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2021
ms.locfileid: "102466272"
---
# <a name="extract-base-class"></a>提取基类

此重构适用于：

- C#

- Visual Basic

**功能：** 提取基类。

**使用时机：** 要将所选类中的成员提取到新基类。

操作原因：手动拉取成员可能会十分耗时，并使你退出工作流。 

## <a name="how-to"></a>操作说明

1. 将脱字号置于类名或突出显示的成员上。

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

3. 选择“将成员拉取到新的基类”。

    ![“提取基类”对话框](media/extract-base-class.png)

此时将打开新的“提取基类”对话框，你可以在其中指定基类的名称以及应放置到的位置。 可以选择想要传输到新基类的成员，然后选中“设为抽象”列中的复选框，来选择将成员设为抽象成员。

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
