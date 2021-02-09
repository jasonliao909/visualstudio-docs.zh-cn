---
title: VS Shell 部署
description: 了解如何使用独立 shell 来确定需要与 DSL 交互的 Visual Studio 功能以及应如何显示该解决方案。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1293593e71aa57d8e74b9035320b3da5108aba09
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99924224"
---
# <a name="vs-shell-deployment"></a>VS Shell 部署

使用独立 shell 可以确定需要与域特定语言交互的 Visual Studio 功能，以及该解决方案应如何显示。 有关 Visual Studio 独立 shell 的详细信息，请参阅 [自定义独立 shell](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)。

若要将 Visual Studio Shell 设置为部署目标：

1. 在 **DslPackage** 项目中，打开 **source.extension.tt**。

2. 在 `<SupportedProducts>` insert：

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   将 *MyIsolatedShell* 替换为你的独立 shell 包的名称。