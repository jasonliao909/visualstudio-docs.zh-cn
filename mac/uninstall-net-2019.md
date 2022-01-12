---
title: Apple Silicon 计算机上安装 Visual Studio for Mac 8.10 和 .NET
description: 在 M1 计算机上使受支持的 .NET 版本在 2019 年正常工作的步骤。
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 11/08/2021
ms.topic: how-to
ms.assetid: db2dc420-63d2-44ef-bdda-a351561dc900
ms.openlocfilehash: 3cfda970cbada8ac746603f2439028552bd08478
ms.sourcegitcommit: 965372ad0d75f015403c1af508080bf799914ce3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "135805554"
---
# <a name="visual-studio-for-mac-810-and-net-on-apple-silicon-machines"></a>Apple Silicon 计算机上安装 Visual Studio for Mac 8.10 和 .NET

在 Apple Silicon 计算机（也称为 M1 或 ARM）上，Visual Studio for Mac 8.10 目前不支持 11 月发布的 .NET 6、.NET 5 和 .NET Core 3.1 x64 SDK。 它还不支持 .NET 6 Arm64 SDK。 如果安装了其中任何一个，则它们将中断 Visual Studio for Mac 8.10，应卸载并安装较旧的 .NET SDK。 

> [!NOTE]
> 此信息特定于 Visual Studio for Mac 2019 (8.10.x) 版本。 有关 Visual Studio for Mac 2022 预览版此过程的信息，请参阅 [Apple Silicon 计算机上的 Visual Studio for Mac 17.0 和 .NET](/visualstudio/mac/uninstall-net-2022) 了解详细信息。

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

1. 安装 .NET 5 和 .NET Core 3.1 x64 SDK 的 10 月版本 
    - [.NET 5.0.402 x64 SDK](https://download.visualstudio.microsoft.com/download/pr/88bc1553-e90f-4a4f-9574-65d9a5065cd2/1d5646e1abb8b4d4a61ba0b0be976047/dotnet-sdk-5.0.402-osx-x64.pkg)
    - [.NET Core 3.1.414 x64 SDK](https://download.visualstudio.microsoft.com/download/pr/0517421d-3300-42c7-a420-e42d55068126/76b722e65c0745962156e622ed76501c/dotnet-sdk-3.1.414-osx-x64.pkg)
2. 重启 Visual Studio for Mac 以检测安装的新 SDK。 
