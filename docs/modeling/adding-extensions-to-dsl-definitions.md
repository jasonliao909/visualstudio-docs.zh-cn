---
title: 向 DSL 定义中添加扩展
description: 了解如何使用 DSL 定义扩展创建特定于域的语言的扩展包， (DSL) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 0f463ae8a71ac3c06e4efbcc7396dbe8b1483dba
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122157626"
---
# <a name="add-extensions-to-dsl-definitions"></a>向 DSL 定义中添加扩展

DSL 定义扩展允许你创建特定于域的语言的扩展包， (DSL) 。 DSL 扩展（包含在 VISUAL STUDIO Integration Extension (VSIX) 中）可以与 DSL 相同的方式安装在用户的计算机上。 可以在运行时动态启用和禁用其他功能。 无需为扩展显式设计 DSL，扩展可以在以后设计，也可以由第三方设计，而无需更改扩展 DSL。

DSL 扩展可以包含以下功能：

- 模型和演示元素的属性

- 形状和连接器的修饰器

- 类、关系、形状和连接器

- 验证约束

- 工具箱项和选项卡

扩展 DSL 的用户可以创建并保存包含其他功能实例的模型。 已安装相应扩展的其他用户可以读取该模型。 未安装扩展的用户无法使用其他功能，但他们可以更新和保存模型，而不会丢失其他功能。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>请参阅

- [相关的博客文章](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)
