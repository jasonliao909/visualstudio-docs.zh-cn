---
title: 为 64 位应用程序部署先决条件|Microsoft Docs
description: 了解可再发行组件，这些可再发行组件可用作ClickOnce 64 位平台上的应用程序部署的先决条件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [Visual Studio], 64-bit
- 64-bit [Visual Studio]
- 64-bit programming [Visual Studio]
- 64-bit applications [Visual Studio]
ms.assetid: 87399e20-5510-41e4-b5b7-4a87c5773f21
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 91209a76acc754a900bfc88d5d488f0b4729703121d1125abc9f25990ca1c9c9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121435553"
---
# <a name="deploy-prerequisites-for-64-bit-applications"></a>部署 64 位应用程序的系统必备
ClickOnce 部署支持 64 位平台上的应用程序安装。 目标平台为“x86”（32 位平台）、“x64”（支持 AMD64 和 EM64T 指令集的计算机）以及“Itanium”（64 位 Itanium 处理器）。

## <a name="prerequisites"></a>先决条件
 下表列出了可用作 64 位应用程序安装的系统必备组件的可再发行组件。

 如果选择不具有 64 位组件的系统必备组件，则可能会看到一条警告，该警告声明选择的程序包不能用于 64 位平台。

| 可再发行组件 | x64 支持 | IA64 支持 |
| - |-------------|--------------|
| [!INCLUDE[vsto_runtime](../deployment/includes/vsto_runtime_md.md)] | 是 | 否 |
| Visual C++ 2010 运行库 (IA64) | 否 | 是 |
| Visual C++ 2010 运行库 (x64) | 是 | 否 |
| Microsoft .NET Framework 4（x86 和 x64） | 是 | |
| Microsoft .NET Framework 4 Client Profil（x86 和 x64） | 是 | |

## <a name="see-also"></a>请参阅
- [部署应用程序、服务和组件](../deployment/deploying-applications-services-and-components.md)
- [如何：使用应用程序安装ClickOnce先决条件](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
- [64 位应用程序](/dotnet/framework/64-bit-apps)