---
title: 删除未用引用
description: 了解如何使用新的“Remove Unused References”命令清理不使用的项目引用和 NuGet 包。
ms.custom: SEO-VS-2021
ms.date: 09/14/2021
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
ms.openlocfilehash: df388659e0776fc15155d338c97334b2c5283468
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128428693"
---
# <a name="remove-unused-references"></a>删除未用引用

此重构适用于：

- C#
- Visual Basic

**内容：** 为 [SDK 样式项目](/dotnet/core/project-sdk/overview)删除未使用的引用。

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