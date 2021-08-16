---
title: 如何：迁移 Domain-Specific 语言项目
description: 提供有关如何将域特定语言项目迁移到最新版本的 Visual Studio 的信息。
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: a3787795a1cb2d5a1691bcac79c6c8319e281610f9ffc9e2173d1d0019610059
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121429014"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>如何：将域特定语言迁移至新版本
你可以将定义和使用特定于域的语言的项目 [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)] 从随分发的版本中迁移 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] 。

 迁移工具作为的一部分提供 [!INCLUDE[vssdk_current_long](../misc/includes/vssdk_current_long_md.md)] 。 此工具可转换使用或定义 DSL 工具 Visual Studio 项目和解决方案。

 必须显式运行迁移工具：在 Visual Studio 中打开解决方案时，该工具不会自动启动。 可在以下路径找到工具和详细指南文档：

 **% Program Files% \ Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

## <a name="before-you-migrate-your-dsl-projects"></a>迁移 DSL 项目之前
 迁移工具将 Visual Studio 项目文件 (**.csproj**) 和解决方案文件 (**.sln**) 进行修改。

#### <a name="to-prepare-projects-for-migration"></a>准备要迁移的项目。

- 请确保可以写入 **.csproj** 和 **.sln** 文件。 如果它们处于源代码管理下，请确保它们已签出。

- 创建要迁移的文件夹的副本。

## <a name="migrating-a-collection-of-projects"></a>迁移项目集合

#### <a name="to-migrate-dsl-projects-and-solutions-to-visual-studio-2010"></a>将 DSL 项目和解决方案迁移到 Visual Studio 2010

1. 启动 DSL 迁移工具。

   - 可以在 Windows 资源管理器 " (或" 文件资源管理器 ") 中双击该工具，或从命令提示符处启动该工具。 该工具位于以下位置：

        **% ProgramFiles% \ Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

2. 选择包含要转换的解决方案和项目的文件夹。

   - 在工具顶部的框中输入路径，或单击 " **浏览**"。

     迁移工具显示定义或使用 Dsl 的项目的树。 该树包括使用 **VisualStudio** 或 **TextTemplating** 程序集的每个项目。

3. 查看项目树，并取消选中不希望转换的项目。

   - 选择项目或解决方案以查看该工具将做出的更改列表。

       > [!NOTE]
       > 显示在 "文件夹名称" 旁边的复选框不起作用。 必须展开文件夹才能检查项目和解决方案。

4. 转换项目。

   1. 单击 " **转换**"。

        在转换每个项目文件之前， _project_**. .csproj** 的副本另 _存为_**vs2008**

        每个解决方案的 **副本均保存为** **vs2008。**

   2. 调查报告的任何失败的转换。

        在文本窗口中报告故障。 此外，树视图还会在未能转换的每个节点上显示一个红色标志。 可以单击节点以获取有关该故障的详细信息。

5. 转换包含成功转换的项目的解决方案中的 **所有模板**。

   1. 打开解决方案。

   2. 单击解决方案资源管理器标题中的 " **转换所有模板** " 按钮。

       > [!NOTE]
       > 可以不必要地执行此步骤。 有关详细信息，请参阅 [如何自动转换所有模板](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\))。

6. 更新转换后的项目中的自定义代码。

   - 尝试生成项目，并调查任何故障。

   - 测试设计器。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>另请参阅

- [相关的博客文章](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)