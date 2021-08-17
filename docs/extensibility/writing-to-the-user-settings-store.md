---
title: 写入用户设置存储 |Microsoft Docs
description: 了解如何通过使用此演练，通过读取和写入用户设置存储来将记事本添加到 Visual Studio 作为外部工具。
ms.custom: SEO-VS-2020
ms.date: 05/23/2019
ms.topic: how-to
ms.assetid: efd27f00-7fe5-45f8-9b97-371af732be97
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b27796000919336e2585d5b3e7c288a88abe261f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122028340"
---
# <a name="writing-to-the-user-settings-store"></a>写入用户设置存储
用户设置是 " **工具/选项** " 对话框、"属性" 窗口和某些其他对话框中的可写设置。 Visual Studio 扩展可以使用这些扩展来存储少量数据。 本演练演示如何通过读取和写入用户设置存储，将记事本添加 Visual Studio 为外部工具。

## <a name="writing-to-the-user-settings-store"></a>写入用户设置存储

1. 创建名为 UserSettingsStoreExtension 的 VSIX 项目，然后添加名为 UserSettingsStoreCommand 的自定义命令。 有关如何创建自定义命令的详细信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

2. 在 UserSettingsStoreCommand 中，添加以下 using 指令：

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    ```

3. 在 MenuItemCallback 中，删除方法的正文并获取用户设置存储，如下所示：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);
    }
    ```

4. 现在查明记事本是否已设置为外部工具。 需要循环访问所有外部工具，以确定 ToolCmd 设置是否为 "记事本"，如下所示：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);

        // Find out whether Notepad is already an External Tool.
        int toolCount = userSettingsStore.GetInt32("External Tools", "ToolNumKeys");
        bool hasNotepad = false;
        CompareInfo Compare = CultureInfo.InvariantCulture.CompareInfo;
        for (int i = 0; i < toolCount; i++)
        {
            if (Compare.IndexOf(userSettingsStore.GetString("External Tools", "ToolCmd" + i), "Notepad", CompareOptions.IgnoreCase) >= 0)
            {
                hasNotepad = true;
                break;
            }
        }
    }

    ```

5. 如果记事本尚未设置为外部工具，请按如下所示进行设置：

    ```vb
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);

        // Find out whether Notepad is already installed.
        int toolCount = userSettingsStore.GetInt32("External Tools", "ToolNumKeys");
        bool hasNotepad = false;
        CompareInfo Compare = CultureInfo.InvariantCulture.CompareInfo;
        for (int i = 0; i < toolCount; i++)
        {
            if (Compare.IndexOf(userSettingsStore.GetString("External Tools", "ToolCmd" + i), "Notepad", CompareOptions.IgnoreCase) >= 0)
            {
                hasNotepad = true;
                break;
            }
        }

        string message = (hasNotepad) ? "Notepad already installed" : "Installing Notepad";
         if (!hasNotepad)
        {
            userSettingsStore.SetString("External Tools", "ToolTitle" + toolCount, "&Notepad");
            userSettingsStore.SetString("External Tools", "ToolCmd" + toolCount, "C:\\Windows\\notepad.exe");
            userSettingsStore.SetString("External Tools", "ToolArg" + toolCount, "");
            userSettingsStore.SetString("External Tools", "ToolDir" + toolCount, "$(ProjectDir)");
            userSettingsStore.SetString("External Tools", "ToolSourceKey" + toolCount, "");
            userSettingsStore.SetUInt32("External Tools", "ToolOpt" + toolCount, 0x00000011);

            userSettingsStore.SetInt32("External Tools", "ToolNumKeys", toolCount + 1);
        }
    }
    ```

6. 测试代码。 请记住，它将记事本添加为外部工具，因此，在第二次运行之前，必须先回滚注册表。

7. 生成代码并开始调试。

8. 在 " **工具** " 菜单上，单击 " **调用 UserSettingsStoreCommand**"。 这会将记事本添加到 "**工具**" 菜单。

9. 现在，应会在 "工具"/"选项" 菜单上看到记事本，单击 **记事本** 应显示记事本的实例。
