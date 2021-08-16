---
title: 新 Project 生成：在幕后，第一部分：Microsoft Docs
description: 请详细了解 Visual Studio 集成开发环境中所发生的情况 (IDE) 创建自己的项目类型 (2) 的第1部分。
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
ms.openlocfilehash: 777f3c199309bb77038a91cdabbf1fd85d3efcb1fcce7dc76808d04ba9e668fe
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432803"
---
# <a name="new-project-generation-under-the-hood-part-one"></a>生成新项目：揭秘，第 1 部分
您是否曾经想过如何创建您自己的项目类型呢？ 想知道创建新项目时究竟发生了什么情况？ 让我们看一下这一幕后，看看究竟会发生什么。

 有多个任务 Visual Studio 坐标：

- 它显示所有可用项目类型的树。

- 它显示每个项目类型的应用程序模板列表，并允许您选择一个。

- 它会收集应用程序的项目信息，例如项目名称和路径。

- 它将此信息传递到项目工厂。

- 它生成当前解决方案中的项目项和文件夹。

## <a name="the-new-project-dialog-box"></a>"新建 Project" 对话框
 当你为新项目选择项目类型时，就会开始。 首先，单击 "**文件**" 菜单上的 "**新建 Project** "。 此时将显示 "**新建 Project** " 对话框，如下所示：

 ![“新建项目”对话框的屏幕截图。](../../extensibility/internals/media/newproject.gif)

 接下来将更详细地介绍。 " **Project 类型**" 树列出了你可以创建的各种项目类型。 选择类似于 **Visual c # Windows** 的项目类型时，会显示一个应用程序模板列表，可帮助您入门。 **Visual Studio 安装的模板** 由 Visual Studio 安装，并可用于计算机的任何用户。 你创建或收集的新模板可以添加到 **"我的模板"** 中，仅供你使用。

 选择 **Windows 应用程序** 之类的模板时，对话框中将显示应用程序类型的说明;在这种情况下，**用于创建具有 Windows 用户界面的应用程序的项目**。

 在 "**新建 Project** " 对话框的底部，你将看到几个收集详细信息的控件。 您看到的控件取决于项目类型，但通常包括项目 **名称** 文本框、 **位置** 文本框和相关的 **浏览** 按钮，以及 **解决方案名称** 文本框和相关 **的 "创建解决方案的目录** " 复选框。

## <a name="populating-the-new-project-dialog-box"></a>填充 "新建 Project" 对话框
 **新 Project** 对话框从何处获取其信息？ 这里有两种使用方法，其中一项已弃用。 "**新建 Project** " 对话框组合并显示从这两种机制获得的信息。

 旧 (弃用) 方法使用系统注册表项和 vsdir 文件。 此机制在 Visual Studio 打开时运行。 较新的方法使用 .vstemplate 文件。 此机制在初始化 Visual Studio 时运行，例如，通过运行

```
devenv /setup
```

 或

```
devenv /installvstemplates
```

### <a name="project-types"></a>项目类型
 **Project 类型** 的根节点的位置和名称（如 **Visual c #** 和 **其他语言**）由系统注册表项决定。 子节点（如 **数据库** 和 **智能设备**）的组织将镜像包含相应 .vstemplate 文件的文件夹的层次结构。 首先，让我们看一下根节点。

#### <a name="project-type-root-nodes"></a>Project键入根节点
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]初始化时，它将遍历系统注册表项的子项，HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\NewProjectTemplates\TemplateDirs 生成并命名 **Project 类型** 树的根节点。 此信息将被缓存以供以后使用。 查看 TemplateDirs \\ {FAE04EC1-301F-11D3-BF4B-00C04F79EFBC} \\ /1 键。 每个条目都是一个 VSPackage GUID。 子项 (/1) 的名称将被忽略，但其状态指示这是 **Project 类型** 的根节点。 根节点可能反过来具有多个子键，它们控制其在 **Project 类型** 树中的外观。 让我们看看其中的一些问题。

##### <a name="default"></a>（默认值）
 这是命名根节点的本地化字符串的资源 ID。 字符串资源位于 VSPackage GUID 所选的附属 DLL 中。

 在此示例中，VSPackage GUID 是

 {FAE04EC1-301F-11D3-BF4B-00C04F79EFBC}

 并且根节点的资源 ID (默认值)  (/1) 为 #2345

 如果在附近的包密钥中查找 GUID 并检查 SatelliteDll 子项，可以找到包含字符串资源的程序集的路径：

 \<Visual Studio installation path>\VC # \VCSPackages\1033\csprojui.dll

 若要验证这一点，请打开文件资源管理器并将 csprojui.dll 拖动到 Visual Studio 目录中。 字符串表显示资源 #2345 具有 **Visual c #** 的标题。

##### <a name="sortpriority"></a>SortPriority
 这确定根节点在 **Project 类型** 树中的位置。

 SortPriority REG_DWORD 0x00000014 (20) 

 优先级越低，树中的位置越高。

##### <a name="developeractivity"></a>DeveloperActivity
 如果此子项存在，则 "开发人员设置" 对话框控制根节点的位置。 例如，

 DeveloperActivity REG_SZ VC#

 指示如果将 Visual Studio 设置为进行开发，则 Visual c # 将为根节点 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 。 否则，它将是 **其他语言** 的子节点。

##### <a name="folder"></a>文件夹
 如果此子项存在，则根节点将成为指定文件夹的子节点。 可能的文件夹列表会出现在项下面

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\11.0\NewProjectTemplates\PseudoFolders

 例如，数据库项目项的文件夹键与 PseudoFolders 中的其他 Project 类型项匹配。 因此，在 " **Project 类型**" 树中，**数据库项目** 将是 **其他 Project 类型** 的子节点。

#### <a name="project-type-child-nodes-and-vstdir-files"></a>Project键入子节点和 vstdir 文件
 **Project 类型** 树中的子节点的位置遵循 ProjectTemplates 文件夹中的文件夹的层次结构。 对于计算机模板 (**Visual Studio 已安装的模板**) ，典型位置是 \Program Files \ Microsoft Visual Studio 14.0 \ Common7\IDE\ProjectTemplates\，而对于 **模板** (的用户模板，典型位置是 \My Documents \) 14.0 \ Templates\ProjectTemplates \\ 。 这两个位置中的文件夹层次结构将合并，以创建 **Project 类型** 树。

 对于 c # 开发人员设置的 Visual Studio， **Project 类型** 树如下所示：

 ![具有 c # 开发人员设置的 Visual Studio 中的 "Project 类型" 文件夹树的屏幕截图。](../../extensibility/internals/media/projecttypes.png)

 对应的 ProjectTemplates 文件夹如下所示：

 ![具有 c # 开发人员设置的 Visual Studio 中 Project 模板文件夹树的屏幕截图。](../../extensibility/internals/media/projecttemplates.png)

 当 "**新建 Project** " 对话框打开时，将 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 遍历 ProjectTemplates 文件夹，并在 " **Project 类型** 树" 中重新创建其结构，并进行一些更改：

- **Project 类型** 树中的根节点取决于应用程序模板。

- 节点名称可以本地化并且可以包含特殊字符。

- 可以更改排序顺序。

##### <a name="finding-the-root-node-for-a-project-type"></a>查找 Project 类型的根节点
 Visual Studio 遍历 ProjectTemplates 文件夹时，它会打开所有 .zip 文件并提取所有 .vstemplate 文件。 .Vstemplate 文件使用 XML 来描述应用程序模板。 有关详细信息，请参阅[New Project 生成：在后台，第二部分](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)。

 \<ProjectType>标记用于确定应用程序的项目类型。 例如，\CSharp\SmartDevice\WindowsCE\1033\WindowsCE-EmptyProject.zip 文件包含一个 EmptyProject 文件，该文件具有以下标记：

```
<ProjectType>CSharp</ProjectType>
```

 \<ProjectType>标记（而不是 ProjectTemplates 文件夹中的子文件夹）确定 **Project 类型** 树中的应用程序根节点。 在此示例中，Windows CE 应用程序将显示在 **visual c #** 根节点下，即使要将 WindowsCE 文件夹移动到 ""，也会在 **visual c #** 根节点下显示 Windows CE 应用程序。

##### <a name="localizing-the-node-name"></a>本地化节点名称
 Visual Studio 遍历 ProjectTemplates 文件夹时，它会检查它找到的所有 vstdir 文件。 vstdir 文件是一个 XML 文件，用于在 "**新建 Project** " 对话框中控制项目类型的外观。 在 vstdir 文件中，使用 \<LocalizedName> 标记来命名 **Project 类型**"节点。

 例如，\CSharp\Database\TemplateIndex.vstdir 文件包含以下标记：

```
<LocalizedName Package="{462b036f-7349-4835-9e21-bec60e989b9c}" ID="4598"/>
```

 这将确定为根节点命名（在本例中为 **数据库**）的本地化字符串的附属 DLL 和资源 ID。 本地化名称可能包含不能用于文件夹名称（如 **.net**）的特殊字符。

 如果没有 \<LocalizedName> 标记，则项目类型由文件夹本身（ **SmartPhone2003**）命名。

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

   打开“Visual Studio”。

10. 打开 "**新建 Project** " 对话框，展开 " **Visual c #** 项目" 节点。

    !["新建 Project" 对话框中的 "Project 类型" 文件夹树的屏幕截图，其中突出显示了展开的 "Visual c # 项目" 节点下的 MyProjectNode。](../../extensibility/internals/media/myprojectnode.png)

    **MyProjectNode** 显示为 Visual c # 的子节点，该节点位于 "Windows" 节点的正下方。

## <a name="see-also"></a>另请参阅
- [生成新项目：揭秘，第 2 部分](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)
