---
title: Apple Silicon 计算机上安装 Visual Studio for Mac 8.10 和 .NET
description: 在 M1 计算机上使受支持的 .NET 版本在 2019 年正常工作的步骤。
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 11/08/2021
ms.topic: how-to
ms.assetid: db2dc420-63d2-44ef-bdda-a351561dc900
ms.openlocfilehash: 9adf8620ffcea870f3f8f7e835d93fba44ddf4f6
ms.sourcegitcommit: fcf47a9c356df7e9636bcab92186923e5c9b8892
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2022
ms.locfileid: "144495776"
---
# <a name="visual-studio-for-mac-810-and-net-on-apple-silicon-machines"></a>Apple Silicon 计算机上安装 Visual Studio for Mac 8.10 和 .NET

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

在 Apple Silicon 计算机上， (也称为 M1 或 ARM) ，Visual Studio for Mac 8.10 不支持 .NET 6 Arm64 SDK。 支持 .NET 5 和 .NET Core 3.1 x64 SDK。 生成项目需要 .NET 6 x64 SDK，因为不支持在 Apple Silicon 计算机上生成 .NET 5 x64 和 .NET Core 3.1 x64 SDK。

Visual Studio for Mac 8.10 不支持 .NET 6，因为编辑器不支持 C# 10。 因此，创建新项目时，“新建Project”对话框不会将 .NET 6.0 显示为选项。

最新的 Visual Studio for Mac 8.10 版本会在检查更新时检测到不支持的 .NET 安装，并在安装支持的 .NET SDK 之前提供删除它。

> [!NOTE]
> 此信息特定于 Visual Studio for Mac 2019 (8.10.x) 版本。 有关 Visual Studio for Mac 2022 预览版此过程的信息，请参阅 [Apple Silicon 计算机上的 Visual Studio for Mac 17.0 和 .NET](/visualstudio/mac/uninstall-net-2022) 了解详细信息。

