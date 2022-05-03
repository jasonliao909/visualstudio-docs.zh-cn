---
title: 版本控制
description: 使用 Visual Studio for Mac 中的 Git 和 Subversion。
ms.topic: overview
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 05/06/2018
ms.assetid: 49917483-28AA-4598-A847-71F1F2E0DCB5
ms.openlocfilehash: 3fb6855e3d954cb615e23959573c9b7bec19cb09
ms.sourcegitcommit: fcf47a9c356df7e9636bcab92186923e5c9b8892
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2022
ms.locfileid: "144477408"
---
# <a name="version-control"></a>版本控制

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

版本控制系统用于管理各种不同版本中的文件，在软件开发中常常由多位开发者贡献。 任何版本控制系统 (VCS) 的主要目的都是找出一种解决方案，使所有用户都可同时对基本代码进行操作。

而任何版本控制系统的核心都是存储库，它可充当所有不同文件的中央数据存储，与文件服务器类似。 但又不同于文件服务器，存储库包含项目的整个历史记录和所做的所有修订。

如果存储库是中央数据存储，那么每个用户都具备一个可在其上操作的本地数据存储是完全合理的。 这被称为“工作副本”。 在 Visual Studio for Mac 中，工作副本将显示在计算机上，就像任何其他本地目录一样，使用户可以从任意文件读取数据或将数据写入这些文件。 但由于 Visual Studio for Mac 具有版本控制系统集成，因此可使用 Subversion 和 Git 而无需离开 IDE。

Subversion 是一个集中式版本控制系统，这表示，有一个服务器包含所有文件和修订，用户可从中签出任何文件的任何版本。 从远程 Subversion 存储库中签出文件时，用户将收到该时间点的存储库快照。

Git 是分布式版本控制系统，使团队可以同时在同一文档上工作。 使用 Git，可能有一个单一服务器包含所有文件，但从此中央源中签出存储库时，整个存储库都会被克隆到本地计算机。

## <a name="basic-concepts"></a>基本概念

Visual Studio for Mac 支持 Git 和 Subversion 这两种版本控制系统。 以下文章介绍了如何通过 Visual Studio for Mac 设置 Git 和 Subversion 存储库，以及简单的功能（如评审、提交和推送更改）。

* [设置 Git 存储库](set-up-git-repository.md)
* [使用 Git](working-with-git.md)
* [设置 Subversion 存储库](set-up-subversion-repository.md)
* [使用 Subversion](working-with-subversion.md)

## <a name="see-also"></a>请参阅

* [Visual Studio 中的版本控制 (Windows)](/visualstudio/version-control/)