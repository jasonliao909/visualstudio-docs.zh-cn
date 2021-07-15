---
title: '&apos;Visual Studio 2017 SDK |Microsoft Docs'
description: Visual Studio SDK 具有适用于 Visual Studio 2017 的新功能和更新的功能，包括更新后的 VSIX 版本 3 格式。
ms.custom: SEO-VS-2020
ms.date: 10/31/2017
ms.topic: conceptual
ms.assetid: 9efcf0a3-dbde-4cab-8ed3-425826a48b2e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0b0b7852fa7e20f4ee6951e57c5c19f4b5454028
ms.sourcegitcommit: 3c6c263a1c0b20f084290ce45295a46027da33b6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/14/2021
ms.locfileid: "113756899"
---
# <a name="what39s-new-in-the-visual-studio-2017-sdk"></a>&#39;2017 SDK Visual Studio新增功能

Visual Studio SDK 具有以下适用于 Visual Studio 2017 的新增和更新的功能。

## <a name="vsix-v3-format"></a>VSIX v3 格式

为了支持 2017 Visual Studio 的轻型安装，VSIX 扩展清单格式已更新为 VSIX v3 (版本 3) 。

新格式支持：

* 显式声明 VSIXInstaller 要检测并安装的先决条件。
* 扩展安装上的 Ngen 程序集。
* 在常规扩展根目录之外安装资产。

若要了解这些更改，请参阅以下主题：

* [2017 年 10 月Visual Studio性更改](breaking-changes-2017.md)
* [VSIX v3 中的 Ngen 支持](ngen-support.md)
* [在扩展文件夹外进行安装](set-install-root.md)
* [有关 2017 Visual Studio扩展的常见问题](faq-2017.yml)

## <a name="migrate-extensibility-project-to-visual-studio-2017"></a>将扩展性项目迁移到 Visual Studio 2017

若要了解如何将扩展性项目及其 VSIX 清单更新到 Visual Studio 2017，请参阅如何：将扩展性项目迁移到[Visual Studio 2017。](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)

## <a name="custom-project-and-item-templates"></a>自定义项目和项模板

从 Visual Studio 2017 开始，将无法再执行对自定义项目和项模板的扫描。 相反，扩展必须提供模板清单文件来描述这些模板的安装位置。 可使用 Visual Studio 2017 来更新 VSIX 扩展。 如果使用 MSI 部署扩展，则必须手动生成模板清单文件。 有关详细信息，请参阅升级 Visual Studio [2017 的自定义项目和项模板](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md)。 有关模板清单架构，可查看 [Visual Studio 模板清单架构参考](../extensibility/visual-studio-template-manifest-schema-reference.md)。

## <a name="updated-extension-performance-guidelines"></a>更新了扩展性能准则

在"管理[](how-to-diagnose-extension-performance.md)[VSPackages"](managing-vspackages.md)下有一篇新的"如何：诊断扩展性能"一文，Visual Studio分析扩展对启动和解决方案加载时间的影响。
