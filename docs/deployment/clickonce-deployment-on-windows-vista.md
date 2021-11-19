---
title: Windows Vista 上的 ClickOnce 部署 | Microsoft Docs
description: 了解 Visual Studio 如何为需要外部清单的 ClickOnce 和免注册 COM 应用程序生成外部 UAC 清单。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- UAC manifest generation
- ClickOnce deployment, Windows
- manifest generation
- Windows, ClickOnce deployment
ms.assetid: b21a0ebc-0ff6-4f49-8993-7d1ad3f8cac2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: f4b19059170e0c296cc7544bc62545691756b8a3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665885"
---
# <a name="clickonce-deployment-on-windows-vista"></a>Windows Vista 上的 ClickOnce 部署

在 Windows Vista 上的用户帐户控制 (UAC) Visual Studio 中生成应用程序通常生成嵌入式清单，它在应用程序的可执行文件中编码为二进制 XML 数据。  ClickOnce 和免注册 COM 应用程序需要外部清单，因此 Visual Studio 为那些包含 UAC 数据的项目生成文件，而不是嵌入式清单。 对于 ClickOnce 和免注册 COM 部署，Visual Studio 使用名为 app.manifest 的文件中的信息生成外部 UAC 清单信息。 对于所有其他情况，Visual Studio 将 UAC 数据嵌入到应用程序的可执行文件中。

Visual Studio 为清单生成提供以下选项：

- 使用嵌入式清单。 在应用程序的可执行文件中嵌入 UAC 数据，并以普通用户身份运行。

   这是默认设置（除非使用 ClickOnce）。 此设置支持 Visual Studio 在 Windows Vista 上的常见运行方式，同时使用 `AsInvoker` 生成内部和外部清单。

- 使用外部清单。 使用 app.manifest 生成外部清单。

   这会使用 app.manifest 中的信息仅生成外部清单。 使用 ClickOnce 或免注册 COM 发布应用程序时，Visual Studio 会向项目添加 app.manifest，然后添加此选项。

- 使用清单。 创建不带清单的应用程序。

   此方法也称为“虚拟化”。 使用此选项可以与早期版本的 Visual Studio 中的现有应用程序兼容。

  新属性可以在项目设计器的“应用程序”页面（仅针对 Visual C# 项目）获得，采用 MSBuild 项目文件格式。

  在 Visual Studio IDE 中配置 UAC 清单生成的方法因项目类型（Visual C# 或 Visual Basic）而异。

  * 有关配置 Visual C# 项目以生成清单的信息，请参阅[应用程序页，项目设计器 (C#)](../ide/reference/application-page-project-designer-csharp.md)。

  * 有关为清单生成配置 Visual Basic 项目的信息，请参阅[应用程序页，项目设计器 (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)。

## <a name="see-also"></a>另请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [用户权限与 Visual Studio](/previous-versions/ms165100(v=vs.100))
- [“项目设计器”->“应用程序”页 (C#)](../ide/reference/application-page-project-designer-csharp.md)
- [“项目设计器”->“应用程序”页 (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)