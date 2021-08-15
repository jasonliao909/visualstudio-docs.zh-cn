---
title: 写入用户设置 Store |Microsoft Docs
description: 了解如何使用此记事本Visual Studio向用户设置存储读取和写入数据，以作为外部工具添加数据。
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
ms.openlocfilehash: cb169700ea55eb8bd4d1a762fa5e8d082c04981df1573255d18ca8d41bb3955a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121334921"
---
# <a name="writing-to-the-user-settings-store"></a>写入用户设置存储
用户设置是可写设置，如"工具 **/** 选项"对话框、属性窗口和某些其他对话框中的设置。 Visual Studio扩展可以使用它们来存储少量数据。 本演练演示如何通过从用户设置存储记事本写入Visual Studio添加数据以用作外部工具。

## <a name="writing-to-the-user-settings-store"></a>写入用户设置存储

1. 创建名为 UserSettingsStoreExtension 的 VSIX 项目，然后添加名为 UserSettingsStoreCommand 的自定义命令。 若要详细了解如何创建自定义命令，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

2. 在 UserSettingsStoreCommand.cs 中，添加以下 using 指令：

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    ```

3. 在 MenuItemCallback 中，删除 方法的主体并获取用户设置存储，如下所示：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);
    }
    ```

4. 现在，确定记事本是否已设置为外部工具。 需要浏览所有外部工具，以确定 ToolCmd 设置是否记事本"，如下所示：

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

5. 如果记事本未设置为外部工具，请设置它，如下所示：

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

6. 测试代码。 请记住，它将记事本工具添加为外部工具，因此必须在再次运行注册表之前回滚注册表。

7. 生成代码并开始调试。

8. 在"**工具"菜单** 上，单击 **"调用 UserSettingsStoreCommand"。** 这会将记事本添加到"**工具"** 菜单。

9. 现在，你应该记事本"工具/选项"菜单上看到 **记事本，此时** 应显示一个记事本。
