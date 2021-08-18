---
title: 使用 设置 Store |Microsoft Docs
description: 了解如何从配置设置存储读取数据，该存储是只读Visual Studio VSPackage 设置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Settings Store, using
ms.assetid: 447ec08a-eca5-40b8-89b0-f98fdf3d39a4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ed4ee9291539575d1ddb7da31849955ff6d182c6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122132231"
---
# <a name="using-the-settings-store"></a>使用设置存储
有两种类型的设置存储：

- 配置设置，这些设置是只读的Visual Studio VSPackage 设置。 Visual Studio将所有已知 .pkgdef 文件的设置合并到此存储中。

- 用户设置，这些设置是可写设置，例如"选项"对话框、属性页和某些其他对话框中的页面上显示的设置。 Visual Studio扩展可能会将这些数据用于本地存储少量数据。

  本演练演示如何从配置设置存储读取数据。 请参阅[写入用户设置存储](../extensibility/writing-to-the-user-settings-store.md)，了解如何写入用户设置存储。

## <a name="creating-the-example-project"></a>创建示例Project
 本部分演示如何使用菜单命令创建简单的扩展项目进行演示。

1. 每个Visual Studio扩展都从包含扩展资产的 VSIX 部署项目开始。 创建名为 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的 VSIX 项目 `SettingsStoreExtension` 。 可以在 Visual C# /扩展性 下的"新建 **Project"对话框中** 找到 **VSIX 项目模板**。

2. 现在，添加名为 **SettingsStoreCommand 的自定义命令项模板**。 在"**添加新项"对话框中**，转到 **"Visual C#/扩展性"，然后选择**"**自定义命令"。** 在 **窗口底部的** "名称"字段中，将命令文件名更改为 **SettingsStoreCommand.cs**。 若要详细了解如何创建自定义命令，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

## <a name="using-the-configuration-settings-store"></a>使用 Configuration 设置 Store
 本部分演示如何检测和显示配置设置。

1. 在 SettingsStorageCommand.cs 文件中，添加以下 using 指令：

   ```
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Settings;
   using Microsoft.VisualStudio.Shell.Settings;
   using System.Windows.Forms;
   ```

2. 在 `MenuItemCallback` 中，删除 方法的主体，并添加以下行获取配置设置存储区：

   ```
   SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
   SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
   ```

    <xref:Microsoft.VisualStudio.Shell.Settings.ShellSettingsManager>是服务的托管帮助程序 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager> 类。

3. 现在，确定是否Windows Phone工具。 代码应如下所示：

   ```
   private void MenuItemCallback(object sender, EventArgs e)
   {
       SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
       SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
       bool arePhoneToolsInstalled = configurationSettingsStore.CollectionExists(@"InstalledProducts\Microsoft Windows Phone Developer Tools");
       string message = "Microsoft Windows Phone Developer Tools: " + arePhoneToolsInstalled;
       MessageBox.Show(message);
   }
   ```

4. 测试代码。 生成项目并启动调试。

5. 在实验实例的"工具"**菜单上**，单击"**调用设置""存储""命令"。**

    应会看到一个消息框，显示 **Microsoft Windows Phone 开发人员工具：** 后跟 **True** 或 **False**。

   Visual Studio设置存储在系统注册表中。

#### <a name="to-use-a-registry-editor-to-verify-configuration-settings"></a>使用注册表编辑器验证配置设置

1. 打开Regedit.exe。

2. 导航到 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0Exp_Config\InstalledProducts\\ 。

    > [!NOTE]
    > 请确保正在查看包含 \14.0Exp_Config\ 而不是 \14.0_Config \\ 的键。 运行实例的实验实例时Visual Studio配置设置在注册表配置单元"14.0Exp_Config"。

3. 展开"\Installed Products\"节点。 如果上述步骤中的消息是 **Microsoft Windows Phone 开发人员工具已安装： True，** 则 \Installed Products\ 应包含 Microsoft Windows Phone 开发人员工具节点。 如果消息为 **Microsoft Windows Phone 开发人员工具已安装：False，** 则 \Installed Products\ 不应包含 Microsoft Windows Phone 开发人员工具节点。
