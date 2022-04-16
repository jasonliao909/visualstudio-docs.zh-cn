---
title: 在混合模式下调试 | Microsoft Docs
description: 请参阅如何在调用应用的项目的属性页中启用混合模式调试（托管代码和本机代码）。
ms.date: 04/15/2022
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging DLLs
- debugging [Visual Studio], mixed-mode
- mixed-mode debugging
ms.assetid: 2859067d-7fcc-46b0-a4df-8c2101500977
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 0a50c63114f2c02eeda23486451888cce85c1669
ms.sourcegitcommit: 2828730cd0e3a4b9f5935858ec2453837fed3211
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2022
ms.locfileid: "142649596"
---
# <a name="how-to-debug-in-mixed-mode-c-c-visual-basic"></a>如何：在混合模式下调试（C#、C++、Visual Basic）

以下过程描述如何为托管代码与本机代码的组合启用调试，这一过程也称为混合模式调试。 下面列出了两种混合模式调试场景：

- 调用 DLL 的应用是用本机代码编写的，而 DLL 是托管代码。

- 调用 DLL 的应用是用托管代码编写的，而 DLL 是用本机代码编写的。 有关详细介绍此场景的教程，请参阅[调试托管代码和本机代码](../debugger/how-to-debug-managed-and-native-code.md)。

可以在调用应用项目的“属性”页面中同时启用托管调试器和本机调试器。 本机应用和托管应用的设置不同。

如果无权访问调用应用的项目，则可以从 DLL 项目调试 DLL。 如果只调试 DLL 项目，则不需要采用混合模式。 有关详细信息，请参阅[如何：从 DLL 项目调试](../debugger/how-to-debug-from-a-dll-project.md)。

> [!NOTE]
> 你看到的对话框和命令可能与本文中的不同，具体取决于你的 Visual Studio 设置或版本。 若要更改设置，请选择“工具” > “导入和导出设置” 。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

## <a name="enable-mixed-mode-debugging-for-a-native-calling-app"></a>为本机调用应用启用混合模式调试

1. 在“解决方案资源管理器”中选择 C++ 项目，然后单击“属性”图标，按 Alt+Enter，或右键单击并选择“属性”  。

1. 在“\<Project> 属性页”对话框中，展开“配置属性”，然后选择“调试”  。

1. 将“调试器类型”设置为“混合”或“自动”  。

1. 选择“确定”。

   ![在 C++ 中启用混合模式调试](../debugger/media/dbg-mixed-mode-from-native.png "启用混合模式调试")

## <a name="enable-mixed-mode-debugging-for-a-managed-calling-app"></a>为托管调用应用启用混合模式调试

1. 在“解决方案资源管理器”中选择 C# 或 Visual Basic 项目，然后选择“属性”图标，按 Alt+Enter，或右键单击并选择“属性”  。

1. 在 **解决方案资源管理器** 中，选择 C# 或Visual Basic项目节点并选择 **“属性**”图标，或右键单击项目节点并选择“**属性**”。

1. 在属性中启用本机代码调试。

    ::: moniker range=">=vs-2022"
    对于 C#，在左窗格中选择 **“调试”** ，选择“ **打开调试启动配置文件 UI**”，然后选择“ **启用本机代码调试** ”复选框，然后关闭属性页以保存更改。
    ![在 C 中启用混合模式调试#](../debugger/media/vs-2022/mixed-mode-enable-native-code-debugging.png)

    对于Visual Basic，请在左窗格中选择“**调试**”，选中“**启用本机代码调试**”复选框，然后关闭属性页以保存更改。

    ![在 Visual Basic 中启用混合模式调试](../debugger/media/mixed-mode-enable-native-code-debugging.png)
    ::: moniker-end
    ::: moniker range="<=vs-2019"
    选择左窗格中的“调试”，再选中“启用本机代码调试”复选框，然后关闭属性页以保存更改 。

    ![启用混合模式调试](../debugger/media/mixed-mode-enable-native-code-debugging.png)

    > [!NOTE]
    > 对于 Visual Studio 2017 和 Visual Studio 2019 中的 .NET Core 应用，必须使用 *launchSettings.json* 文件而不是项目属性来启用混合模式调试。
    ::: moniker-end

## <a name="see-also"></a>请参阅

- [如何：从 DLL 项目调试](../debugger/how-to-debug-from-a-dll-project.md)