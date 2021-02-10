---
title: “生成参数”重构
description: 了解如何使用“快速操作和重构”菜单自动生成方法参数。
ms.custom: SEO-VS-2020
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 33e2be19e3a5a83d89e722aa0c1a1154c8196939
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99968029"
---
# <a name="generate-parameter"></a>生成参数

此重构适用于：

- C#

- Visual Basic

**功能：** 自动生成方法参数。

**使用时机：** 在方法中引用当前上下文中不存在的变量，并收到错误；可以生成参数，来修复代码。 

操作原因：可以在不丢失上下文的前提下快速修改方法签名。

## <a name="how-to"></a>操作说明

1. 请将光标置于变量名称，并按“Ctrl+” 。 触发“快速操作和重构”  菜单。
1. 选择“生成参数”。

   ![生成参数](media/generate-parameter.png) 

## <a name="see-also"></a>另请参阅

- [重构](../refactoring-in-visual-studio.md)
