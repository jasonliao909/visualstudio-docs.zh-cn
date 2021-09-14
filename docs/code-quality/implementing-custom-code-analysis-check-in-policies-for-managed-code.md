---
title: 托管代码的自定义代码分析签入策略
ms.date: 11/04/2016
description: 了解如何创建自定义的代码分析签入策略。 了解如何确保托管Visual Studio符合项目Azure DevOps策略。
ms.custom: SEO-VS-2020
ms.topic: how-to
f1_keywords:
- vs.code.analysis.selecttfsrulesets
- vs.code.analysis.browsefortfsruleset
- vs.code.analysis.policyeditor
ms.assetid: fd029003-5671-4b24-8b6f-032e0a98b2e8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- dotnet
ms.openlocfilehash: 07c393bd9ff0a16bf2c2692a2b92425138af5554
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601290"
---
# <a name="implement-custom-code-analysis-check-in-policies-for-managed-code"></a>实现托管代码的自定义代码分析签入策略

代码分析签入策略指定一组规则，其中Azure DevOps项目的成员必须在源代码中运行这些规则，然后才能签入到版本控制。 Microsoft 提供了一组 *标准规则集，* 用于将代码分析规则分组到功能区域。 *自定义签入策略规则集* 指定一组特定于项目的代码分析规则。 规则集存储在 .ruleset 文件中。

签入策略在项目Azure DevOps级别设置，由版本控制树中 .ruleset 文件的位置指定。 对团队策略自定义规则集的版本控制位置没有限制。

代码分析针对每个项目的属性窗口中的单个代码项目进行配置。 代码项目的自定义规则集由本地计算机上 .ruleset 文件的物理位置指定。 如果所指定的 .ruleset 文件位于代码项目所在的驱动器上，则 Visual Studio 将在项目配置中使用文件的相对路径。

创建一个Azure DevOps自定义规则集的建议做法是，将签入策略 .ruleset 文件存储在不是任何代码项目一部分的特殊文件夹中。 如果将文件存储在专用文件夹中，可以应用限制谁可以编辑规则文件的权限，并且可以轻松地将包含项目的目录结构移动到另一个目录或计算机。

## <a name="create-the-project-custom-check-in-rule-set"></a>创建Project签入规则集

若要为 Azure DevOps项目创建自定义规则集，请首先为 源代码管理器 中的签入 **策略规则集创建一个特殊文件夹**。 然后创建规则集文件，然后将该文件添加到版本控制。 最后，指定规则集作为项目的代码分析签入策略。

> [!NOTE]
> 若要在项目Azure DevOps文件夹，必须先将项目根映射到本地计算机上的位置。

### <a name="to-create-the-version-control-folder-for-the-check-in-policy-rule-set"></a>为签入策略规则集创建版本控制文件夹

1. 在团队资源管理器，展开项目节点，然后单击"**源代码管理"。**

2. 在"**文件夹"** 窗格中，右键单击项目，然后单击"新建 **文件夹"。**

3. 在主源代码管理窗格中，右键单击" **新建** 文件夹"，单击"重命名 **"，然后** 键入规则集文件夹的名称。

### <a name="to-create-the-check-in-policy-rule-set"></a>创建签入策略规则集

1. 在 **“文件”** 菜单上，指向 **“新建”** ，然后单击 **“文件”** 。

2. 在"**类别"列表中**，单击"常规 **"。**

3. 在"**模板"列表中**，双击 **"Code Analysis规则集"。**

4. [指定要](../code-quality/how-to-create-a-custom-rule-set.md) 包括在规则集的规则，然后将规则集文件保存到创建的规则集文件夹中。

### <a name="to-add-the-rule-set-file-to-version-control"></a>将规则集文件添加到版本控制

1. 在 **源代码管理器** 中，右键单击新文件夹，然后单击"**将项添加到文件夹"。**

     有关详细信息，请参阅[Git 和 Azure Repos。](/azure/devops/repos/git/overview?view=vsts&preserve-view=true)

2. 单击创建的规则集文件，然后单击"完成 **"。**

     该文件将添加到源代码管理并签出给你。

3. 在 **"源代码管理器** 详细信息"窗口中，右键单击文件名，然后单击"**签入挂起的更改"。**

4. 在 **"签入"对话框中**，可以选择添加注释，然后单击"**签入"。**

    > [!NOTE]
    > 如果为 Azure DevOps 项目配置了代码分析签入策略，并且已选择"强制签入"以仅包含属于当前解决方案 **的文件**，将触发策略失败警告。 在"策略失败"对话框中，选择" **替代策略失败"并继续签入**。 添加所需的注释，然后单击"确定 **"。**

### <a name="to-specify-the-rule-set-file-as-the-check-in-policy"></a>将规则集文件指定为签入策略

1. 在"**团队"** 菜单上 **，Project 设置**，然后单击"**源代码管理"。**

2. 单击 **"签入策略"，** 然后单击"添加 **"。**

3. 在 **"签入策略"** 列表中，双击"Code Analysis"，并确保选中"为托管Code Analysis强制执行策略"复选框。 

4. 在" **运行此规则集"列表中** ，单击 **\<Select Rule Set from Source Control>** 。

5. 在版本控制中键入签入策略规则集文件的路径。

     路径必须符合以下语法：

     **$/** `TeamProjectName` **/** `VersionControlPath`

    > [!NOTE]
    > 可以使用 以下过程之一复制 **路径源代码管理器：**

    - 在" **文件夹** "窗格中，单击包含规则集文件的文件夹。 复制"源"框中显示的文件夹的版本 **控制路径，** 并手动键入规则集文件的名称。

    - 在详细信息窗口中，右键单击规则集文件，然后单击"属性 **"。** 在" **常规"** 选项卡上，复制"服务器名称 **"中的值**。

## <a name="synchronize-code-projects-to-the-check-in-policy-rule-set"></a>将代码项目同步到签入策略规则集

在代码项目的"属性"对话框中，将项目签入策略规则集指定为代码项目配置的代码分析规则集。 如果规则集与代码项目位于同一驱动器上，则相对路径用于在从文件对话框中选择路径时指定规则集。 相对路径使项目属性设置可移植到使用类似本地版本控制结构的其他计算机。

### <a name="to-specify-a-project-rule-set-as-the-rule-set-of-a-code-project"></a>将项目规则集指定为代码项目的规则集

1. 如有必要，请从版本控制中检索签入策略规则集文件夹和文件。

   可以通过右键单击规则 **集源代码管理器** 然后单击"获取最新版本"，在"规则集" **中执行此步骤**。

2. 在 **解决方案资源管理器** 中，右键单击代码项目，然后单击"属性 **"。**

3. **单击"Code Analysis"。**

4. 如有必要，请单击"配置"和"平台 **"列表中****相应的** 选项。

::: moniker range="vs-2017"

5. 若要每次使用指定的配置生成代码项目时运行代码分析，请选择"生成时 **启用Code Analysis代码分析**" 。

::: moniker-end

::: moniker range=">=vs-2019"

5. 若要每次使用指定的配置生成代码项目时运行代码分析，请在"二进制分析器"部分选择"生成时 **运行**"。

::: moniker-end

6. 在" **运行此规则集"列表中** ，单击 **\<Browse>** 。

8. 选择签入策略规则集文件的本地版本。
