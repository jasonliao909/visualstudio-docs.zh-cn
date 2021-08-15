---
title: '非托管 API 参考 (Office开发Visual Studio) '
description: 非托管 API 引用用于帮助加载托管VSTO外接程序。还可通过实现此接口VSTO外接程序加载程序组件。
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
ms.openlocfilehash: 05a8e1bef15e9299c16fccb39705f45f810e1d8bcfb0b16f99aab9b82ae29708
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121226110"
---
# <a name="unmanaged-api-reference-office-development-in-visual-studio"></a>非托管 API 参考 (Office开发Visual Studio) 

从 2007 Microsoft Office 系统开始，Office 应用程序使用[IManagedAddin](../vsto/imanagedaddin-interface.md)接口接口调用 中包含的 VSTO 外接程序加载程序组件 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 此组件用于帮助加载托管VSTO外接程序。可以通过实现此接口VSTO外接程序加载程序组件。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="in-this-section"></a>本节内容

[IManagedAddin 接口](../vsto/imanagedaddin-interface.md)

一种 COM 接口，可以通过实现该接口来在 Office 应用程序中加载和卸载 VSTO 托管外接程序。
