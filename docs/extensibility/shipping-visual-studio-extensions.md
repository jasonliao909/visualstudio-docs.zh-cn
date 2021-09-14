---
title: 发货Visual Studio扩展|Microsoft Docs
description: 了解如何发布和维护 Visual Studio SDK 扩展，包括使用 .vsix 文件、发布、本地化和更新。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX deployment
- deployment, VSIX
- satellite DLLs, in VSIX packages
ms.assetid: 13cd263d-25f7-488e-9c1a-cff908caedb6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a57cb6732c1b1cb5fa74381ab7c8bdf8208be08d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600682"
---
# <a name="shipping-visual-studio-extensions"></a>传送 Visual Studio 扩展
完成扩展开发后，可以将其安装在其他计算机上，与朋友和同事共享，或将其发布到 Visual Studio Marketplace。 本部分介绍发布和维护扩展需要执行的所有操作：使用 .vsix 文件、发布、本地化和更新。

## <a name="working-with-vsix-extensions"></a>使用 VSIX 扩展
 可以通过创建空白 VSIX 扩展来创建 VSIX 扩展Project，然后将不同的项模板添加到该扩展。 有关详细信息，请参阅[VSIX Project模板](../extensibility/vsix-project-template.md)。

 可以使用 VSIX 格式打包项目模板、项模板、VSPackages、Managed Extensibility Framework (MEF) 组件、工具箱控件、程序集和自定义类型 (这包括 Visual Studio 2017) 的自定义起始页。 VSIX 格式使用基于文件的部署。 有关 VSIX 包详细信息，请参阅 [VSIX 包剖析](../extensibility/anatomy-of-a-vsix-package.md)。

 VSIX 格式不支持安装代码片段。 它还不支持某些其他方案，例如写入 GAC (全局程序集缓存) 或系统注册表。 如果需要在安装中写入 GAC 或注册表，则必须使用 Windows 安装程序。 有关详细信息，请参阅[准备安装程序部署的Windows扩展](../extensibility/preparing-extensions-for-windows-installer-deployment.md)。

## <a name="publishing-your-extension-to-the-visual-studio-marketplace"></a>将扩展发布到 Visual Studio Marketplace
 只需将 .vsix 文件或放入服务器，就可以将扩展分发给其他人。 但是，让大量用户掌握代码的最佳方法就是将代码放在 Visual Studio [Marketplace 上](https://marketplace.visualstudio.com/vs)。 Visual Studio市场扩展通过"扩展Visual Studio **向用户提供**。 有关详细信息，请参阅[查找和使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)。

 有关演示如何将扩展上传到 Visual Studio 的完整示例，请参阅演练：发布 Visual Studio[扩展](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)。

## <a name="private-galleries"></a>Private Galleries
 开发控件、模板和工具时，可以通过将它们发布到 Intranet 上的专用库来与组织共享它们。 有关详细信息，请参阅 [专用库](../extensibility/private-galleries.md)。

## <a name="localizing-your-extension"></a>本地化扩展
 如果打算在不同的区域设置中发布扩展，应考虑本地化它。 有关所涉及的内容的说明，请参阅 [本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)。

## <a name="updating-and-versioning-your-extension"></a>更新扩展和版本控制
 发布扩展后，有一段时间需要更新它。 若要了解如何更新已在 Visual Studio 市场上发布的扩展，请参阅[如何：更新扩展](../extensibility/how-to-update-a-visual-studio-extension.md)。

 可以将扩展设置为支持多个版本的 Visual Studio。 有关详细信息，请参阅支持多个[版本的 Visual Studio。](../extensibility/supporting-multiple-versions-of-visual-studio.md)

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[VSIX 项目模板入门](../extensibility/getting-started-with-the-vsix-project-template.md)|说明如何使用 VSIX 项目模板安装自定义项目模板。|
|[VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)|描述 VSIX 包的组件。|
|[VSIX 项目模板](../extensibility/vsix-project-template.md)|提供有关如何打包和发布扩展的分步说明。|
|[本地化 VSIX 包](../extensibility/localizing-vsix-packages.md)|说明如何使用 extension.vsixlangpack 文件为安装过程提供本地化文本。|
|[如何：更新扩展](../extensibility/how-to-update-a-visual-studio-extension.md)|介绍如何更新系统上的扩展以及如何将更新部署到现有扩展Visual Studio扩展。|
|[如何：将依赖项添加到 VSIX 包](../extensibility/how-to-add-a-dependency-to-a-vsix-package.md)|介绍如何添加对 VSIX 部署包的引用。|
|[准备 Windows Installer 部署的扩展](../extensibility/preparing-extensions-for-windows-installer-deployment.md)|说明如何使用安装程序部署Windows扩展。|
|[对 VSIX 包进行签名](../extensibility/signing-vsix-packages.md)|说明如何对 VSIX 包进行签名。|
|[Private Galleries](../extensibility/private-galleries.md)|说明如何为扩展创建专用库。|
|[支持多个版本的 Visual Studio](../extensibility/supporting-multiple-versions-of-visual-studio.md)|演示如何让扩展支持多个版本的 Visual Studio。|
|[查找 Visual Studio](locating-visual-studio.md)|介绍如何查找自定义Visual Studio部署的实例。|
