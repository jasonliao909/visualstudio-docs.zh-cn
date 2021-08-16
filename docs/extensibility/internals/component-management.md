---
title: 组件管理|Microsoft Docs
description: 了解如何在 Windows 中创建 VSPackage 安装程序时管理 Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], components
- installation [Visual Studio SDK], file management
ms.assetid: 029bffa2-6841-4caa-a41a-442467e1aedc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6ff094b0ad7457eabc569ce10d44a80c1f6db639cc7c855dc4f27c77c68edbc4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121275523"
---
# <a name="component-management"></a>组件管理
安装程序中的任务单元Windows称为 Windows 安装程序组件 (有时称为 WIC，或仅称为) 。 GUID 标识每个 WIC，这是使用安装程序的安装程序的基本安装单元和Windows计数。

 尽管可以使用多种产品来创建 VSPackage 安装程序，但此讨论假设使用 Windows Installer *(.msi) 文件*。 创建安装程序时，必须正确管理文件部署，以便时时进行正确的引用计数。 因此，在混合安装和卸载方案中，产品的不同版本不会相互干扰或破坏。

 在Windows安装程序中，引用计数在组件级别进行。 必须仔细将资源（文件、注册表条目等）组织到组件中。 其他级别的组织（例如模块、功能和产品）可以在不同的方案中提供帮助。 有关详细信息，请参阅 Windows[安装程序基础知识](../../extensibility/internals/windows-installer-basics.md)。

## <a name="guidelines-of-authoring-setup-for-side-by-side-installation"></a>并行安装的创作设置指南

- 将版本之间共享的文件和注册表项创作到其自己的组件中。

     这样，你可以轻松地在下一版本中使用它们。 例如，键入全局注册的库、文件扩展名、在 HKEY_CLASSES_ROOT注册的其他项，等等。

- 将共享组件分组到单独的合并模块中。

     此策略可帮助你正确创作，以继续并行安装。

- 使用相同版本安装程序组件安装共享Windows注册表项。

     如果使用不同的组件，则卸载一个版本控制 VSPackage 但仍安装另一个 VSPackage 时，将卸载文件和注册表项。

- 不要在同一组件中混合使用版本控制项和共享项。

     这样做无法将共享项安装到全局位置，将版本控制项安装到独立位置。

- 没有指向版本控制文件的共享注册表项。

     如果这样做，则安装另一版本控制 VSPackage 时，将覆盖共享密钥。 删除第二个版本后，键指向的文件将消失。

## <a name="see-also"></a>另请参阅
- [在共享 VSPackage 和版本控制 VSPackage 之间选择](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [VSPackage 安装方案](../../extensibility/internals/vspackage-setup-scenarios.md)
