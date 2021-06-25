---
title: 从设置存储获取服务|Microsoft Docs
description: 了解如何使用设置存储查找所有可用服务或确定是否安装了特定服务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 7028d440-d16d-4b08-9b94-eb8cc93b25fc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cb014803945ea88cd6c2c27eee8c120059014a18
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900637"
---
# <a name="get-service-information-from-the-settings-store"></a>从设置存储获取服务信息
可以使用设置存储查找所有可用服务或确定是否安装了特定服务。 必须知道服务类的类型。

## <a name="to-list-the-available-services"></a>列出可用服务

1. 创建名为 的 VSIX `FindServicesExtension` 项目，然后添加名为 的自定义命令 `FindServicesCommand` 。 若要详细了解如何创建自定义命令，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

2. 在 *FindServicesCommand.cs 中*，添加以下 using 指令：

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    using System.Windows.Forms;
    ```

3. 获取配置设置存储，然后找到名为 Services 的子集合。 此集合包括所有可用的服务。 在 `MenuItemCommand` 方法中，删除现有代码并将其替换为以下内容：

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
        string message = "Available services:\n";
        IEnumerable<string> collection = configurationSettingsStore.GetSubCollectionNames("Services");
        int n = 0;
        foreach (string service in collection)
        {
            message += configurationSettingsStore.GetString("Services\\" + service, "Name", "Unknown") + "\n";
        }

        MessageBox.Show(message);
    }
    ```

4. 生成项目并启动调试。 这将显示实验实例。

5. 在实验实例的"工具"**菜单上，** 单击"**调用 FindServicesCommand"。**

     应会看到一个列出所有服务的消息框。

     若要验证这些设置，可以使用注册表编辑器。

## <a name="find-a-specific-service"></a>查找特定服务
 还可使用 <xref:Microsoft.VisualStudio.Settings.SettingsStore.CollectionExists%2A> 方法确定是否安装了特定服务。 必须知道服务类的类型。

1. 在上一过程中创建的项目的 MenuItemCallback 中，搜索配置设置存储区中具有由服务的 GUID 命名的子集合 `Services` 的集合。 在这种情况下，我们将查找帮助服务。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
        string helpServiceGUID = typeof(SVsHelpService).GUID.ToString("B").ToUpper();
        bool hasHelpService = configurationSettingsStore.CollectionExists("Services\\" + helpServiceGUID);
        string message = "Help Service Available: " + hasHelpService;

        MessageBox.Show(message);
    }
    ```

2. 生成项目并启动调试。

3. 在实验实例的"工具"**菜单上，** 单击"**调用 FindServicesCommand"。**

     应会看到一条消息，其文本为 **"帮助服务可用：** 后跟 **True"** 或 **"False"。** 若要验证此设置，可以使用注册表编辑器，如前面步骤所示。
