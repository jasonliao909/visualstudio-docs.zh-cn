---
title: 选择安装位置
description: 了解如何通过将下载缓存、共享组件、SDK 和工具的位置更改到不同的驱动器来减少 Visual Studio 在系统驱动器上的安装占用。 例如，将 C 驱动器中的一些文件移动到 D 驱动器。
ms.date: 09/14/2021
ms.custom: vs-acquisition
ms.topic: how-to
helpviewer_keywords:
- change installation locations for Visual Studio
- select an installation location for Visual Studio files
- move installation files to different drives
- use the D drive
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: be2c18e531af3a0aa6dd059206ce81db7734ab08
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128431793"
---
# <a name="select-the-installation-locations-in-visual-studio"></a>在 Visual Studio 中选择安装位置

::: moniker range=">=vs-2022"

通过更改 Visual Studio 某些文件的位置，可以减少其在系统驱动器上的安装占用。 具体来说，下载缓存以及共享组件、工具和 SDK 可使用其他位置 。

::: moniker-end

::: moniker range="vs-2019"

通过更改 Visual Studio 某些文件的位置，可以减少其在系统驱动器上的安装占用。 具体来说，下载缓存、共享组件、SDK 和工具文件可使用不同位置。

::: moniker-end

::: moniker range="vs-2017"

**版本 15.7 中的新增功能**：通过更改 Visual Studio 某些文件的位置，可以减少其在系统驱动器上的安装占用。 具体来说，下载缓存、共享组件、SDK 和工具文件可使用不同位置。

::: moniker-end

::: moniker range=">=vs-2019"

   > [!NOTE]
   > 某些工具和 SDK 对于安装位置有不同规则。 即使选择另一位置，这些工具和 SDK 也会安装在系统驱动器上。

::: moniker-end

准备好开始了吗？ 操作方法如下。

::: moniker range="vs-2017"

1. 安装 Visual Studio 时，选择“安装位置”选项卡。

   ![显示 Visual Studio 安装程序的“安装位置”选项卡的屏幕截图。](media/vs-installation-locations.png "选择安装位置。")

1. 在“Visual Studio IDE”部分中，接受默认值。 Visual Studio 将安装核心产品并包含特定于此版本的 Visual Studio 的文件。

   ![Visual Studio 安装程序的“安装位置”选项卡的“Visual Studio IDE”部分的屏幕截图。](media/vs-installation-locations-ide.png "接受“安装位置”选项卡的“Visual Studio IDE”部分的默认值。")

   > [!TIP]
   > 如果系统驱动器是固态硬盘 (SSD)，建议你接受系统驱动器上的默认位置。 原因？ 当使用 Visual Studio 进行开发时，将从大量文件进行读取并写入大量文件，这会增加磁盘 I/O 活动。 最好选择最快的驱动器来处理负载。

1. 在“下载缓存”部分，决定是否保留下载缓存，然后决定其文件的存储位置。

     ![Visual Studio 安装程序的“安装位置”选项卡的“下载缓存”部分的屏幕截图。](media/vs-installation-locations-cache.png "选择安装完成后是否保留下载缓存，然后指定要存储文件的驱动器。")

    1. 选中或取消选中“安装完成后保留下载缓存”。

       如果决定不保留下载缓存，则仅临时使用该位置。 此操作不会影响或删除以前的安装内容。

    1. 指定在其中存储下载缓存中的安装文件和清单的驱动器。

        例如，如果选择“使用 C++ 的桌面开发”工作负载，系统驱动器上临时需要的大小为 1.58 GB，安装完成后即会释放。

       > [!IMPORTANT]
       > 该位置在首次安装时进行设置，并且之后无法从安装程序 UI 中更改。 相反，必须[使用命令行参数](use-command-line-parameters-to-install-visual-studio.md)删除下载缓存。

1. 在“共享组件、工具和 SDK”部分，指定要存储由 Visual Studio 并行安装所共享的文件的驱动器。 SDK 和工具也存储在此目录中。

   ![Visual Studio 安装程序的“安装位置”选项卡的“共享组件、工具和 SDK”部分的屏幕截图。](media/vs-installation-locations-shared.png "指定要存储共享组件、工具和 SDK 的位置。")

::: moniker-end

::: moniker range="vs-2019"

1. 安装 Visual Studio 时，选择“安装位置”选项卡。

   ![显示 Visual Studio 安装程序的“安装位置”选项卡的屏幕截图。](media/vs-2019/vs-installer-installation-locations.png "选择安装位置。")

1. 在“Visual Studio IDE”部分中，接受默认值。 Visual Studio 将安装核心产品并包含特定于此版本的 Visual Studio 的文件。

   > [!TIP]
   > 如果系统驱动器是固态硬盘 (SSD)，建议你接受系统驱动器上的默认位置。 原因？ 当使用 Visual Studio 进行开发时，将从大量文件进行读取并写入大量文件，这会增加磁盘 I/O 活动。 最好选择最快的驱动器来处理负载。

1. 在“下载缓存”部分，决定是否保留下载缓存，然后决定其文件的存储位置。

    * 选中或取消选中“安装完成后保留下载缓存”。

       如果决定不保留下载缓存，则仅临时使用该位置。 此操作不会影响或删除以前的安装内容。

    * 指定在其中存储下载缓存中的安装文件和清单的驱动器。

        例如，如果选择“使用 C++ 的桌面开发”工作负载，系统驱动器上临时需要的大小为 1.58 GB，安装完成后即会释放。

       > [!IMPORTANT]
       > 该位置在首次安装时进行设置，并且之后无法从安装程序 UI 中更改。 相反，必须[使用命令行参数](use-command-line-parameters-to-install-visual-studio.md)删除下载缓存。

1. 在“共享组件、工具和 SDK”部分中，请注意它使用在“下载缓存”部分中选择的同一驱动器。 Visual Studio 在\Microsoft\VisualStudio\Shared 目录中存储由并行 Visual Studio 安装共享的文件。 SDK 和工具也存储在此目录中。

::: moniker-end

::: moniker range=">=vs-2022"

1. 安装 Visual Studio 时，选择“安装位置”选项卡。

   :::image type="content" source="media/vs-2022/vs-installer-installation-locations-cplusplus-workload.png" border="false" alt-text="显示 Visual Studio 安装程序的“安装位置”选项卡的屏幕截图。":::

1. 在“Visual Studio IDE”部分中，接受默认路径。 Visual Studio 将安装核心产品并包含特定于此版本的 Visual Studio 的文件。

   > [!TIP]
   > 如果系统驱动器是固态硬盘 (SSD)，建议你将核心产品保留在系统驱动器上。 原因？ 当使用 Visual Studio 进行开发时，将从大量文件进行读取并写入大量文件，这会增加磁盘 I/O 活动。 最好选择最快的驱动器来处理负载。

   > [!IMPORTANT]
   > 仅当首次安装 Visual Studio 时，才可选择其他位置。 如果已安装 Visual Studio 并要更改位置，则必须先将其卸载然后再重新安装。

1. 在“下载缓存”部分，决定是否保留下载缓存，如果要保留，则决定其文件的存储位置。

    * 选中或取消选中“安装完成后保留下载缓存”。

      如果决定不保留下载缓存，则仅临时使用下载缓存位置。 此操作不会影响或删除以前的安装内容。

      例如，如果选择“使用 C++ 的桌面开发”工作负载，则下载缓存位置的临时所需大小为 2.11 GB。 一旦安装完成，下载的缓存文件会被删除，只留下包元数据。

    * 指定要在其中存储下载缓存中的安装文件和清单的文件夹路径（包括驱动器）。

   > [!IMPORTANT]
   > 仅当首次安装 Visual Studio 时，才可选择其他位置。 如果已安装 Visual Studio 并要更改位置，则必须先将其卸载然后再重新安装。

1. 在“共享组件、工具和 SDK”部分，选择要存储由 Visual Studio 并行安装所共享的文件的文件夹。 SDK 和工具也存储在此目录中。

   > [!IMPORTANT]
   > 如果你之前在计算机上安装了 Visual Studio，则无法更改共享组件、工具和 SDK 路径，它将显示为灰色。

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [安装 Visual Studio](install-visual-studio.md)
* [更新 Visual Studio](update-visual-studio.md)
* [修改 Visual Studio](update-visual-studio.md)
* [卸载 Visual Studio](uninstall-visual-studio.md)
