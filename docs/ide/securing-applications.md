---
title: 安全
description: 了解一些安全概念以及有助于有效开发安全应用程序的安全功能。
ms.custom: SEO-VS-2020
ms.date: 06/01/2018
ms.topic: conceptual
helpviewer_keywords:
- security [Visual Studio], applications
- application design, securability
ms.assetid: 7d32c4cf-8bec-4307-a2a8-42f0ceddf3eb
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: d95b640fc6daae8c9fe6734ab6cec5c73f96cd1c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641105"
---
# <a name="secure-applications"></a>安全应用程序

你应该考虑应用程序开发的所有环节（从设计到部署）的安全性。 从尽可能安全地运行 Visual Studio 开始。 请参阅[用户权限](../ide/user-permissions-and-visual-studio.md)。

若要高效地开发安全的应用程序，应对安全概念和开发所针对的平台的安全特性有基本的了解。 你还应对安全编码技术有所了解。

## <a name="code-for-security"></a>代码安全性

导致安全漏洞的大多数编码错误都是由于开发人员在处理用户输入时所做的假定错误，或者是由于他们对开发平台了解不够充分。

- [安全编码准则](/dotnet/standard/security/secure-coding-guidelines)介绍设计 .NET 代码来处理安全系统的不同方式。
- [C++ 安全性最佳做法](/cpp/top/security-best-practices-for-cpp)包含适用于 C++ 开发人员的安全工具和做法相关信息。

## <a name="build-for-security"></a>生成安全性

安全性也是生成过程中的一个重要考虑因素。 一些额外步骤可以提高所部署应用的安全性，并帮助防止未经授权的反向工程、欺骗或其他攻击：

- [Dotfuscator](dotfuscator/index.md) 免费提供，有助于防止 .NET 程序集遭受反向工程和未经授权的使用，如未经授权的调试。
- [强名称签名](managing-assembly-and-manifest-signing.md)可用于唯一标识软件组件，从而防止名称欺骗。

## <a name="see-also"></a>另请参阅

- [.NET 中的安全性](/dotnet/standard/security/index)
- [Azure 安全性](/azure/security/)
- [Windows 10 移动版安全指南](/windows/security/threat-protection/windows-10-mobile-security-guide)
- [Apache Cordova 平台安全功能](/previous-versions/visualstudio/cross-platform/tools-for-cordova/security/best-practices?view=toolsforcordova-2017&preserve-view=true)
- [ASP.NET Core 安全](/aspnet/core/security/?view=aspnetcore-2.1&preserve-view=true)
- [Windows 窗体安全](/dotnet/framework/winforms/windows-forms-security)
