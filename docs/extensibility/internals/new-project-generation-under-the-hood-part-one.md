---
title: 新Project代：在底层，第一部分|Microsoft Docs
description: 详细了解在 IDE Visual Studio 集成开发环境中 (IDE) 创建自己的项目类型时 (第 2 部分) 。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 66778698-0258-467d-8b8b-c351744510eb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 308ed373ecfbecf29702a338ac6a595775c29d2a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122063195"
---
# <a name="new-project-generation-under-the-hood-part-one"></a>生成新项目：揭秘，第 1 部分
曾经考虑过如何创建自己的项目类型？ 想知道创建新项目时实际会发生什么情况？ 让我们看一看一下，看看真正进行什么。

 有几个任务需要Visual Studio坐标：

- 它显示所有可用项目类型的树。

- 它显示每个项目类型的应用程序模板列表，并允许你选择一个模板。

- 它收集应用程序的项目信息，例如项目名称和路径。

- 它将此信息传递给项目工厂。

- 它在当前解决方案中生成项目项和文件夹。

## <a name="the-new-project-dialog-box"></a>"新建Project对话框
 一切从为新项目选择项目类型时开始。 首先，在"文件"菜单 **Project"** 新建 **文件**"。 此时 **会显示Project"** 新建"对话框，如下所示：

 ![“新建项目”对话框的屏幕截图。](../../extensibility/internals/media/newproject.gif)

 接下来将更详细地介绍。 **"Project类型**"树列出了可以创建的各种项目类型。 选择 Visual **C#** Windows等项目类型时，你将看到一个应用程序模板列表，用于入门。 **Visual Studio安装的** 模板由 Visual Studio，并且可供计算机的任何用户使用。 创建或收集的新模板可以添加到" **我的模板"** 中，并且仅可供你使用。

 选择"**应用程序"Windows** 模板时，对话框中会显示应用程序类型的说明;在这种情况下，是 **一个项目，用于创建** 具有 Windows 用户界面 的应用程序。

 在 **"新建** Project"对话框底部，你将看到几个收集详细信息的控件。 你看到的控件取决于项目类型，但通常包括"项目名称"文本框、"位置"文本框和相关"浏览"按钮，以及"解决方案名称"文本框和相关"创建解决方案的目录 **"复选框。** 

## <a name="populating-the-new-project-dialog-box"></a>填充"新建Project对话框
 "新建 **Project** 对话框从何处获取其信息？ 此处有两种机制在工作，其中一种已弃用。 "**新建Project** 对话框合并并显示从这两种机制获取的信息。

 旧方法 (弃) 使用系统注册表项和 .vsdir 文件。 此机制在打开时Visual Studio运行。 较新的 方法使用 .vstemplate 文件。 此机制Visual Studio初始化时运行，例如通过运行

```
devenv /setup
```

 或

```
devenv /installvstemplates
```

### <a name="project-types"></a>项目类型
 根类型根Project（如 **Visual C#** **和其他** 语言）的位置和名称由系统注册表项确定。 子节点（如数据库和智能设备）的组织将镜像包含相应 .vstemplate 文件的文件夹的层次结构。 让我们先看一下根节点。

#### <a name="project-type-root-nodes"></a>Project键入根节点
 初始化时，它将遍历系统注册表项的子HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\NewProjectTemplates\TemplateDirs以生成和命名类型树Project [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **节点**。 此信息将缓存，供以后使用。 查看 TemplateDirs \\ {FAE04EC1-301F-11D3-BF4B-00C04F79EFBC} \\ /1 键。 每个条目都是一个 VSPackage GUID。 忽略 /1 (项的名称) ，但其存在表明这是Project **根** 节点。 根节点可能又具有多个子项，这些子项控制其Project **树** 中的外观。 让我们看一下其中一些。

##### <a name="default"></a>（默认值）
 这是命名根节点的本地化字符串的资源 ID。 字符串资源位于 VSPackage GUID 选择的附属 DLL 中。

 在示例中，VSPackage GUID 为

 {FAE04EC1-301F-11D3-BF4B-00C04F79EFBC}

 资源 ID (/1) 根节点的 (默认值) #2345

 如果在附近的"包"密钥中查找 GUID 并检查 SatelliteDll 子项，则可以找到包含字符串资源的程序集的路径：

 \<Visual Studio installation path>\VC#\VCSPackages\1033\csprojui.dll

 若要验证这一点，请打开文件资源管理器并将csprojui.dll拖动到Visual Studio目录中。 字符串表显示资源#2345标题 **为 Visual C#**。

##### <a name="sortpriority"></a>SortPriority
 这将确定根节点在根类型树Project **位置**。

 SortPriority REG_DWORD 0x00000014 (20) 

 优先级数越低，树中的位置就越高。

##### <a name="developeractivity"></a>DeveloperActivity
 如果存在此子项，则根节点的位置由"开发人员设置控制。 例如，

 DeveloperActivity REG_SZ VC#

 指示 Visual C# 将是根节点，Visual Studio进行 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 开发。 否则，它将是其他语言的 **子节点**。

##### <a name="folder"></a>文件夹
 如果存在此子项，则根节点将成为指定文件夹的子节点。 可能的文件夹列表显示在键下

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\11.0\NewProjectTemplates\PseudoFolders

 例如，"数据库项目"条目具有与 PseudoFolders 中的"其他类型Project"项匹配的"文件夹"键。 因此，**在Project树****中，** 数据库项目将是"其他类型"Project **节点**。

#### <a name="project-type-child-nodes-and-vstdir-files"></a>Project键入子节点和 .vstdir 文件
 项目类型树中子节点 **Project** 位于 ProjectTemplates 文件夹中文件夹的层次结构后。 对于计算机模板 (**Visual Studio** 安装的模板) ，典型位置为 \Program Files\Microsoft Visual Studio 14.0\Common7\IDE\ProjectTemplates\，对于用户模板 (**我的** 模板) ，典型位置为 \我的文档\Visual Studio 14.0\Templates\ProjectTemplates 。 \\ 合并这两个位置的文件夹层次结构，以创建Project **树**。

 对于Visual Studio C# 开发人员设置，Project **类型** 树如下所示：

 ![使用 C# Project设置在 Visual Studio类型文件夹树的屏幕截图。](../../extensibility/internals/media/projecttypes.png)

 相应的 ProjectTemplates 文件夹如下所示：

 ![使用 C# Project设置Visual Studio模板文件夹树的屏幕截图。](../../extensibility/internals/media/projecttemplates.png)

 当"**新建Project** 对话框打开时，遍历 ProjectTemplates 文件夹，并重新创建其Project类型树中的结构，并做出一 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 些更改： 

- 应用程序类型树Project **根** 节点由应用程序模板确定。

- 节点名称可以本地化，可以包含特殊字符。

- 可以更改排序顺序。

##### <a name="finding-the-root-node-for-a-project-type"></a>查找根类型的Project节点
 当Visual Studio ProjectTemplates 文件夹时，它将打开所有.zip文件并提取任何 .vstemplate 文件。 .vstemplate 文件使用 XML 来描述应用程序模板。 有关详细信息，请参阅新[一代Project：在底层，第二部分](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)。

 \<ProjectType>标记确定应用程序的项目类型。 例如，\CSharp\SmartDevice\WindowsCE\1033\WindowsCE-EmptyProject.zip包含一个包含以下标记的 EmptyProject.vstemplate 文件：

```
<ProjectType>CSharp</ProjectType>
```

 \<ProjectType>标记（而不是 ProjectTemplates 文件夹中的子文件夹）确定应用程序在类型树中的Project **节点**。 在示例中，Windows CE应用程序将显示在 **Visual C#** 根节点下，即使将 WindowsCE 文件夹移动到 VisualBasic 文件夹，Windows CE 应用程序仍将出现在 **Visual C#** 根节点下。

##### <a name="localizing-the-node-name"></a>本地化节点名称
 当Visual Studio ProjectTemplates 文件夹时，它会检查找到的任何 .vstdir 文件。 .vstdir 文件是一个 XML 文件，用于控制"新建项目"对话框中项目 **Project** 的外观。 在 .vstdir 文件中，使用 \<LocalizedName> 标记命名Project **节点**。

 例如，\CSharp\Database\TemplateIndex.vstdir 文件包含以下标记：

```
<LocalizedName Package="{462b036f-7349-4835-9e21-bec60e989b9c}" ID="4598"/>
```

 这将确定命名根节点的本地化字符串（本例中为数据库 ）的附属 DLL 和资源 **ID。** 本地化名称可以包含不适用于文件夹名称的特殊字符，例如 **.NET**。

 如果 \<LocalizedName> 不存在标记，则项目类型由文件夹本身 **SmartPhone2003 命名**。

##### <a name="finding-the-sort-order-for-a-project-type"></a>查找 Project 类型的排序顺序
 若要确定项目类型的排序顺序，请使用 vstdir \<SortOrder> 文件。

 例如，\CSharp\ Windows \ Windows vstdir 文件包含以下标记：

```
<SortOrder>5</SortOrder>
```

 \CSharp\Database\TemplateIndex.vstdir 文件具有一个具有较大值的标记：

```
<SortOrder>5000</SortOrder>
```

 标记中的数字越低 \<SortOrder> ，树中的位置就越高，因此 **Windows** 的节点显示在 **Project 类型** 树中的 **数据库** 节点之前。

 如果没有为 \<SortOrder> 某一项目类型指定任何标记，则该项目类型后面的任何项目类型都将按字母顺序显示 \<SortOrder> 。

 请注意，"我的文档 **" ("我的** 文档") 文件夹中没有 vstdir 文件。 用户应用程序项目类型名称未本地化，并按字母顺序显示。

#### <a name="a-quick-review"></a>快速查看
 让我们修改 "**新建 Project** " 对话框，并创建一个新的用户项目模板。

1. 将 MyProjectNode 子文件夹添加到 \Program Files \ Microsoft Visual Studio 14.0 \ Common7\IDE\ProjectTemplates\CSharp 文件夹中。

2. 使用任意文本编辑器在 MyProjectNode 文件夹中创建 MyProject. vstdir 文件。

3. 将以下行添加到 vstdir 文件：

   ```
   <TemplateDir Version="1.0.0">
       <SortOrder>6</SortOrder>
   </TemplateDir>
   ```

4. 保存并关闭 vstdir 文件。

5. 使用任意文本编辑器在 MyProjectNode 文件夹中创建 MyProject 文件。

6. 将以下行添加到 .vstemplate 文件：

   ```
   <VSTemplate Version="2.0.0" Type="Project" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
       <TemplateData>
           <ProjectType>CSharp</ProjectType>
       </TemplateData>
   </VSTemplate>
   ```

7. 保存 .vstemplate 文件并关闭编辑器。

8. 将 .vstemplate 文件发送到新的压缩 MyProjectNode\MyProject.zip 文件夹。

9. 从 "Visual Studio 命令" 窗口中，键入：

    ```
    devenv /installvstemplates
    ```

   打开 Visual Studio。

10. 打开 "**新建 Project** " 对话框，展开 " **Visual c #** 项目" 节点。

    !["新建 Project" 对话框中的 "Project 类型" 文件夹树的屏幕截图，其中突出显示了展开的 "Visual c # 项目" 节点下的 MyProjectNode。](../../extensibility/internals/media/myprojectnode.png)

    **MyProjectNode** 显示为 Visual c # 的子节点，该节点位于 "Windows" 节点的正下方。

## <a name="see-also"></a>请参阅
- [生成新项目：揭秘，第 2 部分](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)
