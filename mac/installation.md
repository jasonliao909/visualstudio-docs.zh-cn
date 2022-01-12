---
title: 安装 Visual Studio 2019 for Mac
description: 介绍如何安装 Visual Studio 2019 for Mac 以及跨平台开发所需的附加组件。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 03/04/2021
ms.technology: vs-ide-install
ms.assetid: 22B1F2CD-32AE-464D-80AC-C8AB4786B015
ms.custom: video
ms.topic: how-to
ms.openlocfilehash: da4efd9bcf57118451e20d3354750ddf1fc15bfd
ms.sourcegitcommit: fc874be3fe4637a23997b4ef2d99a2ee9a499581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2021
ms.locfileid: "135517666"
---
# <a name="install-visual-studio-2019-for-mac"></a>安装 Visual Studio 2019 for Mac

要开始在 macOS 上开发本机跨平台 .NET 应用，请按照下列步骤安装 Visual Studio 2019 for Mac。

 > [!div class="button"]
 > [下载 Visual Studio for Mac](https://visualstudio.microsoft.com/vs/mac/)

## <a name="requirements"></a>要求

- 配备 macOS High Sierra 10.13 或更高版本的 Mac。

要为 iOS 或 macOS 构建 Xamarin 应用，还需要：

- 与最新版本的 Xcode 兼容的 Mac。 请参阅 Apple 的[最低要求文档](https://developer.apple.com/support/xcode/)
- 最新版本的 [Xcode](https://developer.apple.com/xcode)。 如果 Mac 与最新版本不兼容，则可以[使用旧版 Xcode](/xamarin/ios/troubleshooting/questions/old-version-xcode)。
- 一个 Apple ID。 如果没有 Apple ID，请在 https://appleid.apple.com 新建一个。 需要 Apple ID 才可安装和登录 Xcode。

## <a name="installation-instructions"></a>安装说明

1. 从 [Visual Studio for Mac 下载页面](https://visualstudio.microsoft.com/vs/mac/)下载安装程序。
2. 下载完成后，单击 VisualStudioforMacInstaller.dmg 以装载安装程序，然后双击箭头徽标运行它：

    [![单击大箭头开始安装](media/install-installer-sml.png)](media/install-installer.png#lightbox)

3. 可能会收到有关从 Internet 下载应用程序的警告。 单击“打开”。
4. 安装程序检查系统时，请耐心等待：

    [![安装程序会检查系统中是否有已安装的组件](media/install-checking-sml.png)](media/install-checking.png#lightbox)

5. 将出现一条警告，要求确认隐私和许可条款。 请点击链接仔细阅读，如果同意，则按“继续”：

    [![请点击隐私和条款的链接，如果同意，请继续](media/install-privacy.png)](media/install-privacy.png#lightbox)

6. 此时显示可用的工作负载列表。 选择你要使用的组件：

    [![Visual Studio Mac 安装程序中的“你想要安装什么?”屏幕截图，其中显示了可供安装的组件的列表。](media/install-selection.png)](media/install-selection.png#lightbox)

   如果不希望安装所有平台，请参阅以下指南，它们有助于确定要安装的平台：

   |应用类型  |目标  |选择  |说明  |
   |---------|---------|---------|---------|
   |**使用 Xamarin 的应用**| Xamarin.Forms|选择“Android”和“iOS”平台  |你需要安装 [Xcode](https://developer.apple.com/xcode/) |
   ||仅限 iOS|选择“iOS”平台|你需要安装 [Xcode](https://developer.apple.com/xcode/)|
   ||仅限 Android|选择“Android”平台|请注意，还应选择相关的依赖项|
   ||仅限 Mac|选择“macOS (Cocoa)”平台|你需要安装 [Xcode](https://developer.apple.com/xcode/)|
   |**.NET Core 应用程序**|         |选择“.NET Core”平台。|         |
   |**ASP.NET Core Web 应用程序**|         |选择“.NET Core”平台。|         |
   |**Azure Functions**|         |选择“.NET Core”平台。|         |
   |**跨平台 Unity 游戏开发**|         |除了 Visual Studio for Mac 之外，无需安装任何其他平台。| 若要详细了解如何安装 Unity 扩展，请参阅 [Unity 安装指南](./setup-vsmac-tools-unity.md)。|

7. 完成选择后，按下“安装”按钮。
8. 安装程序将在下载并安装 Visual Studio for Mac 和所选工作负载时显示进度。 系统将提示输入密码以授予安装所需的权限。

    [![Visual Studio Mac 安装程序中的屏幕截图，其中显示了适用于 Mac 的 .NET 开发人员工具包的安装进度屏幕。](media/installation-progress.png)](media/installation-progress.png#lightbox)

9. 安装完成后，Visual Studio for Mac 会提示你通过登录并选择要使用的键绑定来个性化安装：

    [![登录到 IDE](media/ide-tour-2019-start-signin.png)](media/ide-tour-2019-start-signin.png#lightbox)

    [![选择要使用的键盘快捷方式](media/ide-tour-2019-keyboard-shortcut.png)](media/ide-tour-2019-keyboard-shortcut.png#lightbox)

如果在企业环境中安装时遇到网络问题，请查看[在有防火墙或代理的情况下进行安装](#install-visual-studio-for-mac-behind-a-firewall-or-proxy-server)的说明。

了解有关[发行说明](/visualstudio/releasenotes/vs2019-mac-relnotes)中的更改详细信息。

> [!NOTE]
> 如果在原始安装期间选择不安装平台或工具（方法为在第 #6 步中取消选择相关项），必须要在稍后添加组件时再次运行安装程序。

## <a name="install-visual-studio-for-mac-behind-a-firewall-or-proxy-server"></a>在防火墙或代理服务器后安装 Visual Studio for Mac

若要在防火墙后面安装 Visual Studio for Mac，必须将某些终结点设置为可供访问，以允许下载所需的工具和更新软件。

配置网络以允许访问下列位置：

- [Visual Studio 终结点](./install-behind-a-firewall-or-proxy-server.md)

## <a name="next-steps"></a>后续步骤

安装 Visual Studio for Mac 后，可以开始编写应用代码。 下面的指南逐步介绍了如何完成后续步骤，即编写和部署项目。

### <a name="ios"></a>iOS

1. [Hello，iOS](/xamarin/ios/get-started/hello-ios/)
2. [设备预配](/xamarin/ios/get-started/installation/device-provisioning/)（以在设备上运行应用程序）。

### <a name="android"></a>Android

1. [了解 Android](/xamarin/android/get-started/hello-android/)
2. [使用 Xamarin Android SDK 管理器](/xamarin/android/get-started/installation/android-sdk?tabs=macos)
3. [Android SDK 仿真器](/xamarin/android/get-started/installation/android-emulator/)
4. [设置设备进行开发](/xamarin/android/get-started/installation/set-up-device-for-development)

### <a name="xamarinforms"></a>Xamarin.Forms

使用 Xamarin.Forms 生成跨平台应用程序：

1. [Xamarin.Forms 快速入门](/xamarin/get-started/quickstarts/)

### <a name="net-core-apps-aspnet-core-web-apps-unity-game-development"></a>.NET Core 应用、ASP.NET Core Web 应用、Unity 游戏开发

有关其他工作负载，请参阅[工作负载](workloads.md)页。

## <a name="related-video"></a>相关视频

> [!Video https://docs.microsoft.com/shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Acquisition/player]

## <a name="see-also"></a>请参阅

- [安装 Visual Studio (Windows)](/visualstudio/install/install-visual-studio)
