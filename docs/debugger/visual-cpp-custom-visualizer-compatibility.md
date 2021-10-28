---
title: Visual C/C++ 自定义可视化工具兼容性
description: Visual Studio 2019 中的新功能可能与旧版 C/C++ 表达式计算器的加载项和自定义可视化工具不兼容。 请参阅本文以获取详细信息。
ms.custom: SEO-VS-2020
ms.date: 01/28/2019
ms.prod: visual-studio-dev16
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- debugging assertions
- assertions, debugging
- assertions, assertion failures
- Assertion Failed dialog box
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.openlocfilehash: 4948a4a3b82e4b713d590ffc9c8f8283ca495ea4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736909"
---
# <a name="visual-cc-custom-visualizer-compatibility"></a>Visual C/C++ 自定义可视化工具兼容性

从 Visual Studio 2019 开始，C++ 包括改进的调试器，该调试器使用外部 64 位进程托管其内存密集型组件。 作为此更新的一部分，必须更新 C/C++ 表达式计算器的某些扩展才能使其与新的调试器兼容。

如果当前正在使用旧版 C/C++ EE 加载项或 C/C++ 自定义可视化工具，则可以转到“工具” > “选项” > “调试”，然后取消选择“在外部进程中加载调试符号(仅限本机)”，禁用此外部进程   。 如果取消选择此选项，IDE (devenv.exe) 进程中的内存使用量将大幅增加。 因此，如果希望调试大型项目，建议与扩展的所有者合作，使其与此调试选项兼容。

如果你是旧版 C/C++ EE 加载项或 C/C++ 自定义可视化工具的所有者，则可以在 [Concord 可扩展性示例 Wiki](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Worker-Process-Remoting) 上找到有关在工作进程中选择加载扩展的详细信息。 你还可以找到 [C/C++ 自定义可视化工具示例](https://github.com/Microsoft/ConcordExtensibilitySamples/tree/master/CppCustomVisualizer)。