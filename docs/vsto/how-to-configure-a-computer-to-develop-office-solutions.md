---
title: 如何：将计算机配置为开发 Office 解决方案
description: 了解如何配置开发计算机，以便您可以在 Visual Studio 中使用 Microsoft Office 开发人员工具。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- prerequisites [Office development in Visual Studio]
- Office development in Visual Studio, installing tools
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: d5868a8a7e8eca8bf75436eed3c2bd17c4238b29
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664743"
---
# <a name="how-to-configure-a-computer-to-develop-office-solutions"></a>如何：将计算机配置为开发 Office 解决方案
  若要配置开发计算机以便可以使用 Visual Studio 中的 Microsoft Office 开发人员工具，请按照本主题中的说明进行操作。 必须在本地计算机上具有管理特权才能执行这些步骤。

### <a name="to-configure-the-development-computer"></a>配置开发计算机

1. 安装包括 Office 开发人员工具的 Visual Studio 版本。 默认安装 Office 开发人员工具。 如果通过选择要安装的功能来自定义 Visual Studio 安装，请确保在安装过程中选择 " **Microsoft Office" 开发人员工具**。 有关包含 Office 开发人员工具的 Visual Studio 版本的详细信息，请参阅[配置计算机以开发 Office 解决方案](../vsto/configuring-a-computer-to-develop-office-solutions.md)。

2. 安装 Visual Studio 中的 Office 开发人员工具支持的 Office 的版本。 有关详细信息，请参阅[配置计算机以开发 Office 解决方案](../vsto/configuring-a-computer-to-develop-office-solutions.md)。

     请确保也为安装的 Office 版本安装的 PIA。 默认情况下，PIA 随 Office 一起安装。 如果修改 Office 安装程序，请确保为你要以其为目标的应用程序选择 " **.net 可编程性支持**" 功能。

3. 如果你使用的是英语版本的 Visual Studio 但对 Windows 使用非英语设置，则可以安装 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 语言包以查看与 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] Windows 相同的消息。 Visual Studio 的非英语版本将自动安装该语言包。 可从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=54246)获取该语言包。

## <a name="see-also"></a>另请参阅

- [&#40;Visual Studio 中的 Office 开发入门&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [如何：安装 Visual Studio Tools for Office 运行时可再发行组件](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [如何：安装 Office 主互操作程序集](../vsto/how-to-install-office-primary-interop-assemblies.md)
