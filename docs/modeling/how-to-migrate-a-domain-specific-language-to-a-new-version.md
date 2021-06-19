---
title: 如何：迁移 Domain-Specific 语言项目
description: 提供有关如何将特定于域的语言项目迁移到最新版本的 Visual Studio。
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: 8119f465e32d3754dc446524286e0a2c12dedc40
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387185"
---
# <a name="how-to-migrate-a-domain-specific-language-to-a-new-version"></a>如何：将域特定语言迁移至新版本
可以将定义和使用域特定语言的项目从随 一起分发 [!INCLUDE[vs2010](../misc/includes/vs2010_md.md)] [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 的 版本迁移到 [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] 。

 迁移工具作为 的一部分提供 [!INCLUDE[vssdk_current_long](../misc/includes/vssdk_current_long_md.md)] 。 该工具将转换Visual Studio DSL 工具的项目和解决方案。

 必须显式运行迁移工具：在 Visual Studio 中打开解决方案时，该工具不会自动Visual Studio。 可在以下路径找到工具和详细指南文档：

 **%Program Files%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

## <a name="before-you-migrate-your-dsl-projects"></a>迁移 DSL 项目之前
 迁移工具修改 **.cspro) j Visual Studio .csproj** (和解决方案 (**.sln) 。**

#### <a name="to-prepare-projects-for-migration"></a>准备要迁移的项目。

- 请确保可以 **写入 .csproj** 和 **.sln** 文件。 如果它们受源代码管理，请确保已签出它们。

- 创建要迁移的文件夹的副本。

## <a name="migrating-a-collection-of-projects"></a>迁移项目集合

#### <a name="to-migrate-dsl-projects-and-solutions-to-visual-studio-2010"></a>将 DSL 项目和解决方案迁移到 Visual Studio 2010

1. 启动 DSL 迁移工具。

   - 可以在命令提示符下双击Windows 资源管理器 (文件资源管理器) 工具。 该工具位于以下位置：

        **%ProgramFiles%\Microsoft Visual Studio 2010 SDK\VisualStudioIntegration\Tools\DSLTools\DslProjectsMigrationTool.exe**

2. 选择包含要转换的解决方案和项目的文件夹。

   - 在工具顶部的框中输入路径，或单击"浏览 **"。**

     迁移工具显示定义或使用 DSL 的项目树。 树包含使用 **Microsoft.VisualStudio.Modeling.Sdk** 或 **TextTemplating** 程序集的每个项目。

3. 查看项目树，并取消选中不想转换的项目。

   - 选择项目或解决方案以查看该工具将所做的更改列表。

       > [!NOTE]
       > 文件夹名称旁出现的复选框不起作用。 必须展开文件夹以检查项目和解决方案。

4. 转换项目。

   1. 单击"**转换"。**

        转换每个项目文件之前，项目 **.csproj** 的副本将另 _存为项目_**.vs2008.csproj**

        每个解决方案 **.sln 的副本** 将另存为 _解决方案_**.vs2008.sln**

   2. 调查报告的任何失败转换。

        在文本窗口中报告失败。 此外，树视图在每个无法转换的节点上显示一个红色标志。 可以单击节点获取有关该失败详细信息。

5. **转换解决方案中包含** 成功转换的项目的所有模板。

   1. 打开解决方案。

   2. 单击 **模板页眉中的** "转换所有模板"解决方案资源管理器。

       > [!NOTE]
       > 可以将此步骤作为不必要的步骤。 有关详细信息，请参阅 [如何自动转换所有模板](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\))。

6. 更新转换后的项目中的自定义代码。

   - 尝试生成项目，并调查任何故障。

   - 测试设计器。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="see-also"></a>另请参阅

- [相关的博客文章](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/)