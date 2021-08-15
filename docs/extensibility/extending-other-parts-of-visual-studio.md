---
title: 扩展服务的其他Visual Studio |Microsoft Docs
description: 了解可扩展Visual Studio UI 的各个部分。 可以创建 VSPackage、写入活动日志并扩展工具箱和状态栏。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces
ms.assetid: 27d2f1e1-2503-4aca-9cfc-707abd07ccf0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b0b3e649bba1687d89fbb3d9d5688649be143463a62525149b3148724331942b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121360009"
---
# <a name="extend-other-parts-of-visual-studio"></a>扩展其他部分Visual Studio

可以扩展 Visual Studio UI 的更多部分。 在这里，我们只展示几个。

## <a name="create-a-vspackage"></a>创建 VSPackage

扩展性的基本构建Visual Studio是 VSPackage。  了解如何添加 VSPackage：使用 [VSPackage 创建扩展](../extensibility/creating-an-extension-with-a-vspackage.md)

## <a name="extend-the-toolbox"></a>扩展工具箱

了解如何向工具箱添加新控件和其他项，以及如何使用工具箱功能：

- [创建 WPF 工具箱控件](../extensibility/creating-a-wpf-toolbox-control.md)

- [创建Windows窗体工具箱控件](../extensibility/creating-a-windows-forms-toolbox-control.md)

## <a name="extend-the-status-bar"></a>扩展状态栏

了解如何读取和写入状态栏和进度栏，以及如何提供动画和其他 UI： [扩展状态栏](../extensibility/extending-the-status-bar.md)。

::: moniker range="vs-2017"

## <a name="create-custom-start-pages"></a>创建自定义起始页

了解如何从头开始或从可下载的起始页示例创建自己的起始页 [：创建自定义起始页](../extensibility/creating-a-custom-start-page.md)。

::: moniker-end

## <a name="write-to-the-activity-log"></a>写入活动日志

了解如何写入活动日志： [如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。
