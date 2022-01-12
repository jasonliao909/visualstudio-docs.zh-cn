---
title: Apple Silicon 计算机上的 Visual Studio for Mac 17.0 和 .NET
description: 在 M1 计算机上使受支持的 .NET 版本在 2022 年正常工作的步骤。
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 11/08/2021
ms.topic: how-to
ms.assetid: 18f722bc-3d9d-4c75-9e77-d66b64784c8d
ms.openlocfilehash: 941169c00a16d9228cde128c59967c35fb1fdceb
ms.sourcegitcommit: 965372ad0d75f015403c1af508080bf799914ce3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "135804592"
---
# <a name="visual-studio-for-mac-170-previews-and-net-on-apple-silicon-machines"></a>Apple Silicon 计算机上的 Visual Studio for Mac 17.0 预览版和 .NET

在安装了旧版 x64 SDK 的 Apple Silicon 计算机上（也称为 M1 或 ARM），需要删除所有现有的 .NET 安装才能使用 .NET 6 GA Arm64 SDK。  

> [!NOTE]
> 此信息特定于 Visual Studio for Mac 2022 Preview (17.0) 版本。 有关 Visual Studio for Mac 2019 版此过程的信息，请参阅 [Apple Silicon 计算机上的 Visual Studio for Mac 8.10 和 .NET](/visualstudio/mac/uninstall-net-2019) 了解详细信息。

## <a name="uninstall-net-from-your-machine"></a>从计算机中卸载 .NET： 

1. 通过右键单击该脚本并选择“另存为”将文件保存到 Mac，从 .NET GitHub 存储库下载[卸载脚本](https://github.com/dotnet/sdk/blob/main/scripts/obtain/uninstall/dotnet-uninstall-pkgs.sh)。
2. 打开“终端”，并将工作目录更改为下载脚本的位置：
 
    ```bash
    cd /location/of/file
    ```
3. 使脚本可执行，并通过 sudo 运行：

    ```bash
    chmod +x dotnet-uninstall-pkgs.sh 
    sudo ./dotnet-uninstall-pkgs.sh
    sudo rm -r /etc/dotnet
    ```  

## <a name="install-supported-net-sdks"></a>安装支持的 .NET SDK

1. [安装 .NET 6 Arm64 SDK](https://download.visualstudio.microsoft.com/download/pr/ed60d37e-7842-4fc2-8250-2bd66073d79e/725d486e04d27e45d2b41c687dc35f49/dotnet-sdk-6.0.100-osx-arm64.pkg)
2. 重启 Visual Studio for Mac 以检测安装的新 SDK。 
