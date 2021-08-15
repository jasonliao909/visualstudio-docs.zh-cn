---
title: 如何：安装Office互操作程序集
description: 了解如何在安装 Microsoft Office时 (PIA) 主互操作Office。
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
ms.openlocfilehash: 503a4430c144f97de1865a3d89975a7478567a36666085794c4acdd712cc05c5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121440820"
---
# <a name="how-to-install-office-primary-interop-assemblies"></a>如何：安装Office互操作程序集
  当你安装 Office 时，安装 Microsoft Office 主互操作程序集 (PIA)。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="to-install-the-pias-when-you-install-office"></a>安装 Office 时安装 PIA

1. 确保具有不超过 2.0 版本的 .NET Framework。

2. 安装Microsoft Office，并确保为要扩展的应用程序选择了 **.NET** 可编程性支持功能 (此功能包含在默认安装) 。

    > [!WARNING]
    > 默认情况下，PIA 在生成解决方案时嵌入在解决方案中，因此，不必将 PIA 分发给用户，作为使用 VSTO 外接程序或自定义项的先决条件。

## <a name="see-also"></a>另请参阅
- [Office主互操作程序集](../vsto/office-primary-interop-assemblies.md)
- [如何：通过Office程序集面向应用程序](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [如何：配置计算机以开发Office解决方案](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [如何：安装Visual Studio Tools for Office可再发行组件](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [Office解决方案开发概述&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [开始&#40;Office开发Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
