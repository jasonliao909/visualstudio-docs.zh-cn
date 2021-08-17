---
title: ClickOnce在 Windows Vista |Microsoft Docs
description: 了解如何Visual Studio为需要外部清单的 ClickOnce Registration-Free COM 应用程序生成外部 UAC 清单。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122104967"
---
# <a name="clickonce-deployment-on-windows-vista"></a>Windows Vista 上的 ClickOnce 部署

在 Visual Studio For User Account Control (UAC) on Windows Vista 上生成应用程序通常生成嵌入的清单，在应用程序的可执行文件中编码为二进制 XML 数据。  ClickOnce COM Registration-Free应用程序需要外部清单，因此Visual Studio为包含 UAC 数据（而不是嵌入清单）的这些项目生成文件。 对于ClickOnce COM Registration-Free，Visual Studio *app.manifest* 文件中的信息生成外部 UAC 清单信息。 对于所有其他情况，Visual Studio将 UAC 数据嵌入应用程序的可执行文件中。

Visual Studio为清单生成提供以下选项：

- 使用嵌入的清单。 在应用程序的可执行文件中嵌入 UAC 数据，并作为普通用户运行。

   这是默认设置 (，除非使用ClickOnce) 。 此设置支持在 Vista Visual Studio操作的常用Windows，同时使用 生成内部和外部清单 `AsInvoker` 。

- 使用外部清单。 使用 *app.manifest 生成外部清单*。

   这会使用 *app.manifest* 中的信息仅生成外部清单。 使用 ClickOnce 或 Registration-Free COM 发布Visual Studio时，Visual Studio *app.manifest* 添加到项目，然后添加此选项。

- 不使用清单。 创建不带清单的应用程序。

   此方法 *也称为虚拟化*。 使用此选项可以与早期版本的 Visual Studio 中的现有应用程序兼容。

  新属性仅在 Visual C# Project 设计器 (的"应用程序"页上) ，MSBuild文件格式提供。 

  在 IDE 中配置 UAC 清单生成的方法Visual Studio Visual C# 或 (项目Visual Basic) 。

  * 有关配置 Visual C# 项目以生成清单的信息，请参阅应用程序页，Project[设计器 (C#) 。 ](../ide/reference/application-page-project-designer-csharp.md)

  * 有关为清单生成配置Visual Basic的信息，请参阅应用程序页，Project[设计器 (Visual Basic) 。 ](../ide/reference/application-page-project-designer-visual-basic.md)

## <a name="see-also"></a>请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [用户权限与 Visual Studio](/previous-versions/ms165100(v=vs.100))
- [“项目设计器”->“应用程序”页 (C#)](../ide/reference/application-page-project-designer-csharp.md)
- [“项目设计器”->“应用程序”页 (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)