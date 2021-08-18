---
title: 自定义模型资源管理器
description: 了解如何更改特定于域的语言设计器的资源管理器的外观和行为。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.dsldesigner.explorerbehavior
helpviewer_keywords:
- Domain-Specific Language Tools, Domain-Specific Language Explorer
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 6c3163910921bbf5d84e14df9554ca43cde17427
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122048032"
---
# <a name="customizing-the-model-explorer"></a>自定义模型资源管理器
可以更改特定于域的语言设计器的资源管理器的外观和行为，如下所示：

- 更改窗口标题。

- 更改选项卡图标。

- 更改节点的图标。

- 隐藏节点。

## <a name="changing-the-window-title"></a>更改窗口标题
 若要更改生成的资源管理器的窗口标题，请在 **DSL** 资源管理器中选择"资源管理器行为"，然后在"属性"窗口中，将 **"标题**"属性设置为想要的标题。

## <a name="changing-the-tab-icon"></a>更改选项卡图标
 若要更改资源管理器的选项卡图标，请使用一个 16x16 像素.bmp图标。 将图标文件放在 \DslPackage\Resources\ 文件夹中，然后将文件名更改为 **ModelExplorerToolWindowBitmaps.bmp。** 例如，你可以将 Visual Studio setup.ico 图标文件更改为.bmp格式，并将其重命名为 **DSLLanguageName\DslPackage\Resources\ModelExplorerToolWindowBitmaps.bmp。** 生成的设计器将在资源管理器的选项卡上显示此图标，该图标与 **解决方案资源管理器。**

## <a name="setting-custom-icons-on-explorer-nodes"></a>在资源管理器节点上设置自定义图标
 可以使用资源管理器节点设置自定义资源管理器中的节点。 以下过程演示如何向节点添加图标。

#### <a name="to-add-an-icon-to-an-explorer-node"></a>向资源管理器节点添加图标

1. 使用 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] Task Flow 解决方案模板创建解决方案。

2. 在解决方案.bmp **Dsl\Resources** 文件夹中，放入包含 16x16 像素图标的 16x16 像素的文件。

3. 在 **DSL 资源管理器中**，右键单击"**资源管理器行为**"，然后单击"添加新 **资源管理器节点设置"。**

    **ExplorerNodeSettings** 节点显示在"自定义节点"节点 **设置** 下。

4. 选择 **"资源管理器""节点""** 设置"，然后在"属性 **"** 窗口中，将 **"类"设置为**"执行 **组件"。**

5. 将 **"要显示的图标"** 设置为图标文件的路径。

6. 转换所有模板，然后生成并运行解决方案。

7. 在生成的设计器中，打开示例关系图。

    资源管理器应显示三个 **包含** 图标的 Actor 节点。

> [!NOTE]
> 如果为生成的资源管理器中显示的任何元素设置了节点图标，则所有资源管理器节点将显示该图标。 如果未设置任何图标，节点将显示默认图标。

## <a name="changing-the-name-displayed-on-an-explorer-node"></a>更改资源管理器节点上显示的名称
 可以更改模型元素名称在资源管理器中的显示方式。 以下过程演示如何在注释节点中显示注释引用的任务的名称。 

#### <a name="to-display-a-property"></a>显示属性

1. 打开在之前过程中创建的解决方案。

2. 确保 Comment **仅引用单个** 域类，只需将属性名称 **"主题** "的角色的乘数设置为 0..1。 属性名称应变为 **Subject**，关系名称应变为 **CommentReferencesSubject**。

3. 在 **DSL 资源管理器中**，右键单击"**资源管理器行为**"，然后单击"添加新 **资源管理器节点设置"。**

     **ExplorerNodeSettings** 节点显示在"自定义节点"节点 **设置** 下。

4. 选择 **"资源管理器""节点""** 设置"，然后在"属性 **"** 窗口中，将 **"类"** 设置为"**注释"。**

5. 右键单击"**注释"** 节点，然后单击"**添加新属性路径"。**

     将出现名为"属性显示" **的新节点**。

6. 选择 **"显示的属性**"，然后在"属性 **"** 窗口中，单击"属性 **路径"的值字段**。 选择 **"注释**"，**然后选择"CommentReferencesSubject"，** 然后选择 **"FlowElement"。** 生成的路径应类似于 **CommentReferencesSubject.Subject/！主题**。

7. 在"属性"的值 **字段中，** 选择"名称 **"。**

8. 转换所有模板，然后生成并运行解决方案。

9. 在生成的设计器中，打开示例关系图。

10. 在 **关系图上的注释** 元素和 **Task1 元素之间** 绘制注释连接器。

     资源管理器节点应将注释显示为 **Task1**。

## <a name="hiding-nodes"></a>隐藏节点
 可以通过将节点的路径添加到 DSL 资源管理器 的"隐藏节点"节点来 **隐藏资源管理器中的节点**。 以下过程演示如何隐藏 **注释** 节点。

#### <a name="to-hide-an-explorer-node"></a>隐藏资源管理器节点

1. 打开在之前过程中创建的解决方案。

2. 在 **DSL 资源管理器中**，右键单击"**资源管理器行为"，** 然后单击"**添加新域路径"。**

     " **域路径"** 节点显示在"隐藏 **节点"下**。

3. 选择 **"域路径**"，然后在"属性 **"** 窗口中，单击"路径定义 **"的值字段**。 选择 **"FlowGraph"，** 然后选择 **"FlowGraphHasComments"。** 生成的路径应类似于 **FlowGraphHasComments.Comments**

4. 转换所有模板，然后生成并运行解决方案。

5. 在生成的设计器中，打开示例关系图。

     资源管理器应只显示 **Actors** 节点，并且不应显示 **"注释"** 节点。

## <a name="see-also"></a>请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))