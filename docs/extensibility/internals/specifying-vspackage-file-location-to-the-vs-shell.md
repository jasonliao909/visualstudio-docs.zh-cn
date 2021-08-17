---
title: 将 VSPackage 文件位置指定为 VS Shell |Microsoft Docs
description: 了解如何使用户能够Visual Studio程序集 DLL 以加载 VSPackage。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, file location
- VSPackages, managed package file location
ms.assetid: beb8607a-4183-4ed2-9ac8-7527f11513b1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 0c3d04c96291c3c7e40fe1c7a7eeb63bb5a3252fc12070700fc1c5d15eaa2ce2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432067"
---
# <a name="specifying-vspackage-file-location-to-the-vs-shell"></a>指定 VS Shell 的 VSPackage 文件位置
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 必须能够找到程序集 DLL 才能加载 VSPackage。 可以通过各种方式找到它，如下表所述。

| 方法 | 说明 |
| - | - |
| 使用 CodeBase 注册表项。 | CodeBase 密钥可用于指示从任何完全限定的文件路径加载 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage 程序集。 键的值应为 DLL 的文件路径。 这是加载包程序集 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的最佳方法。 此方法有时称为"CodeBase/专用安装目录技术"。 在注册过程中，代码库的值通过 类型的实例传递到注册属性 <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.RegistrationContext> 类。 |
| 将 DLL 放入 **PrivateAssemblies** 目录。 | 将程序集放在 **目录的 PrivateAssemblies** 子 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 目录中。 将自动检测 **位于 PrivateAssemblies** 中的程序集，但在"添加引用"**对话框中不可见。** **PrivateAssemblies** 和 **PublicAssemblies** 之间的区别在于 **，PublicAssemblies** 中的程序集在"添加引用"**对话框中枚举。** 如果选择不使用"CodeBase/专用安装目录"技术，应安装到 **PrivateAssemblies** 目录中。 |
| 使用强名称程序集和程序集注册表项。 | 程序集密钥可用于显式指示加载 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 名为 VSPackage 的强程序集。 键的值应为程序集的强名称。 |
| 将 DLL 放入 **PublicAssemblies** 目录。 | 最后，程序集也可以放入 **PublicAssemblies** 子目录中。 将自动检测位于 **PublicAssemblies** 中的程序集，并且也会显示在 中的 **"添加引用** "对话框中 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。<br /><br /> VSPackage 程序集应仅放置在 **PublicAssemblies** 目录中，如果它们包含旨在供其他 VSPackage 开发人员重用的托管组件。 大多数程序集不满足此条件。 |

> [!NOTE]
> 将强名称签名程序集用于所有依赖程序集。 这些程序集还应安装在你自己的目录中，或者安装在 GAC (全局) 。 这可防范与基文件名相同的程序集（称为弱名称绑定）发生冲突。
