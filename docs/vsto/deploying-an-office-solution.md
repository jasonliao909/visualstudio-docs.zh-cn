---
title: 部署Office解决方案
description: 可以使用 ClickOnce 或 Windows Installer 来部署 Office 解决方案。 通过使用ClickOnce，可以减少部署解决方案所需的步骤数。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ClickOnce deployment [Office development in Visual Studio], event viewer
- deploying applications [Office development in Visual Studio], event viewer
- Office applications [Office development in Visual Studio], deploying Office solutions
- Office development in Visual Studio, deploying Office solutions
- ClickOnce deployment [Office development in Visual Studio], troubleshooting
- deploying applications [Office development in Visual Studio], Office solutions (2007 system)
- Office development in Visual Studio, troubleshooting
- Office development in Visual Studio, event viewer
- ClickOnce deployment [Office development in Visual Studio], about ClickOnce solution deployments
- Office solutions [Office development in Visual Studio], deploying
- deploying applications [Office development in Visual Studio], troubleshooting
- solutions [Office development in Visual Studio], deploying Office solutions (2007 system)
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 2345e66ac6d13e4110db7b660d227963bf7abae1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122130671"
---
# <a name="deploy-an-office-solution"></a>部署Office解决方案
  可以使用 ClickOnce 或 Windows Installer 来部署 Office 解决方案。 通过使用 ClickOnce，可以减少部署和更新解决方案所需的步骤数。 如果使用 Windows Installer，可以控制解决方案的安装方式，以及在用户安装解决方案时，安装程序显示的页。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="deploy-a-solution-by-using-clickonce"></a>使用解决方案部署ClickOnce
 使用 ClickOnce 部署解决方案时，可将其发布到一个中心位置，用户能够从中安装并运行解决方案。 可以更新解决方案，而无需将新的安装程序分发给用户。  此部署选项更简单，但无法显示用户自定义安装页。 此外，必须在包含多个用户的任何计算机上多次安装解决方案。 请参阅[使用 Office 部署 ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md)解决方案。

## <a name="deploy-a-solution-by-using-windows-installer"></a>使用安装程序部署Windows解决方案
 使用 Windows Installer 部署解决方案时，可将安装程序分发给用户，用户将使用此程序安装解决方案。 安装程序可以同时为一台计算机上的所有用户安装解决方案，而非仅当前用户。 还可以更好地控制在用户安装解决方案时显示给用户的选项。 例如，可以显示许可协议或者使用户安装解决方案的特定组件。 不过，如果更新解决方案，必须分发一个新的安装程序。 请参阅[使用 Office 安装程序 部署Windows解决方案](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)。

## <a name="see-also"></a>请参阅
- [安全Office解决方案](../vsto/securing-office-solutions.md)
- [使用 Office 部署 ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md)
- [使用 Office 安装程序部署 Windows 解决方案](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md)
- [解决方案Office疑难解答](../vsto/troubleshooting-office-solution-deployment.md)
