---
title: .NET Core 支持
description: 本文档介绍了 Visual Studio for Mac 中的 .NET Core 版本支持
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 05/02/2022
ms.custom: devdivchpfy22
ms.assetid: 8B8CEBE8-00DA-4AD1-8193-77F58B57F244
ms.openlocfilehash: 7900505772a5e10666db48237e5a24a321349530
ms.sourcegitcommit: 3034382894e610b55f3ad07e737fa59b91680869
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2022
ms.locfileid: "144547807"
---
# <a name="supported-versions-of-net"></a>支持的 .NET 版本

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

下表说明了 Visual Studio for Mac 稳定版和预览版支持的 .NET Core 版本：

| .NET Core SDK 版本 |Visual Studio for Mac 8.1 | Visual Studio for Mac 8.2 | Visual Studio for Mac 8.3 | Visual Studio for Mac 8.4 | Visual Studio for Mac 8.5 | Visual Studio for Mac 8.6 | Visual Studio for Mac 8.7 | Visual Studio for Mac 8.8 | Visual Studio for Mac 8.9 | Visual Studio for Mac 8.10 |
|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|---------|
|v2.1.0 - v2.1.5xx | | | | | | | | | | |
|v2.1.600 + |✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|
|v2.2.1 - v2.2.1xx | | | | | | | | | | |
|v2.2.200 + |✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|
|v3.0 | | |✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|
|v3.1 | | | |✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|✔︎|
|v5.0 | | | | | |✔︎|✔︎|✔︎|✔︎|✔︎|

> [!IMPORTANT]
> 不支持 .NET Core SDK 的预览版；请更新到已发布版本。 安装 Visual Studio for Mac 8.4 时，将安装 .NET Core v3.1 的已发布版本。

> [!IMPORTANT]
> 如果之前将 .NET Core v2.2.1xx 与 Visual Studio for Mac 8.0 配合使用，则需要手动更新到上表所列的受支持的 .NET Core 版本。 建议使用 [2.1.700](https://dotnet.microsoft.com/download/dotnet-core/2.1) 或 [2.2.300](https://dotnet.microsoft.com/download/dotnet-core/2.2) 版本

* 默认情况下，将为 8.4、8.5 和 8.6 安装 .NET Core v3.1。
* 默认情况下，将为 8.3 安装 .NET Core v3.0。
* 默认为使用安装程序安装 .NET Core v2.1.701（对于 8.1，则默认安装 v2.1.700）。
* 若要访问任何其他 .NET Core 版本，请访问 [dotnet 页面](https://dotnet.microsoft.com/download/dotnet-core)。
* 使用 .NET Core 3.0 时，默认情况下将使用 C# 版本 8。 使用 .NET Core 2.x 时，默认情况下使用 C# 7.3。 请参阅 [C# 语言版本控制](/dotnet/csharp/language-reference/configure-language-version)了解更多信息。
* 有关如何安装 Visual Studio for Mac 预览版的信息，请参阅[安装预览版](./install-preview.md)指南。