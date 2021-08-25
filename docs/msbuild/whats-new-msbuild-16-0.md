---
title: MSBuild 16.0 中的新增功能 | Microsoft Docs
description: 了解已针对 MSBuild 16.0 更改和更新的功能和属性，并链接到发行说明。
ms.custom: SEO-VS-2020
ms.date: 03/11/2019
ms.topic: conceptual
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: 8c0d085acc2d392c6db156be2bc16743774b60d9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122093648"
---
# <a name="whats-new-in-msbuild-160"></a>MSBuild 16.0 中的新增功能

本文介绍 MSBuild 16.0 中已更新的功能和属性。 有关详细的发行说明，请参阅 [MSBuild 16.0](https://github.com/microsoft/msbuild/releases/tag/v16.0.461.62831)。

## <a name="changed-path"></a>更改的路径

 MSBuild 安装在每版 Visual Studio 下的 \Current  文件夹中，可执行文件位于 \Bin  子文件夹中。 例如，与 Visual Studio 2019 Community 一起安装的 MSBuild.exe  的路径为 C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\MSBuild\Current\Bin\MSBuild.exe  。你也可以使用以下 PowerShell 模块来定位 MSBuild: [vssetup.powershell](https://github.com/Microsoft/vssetup.powershell)。

## <a name="changed-properties"></a>更改的属性

 下列 MSBuild 属性已因新版本号而更新。

- 此版工具的 `MSBuildToolsVersion` 为“Current”。 程序集版本与 Visual Studio 2017 中的程序集版本相同，为 15.1.0.0。

- 此版工具的 `VisualStudioVersion` 为“16.0”

## <a name="change-waves"></a>更改波次

自 MSBuild 16.8 起，可以有选择地选择是否禁用 MSBuild 中某些潜在的颠覆性更改。 请参阅[变更波](change-waves.md)。

## <a name="updates"></a>更新

MSBuild（和 Visual Studio）现面向 .NET Framework 4.7.2。 若想要使用新的 MSBuild API 功能，必须升级程序集，但现有代码将继续工作。

## <a name="see-also"></a>请参阅

- [MSBuild](../msbuild/msbuild.md)
