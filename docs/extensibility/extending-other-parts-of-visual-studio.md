---
title: 扩展 Visual Studio 的其他部分 |Microsoft Docs
description: 了解可以扩展 Visual Studio UI 的各个部分。 你可以创建 VSPackage，写入活动日志，并扩展工具箱和状态栏。
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
ms.openlocfilehash: 0dd73c9a03161d34a040799ba6e0d65b909dd1d1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122159446"
---
# <a name="extend-other-parts-of-visual-studio"></a>扩展 Visual Studio 的其他部分

可以扩展 Visual Studio UI 的更多部分。 这里只是几个例子。

## <a name="create-a-vspackage"></a>创建 VSPackage

Visual Studio 扩展性的基本构建基块 vspackage。  了解如何添加 VSPackage： [使用 VSPackage 创建扩展](../extensibility/creating-an-extension-with-a-vspackage.md)

## <a name="extend-the-toolbox"></a>扩展工具箱

了解如何将新控件和其他项添加到 "工具箱"，以及如何使用工具箱功能：

- [创建 WPF 工具箱控件](../extensibility/creating-a-wpf-toolbox-control.md)

- [创建 Windows 窗体工具箱控件](../extensibility/creating-a-windows-forms-toolbox-control.md)

## <a name="extend-the-status-bar"></a>扩展状态栏

了解如何读取和写入状态栏和进度栏，以及如何提供动画和其他 UI： [扩展](../extensibility/extending-the-status-bar.md)状态栏。

::: moniker range="vs-2017"

## <a name="create-custom-start-pages"></a>创建自定义起始页

了解如何从头开始创建自己的起始页或从可下载的起始页示例： [创建自定义起始页](../extensibility/creating-a-custom-start-page.md)。

::: moniker-end

## <a name="write-to-the-activity-log"></a>写入活动日志

了解如何 [使用活动日志](../extensibility/how-to-use-the-activity-log.md)进行写入操作。
