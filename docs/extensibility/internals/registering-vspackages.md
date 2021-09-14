---
title: 注册 VSPackages |Microsoft Docs
description: .pkgdef 文件包含信息，否则会添加到系统注册表。 了解如何Visual Studio .pkgdef 文件来描述/查找 VSPackage。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, registering
- registration, managed VSPackages
ms.assetid: 79b9424e-7e9b-4fc8-9b9f-00212674573c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b8f4f56bd2f033501e8482fbd813aa72e1cb2bf9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664320"
---
# <a name="registering-vspackages"></a>注册 VSPackage
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 依赖于 .pkgdef 文件来描述和查找 VSPackage。 .pkgdef 文件包含将添加到系统注册表的所有注册信息。 通过将属性添加到源代码，然后在生成的程序集上运行 [CreatePkgDef](../../extensibility/internals/createpkgdef-utility.md) 实用工具以生成 .pkgdef 文件来注册托管 VSPackage。

## <a name="in-this-section"></a>本节内容
- [指定 VS Shell 的 VSPackage 文件位置](../../extensibility/internals/specifying-vspackage-file-location-to-the-vs-shell.md)

 描述 VSPackage 的加载路径。

- [注册和注销 VSPackage](../../extensibility/registering-and-unregistering-vspackages.md)

 说明如何注册 VSPackage。
