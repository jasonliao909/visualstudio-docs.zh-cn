---
title: Visual Studio 2019 中的 JavaScript 和 TypeScript
description: 了解 Visual Studio 2019 如何为 JavaScript 开发提供丰富的支持，且既可以直接使用 JavaScript 也可以使用 TypeScript 编程语言来提供。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 03/16/2020
ms.technology: vs-javascript
ms.topic: conceptual
dev_langs:
- JavaScript
- TypeScript
- DHTML
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: '>= vs-2019'
ms.openlocfilehash: 267bd8567b60a66bcf9d78c3aef8f02bbc942e0d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126642083"
---
# <a name="javascript-and-typescript-in-visual-studio-2019"></a>Visual Studio 2019 中的 JavaScript 和 TypeScript

## <a name="overview"></a>概述

Visual Studio 2019 为 JavaScript 开发提供了丰富的支持，既可以直接使用 JavaScript，也可以使用 [TypeScript 编程语言](http://www.typescriptlang.org/)，其开发目的是提供更高效且充满乐趣的 JavaScript 开发体验，尤其是在大规模开发项目的时候。 对于许多应用程序类型和服务，可以在 Visual Studio 中编写 JavaScript 或 TypeScript 代码。

## <a name="javascript-language-service"></a>JavaScript 语言服务

Visual Studio 2019 中的 JavaScript 体验由提供 TypeScript 支持的相同引擎提供支持。 这为你提供更好的功能支持、丰富度和即时现成集成。

还原到旧版 JavaScript 语言服务的选项不再可用。 用户现在可以使用现成的新 JavaScript 语言服务。 新的语言服务仅基于 TypeScript 语言服务，由静态分析提供支持。 这使我们能够提供更好的工具，因此 JavaScript 代码可以从基于类型定义的更丰富的 IntelliSense 中受益。 新服务是轻量服务，比传统服务消耗更少的内存，代码可以缩放，因而可以提供更好的性能。 我们还改进了语言服务的性能以处理更大的项目。

## <a name="typescript-support"></a>TypeScript 支持

Visual Studio 2019 提供了若干选项，用于将 TypeScript 编译集成到项目中：

* [TypeScript NuGet 包](https://www.nuget.org/packages/Microsoft.TypeScript.MSBuild)。 当 TypeScript 3.2 或更高版本的 NuGet 包安装到项目中时，将在编辑器中加载相应版本的 TypeScript 语言服务。
* [TypeScript npm 包](https://www.npmjs.com/package/typescript)。 当 TypeScript 2.1 或更高版本的 npm 包安装到项目中时，将在编辑器中加载相应版本的 TypeScript 语言服务。
* TypeScript SDK（在 Visual Studio 安装程序中默认提供），以及 [VS Marketplace](https://marketplace.visualstudio.com/items?itemName=TypeScriptTeam.typescript-395) 中提供的独立 SDK 下载。

> [!TIP]
> 对于使用 Visual Studio 2019 开发的项目，我们鼓励你使用 TypeScript NuGet 或 TypeScript npm 包，以实现跨不同平台和环境的更高可移植性。 有关详细信息，请参阅[使用 NuGet 编译 TypeScript 代码](../javascript/compile-typescript-code-nuget.md)和[使用 tsc 编译 TypeScript 代码](../javascript/compile-typescript-code-npm.md)。

## <a name="projects"></a>项目

Visual Studio 2019 不再支持 UWP JavaScript 应用。 无法创建或打开 JavaScript UWP 项目（扩展名为“.jsproj”  的文件）。 有关详细信息，请参阅有关[创建在 Windows 上运行良好的渐进式 Web 应用 (PWA)](/microsoft-edge/progressive-web-apps-chromium) 的文档。
