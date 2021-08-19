---
title: Visual StudioSDK |Microsoft Docs
description: Visual Studio SDK 有助于扩展功能或向 Visual Studio 添加新功能。 了解可用于扩展 Visual Studio 的一些方式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSSDK.v90.StartPage
helpviewer_keywords:
- Visual Studio SDK
- VS SDK (see Visual Studio SDK)
- Visual Studio, SDK
ms.assetid: 1f7c348a-114c-4243-b392-3531e9c9c6fd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f61ad24a7a94827720de388ed957f1c33dc7bc8c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122078604"
---
# <a name="visual-studio-sdk"></a>Visual Studio SDK
Visual Studio SDK 可帮助你扩展 Visual Studio 功能或将新功能集成到 Visual Studio 中。 可以将扩展分发给其他用户以及 Visual Studio Marketplace。 以下是一些扩展 Visual Studio 的方式：

- 向 IDE 添加命令、按钮、菜单和其他 UI 元素

- 添加工具窗口以实现新功能

- 扩展给定语言的 IntelliSense，或为新的编程语言提供 IntelliSense

- 使用轻型电灯泡提供帮助开发人员编写更好代码的提示和建议

- 启用新语言支持

- 添加自定义项目类型

- 通过 Visual Studio Marketplace 向数百万开发人员提供

  如果之前从未编写过 Visual Studio 扩展，则应该了解有关这些功能的详细信息，并[开始开发 Visual Studio 扩展](../extensibility/starting-to-develop-visual-studio-extensions.md)。

## <a name="install-the-visual-studio-sdk"></a>安装 Visual Studio SDK
 Visual Studio SDK 是 Visual Studio 安装程序中的一项可选功能。 也可稍后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="whats-new-in-the-visual-studio-sdk"></a>Visual Studio SDK 的新增功能
 Visual Studio SDK 具有一些新功能，例如同步加载扩展警告和 VSIX v3 格式以及重大更改，这可能要求你更新扩展。 有关详细信息，请参阅[Visual Studio 2019 sdk 的新增功能](../extensibility/whats-new-visual-studio-2019-sdk.md)和[Visual Studio 2017 sdk 的新增功能](../extensibility/what-s-new-in-the-visual-studio-2017-sdk.md)。

## <a name="visual-studio-user-experience-guidelines"></a>Visual Studio 用户体验指南
 获取有关在[Visual Studio 用户体验指南](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)中设计扩展 UI 的极佳技巧。

 你还可以了解如何在高 DPI 设备上提供扩展，并显示 [地址 DPI 问题](../extensibility/addressing-dpi-issues2.md) 一文。

 利用 [映像服务和目录](../extensibility/image-service-and-catalog.md) 获得极佳的图像管理，并提供高 DPI 和主题的支持。

## <a name="find-and-install-existing-visual-studio-extensions"></a>查找并安装现有 Visual Studio 扩展
 可以在 "**工具**" 菜单上的 "**扩展和更新**" 对话框中找到 Visual Studio 扩展。 有关详细信息，请参阅[查找和使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)。 你还可以在[Visual Studio Marketplace](https://marketplace.visualstudio.com/)中找到扩展

## <a name="visual-studio-sdk-reference"></a>Visual StudioSDK 参考
 可以在[Visual Studio sdk 参考](../extensibility/visual-studio-sdk-reference.md)中找到 Visual Studio sdk API 引用。

## <a name="visual-studio-sdk-samples"></a>Visual StudioSDK 示例
 你可以在[Visual Studio 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)中找到 GitHub 上 VS SDK 扩展的开源示例。 此 GitHub 存储库包含演示 Visual Studio 中的各种可扩展功能的示例。

## <a name="other-visual-studio-sdk-resources"></a>其他 Visual Studio SDK 资源
 如果对 VSSDK 有疑问或想要分享开发扩展的经验，可以使用[Visual Studio 扩展性论坛](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx)或[ExtendVS Gitter Chatroom](https://gitter.im/Microsoft/extendvs)。

 可以在 [VSX Arcana 博客](/archive/blogs/vsx/) 和 Microsoft mvp 编写的大量博客中找到详细信息：

- [收藏夹 Visual Studio 扩展](https://scottdorman.blog/2014/10/05/favorite-visual-studio-extensions/)

- [Visual Studio 扩展性](http://www.visualstudioextensibility.com/overview/vs/)

- [扩展 Visual Studio](https://blog.slaks.net/2013-10-18/extending-visual-studio-part-1-getting-started/)

## <a name="see-also"></a>请参阅

- [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)
- [如何：将扩展性项目迁移到 Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md)
- [常见问题解答：将外接程序转换为 VSPackage 扩展](/previous-versions/visualstudio/visual-studio-2015/extensibility/faq-converting-add-ins-to-vspackage-extensions?preserve-view=true&view=vs-2015)
- [在托管代码中管理多个线程](../extensibility/managing-multiple-threads-in-managed-code.md)
- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)
- [将命令添加到工具栏](../extensibility/adding-commands-to-toolbars.md)
- [扩展和自定义工具窗口](../extensibility/extending-and-customizing-tool-windows.md)
- [编辑器和语言服务扩展](../extensibility/editor-and-language-service-extensions.md)
- [扩展项目](../extensibility/extending-projects.md)
- [扩展用户设置和选项](../extensibility/extending-user-settings-and-options.md)
- [创建自定义项目和项模板](../extensibility/creating-custom-project-and-item-templates.md)
- [扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md)
- [扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)
- [使用和提供服务](../extensibility/using-and-providing-services.md)
- [管理 VSPackage](../extensibility/managing-vspackages.md)
- [Visual Studio 隔离 shell](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)
- [装运 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)
- [深入探究 Visual Studio SDK](../extensibility/internals/inside-the-visual-studio-sdk.md)
- [支持 Visual Studio SDK](../extensibility/support-for-the-visual-studio-sdk.md)
- [Visual StudioSDK 参考](../extensibility/visual-studio-sdk-reference.md)