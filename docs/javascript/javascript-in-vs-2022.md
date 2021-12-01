---
title: Visual Studio 2022 中的 JavaScript 和 TypeScript
description: 了解 Visual Studio 2022 如何为 JavaScript 开发（无论是直接使用 JavaScript 进行开发，还是使用 TypeScript 编程语言进行开发）提供丰富的支持。
titleSuffix: ''
ms.date: 09/27/2021
ms.technology: vs-javascript
ms.topic: conceptual
dev_langs:
- JavaScript
- TypeScript
- DHTML
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: '>= vs-2022'
ms.openlocfilehash: 9b4ff4d4f0e345cd9cb69c98355d929f6209da09
ms.sourcegitcommit: d63ba1eff845d41ca095efb14b499ea96c4b6eba
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2021
ms.locfileid: "129561069"
---
# <a name="javascript-and-typescript-in-visual-studio-2022"></a>Visual Studio 2022 中的 JavaScript 和 TypeScript

## <a name="overview"></a>概述

Visual Studio 2022 为 JavaScript 开发（无论是直接使用 JavaScript 进行开发，还是使用  [TypeScript 编程语言](http://www.typescriptlang.org/)进行开发）提供丰富的支持。TypeScript 编程语言的开发目的是提供更高效且充满乐趣的 JavaScript 开发体验，尤其是在大规模开发项目的时候。 对于许多应用程序类型和服务，可以在 Visual Studio 中编写 JavaScript 或 TypeScript 代码。 

## <a name="javascript-language-service"></a>JavaScript 语言服务 

Visual Studio 2022 中的 JavaScript 体验由提供 TypeScript 支持的同一引擎提供支持。 该引擎为你提供更好的功能支持、丰富度和即时现成集成。 

还原到旧版 JavaScript 语言服务的选项不再可用。 用户可以使用现成的新 JavaScript 语言服务。 新的语言服务仅基于 TypeScript 语言服务，由静态分析提供支持。 该服务使我们能够为你提供更好的工具，因此 JavaScript 代码可以从基于类型定义的更丰富的 IntelliSense 中受益。 新服务是轻量服务，比传统服务消耗更少的内存，代码可以缩放，因而可以提供更好的性能。 我们还改进了语言服务的性能以处理更大的项目。 

## <a name="typescript-support"></a>TypeScript 支持 

默认情况下，Visual Studio 2022 为 JavaScript 和 TypeScript 文件（用于为 IntelliSense 提供支持）提供语言支持，无需任何特定项目配置。  

对于编译 TypeScript，Visual Studio 使你可以灵活地选择要对每个项目使用的 TypeScript 版本。 

在 MSBuild 编译方案中，建议使用 [TypeScript NuGet 包](https://www.nuget.org/packages/Microsoft.TypeScript.MSBuild)方法为项目添加 TypeScript 编译支持。 当你首次向项目添加 TypeScript 文件时，Visual Studio 会为你提供添加此包的选项。 你还可以随时通过 NuGet 包管理器来使用此包。 使用 NuGet 包时，相应的语言服务版本将用于项目中的语言支持。 注意：此包的最低支持版本为 3.6。 

为 npm 配置的项目可通过添加 [TypeScript npm 包](https://www.npmjs.com/package/typescript)来指定其自己的 TypeScript 语言服务版本。 可以在支持的项目中使用 npm 管理器来指定版本。 注意：此包的最低支持版本为 2.1。

TypeScript SDK 已在 Visual Studio 2022 中弃用。 依赖于该 SDK 的现有项目应升级为使用 NuGet 包。 对于无法立即升级的项目，仍可使用在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TypeScriptTeam.typescript-442) 上提供的 SDK，它在 Visual Studio 安装程序中作为可选组件提供。 

> [!TIP] 
> 对于使用 Visual Studio 2022 开发的项目，我们鼓励你使用 TypeScript NuGet 或 TypeScript npm 包，以实现跨不同平台和环境的更高可移植性。 有关详细信息，请参阅 [使用 NuGet 编译 TypeScript 代码](../javascript/compile-typescript-code-nuget.md)和 [使用 tsc 编译 TypeScript 代码](../javascript/compile-typescript-code-npm.md)。 

## <a name="project-templates"></a>项目模板 

从 Visual Studio 2022 开始，会有一个新的 JavaScript/TypeScript 项目类型 (.esproj)，你可以使用该类型在 Visual Studio 中创建单独的 Angular、React 和 Vue 项目。 这些前端项目使用已安装在本地计算机上的框架 CLI 工具创建，因此模板版本取决于你。  

在这些新项目中，你可以运行 JavaScript 和 TypeScript 单元测试，使用 npm 管理器轻松添加和连接 ASP.NET Core API 项目并下载 npm 模块。 查看一些快速入门和教程即可开始操作。 如果需要详细信息，可参阅[此博客文章](https://devblogs.microsoft.com/visualstudio/the-new-javascript-typescript-experience-in-vs-2022-preview-3/)。