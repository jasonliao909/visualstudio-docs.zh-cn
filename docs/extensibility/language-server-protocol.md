---
title: 语言服务器协议概述|Microsoft Docs
description: 了解语言服务器协议如何提供一个有用的框架，用于向各种工具公开语言功能。
ms.custom: SEO-VS-2020
ms.date: 11/14/2017
ms.topic: conceptual
ms.assetid: 6a7d93c2-31ea-4bae-8b29-6988a567ddf2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 652164ec8553f0a332130d01f9c9d3a6d0537224
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122152310"
---
# <a name="language-server-protocol"></a>语言服务器协议

## <a name="what-is-the-language-server-protocol"></a>什么是语言服务器协议？

在编辑器或 IDE 中支持丰富的编辑功能（如源代码自动完成或转到定义）在传统上非常具有挑战性且非常耗时。 通常，它需要在扫描程序 (分析器、类型检查器、生成器) 编辑器或 IDE 编程语言中编写域模型。 例如，在 Eclipse IDE 中为 C/C++ 提供支持的 Eclipse CDT 插件是使用 Java 编写的，因为 Eclipse IDE 本身是用 Java 编写的。 遵循此方法，这意味着在 TypeScript 中实现适用于 Visual Studio Code 的 C/C++ 域模型，在 C# 中为 Visual Studio。

如果开发工具可以重复使用现有的特定于语言的库，则创建特定于语言的域模型也容易得多。 但是，这些库通常在编程语言本身中实现 (例如，良好的 C/C++ 域模型在 C/C++) 。 从技术上来说，将 C/C++ 库集成到用 TypeScript 编写的编辑器中是可行但难以完成的工作。

### <a name="language-servers"></a>语言服务器

另一方法是在其自己的进程中运行库，并使用进程间通信来与它通信。 来回发送的消息构成了协议。 语言服务器协议 (LSP) 是标准化开发工具和语言服务器进程之间交换的消息。 使用语言服务器或证明不是新想法或新想法。 Vim 和 Emacs 等编辑器一直在执行此操作一段时间，以提供语义自动完成支持。 LSP 的目标是简化这些类型的集成，并为向各种工具公开语言功能提供有用的框架。

使用通用协议，可以重新使用语言域模型的现有实现，将编程语言功能集成到开发工具中， 语言服务器后端可以 PHP、Python 或 Java 编写，LSP 可将其轻松集成到各种工具中。 协议在通用的抽象级别工作，以便工具可以提供丰富的语言服务，而无需完全了解特定于基础域模型的细微差别。

## <a name="how-work-on-the-lsp-started"></a>LSP 上的工作如何启动

LSP 已随着时间的推移而发展，目前为版本 3.0。 它从 OmniSharp 选取语言服务器的概念开始，为 C# 提供丰富的编辑功能。 OmniSharp 最初使用具有 JSON 有效负载的 HTTP 协议，并且已集成到多个[](https://code.visualstudio.com)编辑器中，Visual Studio Code。

大约在同一时间，Microsoft 开始在 TypeScript 语言服务器上工作，其思路是支持 Emacs 和 Sublime Text 等编辑器中的 TypeScript。 在此实现中，编辑器通过 stdin/stdout 与 TypeScript 服务器进程通信，并使用受 V8 调试器协议启发的 JSON 有效负载用于请求和响应。 TypeScript 服务器已集成到 TypeScript Sublime 插件中，VS Code用于丰富 TypeScript 编辑。

集成两个不同的语言服务器后，VS Code团队开始探索编辑器和 ID 的公用语言服务器协议。 公共协议使语言提供程序能够创建一个供不同 ES 使用的语言服务器。 语言服务器使用者只需实现协议的客户端一次。 这为语言提供程序和语言使用者都产生一种多胜的情况。

语言服务器协议从 TypeScript 服务器使用的协议开始，通过受语言 API 启发的更多语言VS Code扩展。 协议使用 JSON-RPC 进行远程调用，因为该协议简单且具有现有库。

该VS Code团队通过实现多个 linter 语言服务器来原型化协议，这些服务器响应对 lint (扫描) 文件的请求，并返回一组检测到的警告和错误。 目标是在用户编辑文档时对文件进行 lint 处理，这意味着编辑器会话期间将有许多 linting 请求。 使服务器保持正常运行是有意义的，以便无需为每个用户编辑启动新的 linting 进程。 实现了多个 linter 服务器，VS Code ESLint 和 TSLint 扩展。 这两个 linter 服务器均在 TypeScript/JavaScript 中实现，并Node.js。 它们共享一个库，用于实现协议的客户端和服务器部分。

## <a name="how-the-lsp-works"></a>LSP 的工作原理

语言服务器在其自己的进程中运行，Visual Studio或VS Code通过 JSON-RPC 使用语言协议与服务器通信。 在专用进程中运行的语言服务器的另一个优点是可以避免与单个进程模型相关的性能问题。 如果客户端和服务器都写入了客户端和服务器，则实际传输通道可以是 stdio、套接字、命名管道或节点 ipc Node.js。

下面是一个示例，说明工具和语言服务器在例程编辑会话期间如何通信：

![lsp 流程图](media/lsp-flow-diagram.png)

* 用户打开 **一** (工具中称为) 文档"的文件：该工具通知语言服务器文档已打开 ("textDocument/didOpen") 。 从现在开始，文档内容的事实不再在文件系统上，而是由工具保留在内存中。

* 用户 **进行** 编辑：该工具会通知服务器文档更改 ('textDocument/didChange') 并且语言服务器会更新程序的语义信息。 发生这种情况时，语言服务器会分析此信息，并通知工具检测到的错误和警告 ( textDocument/publishDiagnostics ) 。

* 用户对编辑器中的符号执行"转到定义"：该工具发送具有两个参数的"textDocument/definition"请求： (1) 文档 URI 和 (2) 从启动"转到定义"请求到服务器的文本位置。 服务器使用文档 URI 和符号定义在文档内的位置进行响应。

* 用户关闭文档 (文件 **) ：** 从工具发送"textDocument/didClose"通知，通知语言服务器文档现在不再在内存中，并且文件系统上的当前内容现在是最新的。

此示例说明了协议如何在编辑器功能（如"转到定义"、"查找所有引用"）级别与语言服务器通信。 协议使用的数据类型是编辑器或 IDE"数据类型"，如当前打开的文本文档和光标的位置。 数据类型不在编程语言域模型级别，这通常提供抽象语法树和编译器符号 (例如解析的类型、命名空间、...) 。这大大简化了协议。

现在，让我们更详细地了解一下"textDocument/definition"请求。 下面是 C++ 文档中"转到定义"请求的客户端工具和语言服务器之间的有效负载。

这是请求：

```json
{
    "jsonrpc": "2.0",
    "id" : 1,
    "method": "textDocument/definition",
    "params": {
        "textDocument": {
            "uri": "file:///p%3A/mseng/VSCode/Playgrounds/cpp/use.cpp"
        },
        "position": {
            "line": 3,
            "character": 12
        }
    }
}
```

响应为：

```json
{
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
        "uri": "file:///p%3A/mseng/VSCode/Playgrounds/cpp/provide.cpp",
        "range": {
            "start": {
                "line": 0,
                "character": 4
            },
            "end": {
                "line": 0,
                "character": 11
            }
        }
    }
}
```

回顾一下，在编辑器级别（而不是编程语言模型级别）描述数据类型是语言服务器协议成功的原因之一。 与跨不同编程语言标准化抽象语法树和编译器符号相比，标准化文本文档 URI 或游标位置要简单得多。

当用户使用不同的语言时，VS Code通常启动每个编程语言的语言服务器。 以下示例演示了一个会话，其中用户处理 Java 和 SASS 文件。

![java 和 sass](media/lsp-java-and-sass.png)

### <a name="capabilities"></a>功能

并非每个语言服务器都可以支持协议定义的所有功能。 因此，客户端和服务器通过"功能"公布其支持的功能集。 例如，服务器宣布它可以处理"textDocument/definition"请求，但可能不会处理"workspace/symbol"请求。 同样，客户端可以宣布，他们可以在保存文档之前提供"即将保存"通知，以便服务器可以计算文本编辑以自动格式化编辑的文档。

## <a name="integrating-a-language-server"></a>集成语言服务器

语言服务器与特定工具的实际集成不是由语言服务器协议定义的，而由工具实现者决定。 某些工具通过具有可启动和与任何类型的语言服务器通信的扩展，以通用方式集成语言服务器。 其他语言VS Code，为每个语言服务器创建自定义扩展，以便扩展仍能够提供一些自定义语言功能。

为了简化语言服务器和客户端的实现，客户端和服务器部件有库或 SDK。 这些库适用于不同的语言。 例如，有一个语言客户端[npm](https://www.npmjs.com/package/vscode-languageclient)模块，用于简化语言服务器与 VS Code 扩展的集成，另一个语言服务器[npm](https://www.npmjs.com/package/vscode-languageserver)模块使用 Node.js。 这是支持 [库的当前](https://github.com/Microsoft/language-server-protocol/wiki/Protocol-Implementations) 列表。

## <a name="using-the-language-server-protocol-in-visual-studio"></a>在 Visual Studio

* [添加语言服务器协议扩展](adding-an-lsp-extension.md)- 了解如何将语言服务器集成到 Visual Studio。
