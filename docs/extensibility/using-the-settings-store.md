---
title: 使用设置存储 |Microsoft Docs
description: 了解如何从配置设置存储中读取数据，这些数据是只读的 Visual Studio 和 VSPackage 设置。
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
ms.openlocfilehash: 5777959fe8ca21d3e560f935285ca8a0a3885a441a0118f6ade8a40b208a5bc7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121375138"
---
# <a name="using-the-settings-store"></a>使用设置存储
有两种类型的设置存储：

- 配置设置，这些设置是只读的 Visual Studio 和 VSPackage 设置。 Visual Studio 将 .pkgdef 文件中的设置合并到此存储中。

- 用户设置，这是可写的设置，例如在 " **选项** " 对话框、属性页和某些其他对话框中的页面上显示的设置。 Visual Studio 扩展可能会将其用于少量数据的本地存储。

  此演练演示如何从配置设置存储中读取数据。 有关如何写入用户设置存储的说明，请参阅[写入用户设置存储](../extensibility/writing-to-the-user-settings-store.md)。

## <a name="creating-the-example-project"></a>创建示例 Project
 本部分演示如何使用用于演示的菜单命令创建简单的扩展项目。

1. 每个 Visual Studio 扩展都从包含扩展资产的 VSIX 部署项目开始。 创建一个 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 名为的 VSIX 项目 `SettingsStoreExtension` 。 可以在 "**新建 Project** " 对话框中的 " **Visual c #/扩展性**" 下找到 VSIX 项目模板。

2. 现在，添加一个名为 **SettingsStoreCommand** 的自定义命令项模板。 在 " **添加新项** " 对话框中，切换到 " **Visual c #/扩展性** "，然后选择 " **自定义命令**"。 在窗口底部的 " **名称** " 字段中，将命令文件名更改为 **SettingsStoreCommand**。 有关如何创建自定义命令的详细信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

## <a name="using-the-configuration-settings-store"></a>使用配置设置存储
 本部分说明如何检测和显示配置设置。

1. 在 SettingsStorageCommand 文件中，添加以下 using 指令：

   ```
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Settings;
   using Microsoft.VisualStudio.Shell.Settings;
   using System.Windows.Forms;
   ```

2. 在中 `MenuItemCallback` ，删除方法的主体，并添加以下行以获取配置设置存储：

   ```
   SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
   SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
   ```

    <xref:Microsoft.VisualStudio.Shell.Settings.ShellSettingsManager>是服务上的托管帮助器类 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager> 。

3. 现在，确定是否安装了 Windows Phone 工具。 代码应如下所示：

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

5. 在实验实例中，单击 " **工具** " 菜单上的 " **调用 SettingsStoreCommand**"。

    应该会看到一个消息框，指出 **Microsoft Windows Phone 开发人员工具：** 后跟 **True** 或 **False**。

   Visual Studio 将设置存储在系统注册表中。

#### <a name="to-use-a-registry-editor-to-verify-configuration-settings"></a>使用注册表编辑器验证配置设置

1. 打开 Regedit.exe。

2. 导航到 HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0Exp_Config\InstalledProducts\\ 。

    > [!NOTE]
    > 请确保正在查看包含 \ 14.0Exp_Config 的密钥，而非 14.0_Config \\ 。 运行 Visual Studio 的实验实例时，配置设置位于注册表配置单元 "14.0Exp_Config" 中。

3. 展开 "\Installed Products \" 节点。 如果前面步骤中的消息是 " **microsoft Windows Phone 开发人员工具已安装： True**，则 \Installed Products \ 应包含 microsoft Windows Phone 开发人员工具节点。 如果消息为 **Microsoft Windows Phone 开发人员工具已安装： False**，则 \Installed Products \ 不应包含 microsoft Windows Phone 开发人员工具节点。
