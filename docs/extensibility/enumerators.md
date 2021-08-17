---
title: 枚举器 |Microsoft Docs
description: 了解源代码管理插件 API 中的枚举器数据类型，包括命令代码、消息、文件状态代码和目录状态代码。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, enumerators
ms.assetid: a60030c5-e1d1-47e1-84bb-cbfe838ab479
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 4451735a5fa5127614a385be3010f1ea4bf9ad01
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122070337"
---
# <a name="enumerators"></a>枚举器
本节列出源代码管理插件必须知道的源代码管理插件 API 中的枚举器数据类型。

## <a name="in-this-section"></a>本节内容
- [命令代码](../extensibility/command-code-enumerator.md) 枚举 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) 和 [SccPopulateList](../extensibility/sccpopulatelist-function.md) 函数的选项。

- [消息](../extensibility/message-enumerator.md) 枚举用于打印回调的标志 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)。

- [文件状态代码](../extensibility/file-status-code-enumerator.md) 包含指定源代码管理下的文件状态的命名常量值。

- [目录状态代码](../extensibility/directory-status-code-enumerator.md) 包含指定源代码管理下的目录状态的命名常量值。

## <a name="related-sections"></a>相关章节
- [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md) 定义源代码管理插件 SDK 并介绍所包含的资源。

- [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) 提示用户输入给定命令的高级选项。

- [SccPopulateList](../extensibility/sccpopulatelist-function.md) 检查文件列表的当前状态。 此外， `pfnPopulate` 如果文件与的条件不匹配，则使用函数通知调用方 `nCommand` 。

- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md) 描述 [SccOpenProject](../extensibility/sccopenproject-function.md) 用于通过 IDE 显示源代码管理插件消息的回调函数。

- [源代码管理插件](../extensibility/source-control-plug-ins.md) 提供源代码管理插件 API 中所有元素的完整列表。
