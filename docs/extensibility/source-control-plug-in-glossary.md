---
title: 源代码管理插件术语表|Microsoft Docs
description: 本文包含与源代码管理插件 SDK 文档相关的有用术语和定义。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- glossary [Visual Studio SDK]
- source control plug-ins, glossary
ms.assetid: f224bbc9-38fc-4c80-ab09-51dcc8969f8e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 45d4c946e78a611d7e4837366fbbf618f317c775d7d362f2807ccd40d084b1c9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121358943"
---
# <a name="source-control-plug-in-glossary"></a>源代码管理插件词汇表
以下有用的术语和定义与源代码管理插件 SDK 文档相关。

## <a name="definitions"></a>定义
 签入 当用户对工作副本进行更改时，用户必须将工作副本的更改发送到中央源代码管理存储库。 这将创建可供其他用户使用的文件的新修订版本。 此过程称为签入。

 签出 从存储库请求工作副本的行为，告知存储库你修改它的意图。 工作副本反映项目在签出时的状态。

 客户端 使用源代码管理系统的程序。 就本文档来说，它是 Visual Studio IDE。

 注释 描述用户在执行源代码管理操作时可附加到修订版本的更改的消息。

 冲突 当两个用户尝试签入对同一文件的同一区域所做的更改时的情况。 通常，必须执行合并。

 目录 客户端本地文件夹称为目录。 这是用户实际进行更改的副本。 给定项目可以有许多工作副本;通常，每个开发人员都有自己的副本。

 获取获取操作将用户的工作副本与存储库副本一起更新。 与结帐不同，当用户只需要最新副本但打算不进行更改时，将执行 get。

 历史记录 它通常是源代码管理存储库中完成的所有签出、签入、更新、标记和发布的摘要。

 IDE 通常是指Visual Studio开发环境。 但是，它还可以引用识别源代码管理插件 API 的其他客户端环境。

 合并 合并 合并两个或多个源代码文件的过程，以形成一个新文件，其中合并了以前文件的所有功能。 在两个或多个开发人员同时处理文件的版本控制中，此概念至关重要。

 Project源代码管理文件夹通常称为项目。 这与项目中的项目或解决方案没有任何Visual Studio。

 插件 通过实现源代码管理插件 API 提供源代码管理功能的 DLL。

 存储库 源代码管理系统存储项目的完整修订历史记录的主副本。 每个项目只有一个存储库。

 修订版 文件或一组文件的历史记录中已提交更改。 修订是持续更改项目中的一个快照。

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
