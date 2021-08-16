---
title: VS Shell 部署
description: 了解独立 shell 如何让你确定Visual Studio DSL 交互所需的功能，以及该解决方案的显示方式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: e8a9ab2f0cff7e405849c58ed4724f76ad7cd4e74050cda8767348d90fc3771f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121443823"
---
# <a name="vs-shell-deployment"></a>VS Shell 部署

使用独立的 shell，Visual Studio与域特定语言交互所需的特定功能以及该解决方案的显示方式。 有关独立 shell Visual Studio，请参阅[自定义独立 Shell。](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

若要将 Visual Studio Shell 设置为部署目标：：

1. 在 **DslPackage 项目中** ， **打开** source.extension.tt。

2. 在 `<SupportedProducts>` "插入"下：

   ```xml
   <IsolatedShell Version="1.0">MyIsolatedShell</IsolatedShell>
   ```

   将 *MyIsolatedShell* 替换为独立 shell 包的名称。