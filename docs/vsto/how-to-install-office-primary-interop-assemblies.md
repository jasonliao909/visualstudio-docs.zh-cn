---
title: 如何：安装 Office 主互操作程序集
description: 了解如何在安装 Office (pia) 安装 Microsoft Office 主互操作程序集。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- primary interop assemblies [Office development in Visual Studio], installing
- Office primary interop assemblies, installing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: d0a5ffcf0a7c9c3533eee85953b26d9341a537a2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122100018"
---
# <a name="how-to-install-office-primary-interop-assemblies"></a>如何：安装 Office 主互操作程序集
  当你安装 Office 时，安装 Microsoft Office 主互操作程序集 (PIA)。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="to-install-the-pias-when-you-install-office"></a>安装 Office 时安装 PIA

1. 确保具有不超过 2.0 版本的 .NET Framework。

2. 安装 Microsoft Office 并确保为要扩展的应用程序选择 " **.net 可编程性支持**" 功能 (此功能包含在默认的安装) 中。

    > [!WARNING]
    > 默认情况下，当你生成 pia 时，pia 嵌入到你的解决方案中，因此你不必将 pia 分发给用户作为使用 VSTO 外接程序或自定义项的先决条件。

## <a name="see-also"></a>请参阅
- [Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)
- [如何：通过主互操作程序集面向 Office 应用程序](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [如何：将计算机配置为开发 Office 解决方案](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [如何：安装 Visual Studio Tools for Office 运行时可再发行组件](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [Office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [&#40;Visual Studio 中的 Office 开发入门&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
