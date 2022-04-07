---
title: 对 using 排序
description: 如何对文件顶部的 `using` 指令排序，来让它们按字母顺序排序。
ms.date: 04/05/2022
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-general
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 3d4000809f5645cfcc21d925e33ce081efd6b411
ms.sourcegitcommit: 8623082339d642f30efe98e4a759b8f023a210cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2022
ms.locfileid: "141489108"
---
# <a name="sort-usings"></a>对 using 排序

此重构适用于：

- C#

- Visual Basic

内容：对 using 排序。

适用情况：需要对文件顶部的 `using` 指令排序，让它们按字母顺序排序。 

原因：这样便于查找 using 指令。

## <a name="how-to"></a>操作方法

1. 从菜单栏中选择“编辑”。
2. 选择“Intellisense” > “对 Using 排序” 。

   ![对 using 排序](media/sort-usings.png)

3. 还可以为 `using`**ToolsOptionsText** >  >  **EditorC** > **#** > **Advanced** 中的指令配置不同的设置。

   ![使用配置选项排序](media/sort-usings-configuration-options.png)

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
