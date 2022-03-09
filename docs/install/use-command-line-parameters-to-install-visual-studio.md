---
title: 使用命令行参数安装 Visual Studio
titleSuffix: ''
description: 了解如何使用命令行参数来控制或自定义 Visual Studio 安装。
ms.date: 3/3/2022
ms.topic: conceptual
f1_keywords:
- command-line parameters
- switches
- command prompt
ms.assetid: 480f3cb4-d873-434e-a8bf-82cff7401cf2
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: fd941f65dd5571f8c95e0900c9aecee2b8cecf09
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139551295"
---
# <a name="use-command-line-parameters-to-install-update-and-manage-visual-studio"></a>使用命令行参数来安装、更新和管理 Visual Studio

以编程方式或从命令提示符安装 Visual Studio 时，可以使用各种命令行参数来控制或自定义安装并执行以下操作：

- 使用预先选择的特定选项和行为来启动客户端上的安装。
- 自动执行安装或更新过程。
- 创建或维护产品文件的网络布局，以便安装或更新客户端计算机。

下面所述的命令行选项可以与安装引导程序结合使用，安装引导程序是小型 (~ 1 MB) 文件 (例如，vs_enterprise.exe) 启动下载过程，或与安装程序一起使用。 下面列出的所有命令和参数均用于处理引导程序，除非显式指定为仅安装程序。 请注意，如果通过布局安装 Visual Studio，则客户端计算机可能只有可用于编程执行的安装程序。 

还可以使用可从 [Microsoft 更新目录](https://catalog.update.microsoft.com)下载的管理员更新包，以编程方式更新网络布局。 若要详细了解如何这样做，请参阅[更新或修改布局](create-a-network-installation-of-visual-studio.md#update-the-layout-to-a-specific-version-of-the-product)文档。  

::: moniker range="vs-2017"

若要获取 Visual Studio 2017 版本 15.9 的引导程序，请下载以下引导程序文件之一：

| **版本**                                  | **引导程序**       |
|----------------------------------------------|---------------------|
| Visual Studio Enterprise 2017 版本 15.9   | [vs_enterprise.exe](https://aka.ms/vs/15/release/vs_enterprise.exe)  |
| Visual Studio Professional 2017 版本 15.9 | [vs_professional.exe](https://aka.ms/vs/15/release/vs_professional.exe)  |
| Visual Studio 生成工具 2017 版本 15.9  | [vs_buildtools.exe](https://aka.ms/vs/15/release/vs_buildtools.exe)   |

::: moniker-end

::: moniker range="vs-2019"

可以从下表中获取 Visual Studio 2019 引导程序。 或者，如果需要特定版本的 Visual Studio 2019，请转到 [Visual Studio 2019 版本](/visualstudio/releases/2019/history#installing-an-earlier-release)页，该页包含指向所选 Visual Studio 版本的固定版本引导程序的链接。

| **版本**                     | **引导程序**                                                             |
|---------------------------------|------------------------------------------------------------------------------|
| Visual Studio 2019 Enterprise 版本 16.11   | [vs_enterprise.exe](https://aka.ms/vs/16/release/vs_enterprise.exe)     |
| Visual Studio 2019 Professional 版本 16.11| [vs_professional.exe](https://aka.ms/vs/16/release/vs_professional.exe) |
| Visual Studio 2019 生成工具版本 16.11 | [vs_buildtools.exe](https://aka.ms/vs/16/release/vs_buildtools.exe)     |

::: moniker-end

::: moniker range=">=vs-2022"

若要获取始终安装最新当前频道版本的 Visual Studio 2022 的最新引导程序，请下载以下文件之一。 或者，如果要安装 Visual Studio 2022 的特定版本或特定频道，请转到 [Visual Studio 2022 版本历史记录](/visualstudio/releases/2022/release-history#release-dates-and-build-numbers)页，该页包含指向每个服务版本的固定版本引导程序的链接。 

| **版本**                      | **引导程序**                                                                                   |
|----------------------------|-------------------------------------------------------------------------------------------|
| Visual Studio 2022 Enterprise   | [vs_enterprise.exe](https://aka.ms/vs/17/release/vs_enterprise.exe)     |
| Visual Studio 2022 Professional | [vs_professional.exe](https://aka.ms/vs/17/release/vs_professional.exe) |
| Visual Studio 2022 Community    | [vs_community.exe](https://aka.ms/vs/17/release/vs_community.exe)       |
| Visual Studio 2022 生成工具   | [vs_buildtools.exe](https://aka.ms/vs/17/release/vs_buildtools.exe)         |

::: moniker-end

::: moniker range="vs-2017"

>[!TIP]
>如果以前下载过引导程序文件，并且想要验证其版本，操作方法如下。 在 Windows 中，打开文件资源管理器，右键单击引导程序文件，依次选择“属性”、“详细信息”选项卡，然后查看“产品版本”号    。 若要将该编号与 Visual Studio 的版本匹配，请参阅 [Visual Studio 内部版本号和发布日期](visual-studio-build-numbers-and-release-dates.md)页。

::: moniker-end

::: moniker range="vs-2019"

>[!TIP]
>如果以前下载过引导程序文件，并且想要验证其版本，则操作方法如下。 在 Windows 中，打开文件资源管理器，右键单击引导程序文件，依次选择“属性”、“详细信息”选项卡，然后查看“产品版本”号    。 若要将该编号与 Visual Studio 的版本匹配，请参阅 [Visual Studio 2019 版本](/visualstudio/releases/2019/history)页面底部的表。

::: moniker-end

::: moniker range=">=vs-2022"

>[!TIP]
>如果你之前下载了一个引导程序文件，并且想要验证它将安装的版本，操作方法如下。 在 Windows 中，打开“文件资源管理器”，右键单击该引导程序文件，选择“属性”，然后选择“详细信息”选项卡。“产品版本”字段将描述该引导程序将安装的[频道和版本](/visualstudio/releases/2022/vs2022-release-rhythm)  。 版本号应始终读取为“指定内容的最新服务版本”，除非显式指定，否则频道为“当前”。 因此，产品版本为 LTSC 17.0 的引导程序将安装 17.0 LTSC 频道上提供的最新 17.0.x 服务版本。 产品版本仅显示“Visual Studio 2022”的引导程序将在当前频道上安装最新版本的 Visual Studio 2022。

::: moniker-end

可在以下位置找到 Visual Studio 安装程序： `C:\Program Files (x86)\Microsoft Visual Studio\Installer\setup.exe` 。 请注意，不能以编程方式从安装程序所在的同一目录启动安装程序。   

## <a name="install-update-modify-repair-uninstall-and-export-commands-and-command-line-parameters"></a>安装、更新、修改、修复、卸载和导出命令以及命令行参数

以编程方式调用 Visual Studio 引导程序或安装程序以安装产品或维护布局时，第一个参数是命令 (谓词) 描述要执行的操作。 后续的可选命令行参数带两个短划线 (--) 作为前缀，将进一步定义该操作的发生方式。 所有 Visual Studio 命令行参数均不区分大小写，可以在[命令行参数示例](command-line-parameter-examples.md)页上查看更多示例。

语法示例：`vs_enterprise.exe [command] <optional parameters>...`

| **命令** | **说明**                                                                                                         |
|-------------|-------------------------------------------------------------------------------------------------------------------------|
| (空白)     | 默认的命令不仅安装该产品，还用于所有布局维护操作。                    |
| `modify`    | 修改已安装的产品。                                                                                          |
| `update`    | 更新已安装的产品。                                                                                           |
| `repair`    | 修复已安装的产品。                                                                                           |
| `uninstall` | 卸载已安装的产品。                                                                                        |
| `export`    | 将安装所选内容导出到安装配置文件。 **注意**：只能与 vs_installer.exe 或 setup.exe 一起使用。 |

> [!IMPORTANT]
> 当指定多种不同的工作负载、组件或语言时，必须对每项重复运行 `--add` 或 `--remove` 命令行开关。

| **参数**                                     | **说明**                                                            |
|----------------------------------------------------|----------------------------------------------------------------------|
| `--installPath <dir>`                              | 对于默认安装命令，此参数是 **可选** 的，用于说明实例在客户端计算机上的安装位置。 对于其他命令，如 update 或 modify，此参数是 **必需** 的，用于指示实例在执行操作时使用的安装目录。  |
| `--add <one or more workload or component IDs>`    | **可选**：在 install 或 modify 命令期间，这个可重复参数会指定要添加的一个或多个工作负载或组件 ID。 将安装项目的所需组件，而不是建议组件或可选组件。 可以使用 `--includeRecommended` 和/或 `--includeOptional` 参数来全局性地控制更多组件。 若要包括多个工作负荷或组件，请重复 `--add` 命令（例如，`--add Workload1 --add Workload2`）。 若要更精确地进行控制，可以将 `;includeRecommended` 或 `;includeOptional` 追加到 ID 中（例如，`--add Workload1;includeRecommended` 或 `--add Workload2;includeRecommended;includeOptional`）。 有关详细信息，请参阅[工作负载和组件 ID](workload-and-component-ids.md) 页。 |
| `--remove <one or more workload or component IDs>` | **可选**：在 modify 命令期间，这个可重复参数会指定要删除的一个或多个工作负载或组件 ID。 该参数是 `--add` 参数的补充或与其行为相似。   |
| `--addProductLang <language-locale>`               | **可选**：在 install 或 modify 命令期间，这个可重复参数会指定要随产品一起安装的用户界面语言包。 如果不存在，安装过程将使用对应于计算机区域设置的语言包。 有关详细信息，请参阅本页的[语言区域设置列表](#list-of-language-locales)部分。  |
| `--removeProductLang <language-locale>`            | **可选**：在 install 或 modify 命令期间，这个可重复参数会确定要从产品中删除的用户界面语言包。  该参数是 `--addProductLang` 参数的补充或与其行为相似。 |
| `--in <path>`                                      | **可选**：[响应文件](automated-installation-with-response-file.md)的 URI 或路径，文件可包含配置设置。  |
| `--all`                                            | **可选**：在 install 或 modify 命令期间，这个参数会促使安装产品的所有工作负载和组件。  |
| `--allWorkloads`                                   | **可选**：在 install 或 modify 命令期间，这个参数将安装除建议的组件或可选组件外的所有工作负载和组件。  |
| `--includeRecommended`                             | **可选**：在 install 或 modify 命令期间，这个参数会包含已安装的任何工作负载的建议组件，但不包含可选组件。 可使用 `--allWorkloads` 或 `--add` 指定工作负载。  |
| `--includeOptional`                                | **可选**：在 install 或 modify 命令期间，这个参数会包含已安装的任何工作负载的可选组件，但不包含建议组件。 可使用 `--allWorkloads` 或 `--add` 指定工作负载。 |
| `--quiet, -q`                                      | **可选**：这个参数可与任何命令一起使用，可在命令执行时阻止显示任何用户界面。    |
| `--passive, -p`                                    | **可选**：这个参数会导致用户界面以非交互式方式显示。 此参数与 `--quiet` 参数是互斥的，事实上还会替代后者。   |
| `--norestart`                                      | **可选**：这个参数必须与 `--passive` 或 `--quiet` 参数配对使用。  在 install、update 或 modify 命令期间，如果添加 `--norestart` 参数，会延迟所有必要的重启行为。    |
| `--force`                                          | **可选**：这个参数会强行关闭 Visual Studio，即使有正在使用的 Visual studio 进程也是如此。   |
| `--installWhileDownloading`                        | **可选**：在 install、update 或 modify 命令期间，这个参数使 Visual Studio 能够同时下载和安装产品。 这是默认体验。  |
| `--downloadThenInstall`                            | **可选**：在 install、update 或 modify 命令期间，这个参数会强制性地让 Visual Studio 在安装所有文件之前先下载这些文件。 它与 `--installWhileDownloading` 参数互斥。   |
| `--channelURI`                                     | **可选**：在更新命令期间，可以传递新的 channelURI 来更改更新设置位置。  建议与 --installPath 参数配对，以便非常明确地显示要配置的Visual Studio实例。 请参阅 [--channelURI 的语法示例](/visualstudio/install/command-line-parameter-examples#using---channelURI) |
| `--nickname <name>`                                | **可选**：在 install 命令期间，这个参数会定义要分配给已安装的产品的昵称。 别名长度不能超过 10 个字符。 |
| `--productKey`                                     | **可选**：在 install 命令期间，这个参数会定义要用于已安装的产品的产品密钥。 由 25 个字母数字字符组成，格式为 `xxxxxxxxxxxxxxxxxxxxxxxxx`。  |
| `--help, --?, -h, -?`                              | 显示此页的脱机版本。     |
| `--config <path>`                                  | **可选**：在安装或修改操作期间，这将根据以前保存的安装配置文件确定要添加的工作负载和组件。 此操作是附加的，如果文件中不存在任何工作负载或组件，也不会删除任何工作负载或组件。 此外，不会添加不适用于该产品的项目。 在导出操作期间，这将确定保存安装配置文件的位置。                           |

## <a name="layout-command-and-command-line-parameters"></a>布局命令和命令行参数

所有布局管理操作都是使用引导程序 exe 运行的，它们假定命令是默认的"安装" (空白) ，而不考虑是创建还是更新布局。 因此，所有布局管理操作都始于必需的初始 `--layout` 参数。 下表介绍了使用命令行[创建或更新布局](create-a-network-installation-of-visual-studio.md)时可使用的其他参数。 

| **布局参数**                           | **说明**                                        |
|-------------------------------------------------|----------------------------------------------------------------------|
| `--layout <dir>`                                | 指定用于创建或更新脱机安装缓存的目录。 有关详细信息，请参阅[创建 Visual Studio 的网络安装](create-a-network-installation-of-visual-studio.md)。                       |
| `--lang <one or more language-locales>`         | **可选**：与 `--layout` 结合使用，以准备脱机安装缓存，以便使用包含指定语言的资源包。 有关详细信息，请参阅本页的[语言区域设置列表](#list-of-language-locales)部分。       |
| `--add <one or more workload or component IDs>` | **可选**：要添加的一个或多个工作负荷或组件 ID。 将安装项目的所需组件，而不是建议组件或可选组件。 可以使用 `--includeRecommended` 和/或 `--includeOptional` 全局控制其他组件。 若要更精确地进行控制，可以将 `;includeRecommended` 或 `;includeOptional` 追加到 ID 中（例如，`--add Workload1;includeRecommended` 或 `--add Workload2;includeOptional`）。 有关详细信息，请参阅[工作负载和组件 ID](workload-and-component-ids.md) 页。 <br/>**注意**：如果使用了 `--add`，只会下载指定的工作负载和组件及其依赖项。 如果未指定 `--add`，所有工作负载和组件都会下载到布局中。 |
| `--includeRecommended`                          | **可选**：包含所有已安装工作负载的推荐组件，但不包含可选组件。 可使用 `--allWorkloads` 或 `--add` 指定工作负载。         |
| `--includeOptional`                             | **可选**：添加布局中包含的任何工作负载的推荐 *和* 可选组件。 可使用 `--add` 指定工作负载。                        |
| `--keepLayoutVersion`                           | **可选**：将更改应用到布局中，而不更新布局中包含的产品版本。   |
| `--useLatestInstaller`         | **Optional**：如果存在，则最新版 Visual Studio 安装程序将包含在布局中，即使它属于较新版本的产品。 如果要利用最新安装程序中提供的新功能或 bug 修补程序，这非常有用。 有关详细信息，请参阅[配置布局以始终使用最新安装程序](create-a-network-installation-of-visual-studio.md#configure-the-layout-to-always-include-and-provide-the-latest-installer)文档。 |
| `--verify`                                      | **可选**：验证布局内容。 将列出所有损坏或缺失的文件。            |
| `--fix`                                         | **可选**：验证布局内容。  如果任何文件损坏或缺失，将重新进行下载。 必须连接 Internet，才能修复布局。           |
| `--clean <one or more paths to catalogs>`       | **可选**：从已更新到新版本的布局中删除旧版组件。    |

| **高级布局参数** | **说明**                                  |
|--------------------------------|--------------------------------------------------|
| `--channelId <id>`             | **可选**：要安装的实例的通道 ID。 如果指定了 `--installPath`，则此参数对于 install 命令是必需参数，对于其他命令则可忽略。        |
| `--channelUri <uri>`           | **可选**：通道清单的 URI。 此值可控制[更新的源位置](update-visual-studio.md#configure-source-location-of-updates-1)，初始值[在布局的 response.json 文件中配置](create-a-network-installation-of-visual-studio.md#configure-initial-client-installation-defaults-for-this-layout)。 有关可能 [的值，请参阅 --channelURI](/visualstudio/install/command-line-parameter-examples#using---channelURI) 的语法示例。 如果不需要更新，`--channelUri` 可指向不存在的文件（例如 --channelUri C:\doesntExist.chman）。 此参数可用于 install 命令；其他命令则可忽略。  |
| `--installChannelUri <uri>`    | **可选**：要用于安装的通道清单的 URI。  指定的 URI（指定 时必须指定）用于检测更新。 此参数可用于 install 命令；其他命令则可忽略。  |
| `--installCatalogUri <uri>`    | **可选**：要用于安装的目录清单的 URI。 如果指定此选项，通道管理器会先尝试通过此 URI 下载目录清单，然后再在安装通道清单中使用 URI。 此参数用于支持脱机安装，安装期间会使用已下载的产品目录创建布局缓存。 此参数可用于 install 命令；其他命令则可忽略。    |
| `--productId <id>`             | **可选**：将要安装的实例的产品 ID。 在正常安装条件下，这是预填充的。 `productID` 类似于“Microsoft.VisualStudio.Product.Enterprise”。 |
| `--wait`                       | **可选**：进程会先等待安装完成，然后再返回退出代码。 在需要等待安装完成以处理来自该安装的返回代码的自动安装中，这非常有用。      |
| `--locale <language-locale>`   | **可选**：更改安装程序本身的用户界面的显示语言。 将保留设置。 有关详细信息，请参阅本页的[语言区域设置列表](#list-of-language-locales)部分。     |
| `--cache`                      | **可选**：如果指定，将在安装后保存包，以便后续修复时使用。 这会替代用于后续安装、修复或修改的全局策略设置。 默认策略是缓存包。 对于卸载命令，忽略此选项。 有关详细信息，请了解如何[禁用或移动包缓存](disable-or-move-the-package-cache.md)。   |
| `--nocache`                    | **可选**：如果指定，将在安装或修复完成后删除包。 只有在需要时才会重新下载，并且会在使用后再次删除。 这会替代用于后续安装、修复或修改的全局策略设置。 默认策略是缓存包。 对于卸载命令，忽略此选项。 有关详细信息，请了解如何[禁用或移动包缓存](disable-or-move-the-package-cache.md)。    |
| `--noUpdateInstaller`          | **可选**：如果存在，指定无提示安装时阻止安装程序进行自我更新。 如果在需要更新安装程序时通过无提示安装指定 noUpdateInstaller，则安装程序将忽略该命令并返回非零退出代码。   |
| `--noWeb`                      | **可选**：如果存在，Visual Studio 安装程序将使用布局目录中的文件来安装 Visual Studio。 如果用户尝试安装不在布局中的组件，安装程序将失败。  有关详细信息，请参阅[从网络安装点进行部署](create-a-network-installation-of-visual-studio.md)。 <br/><br/> **重要说明**：此开关不会阻止 Visual Studio 安装程序检查更新。 有关详细信息，请参阅[控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)。 |
| `--path <name>=<path>`         | **可选**：用于指定安装的自定义安装路径。 支持的路径名称有 shared、cache 和 install。    |
| `--path cache=<path>`          | **可选**：使用指定的位置下载安装文件。 只可以在首次安装 Visual Studio 时设置此位置。 示例： `--path cache="C:\VS\cache"`   |
| `--path shared=<path>`         | **可选**：包含用于并行 Visual Studio 安装的共享文件。 某些工具和 SDK 会安装到此驱动器上的某个位置，而其他一些工具可能会替代此设置并安装到另一个驱动器。 示例： `--path shared="C:\VS\shared"` <br/><br/>**重要说明**：只能在首次安装 Visual Studio 时对此设置一次。     |
| `--path install=<path>`        | **可选**：等效于 `–-installPath`。 具体而言，`--installPath "C:\VS"` 与 `--path install="C:\VS"` 等效。 一次只能使用其中一个命令。     |

## <a name="configure-source-location-of-updates-command-and-command-line-parameters"></a>配置 updates 命令和命令行参数的源位置
可以通过在客户端计算机上使用安装程序或引导程序，并传递所需的更新通道，以编程方式配置给定 Visual Studio 实例的更新的源位置。  

| **modifySettings 参数**                   | **说明**                                        |
|-------------------------------------------------|----------------------------------------------------------------------|
| `--installPath <dir>`                           | **建议使用** 来指定要Visual Studio实例。  |
| `--newChannelUri`                               | **必需**：通道清单的 URI。 此值指定更新的下 [一个源位置](update-visual-studio.md#configure-source-location-of-updates-1) 。 有关可能 [的值，请参阅 --channelURI](/visualstudio/install/command-line-parameter-examples#using---channelURI) 的语法示例。 如果不需要更新，`--channelUri` 可指向不存在的文件（例如 --channelUri C:\doesntExist.chman）。 |
| `--channelUri`                               | 旧通道清单的 URI。 如果 --installPath 未知，可以使用 。 必须与 productID 结合使用，以标识要处理正确的 实例。 |
| `--productId <id>`                           | 如果指定了 --channelUri，则必须使用 ，并且用于标识要处理正确的 实例。 `productID` 类似于“Microsoft.VisualStudio.Product.Enterprise”。 |
| `--quiet, -q`                                   | **可选**：此参数可防止在执行命令时显示任何用户界面。    |

语法示例： 

`C:\>"C:\Program Files (x86)\Microsoft Visual Studio\Installer\setup.exe" modifySettings --installPath "C:\Program Files\Microsoft\Visual Studio\2022\Enterprise" --newChannelURI https://aka.ms/vs/17/release.LTSC.17.0/channel`

`C:\>"C:\Program Files\Microsoft\Visual Studio\2022\Enterprise\vs_enterprise.exe" modifySettings --channelURI https://aka.ms/vs/17/release.LTSC.17.0/channel --productID Microsoft.VisualStudio.Product.Enterprise --newChannelURI \\layoutserver\share\path\channelmanifest.json --quiet`

## <a name="administrator-update-command-and-command-line-parameters"></a>管理员更新命令和命令行参数

可以从目录下载 **管理员** Microsoft 更新 [，](https://catalog.update.microsoft.com) 并使用它来更新客户端安装或布局。 

如果要将布局更新到特定版本的 Visual Studio，只需将管理员更新下载到承载该布局的计算机，打开该计算机上的命令提示符并运行如下所示的命令：`visualstudioupdate-17.0.0to17.1.5.exe layout --layoutPath c:\VSLayout`

在客户端上，如果将管理员更新下载到客户端计算机上的安装目录中，只需双击文件即可应用更新。 还可以打开命令窗口并传递下面的某些参数来更改默认行为。 

如果要通过 Microsoft Endpoint Manager (SCCM) 部署管理员更新，可以使用以下参数来修改包以调整行为。 还可以通过客户端计算机上的配置文件来控制参数。 有关详细信息，请参阅[配置管理员更新的方法](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update)

请注意，除非指定了布局谓词，否则所有管理员更新参数默认在"更新"上下文中运行。

| **管理员更新参数**           | **说明**  |
|-----------------------------------------------|------------------|
| `--installerUpdateArgs [optional parameters]` | 此参数充当与管理员更新方案相关的特定参数的“直通数组”。 为此目的启用的可选参数包括： <br/><br/> `--quiet`：这是管理员更新的默认体验，此处出于完整性的目的列出了该体验。 <br/> `--passive`：此参数会替代 `--quiet` 参数。  这会导致用户界面以非交互式方式显示。 <br/>`--norestart`：此参数必须与 `--quiet` 或 `--passive` 一起使用，会导致任何必要的重启行为延迟。 <br/>`--noWeb`：此参数会阻止 Visual Studio 在 internet 上查找产品更新。 <br/>`--force`：此参数会强行关闭 Visual Studio，即使 Visual studio 正在使用中也是如此。 请谨慎使用此参数，因为有可能会导致工作丢失。 此参数必须在用户上下文中使用。 <br/>`--installWhileDownloading`：此参数使 Visual Studio 能够同时下载和安装产品。 这是管理员更新的默认体验，此处出于完整性的目的列出了该体验。 <br/>`--downloadThenInstall`：此参数强制 Visual Studio 在安装所有文件之前先下载文件。 它与 `--installWhileDownloading` 参数互斥。 |
| `--checkPendingReboot`                        | 如果计算机上有挂起的重启，更新将中止，无论导致该更新的是哪个应用程序。 默认情况下，系统不检查是否有挂起的重启。    |

语法示例：`visualstudioupdate-16.9.0to16.9.4.exe --installerUpdateArgs=--force,--noWeb --checkPendingReboot`

## <a name="list-of-workload-ids-and-component-ids"></a>工作负荷 ID 和组件 ID 列表

有关按 Visual Studio 产品排序的工作负载和组件 ID 的列表，请参阅 [Visual Studio 工作负载和组件 ID](workload-and-component-ids.md) 页。

## <a name="list-of-language-locales"></a>语言区域设置列表

| **语言-区域设置** | **语言**          |
|---------------------|-----------------------|
| Cs-cz               | 捷克语                 |
| De-de               | 德语                |
| En-us               | 英语               |
| Es-es               | 西班牙语               |
| Fr-fr               | 法语                |
| It-it               | 意大利语               |
| Ja-jp               | 日语              |
| Ko-kr               | 韩语                |
| Pl-pl               | 波兰语                |
| Pt-br               | 葡萄牙语 - 巴西   |
| Ru-ru               | 俄语               |
| Tr-tr               | 土耳其语               |
| Zh-cn               | 简体中文  |
| Zh-tw               | 繁体中文 |

## <a name="error-codes"></a>错误代码

`%ERRORLEVEL%` 环境变量设为下列值之一，具体视操作结果而定：

[!INCLUDE[install-error-codes-md](includes/install-error-codes-md.md)]

每个操作都会在指明安装进度的 `%TEMP%` 目录中生成多个日志文件。 按日期对文件夹进行排序，再查找以“`dd_bootstrapper`”、“`dd_client`”和“`dd_setup`”开头的文件，分别查找安装引导程序、安装程序应用和安装程序引擎。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

- [Visual Studio 安装命令行参数示例](command-line-parameter-examples.md)
- [创建 Visual Studio 的脱机安装](create-an-offline-installation-of-visual-studio.md)
- [通过响应文件自动执行 Visual Studio 安装](automated-installation-with-response-file.md)
- [Visual Studio 工作负荷和组件 ID](workload-and-component-ids.md)
