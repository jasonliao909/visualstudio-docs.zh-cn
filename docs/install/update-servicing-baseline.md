---
title: 在维修基线上更新 Visual Studio
description: 了解如何配置和更新 Visual Studio 以保持在维护服务基线上。
ms.date: 2/4/2022
ms.topic: conceptual
ms.assetid: ''
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
monikerRange: '>=vs-2019'
ms.openlocfilehash: 4005893e17dfd81db2fcc23b05e0a03ea02fae2f
ms.sourcegitcommit: b9c5ca58f380ee102153b69656cb062b3d2dab8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/10/2022
ms.locfileid: "138427877"
---
# <a name="visual-studio-and-servicing-baselines"></a>Visual Studio 和维护基线

在产品生命周期内经常更新 Visual Studio。 有两种主要类型的更新：功能更新和服务更新。 功能更新通过次版本号的更改来指示，如16.4 到16.5，它们包含重要的产品更新。 服务更新由重要的质量或安全修补程序组成，它们通过服务版本号的更改（例如16.7.8 到16.7.9）来表示。 

维护基准（也称为 Long-Term 服务通道 (LTSC) 是受支持的特定次要版本，与其他次要版本相比，该版本的年份比其他次要版本长。 维护基准的目的是为 Enterprise 和 Professional 客户提供一种方式来采用和保持非常稳定的产品，并在安全的同时最大限度地降低兼容性风险。 有关支持安全基线的信息，请参阅[Visual Studio 支持生命周期](/visualstudio/productinfo/vs-servicing)文档。

## <a name="how-to-configure-your-client-machine-to-stay-on-a-servicing-baseline"></a>如何将客户端计算机配置为保留在服务基线上

在 Visual Studio 2019 中，保留服务基线是一项挑战。 必须使用[My.VisualStudio.Com](https://my.visualstudio.com/Downloads)或[Visual Studio 2019 发行历史记录页](/visualstudio/releases/2019/history)上提供的特定次要版本引导程序，以使用所需的特定版本更新客户端或布局。 有时还需要执行其他自定义来微调体验。  

在 Visual Studio 2022 中，我们大大提高了将客户端计算机配置为保持维护服务基准的体验。 你现在可以使用 Visual Studio 2022 安装程序，它也可以由较旧版本的 Visual Studio （如 Visual Studio 2019）使用，你现在可以使用 "**更新设置**" 对话框或 `modifySettings` 命令 [配置你的客户端将从何处获取其更新](/visualstudio/install/update-visual-studio?view=vs-2022&preserve-view=true#configure-source-location-of-updates-1)。 这些更新源位置被称为“通道“，你可以在[Visual Studio 发行节奏](/visualstudio/productinfo/release-rhythm)文档中找到更多关于通道目的和可用性的信息。 Microsoft 使当前用户和预览频道均可供所有人使用，Long-Term 维护渠道 (LTSCs) 可供 Enterprise 和 Professional 客户使用。 IT 管理员还可以配置网络布局作为客户端可以访问的有效更新源位置。 

在这种情况下，"更新源位置" 和相应的 "通知" 标志由客户端的 `--channelUri` 值控制。 
   - 对于附加到网络布局的客户端计算机，此值通常通过布局的自定义响应 json 文件中的 `channelUri` 值传入。 有关详细信息，请参阅 [从网络布局安装时配置客户端默认值](/visualstudio/install/create-a-network-installation-of-visual-studio?#configure-initial-client-installation-defaults-for-this-layout)。
   - 对于使用 internet 上的引导程序安装了该产品的客户端计算机，你可以通过以下方式来禁用更新通知，以及从 internet 更新 Visual Studio 的功能，方法是在最初安装该产品时 (示例) 。 此方法将阻止你接收有关安全更新的通知，因此，在可能的情况下，我们不建议你这样做。
   
```shell
vs_enterprise.exe --channelUri c:\doesnotexist.chman
```

## <a name="how-to-stay-on-a-servicing-baseline"></a>如何访问维护基线

若提供了维护基线更新，[My.VisualStudio.com](https://my.visualstudio.com/Downloads?q=visual%20studio%202019%20version%2016.0) 将向该维护更新提供不可编辑版本的引导程序文件。

对于使用网络布局安装进行部署的管理员，管理员应更新[布局位置](create-a-network-installation-of-visual-studio.md#update-or-modify-your-layout)。 从该位置安装的客户端将收到更新通知。 如果必须将更新部署到客户端，请按照[这些说明](update-a-network-installation-of-visual-studio.md)操作。 通过修改“response.json”来获取更新时，请不要添加其他工作负载、组件或语言。 更新产品后，必须以“修改”部署的形式管理这些设置。

对于基于 Internet 的安装，请在客户端上使用指向不存在的通道清单的 `--channelUri` 参数运行新的不可编辑版本的引导程序。 若使用安静或被动模式部署更新，请使用下面的两个独立的命令：

1. 更新 Visual Studio 安装程序：

    ```shell
    vs_enterprise.exe --quiet --update
    ```

::: moniker range="vs-2019"
 
2. 更新 Visual Studio 应用程序本身：
    ```shell
    vs_enterprise.exe update --installPath "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" --quiet --wait --norestart --channelUri c:\doesnotexist.chman
    ```

::: moniker-end

::: moniker range=">=vs-2022"

2. 更新 Visual Studio 应用程序本身：
    ```shell
    vs_enterprise.exe update --installPath "C:\Program Files\Microsoft Visual Studio\2022\Enterprise" --quiet --wait --norestart --channelUri c:\doesnotexist.chman
    ```

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>另请参阅

* [安装 Visual Studio](install-visual-studio.md)
* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [用于检测和管理 Visual Studio 实例的工具](tools-for-managing-visual-studio-instances.md)
* [如何在响应文件中定义设置](automated-installation-with-response-file.md)
* [控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)
* [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing/)
