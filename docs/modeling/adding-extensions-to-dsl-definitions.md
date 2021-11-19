---
title: 向 DSL 定义中添加扩展
description: 了解如何使用 DSL 定义扩展来创建一个针对域特定语言 (DSL) 的扩展包。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666189"
---
# <a name="add-extensions-to-dsl-definitions"></a>向 DSL 定义中添加扩展

使用 DSL 定义扩展，可创建一个针对域特定语言 (DSL) 的扩展包。 DSL 扩展包含在 Visual Studio 集成扩展 (VSIX) 中，可采用与 DSL 相同的方式安装在用户的计算机上。 在运行时可动态启用和禁用附加功能。 DSL 不必针对扩展而进行显式设计，扩展可在之后设计，也可以由第三方设计，而无需更改扩展 DSL。

DSL 扩展可包含以下功能：

- “模型”和“表示”元素的属性

- 形状和连接符的修饰器

- 类、关系、形状和连接符

- 验证约束

- 工具箱项和选项卡

扩展 DSL 的用户可创建和保存包含附加功能实例的模型。 其他已安装适当扩展的用户可读取该模型。 尚未安装扩展的用户不能使用附加功能，但可在不丢失附加功能的情况下更新和保存模型。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>另请参阅

- [相关的博客文章](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)
