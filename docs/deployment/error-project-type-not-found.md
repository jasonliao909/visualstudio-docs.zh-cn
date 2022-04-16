---
title: '错误：在安装程序 (Windows找不到项目类型，ClickOnce) '
description: 解决无法加载Windows安装程序或ClickOnce项目时出现以下错误消息：找不到此项目类型的应用程序。
ms.date: 04/11/2022
ms.topic: error-reference
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- error, deployment
- deployment error
- application not found
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: c151d82cd6ff3caa6577bd5f7377d977a9e61881
ms.sourcegitcommit: d4b6b9ecdceffcb12fddeac8e02273b3a3c30521
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2022
ms.locfileid: "142643522"
---
# <a name="error-the-application-which-this-project-type-is-based-on-was-not-found-windows-installer-or-clickonce"></a>错误：找不到此项目类型基于的应用程序， (Windows安装程序或ClickOnce) 

尝试加载ClickOnce或Windows安装程序项目时，可能会收到此错误： ```<path to project file>: The application which this project type is based on was not found. Please try this link for further information: <link>```

此消息指示项目要求未为Visual Studio版本安装组件。

## <a name="to-correct-this-error"></a>更正此错误

- 确保为项目类型安装所需的Visual Studio工作负荷。 选择 **ToolsGet** >  **工具和功能** 以打开Visual Studio 安装程序。 对于 Windows Installer 或 ClickOnce，工作负荷是使用 C++ 进行 .NET 桌面开发或桌面开发。

- 对于 Windows Installer 项目，可能需要安装 [Visual Studio 安装程序 Projects 扩展](../deployment/installer-projects-net-core.md)。

- 如果项目是使用 Flexera Software 的 InstallShield 创建的，则可能需要修复安装， (升级Visual Studio) 后可能会发生这种情况。

- 安装所需的组件后，关闭并重新打开Visual Studio，然后重新加载项目。

## <a name="see-also"></a>另请参阅

[Visual Studio](../deployment/deploying-applications-services-and-components.md)
[创建安装程序包](../deployment/deploying-applications-services-and-components.md#create-an-installer-package-windows-desktop)中的部署