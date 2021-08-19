---
title: 删除未用引用
description: 了解如何使用新的“Remove Unused References”命令清理不使用的项目引用和 NuGet 包。
ms.custom: SEO-VS-2021
ms.date: 06/01/2021
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
ms.openlocfilehash: 19fe9badea98eafa040557d6d373ad72df588229
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122143594"
---
# <a name="remove-unused-references"></a>删除未用引用

此重构适用于：

- C#
- Visual Basic

**内容：** 允许你删除未用的引用。

**时间：** 想清理不使用的项目引用和 NuGet 包。 

**原因：** 删除没有使用的项目引用可帮助节省空间并缩短应用程序的启动时间，因为这需要花费时间来加载每个模块，并避免编译器加载永远不会使用的元数据。

## <a name="how-to"></a>操作方法

1. 在解决方案资源管理器中，右键单击项目名称或依赖项节点。

2. 选择“删除未用引用”。

    ![“删除未用引用”命令](media/remove-unused-references-command.png)

3. “删除未用引用”对话框将打开，显示源代码中没有使用的引用。 系统将预先选中未使用的引用以进行删除，同时提供通过在“操作”下拉菜单中选择 `Keep` 来保留引用的选项。

    ![“删除未用引用”对话框](media/remove-unused-references-dialog.png)

5. 单击 `Apply` 以删除所选引用。 

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)