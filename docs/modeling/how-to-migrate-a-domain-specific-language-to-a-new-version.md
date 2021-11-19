---
title: 如何：迁移域特定语言项目
description: 提供有关如何将域特定语言项目迁移到 Visual Studio 最新版本的信息。
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: bf568d319fad994746cdee7eb9554f88304b4878
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665999"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>如何：将域特定语言迁移至新版本
你可以将定义和使用域特定语言的项目从随 [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] 一起分发的 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 版本中迁移到 [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)]。

 迁移工具作为 [!INCLUDE[vssdk_current_long](../misc/includes/vssdk_current_long_md.md)] 的一部分提供。 此工具可转换使用或定义 DSL 工具的 Visual Studio 项目和解决方案。

 必须显式运行迁移工具：在 Visual Studio 中打开解决方案时，该工具不会自动启动。 可在以下路径找到工具和详细指导文档：

 % Program Files% \ Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe

## <a name="before-you-migrate-your-dsl-projects"></a>迁移 DSL 项目之前
 迁移工具修改 Visual Studio 项目文件 (.csproj) 和解决方案文件 (.sln) 。

#### <a name="to-prepare-projects-for-migration"></a>准备项目以进行迁移。

- 确保可以写入 .csproj 和 .sln 文件 。 如果它们处于源代码管理下，请确保它们已签出。

- 创建一个要迁移的文件夹的副本。

## <a name="migrating-a-collection-of-projects"></a>迁移一个项目集合

#### <a name="to-migrate-dsl-projects-and-solutions-to-visual-studio-2010"></a>将 DSL 项目和解决方案迁移到 Visual Studio 2010

1. 启动 DSL 迁移工具。

   - 可以在 Windows 资源管理器（或文件资源管理器）中双击该工具，或从命令提示符处启动该工具。 该工具位于以下位置：

        %ProgramFiles%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe

2. 选择包含要转换的解决方案和项目的文件夹。

   - 在工具顶部框中输入路径，或单击“浏览”。

     迁移工具显示定义或使用 DSL 的项目树。 该树包括使用 Microsoft.VisualStudio.Modeling.Sdk 或 TextTemplating 程序集的每个项目 。

3. 查看项目树，并取消选中不希望转换的项目。

   - 选择一个项目或解决方案以查看该工具将进行的更改列表。

       > [!NOTE]
       > 显示在文件夹名称旁边的复选框不起作用。 必须展开文件夹才能对项目和解决方案进行检查。

4. 转换项目。

   1. 单击“转换”。

        在转换每个项目文件之前，将 project.csproj 的副本另存为 project.vs2008.csproj

        每个 solution.sln 的副本均另存为 solution.vs2008.sln

   2. 对报告的任何失败转换进行调查。

        在文本窗口中报告失败。 此外，树视图还会在未能转换的每个节点上显示一个红色标志。 可以单击节点以获取有关该失败的详细信息。

5. 在包含成功转换的项目的解决方案中转换所有模板。

   1. 打开解决方案。

   2. 单击解决方案资源管理器标题中的“转换所有模板”按钮。

       > [!NOTE]
       > 可以不必执行此步骤。 有关详细信息，请参阅[如何自动转换所有模板](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\))。

6. 更新已转换项目中的自定义代码。

   - 尝试生成项目，并对任何失败进行调查。

   - 测试设计器。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>另请参阅

- [相关的博客文章](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)