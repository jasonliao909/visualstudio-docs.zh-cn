---
title: 卸载 Visual Studio for Mac
description: 了解如何卸载或删除Visual Studio for Mac和相关工具。
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 04/27/2022
ms.custom: devdivchpfy22
ms.technology: vs-ide-install
ms.assetid: 4EB95F75-BC2E-4982-9564-2975805712D8
ms.topic: how-to
ms.openlocfilehash: 14fbaa0d71c882440d27af1edb0876444e707366
ms.sourcegitcommit: 2d45e5df52cec5dc1c3051e7d7cc4978daeb232c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2022
ms.locfileid: "144841051"
---
# <a name="uninstall-visual-studio-for-mac"></a>卸载 Visual Studio for Mac 

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

可以通过导航到相关部分，使用本指南单独卸载Visual Studio for Mac中的每个组件。 建议使用 [“卸载脚本](#uninstall-scripts) ”部分中提供的脚本来卸载所有内容。

本文适用于Visual Studio for Mac。 如果要查找有关VS Code的信息，请参阅[Visual Studio Code设置](https://code.visualstudio.com/docs/setup/setup-overview)。

> [!NOTE]
> 我们想详细了解你为何要卸载 Visual Studio for Mac，便于我们进行改进。 请花几分钟的时间[分享你的反馈](https://aka.ms/vs/mac/uninstallsurvey)。 谢谢！

## <a name="uninstall-scripts"></a>卸载脚本

有两个脚本可用于从计算机中卸载Visual Studio for Mac和所有组件：

- [Visual Studio 和 Xamarin 脚本](#visual-studio-for-mac-and-xamarin-script)
- [.NET Core 脚本](#net-core-script)

以下部分提供有关下载和使用脚本的信息。

### <a name="visual-studio-for-mac-and-xamarin-script"></a>Visual Studio for Mac 和 Xamarin 脚本

可通过使用[卸载脚本](https://raw.githubusercontent.com/MicrosoftDocs/visualstudio-docs/master/mac/resources/uninstall-vsmac.sh)一次性卸载 Visual Studio 和 Xamarin 组件。

卸载脚本包含本文中找到的大部分命令。 脚本中有三个主要遗漏，由于可能的外部依赖项，不包括这些遗漏。 若要删除，请跳转到下面的相关部分并手动删除它们：

- **[卸载 Mono](#uninstall-mono-sdk-mdk)**
- **[卸载 Android AVD](#uninstall-android-avd)**
- **[卸载 Android SDK 和 Java SDK](#uninstall-android-sdk-and-java-sdk)**

要运行脚本，请执行以下步骤：

1. 右键单击脚本并选择“另存为”以在 Mac 上保存文件。
2. 打开“终端”，并将工作目录更改为下载脚本的位置：

    ```bash
    cd /location/of/file
    ```

3. 使脚本可执行文件，并使用 **sudo** 运行它：

    ```bash
    chmod +x ./uninstall-vsmac.sh
    sudo ./uninstall-vsmac.sh
    ```

4. 最后，删除卸载脚本，并删除停靠位置中的 Visual Studio for Mac（如果有）。

### <a name="net-core-script"></a>.NET Core 脚本

.NET Core 的卸载脚本位于 [dotnet cli 存储库](https://raw.githubusercontent.com/dotnet/cli/master/scripts/obtain/uninstall/dotnet-uninstall-pkgs.sh)

要运行脚本，请执行以下步骤：

1. 右键单击脚本并选择“另存为”以在 Mac 上保存文件。
2. 打开“终端”，并将工作目录更改为下载脚本的位置：

    ```bash
    cd /location/of/file
    ```

3. 使脚本可执行，并通过 sudo 运行：

    ```bash
    chmod +x ./dotnet-uninstall-pkgs.sh
    sudo ./dotnet-uninstall-pkgs.sh
    ```

4. 最后，删除 .NET Core 卸载脚本。

## <a name="manually-removing-visual-studio-for-mac"></a>手动删除Visual Studio for Mac

如果想要手动删除Visual Studio for Mac及其依赖项 (，而不是使用上一部分) 中的脚本，本部分总结了应遵循的步骤。 

从 Mac 卸载Visual Studio的第一步是在 **“应用程序**”目录中找到 **Visual Studio** 应用并将其拖到 **“回收站**”。 或者，单击控件并选择“ **移动到回收站** ”，如下图所示：

::: moniker range="vsmac-2019"

![显示Visual Studio应用程序中“移动到回收站”选项的屏幕截图。](media/uninstall-image1.png)

::: moniker-end

::: moniker range="vsmac-2022"

:::image type="content" source="media/vsmac-2022/move-vsmac-application-to-trash.png" alt-text="显示如何卸载Visual Studio for Mac应用程序的屏幕截图。":::

::: moniker-end

删除此应用捆绑包会删除Visual Studio for Mac，但文件系统上可能仍有其他文件（如 Xamarin SDK、.NET SDK 或 iOS 开发工具）。

要删除 Visual Studio for Mac 的所有痕迹，请在终端运行以下命令：

::: moniker range="vsmac-2019"

```bash
sudo rm -rf "/Applications/Visual Studio.app"
rm -rf ~/Library/Caches/VisualStudio
rm -rf ~/Library/Preferences/VisualStudio
rm -rf ~/Library/Preferences/Visual\ Studio
rm -rf ~/Library/Logs/VisualStudio
rm -rf ~/Library/VisualStudio
rm -rf ~/Library/Preferences/Xamarin/
rm -rf ~/Library/Application\ Support/VisualStudio
```

::: moniker-end

::: moniker range="vsmac-2022"

```bash
sudo rm -rf "/Applications/Visual Studio.app"
rm -rf ~/Library/Caches/VisualStudio
rm -rf ~/Library/Preferences/VisualStudio
rm -rf ~/Library/Preferences/Visual\ Studio
rm -rf ~/Library/Logs/VisualStudio
rm -rf ~/Library/VisualStudio
rm -rf ~/Library/Preferences/Xamarin/
rm -rf ~/Library/Application\ Support/VisualStudio
```

::: moniker-end

你可能还想要删除包含各种 Xamarin 文件和文件夹的以下目录。 但是，此目录包含 Android 签名密钥。 有关详细信息，请参阅 **[卸载 Android SDK 和 Java SDK](#uninstall-android-sdk-and-java-sdk)** 部分：

```bash
rm -rf ~/Library/Developer/Xamarin
```

## <a name="uninstall-mono-sdk-mdk"></a>卸载 Mono SDK (MDK)

Mono 是 Microsoft .NET Framework 的开放源代码实现，可供所有 Xamarin 产品（Xamarin.iOS、Xamarin.Android 和 Xamarin.Mac）使用，让用户能使用 C# 开发这些平台。

> [!WARNING]
> 除 Visual Studio for Mac 之外，还有其他应用程序使用 Mono，例如 Unity。
> 卸载 Mono 前，请确保 Mono 上没有其他依赖项。

若要从计算机删除 Mono Framework，请在终端运行以下命令：

```bash
sudo rm -rf /Library/Frameworks/Mono.framework
sudo pkgutil --forget com.xamarin.mono-MDK.pkg
sudo rm -rf /etc/paths.d/mono-commands
```

## <a name="uninstall-xamarinandroid"></a>卸载 Xamarin.Android

安装和使用 Xamarin.Android 需要许多项，例如 Android SDK 和 Java SDK。

使用以下命令删除 Xamarin.Android：

```bash
sudo rm -rf /Developer/MonoDroid
rm -rf ~/Library/MonoAndroid
sudo pkgutil --forget com.xamarin.android.pkg
sudo rm -rf /Library/Frameworks/Xamarin.Android.framework
```

### <a name="uninstall-android-sdk-and-java-sdk"></a>卸载 Android SDK 和 Java SDK

开发 Android 应用程序需要 Android SDK。 要完全删除 Android SDK 的所有部分，请在 ~/Library/Developer/Xamarin/ 中找到相关文件，并将其移到回收站 。

> [!WARNING]
> 请注意，由Visual Studio for Mac生成的 Android 签名密钥位于 `~/Library/Developer/Xamarin/Keystore`。 请务必适当备份，或避免在要保留密钥存储时删除此目录。

无需卸载 Java SDK (JDK) ，因为它已预打包为 Mac OS X/macOS 的一部分。

### <a name="uninstall-android-avd"></a>卸载 Android AVD

> [!WARNING]
> 除 Visual Studio for Mac 之外，还有其他应用程序使用 Android AVD 和这些附加 Android 组件，如 Android Studio。 删除此目录可能会导致项目在 Android Studio 中中断。

若要删除任何 Android AVD 和其他 Android 组件，请使用以下命令：

```bash
rm -rf ~/.android
```

要仅删除 Android AVD，请使用以下命令：

```bash
rm -rf ~/.android/avd
```

## <a name="uninstall-xamarinios"></a>卸载 Xamarin.iOS

Xamarin.iOS 支持使用 C# 或 F# 通过 Visual Studio for Mac 开发 iOS 应用程序。

在终端使用以下命令从文件系统删除所有 Xamarin.iOS 文件：

```bash
rm -rf ~/Library/MonoTouch
sudo rm -rf /Library/Frameworks/Xamarin.iOS.framework
sudo rm -rf /Developer/MonoTouch
sudo pkgutil --forget com.xamarin.monotouch.pkg
sudo pkgutil --forget com.xamarin.xamarin-ios-build-host.pkg
sudo pkgutil --forget com.xamarin.xamarin.ios.pkg
```

## <a name="uninstall-xamarinmac"></a>卸载 Xamarin.Mac

可以使用以下两个命令从计算机中删除 Xamarin.Mac，这些命令分别从 Mac 中删除产品和许可证：

```bash
sudo rm -rf /Library/Frameworks/Xamarin.Mac.framework
rm -rf ~/Library/Xamarin.Mac
```

## <a name="uninstall-workbooks-and-inspector"></a>卸载工作簿和检查器

从 1.2.2 开始，可以通过在终端中运行以下命令卸载Xamarin Workbooks &检查器：

```bash
sudo /Library/Frameworks/Xamarin.Interactive.framework/Versions/Current/uninstall
```

需要在旧版本手动删除以下项目：

* 在 `"/Applications/Xamarin Workbooks.app"` 删除 Workbooks 应用
* 在 `"Applications/Xamarin Inspector.app"` 删除 Inspector 应用
* 删除加载项：`"~/Library/Application Support/XamarinStudio-6.0/LocalInstall/Addins/Xamarin.Interactive"` 和 `"~/Library/Application Support/XamarinStudio-6.0/LocalInstall/Addins/Xamarin.Inspector"`
* 在 `/Library/Frameworks/Xamarin.Interactive.framework` 和 `/Library/Frameworks/Xamarin.Inspector.framework` 删除 Inspector 和支持文件

## <a name="uninstall-the-xamarin-profiler"></a>卸载 Xamarin Profiler

```bash
sudo rm -rf "/Applications/Xamarin Profiler.app"
```

## <a name="uninstall-the-visual-studio-installer"></a>卸载 Visual Studio 安装程序

使用以下命令删除 Xamarin 通用安装程序的所有痕迹：

```bash
rm -rf ~/Library/Caches/XamarinInstaller/
rm -rf ~/Library/Caches/VisualStudioInstaller/
rm -rf ~/Library/Logs/XamarinInstaller/
rm -rf ~/Library/Logs/VisualStudioInstaller/
rm -rf ~/Library/Preferences/Xamarin/
rm -rf "~/Library/Preferences/Visual Studio/"
```

* * *

## <a name="see-also"></a>请参阅

- [卸载 Visual Studio (Windows)](/visualstudio/install/uninstall-visual-studio)
- [卸载 Visual Studio Code](https://github.com/Microsoft/vscode/issues/52151)
