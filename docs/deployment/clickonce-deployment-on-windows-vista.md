---
title: ClickOnceWindows Vista 上的部署 |Microsoft Docs
description: 了解 Visual Studio 如何为需要外部清单的 ClickOnce 和 Registration-Free COM 应用程序生成外部 UAC 清单。
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
ms.openlocfilehash: 0da4733f77f9f4d2b896d93f4aba9ec6d05bcadd411f2d2269e2d67ff8e1f016
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121452987"
---
# <a name="clickonce-deployment-on-windows-vista"></a>Windows Vista 上的 ClickOnce 部署

在 Visual Studio 中为用户帐户控制生成应用程序 (Windows Vista 上的 UAC) 通常会生成在应用程序的可执行文件中编码为二进制 XML 数据的嵌入清单。  ClickOnce 和 Registration-Free COM 应用程序需要外部清单，因此 Visual Studio 会为包含 UAC 数据而不是嵌入清单的这些项目生成一个文件。 对于 ClickOnce 和 Registration-Free COM 部署，Visual Studio 使用名为 *app.config* 的文件中的信息生成外部 UAC 清单信息。 对于所有其他情况，Visual Studio 将 UAC 数据嵌入应用程序的可执行文件中。

Visual Studio 提供了以下清单生成选项：

- 使用嵌入的清单。 在应用程序的可执行文件中嵌入 UAC 数据，并以普通用户身份运行。

   这是默认设置，除非使用 ClickOnce)  (。 此设置支持 Visual Studio 在 Windows Vista 上运行的常见方式，并使用生成内部和外部清单 `AsInvoker` 。

- 使用外部清单。 使用 *app.config* 生成外部清单。

   仅通过使用 *app.config* 中的信息生成外部清单。 使用 ClickOnce 或 Registration-Free COM 发布应用程序时，Visual Studio 会将 *app.config* 添加到项目中，然后添加此选项。

- 不使用清单。 创建不带清单的应用程序。

   此方法也称为 *虚拟化*。 使用此选项与 Visual Studio 早期版本中的现有应用程序兼容。

  新属性在 "Project 设计器" 的 "**应用程序**" 页上提供 (仅适用于 Visual c # 项目) 和 MSBuild 项目文件格式。

  在 Visual Studio IDE 中配置 UAC 清单生成的方法有所不同，具体取决于 Visual c # 或 Visual Basic)  (项目类型。

  * 有关为生成清单配置 Visual c # 项目的信息，请参阅[应用程序页 Project 设计器 (c # ) ](../ide/reference/application-page-project-designer-csharp.md)。

  * 有关为清单生成配置 Visual Basic 项目的信息，请参阅[应用程序页 Project 设计器 (Visual Basic) ](../ide/reference/application-page-project-designer-visual-basic.md)。

## <a name="see-also"></a>请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [用户权限与 Visual Studio](/previous-versions/ms165100(v=vs.100))
- [“项目设计器”->“应用程序”页 (C#)](../ide/reference/application-page-project-designer-csharp.md)
- [“项目设计器”->“应用程序”页 (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)