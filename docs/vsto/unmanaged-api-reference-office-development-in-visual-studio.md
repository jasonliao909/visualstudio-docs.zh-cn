---
title: Visual Studio) 中 (Office 开发的非托管 API 参考
description: 非托管 API 参考用于帮助加载 VSTO 加载项。还可以通过实现此接口来创建自己的 VSTO 外接程序加载程序组件。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 08/14/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, reference
- Office development in Visual Studio, unmanaged API reference
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 132c4ba7286ae04d7e9c64a1a6306fc14b2ea650
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122082733"
---
# <a name="unmanaged-api-reference-office-development-in-visual-studio"></a>Visual Studio) 中 (Office 开发的非托管 API 参考

从 2007 Microsoft Office 系统开始，Office 应用程序使用[IManagedAddin 接口](../vsto/imanagedaddin-interface.md)接口调用随附的 VSTO 外接程序加载程序组件 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 此组件用于帮助加载 VSTO 加载项。可以通过实现此接口来创建自己的 VSTO 外接程序加载程序组件。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="in-this-section"></a>本节内容

[IManagedAddin 接口](../vsto/imanagedaddin-interface.md)

一种 COM 接口，可以通过实现该接口来在 Office 应用程序中加载和卸载 VSTO 托管外接程序。
