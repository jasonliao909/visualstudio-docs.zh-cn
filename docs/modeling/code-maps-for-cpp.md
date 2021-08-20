---
title: 请参阅 c + + 源文件和头文件之间的依赖关系
description: 提供有关 c + + 项目的代码图的信息。
ms.date: 05/16/2018
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
ms.custom: SEO-VS-2020
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 572f0daff0d4ca114f3c718f0334eeced32e42fc
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122157561"
---
# <a name="code-maps-for-c-projects"></a>C + + 项目的代码映射

如果要创建更多 C++ 项目的完整代码图，请在这些项目上设置浏览信息编译器选项 (**/FR**)。 否则，将出现一条消息并提示你设置此选项。 如果选择“确定” ，就只会为当前代码图设置选项。 可以选择隐藏所有之后的代码图的信息。

打开包含 Visual C++ 项目的解决方案时，可能需要花一些时间来更新 IntelliSense 数据库。 在此期间，你可能无法为标头 (*.h* 或) 文件创建代码图， `#include` 直到 IntelliSense 数据库完成更新。 你可在 Visual Studio 状态栏中监视更新进度。

- 若要查看解决方案中所有源文件和头文件之间的依赖关系，请选择 "**体系结构**  >  **生成包含文件 Graph**。

   ![本机代码的依赖项关系图](../modeling/media/dependencygraphgeneral_nativecode.png)

- 若要查看当前打开文件和相关的源文件以及头文件之间的依赖关系，请打开相关的源文件或头文件。 在文件内的任何地方打开文件快捷菜单。 选择“生成包含文件的关系图” 。

   ![.h 文件的第一级依赖项关系图](../modeling/media/dependencygraph_native_firstlevel.png)

## <a name="troubleshoot-code-maps-for-c-and-c-code"></a>C 和 c + + 代码的代码图疑难解答

C 和 C++ 代码不支持这些项：

- 基类型不会显示在包含父层次结构的图中。

- 大多数“显示”  菜单项不适用于 C 和 C++ 代码。

当你为 C 和 c + + 代码创建代码图时，可能会出现这些问题：

|**问题**|可能的原因 |**分辨率**|
|-|-|-|
|未能生成代码图。|解决方案中没有项目成功生成过。|修复出现的生成错误，然后重新生成代码图。|
|尝试从 "**体系结构**" 菜单生成代码图时，Visual Studio 将停止响应。|程序数据库 (.pdb) 文件可能已损坏。<br /><br /> pdb 文件将存储调试信息，例如，类型、方法和源文件信息。|重新生成解决方案，然后重试。|
|禁用 IntelliSense 浏览器数据库的某些设置。|可能会在 "Visual Studio **选项**" 对话框中禁用某些 IntelliSense 设置。|打开设置以启用它们。<br /><br /> 请参阅 [选项、文本编辑器、C/c + +、高级](../ide/reference/options-text-editor-c-cpp-advanced.md)。|
|消息“未知方法”  将出现在方法节点上。<br /><br /> 由于无法解析方法的名称，导致出现此问题。|二进制文件可能没有基重定位表。|在链接器中打开 **/FIXED:NO** 选项。|
||无法生成程序数据库 (.pdb) 文件。<br /><br /> pdb 文件将存储调试信息，例如，类型、方法和源文件信息。|在链接器中打开 **/DEBUG** 选项。|
||无法在预期位置打开或找到 .pdb 文件。|确保 .pdb 文件位于预期位置。|
||已从 .pdb 文件中去除调试信息。|如果链接器中已使用 **/PDBSTRIPPED** 选项，则改为包含完整的 .pdb 文件。|
||调用方不是函数，它是二进制文件中的形式转换 (thunk) 或数据节中的指针。|当调用方是形式转换 (thunk) 时，尝试使用 `_declspec(dllimport)` 以避免形式转换 (thunk)。|

## <a name="see-also"></a>请参阅

- [使用代码图映射依赖关系](../modeling/map-dependencies-across-your-solutions.md)
