---
title: VS Shell 部署
description: 了解如何使用独立 Shell 确定与 DSL 交互的所需 Visual Studio 功能，以及应如何显示该解决方案。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: c521e68f8e26d636cfccaccc607c4a03a2d5b714
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665497"
---
# <a name="vs-shell-deployment"></a>VS Shell 部署

使用独立 Shell 可确定与域特定语言交互的所需 Visual Studio 功能，以及应如何显示该解决方案。 有关 Visual Studio 独立 Shell 的详细信息，请参阅[自定义独立 Shell](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)。

将 Visual Studio Shell 设置为部署目标：

1. 在“DslPackage”项目中，打开“source.extension.tt” 。

2. 在 `<SupportedProducts>` 下，插入：

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   将“MyIsolatedShell”替换为你的独立 Shell 包的名称。