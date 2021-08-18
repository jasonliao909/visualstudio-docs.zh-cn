---
title: 部署 Project 类型 |Microsoft Docs
description: 在 Visual Studio SDK 中了解如何使用新的项目类型聚合器和 Windows Installer 包来部署托管代码项目类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], managed-code
- projects [Visual Studio SDK], aggregator
ms.assetid: 7f132f67-8589-464c-90dc-0d57ae02aa8f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 7b3cacbb9a816171209cc5f1cbdd87ed4a1d7a7b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122086633"
---
# <a name="deploy-project-types"></a>部署项目类型
[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]安装新的项目类型聚合器 (*ProjectAggregator2.dll*) ，以及用于重新 *分发 (ProjectAggregator2.msi) 的* Windows Installer 包。 必须为托管代码项目类型使用新的聚合器。 ProjectAggregator2 解决了 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目聚合函数中的限制，使托管代码项目类型不能正常工作。 以下步骤介绍如何将 VSPackage 更改为使用新的聚合器。

1. 从解决方案中删除 NativeHierarchyWrapper 项目。

2. 从安装程序中删除任何 NativeHierarchyWrapper 二进制文件。

3. 将 *ProjectAggregator2.msi* 添加到设置。
