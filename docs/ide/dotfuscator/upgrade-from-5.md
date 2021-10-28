---
title: 从 Dotfuscator Community 5 进行升级
ms.date: 07/21/2021
ms.devlang: dotnet
ms.topic: how-to
keywords: Dotfuscator, Dotfuscator Community, Dotfuscator CE, PreEmptive, PreEmptive Solutions, PreEmptive Protection, 保护, 社区版, 模糊处理, .NET, 免费, Visual Studio 2019, Visual Studio 2017, Visual Studio, 升级, 命令行
helpviewer_keywords:
- PreEmptive Protection Dotfuscator
- Dotfuscator Community Edition
- Dotfuscator CE
- Dotfuscator Community
- Dotfuscator
- obfuscation
- protection
- Dotfuscator upgrade
- upgrade Dotfuscator
- upgrading Dotfuscator
- register Dotfuscator
- registering Dotfuscator
- Dotfuscator command line
- Dotfuscator Professional
description: 了解如何升级 Visual Studio 中包含的免费 Dotfuscator Community 5 副本。
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.openlocfilehash: c1a6375a26325ca6f297b78a3024117e6e39132f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126642192"
---
# <a name="upgrade-from-dotfuscator-community-5"></a>从 Dotfuscator Community 5 进行升级

了解如何升级到 PreEmptive Protection - Dotfuscator Community 6。

根据你的安装历史记录和 Visual Studio 的版本，你当前可能正在运行 Dotfuscator Community 5，即之前的主版本。 如果是这样，那么应进行升级，因为必须确保为代码提供[最新的保护措施][always-improving]。 升级是免费的。

本文介绍如何确定当前拥有的版本，如何升级到版本 6（如有必要），以及这两个版本之间不同的已替换或删除的功能。

## <a name="determine-the-dotfuscator-version"></a>确定 Dotfuscator 版本

如果不确定正在运行哪个 Dotfuscator 版本，可以通过执行以下选项之一来确定版本：

* 通过转到 Visual Studio 的“工具”菜单并选择“PreEmptive Protection - Dotfuscator Community”启动 Dotfuscator Community [图形用户界面][gui] (GUI) 。

  从 Dotfuscator GUI，打开“帮助”菜单，并选择“关于...”以显示“关于”屏幕 。
  
  此屏幕将列出 Dotfuscator 的版本。

* 如果[命令行接口][cli]（如 [Xamarin][xamarin] 应用中的）的生成中集成了 Dotfuscator，则还可以查看行的生成日志，如下示例所示：

  ```no-highlight
  Dotfuscator Community Version 5.42.0.9514-e0e25f754
  ```

  可能需要增加生成的详细程度才能看到此文本。
  对于 Visual Studio，请参阅[详细程度设置][verbosity]。

版本的第一个整数（第一个点 `.` 之前）指示 Dotfuscator 的主要版本。 如果第一个整数是 `5`，则应在此页上执行升级步骤，以便可以利用最新 Dotfuscator 6 功能和保护更新。

## <a name="upgrade-instructions"></a>升级说明

本部分包含一组说明，说明如何将 Dotfuscator Community 的典型用法从版本 5 升级到版本 6。

### <a name="install-dotfuscator-6"></a>安装 Dotfuscator 6

Dotfuscator Community 作为 Visual Studio 的扩展进行分发。 Dotfuscator 6 的安装说明具体取决于所具有的 Visual Studio 版本：

* **Visual Studio 2019** Dotfuscator Community 6 在更高版本的 Visual Studio 2019（版本 16.10.0 及更高版本）中提供。
  [ Visual Studio 2019 升级][vs-update]至最新版本。 更新 Visual Studio 会自动将任何 Dotfuscator Community 5 安装升级到 Dotfuscator Community 6。

    * 如果尚未安装 Dotfuscator，请先更新 Visual Studio，然后参阅[安装][install]。

    * 除了 Visual Studio 的发布版本外，还可以从 [Dotfuscator 下载][download]页获得最新版本的 Dotfuscator Community。

* **Visual Studio 2017** 此版本的 Visual Studio 仅随 Dotfuscator Community 5 一起提供。
  但是，可以通过转到 [Dotfuscator 下载][download]页并选择相应的下载链接，来安装或升级到 Dotfuscator Community 6。

  运行下载的 `.vsix` 文件，然后按照提示将 Dotfuscator Community 6 安装到 Visual Studio。 现有 Dotfuscator Community 5 安装也将进行升级。

* **Visual Studio 早期版本** 这些版本的 Visual Studio 不支持 Dotfuscator Community 6。
  建议升级到较新 Visual Studio 版本，或[从 Dotfuscator Community 升级到 Dotfuscator Professional][pro]。

如果之前已[注册][register] Dotfuscator Community 5，则首次运行 Dotfuscator Community 6 时，会自动转换该注册。

<a name="steps-cli"></a>

### <a name="update-paths-to-the-cli"></a>更新 CLI 的路径

如果之前使用 Dotfuscator 5 的[命令行接口][cli] (CLI) 保护应用，则需要更新任何项目中 CLI 的路径，并生成引用它的脚本。 它包含使用 Dotfuscator Community 的 [Xamarin][xamarin] 集成的项目。

Dotfuscator CLI 的路径现在可能无效的原因是，与 Dotfuscator Community 一起安装的一些可执行文件的名称已在 Dotfuscator 6 中更改。 此更改使这些可执行文件名称在 Dotfuscator Community 和 Dotfuscator Professional 中相同。

| 执行文件所属...                     | Dotfuscator 5         | Dotfuscator 6         |
|---------------------------------------|-----------------------|-----------------------|
| [GUI][gui] | `dotfuscator.exe`     | `dotfuscatorUI.exe`   |
| [CLI][cli]   | `dotfuscatorCLI.exe`  | `dotfuscator.exe`     |

> [!NOTE]
> 如果在 Visual Studio 主版本之间进行升级或切换 Visual Studio 版本，则 CLI 路径可能也会无效，因为 Dotfuscator CLI 安装在 Visual Studio 安装目录下。
下面列出的症状和解决方案也适用于此情景。

如果生成使用的是无效的 Dotfuscator CLI 路径，则可能会出错，如以下示例之一所示：

`'"[...]\PreEmptiveSolutions\DotfuscatorCE\dotfuscatorCLI.exe"' is not recognized as an internal or external command,
operable program or batch file.`

`The command ""[...]\PreEmptiveSolutions\DotfuscatorCE\dotfuscatorCLI.exe" Dotfuscator.xml" exited with code 9009.`

`When the DotfuscatorXamarinEnabled property is 'true', the Dotfuscator command line interface specified by
DotfuscatorXamarinCliPath ('[...]\DotfuscatorCE\dotfuscatorCLI.exe') must exist.`

若要更新生成以使用正确的 CLI 路径：

1. 通过转到 Visual Studio 的“工具”菜单并选择“PreEmptive Protection - Dotfuscator Community”，启动 Dotfuscator Community [GUI][gui] 。
   
2. 在 Dotfuscator Community GUI，转到“工具”菜单，并选择“Dotfuscator 命令提示符” 。

3. 在打开的命令提示符中键入 `where dotfuscator.exe`。
   将显示的第一个路径复制到纯文本文档，供以后参考。 此路径是 Dotfuscator Community 6 CLI 的新路径。

4. 根据生成系统情况打开项目或生成配置。

    * 对于 Visual Studio 项目，将需要以纯文本形式打开项目文件（`.csproj`、`.vbproj` 或 `.fsproj`）。 在 Visual Studio 中[打开项目](../solutions-and-projects-in-visual-studio.md#project-file)。
    
    * 如果之前使用 Dotfuscator Community 的 [Xamarin][xamarin] 集成保护 Xamarin 应用，请回想一下，Dotfuscator 分别集成到了每个应用项目（如 `MyProject.Android.csproj` 和 `MyProject.iOS.csproj`）中，而不是集成到共享库项目中。
      需要更新当前使用 Dotfuscator 的所有应用项目。

5. 查找项目中使用了 Dotfuscator Community 5 CLI 的旧路径的任何位置或生成配置。
   它通常是以 `dotfuscatorCLI.exe` 结尾的路径。

    * 使用 Dotfuscator Community 的 [Xamarin][xamarin] 集成更新项目时，旧路径将位于 `<DotfuscatorXamarinCliPath>` 和 `</DotfuscatorXamarinCliPath>` 标记之间。

6. 将步骤 5 中的旧路径替换为在步骤 3 中记下的新路径。
   
   如果其中一个旧路径不是绝对路径，则应根据上下文适当调整新路径。
   在下面的示例中，旧路径中使用了 `VSInstallDir` 环境变量，因此相应的新路径也应如此。

    * 步骤 3 中的新路径：`C:\Program Files (x86)\Microsoft Visual Studio\2019\Preview\Common7\IDE\Extensions\PreEmptiveSolutions\DotfuscatorCE\dotfuscator.exe`
    * 项目文件的旧路径：`%VSInstallDir%\Common7\IDE\Extensions\PreEmptiveSolutions\DotfuscatorCE\dotfuscatorCLI.exe`
    * 项目文件的新路径：`%VSInstallDir%\Common7\IDE\Extensions\PreEmptiveSolutions\DotfuscatorCE\dotfuscator.exe`

7. 如果使用源代码管理系统（如 Git），请确保步骤 6 中的更改反映在该系统中。
   将这些更改分发给团队的其他成员，因为这可能适合你的系统和组织。

> [!WARNING]
> 由于 `dotfuscator.exe` 在 Dotfuscator 5 中引用图形用户界面 (GUI)，而在 Dotfuscator 6 中引用命令行接口 (CLI)，因此在更新跨多台计算机共享的生成脚本时请谨慎操作。
>
> 如果安装了 Dotfuscator 5 的计算机运行针对 Dotfuscator 6 进行了更新的脚本，会导致脚本启动图形用户界面，而不是预期的命令行接口。 这可能会导致生成成功，尽管未应用 Dotfuscator 的保护，这意味着不会保护输出包。
>
> 在其他情况下，它可能会导致生成失败。
>
> 若要避免这些情况，请在所有计算机中将 Dotfuscator Community 从版本 5 升级到版本 6，并同时生成脚本。

<a name="steps-config-files"></a>

### <a name="upgrade-dotfuscator-config-files"></a>升级 Dotfuscator 配置文件

在 Dotfuscator 6 之前创建的全部 Dotfuscator 配置文件（如 `Dotfuscator.xml`）将需要升级。

如果尝试使用旧配置文件运行 Dotfuscator CLI，将出现错误，如以下示例所示：

`Dotfuscator Engine Initialization error: PreEmptive Analytics, Authenticode signing, and the Introduce Explicit Method Overrides
setting are no longer supported. Please open your Dotfuscator config in the Config Editor which will automatically upgrade it.`

> [!IMPORTANT]
> 即使未使用上述功能，你也会收到此错误，并且需要升级配置文件。

升级配置文件：

1. 通过转到 Visual Studio 的“工具”菜单并选择“PreEmptive Protection - Dotfuscator Community”启动 Dotfuscator Community [图形用户界面][gui] (GUI) 。

2. 打开问题中的 Dotfuscator 配置文件 (Ctrl+O)。

3. 以下消息将显示在“生成输出”选项卡中：

    `PreEmptive Analytics, Authenticode signing, and the Introduce Explicit Method Overrides setting are no longer supported.
   The associated settings have been removed. Please save your upgraded Dotfuscator config.`

4. 存储已更新的 Dotfuscator 配置文件 (Ctrl+S)。

5. 如果使用源代码管理系统（如 Git），请确保 Dotfuscator 配置文件的更改在该系统中得到反映。
   将这些更改分发给团队的其他成员，因为这可能适合你的系统和组织。

### <a name="update-xamarin-integration"></a>更新 Xamarin 集成

如果将 Dotfuscator Community 5 集成到 [Xamarin][xamarin] 项目中，[其中一个步骤][xamarin-download]中需要下载自定义 MSBuild 目标和任务，如 `PreEmptive.Dotfuscator.Xamarin.targets`。 这些目标和任务已在 Dotfuscator Community 6 中更新，因此需要将旧版本替换为新版本。

更新 Xamarin 集成文件：

1. 找到最初下载这些文件的目录。
   [说明][xamarin-download]中提供的示例使用名为 `PreEmptive.Dotfuscator.Xamarin` 的子目录，但你可能将文件下载到了其他目录中，该目录可能有也可能没有与 Dotfuscator 无关的文件。

2. 在步骤 1 的目录中，删除与 Dotfuscator Xamarin 集成相关的文件。

3. 下载当前版本的以下用户指南部分中链接的 ZIP 文件：[下载 Dotfuscator 的 MSBuild 目标和任务的自定义集][xamarin-download]。

4. 将 ZIP 文件的内容提取到步骤 1 中提到的目录。

5. 如果使用源代码管理系统（如 Git），请确保旧文件的删除和新文件的添加在该系统中得到反映。
   根据系统类型，这些更改可能会显示为文件更改内容，而不是被替换。
   将这些更改分发给团队的其他成员，因为这可能适合你的系统和组织。

此页上的其他小节也适用于 Xamarin 项目，因此请务必查看本页的其余说明。

### <a name="update-references-to-attribute-libraries"></a>更新对属性库的引用

Dotfuscator 使你能够通过源代码中的 [.NET 属性][dotnet-attributes]配置某些功能。
如果项目正在使用此类属性，你可能需要更新这些属性，以解决 Dotfuscator 6 中的更改。

#### <a name="obfuscation-attributes"></a>混淆属性

[混淆属性][attributes-obfuscation]没有发生更改。 这些属性在 .NET 基类库中定义，Dotfuscator Community 6 将继续遵循这些属性的定义。

<a name="steps-attrs-check"></a>

#### <a name="check-attributes"></a>检查属性

包含[检查属性][attributes-checks]的库已更改。 在 Dotfuscator Community 5 中，它作为文件与 Dotfuscator 本身一起分发。 从 Dotfuscator Community 6 开始，它改为作为公共 NuGet 包分发。

如果尝试生成仍引用旧位置的 Visual Studio 项目，可能会出现错误，如以下示例所示：

`The type or namespace name 'PreEmptive' could not be found
(are you missing a using directive or an assembly reference?)`

`The type or namespace name 'TamperCheckAttribute' could not be found
(are you missing a using directive or an assembly reference?)`

你还可能得到此警告：

`Could not resolve this reference. Could not locate the assembly "PreEmptive.Attributes". Check to make sure the assembly exists
on disk. If this reference is required by your code, you may get compilation errors.`

更新项目以使用新位置：

1. 删除项目程序集对 `PreEmptive.Attributes.dll` 的引用。

2. 向项目添加 NuGet 包引用 `PreEmptive.Protection.Checks.Attributes`。
    包在默认 NuGet 源 [nuget.org][nuget-org] 上提供。

还删除了每个检查属性的 `ExtendedKey` 参数。
这些参数在 Dotfuscator Community 5 中被忽略，但如果源代码依然使用这些参数，就需要删除这些使用过程，以便项目进行编译。

<a name="steps-attrs-analytics"></a>

#### <a name="instrumentation-attributes"></a>检测属性

检测属性用于在 Dotfuscator 5 中配置 PreEmptive Analytics 功能。 但是，PreEmptive Analytics 在 Dotfuscator 6 中已删除，请参阅“已删除的功能”子节 [PreEmptive Analytics](#removed-analytics)。 因此，检测属性也已删除。

如果尝试生成使用检测属性的 Visual Studio 项目，可能会收到与[检查属性](#steps-attrs-check)中记录的错误和警告类型相同的错误和警告，其中的属性名称会有不同（例如是 `FeatureAttribute` 而不是 `TamperCheckAttribute`）。

如果尝试在包含检测属性用法的已生成的程序集上运行 Dotfuscator，将出现错误，如以下示例所示：

`The PreEmptive.Attributes.FeatureAttribute attribute (annotating SomeNamespace.SomeType::SomeMethod) is not recognized
by this version of Dotfuscator.`

若要解决这些问题，需要从源代码中删除检测属性的所有用法。
还需要删除对定义属性的库 `PreEmptive.Attributes.dll` 的程序集引用。
（如果还使用了此库中定义的检查属性，这些属性已移动；请参阅上面的[检查属性](#steps-attrs-check)。）

## <a name="removed-features"></a>删除的功能

Dotfuscator Community 6 引入了 Dotfuscator Community 5 中的中断性变更。 如果你一直在使用 Dotfuscator Community 5，本部分将介绍如何处理可能需要修改生成或影响 Dotfuscator 输出的更改。

可在[更改日志][changelog]中查看更改的完整列表。

<a name="removed-analytics"></a>

### <a name="preemptive-analytics"></a>PreEmptive Analytics

Dotfuscator 6 不支持 PreEmptive Analytics，包括“检查遥测”。 但是，仍支持[检查][checks-overview]本身（包括[应用程序通知][checks-notification]和[检查操作][checks-actions]）。

若要使用 Dotfuscator 6，需要[升级配置文件](#steps-config-files)，以删除 PreEmptive Analytics 设置。

如果使用代码内属性配置 PreEmptive Analytics，将需要[从源代码删除它们](#steps-attrs-analytics)，并重新生成输入程序集，然后 Dotfuscator 6 便可保护这些程序集。

如果某个检查检测到无效状态后（如[检测到篡改][tamper]时）使用“检查遥测”进行报告，可以将其替换成一个自定义[应用程序通知][checks-notification]，该通知向 [Azure Application Insights][application-insights] 或你选择的其他服务报告事件。

### <a name="unsupported-application-types"></a>不受支持的应用程序类型

Dotfuscator 6 不再支持以下应用程序类型：

* Windows Phone
* WinRT（Windows 8 应用）
* Silverlight
* Unity（游戏引擎）

此外，通用 Windows 平台 (UWP) 应用仅支持 [Xamarin][xamarin] 方案。

若要保护其他类型的 UWP 应用，请[升级到 Dotfuscator Professional][pro] 并遵循[保护应用][pro-pya]说明。

### <a name="unsupported-inputs"></a>不支持的输入

Dotfuscator Community 不再支持将通用 Windwos 平台 (UWP) `.appx` 包作为[输入][inputs]。 可以继续使用 [Xamarin][xamarin] 集成来保护面向 UWP 的 Xamarin 应用。 若要保护其他类型的 UWP 应用，请[升级到 Dotfuscator Professional][pro] 并遵循[保护应用][pro-pya]说明。

此外，`.xap` 包将不再作为输入，因为不再支持 Silverlight。

### <a name="introduce-explicit-method-overrides"></a>引入显式方法重写

用于引入显式方法重写的“重命名”选项已从 Dotfuscator 中删除。 若要使用 Dotfuscator 6，需要[升级配置文件](#steps-config-files)，以删除该设置。

[changelog]: https://www.preemptive.com/support/dotfuscator-support/dotfuscator-ce-change-log
[download]: https://www.preemptive.com/products/dotfuscator/downloads
[always-improving]: https://www.preemptive.com/always-improving
[vs-update]: ../../install/update-visual-studio.md

[install]: https://www.preemptive.com/dotfuscator/ce/docs/help/intro_install.html
[register]: https://www.preemptive.com/dotfuscator/ce/docs/help/intro_register.html
[pro]: https://www.preemptive.com/dotfuscator/ce/docs/help/intro_upgrades.html
[pro-pya]: https://www.preemptive.com/dotfuscator/pro/userguide/en/getting_started_protect.html

[gui]:  https://www.preemptive.com/dotfuscator/ce/docs/help/getting_started_gui.html
[cli]: https://www.preemptive.com/dotfuscator/ce/docs/help/intro_cli.html
[xamarin]: https://www.preemptive.com/dotfuscator/ce/docs/help/getting_started_xamarin.html
[xamarin-download]: https://www.preemptive.com/dotfuscator/ce/docs/help/getting_started_xamarin.html#pctoc-download-the-custom-set-of-msbuild-targets-and-tasks-for-dotfuscator

[inputs]: https://www.preemptive.com/dotfuscator/ce/docs/help/gui_inputs.html

[checks-overview]: https://www.preemptive.com/dotfuscator/ce/docs/help/checks_overview.html
[checks-notification]: https://www.preemptive.com/dotfuscator/ce/docs/help/checks_overview.html#pctoc-application-notification
[checks-actions]: https://www.preemptive.com/dotfuscator/ce/docs/help/checks_overview.html#pctoc-check-actions
[tamper]: https://www.preemptive.com/dotfuscator/ce/docs/help/checks_tamper.html

[attributes-checks]: https://www.preemptive.com/dotfuscator/ce/docs/help/attributes_checks.html
[attributes-obfuscation]: https://www.preemptive.com/dotfuscator/ce/docs/help/attributes_obfuscation.html

[verbosity]: ../how-to-view-save-and-configure-build-log-files.md#to-change-the-amount-of-information-included-in-the-build-log
[dotnet-attributes]: /dotnet/standard/attributes
[application-insights]: /azure/azure-monitor/app/app-insights-overview
[nuget-org]: https://www.nuget.org/
