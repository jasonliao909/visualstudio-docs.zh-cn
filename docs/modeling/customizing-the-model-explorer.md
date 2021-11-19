---
title: 自定义模型资源管理器
description: 了解如何为域特定语言设计器更改资源管理器的外观和行为。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671886"
---
# <a name="customizing-the-model-explorer"></a>自定义模型资源管理器
可以为域特定语言设计器更改资源管理器的外观和行为，如下所示：

- 更改窗口标题。

- 更改选项卡图标。

- 更改节点图标。

- 隐藏节点。

## <a name="changing-the-window-title"></a>更改窗口标题
 若要更改生成的资源管理器的窗口标题，请在“DSL 资源管理器”中选择“资源管理器行为”，然后在“属性”窗口中将“标题”属性设置为所需的标题   。

## <a name="changing-the-tab-icon"></a>更改选项卡图标
 若要更改资源管理器的选项卡图标，请使用 .bmp 文件中的 16x16 像素图标。 将图标文件放在 \DslPackage\Resources\ 文件夹中，然后将文件名更改为 ModelExplorerToolWindowBitmaps.bmp。 例如，可以将 Visual Studio setup.ico 图标文件更改为 .bmp 格式并将其重命名为 DSLLanguageName\DslPackage\Resources\ModelExplorerToolWindowBitmaps.bmp。 当此图标与解决方案资源管理器停靠在一起时，生成的设计器将在资源管理器的选项卡上显示该图标。

## <a name="setting-custom-icons-on-explorer-nodes"></a>在资源管理器节点上设置自定义图标
 可以使用资源管理器节点设置自定义资源管理器中的节点。 以下过程演示如何向节点添加图标。

#### <a name="to-add-an-icon-to-an-explorer-node"></a>向资源管理器节点添加图标

1. 使用任务流解决方案模板创建 [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] 解决方案。

2. 将包含 16x16 像素图标的 .bmp 文件放入解决方案的 Dsl\Resources 文件夹中。

3. 在“DSL 资源管理器”中，右键单击“资源管理器行为”，然后单击“添加新的资源管理器节点设置”  。

    ExplorerNodeSettings 节点将显示在“自定义节点设置”节点下 。

4. 选择“ExplorerNodeSettings”，然后在“属性”窗口中，将“类”设置为“参与者”   。

5. 将“要显示的图标”设置为图标文件的路径。

6. 转换所有模板，然后生成并运行解决方案。

7. 在生成的设计器中，打开示例关系图。

    资源管理器应会显示三个带有图标的“参与者”节点。

> [!NOTE]
> 如果为生成的资源管理器中显示的任何元素都设置了节点图标，则所有资源管理器节点都将显示该图标。 如果未设置图标，节点将显示默认图标。

## <a name="changing-the-name-displayed-on-an-explorer-node"></a>更改资源管理器节点上显示的名称
 可以更改模型元素名称在资源管理器中的显示方式。 以下过程显示了如何在注释节点中显示由“注释”引用的“任务”的名称 。

#### <a name="to-display-a-property"></a>显示属性

1. 打开在前面的过程中创建的解决方案。

2. 通过将具有属性名称“Subjects”的角色的多重性设置为 0..1，确保“注释”仅引用单个域类 。 属性名称应为“Subject”，关系名称应变为“CommentReferencesSubject” 。

3. 在“DSL 资源管理器”中，右键单击“资源管理器行为”，然后单击“添加新的资源管理器节点设置”  。

     ExplorerNodeSettings 节点将显示在“自定义节点设置”节点下 。

4. 选择“ExplorerNodeSettings”，然后在“属性”窗口中，将“类”设置为“注释”   。

5. 右键单击“注释”节点，然后单击“添加新属性路径” 。

     将出现一个名为“显示的属性”的新节点。

6. 选择“显示的属性”，然后在“属性”窗口中，单击“属性路径”字段值  。 依次选择“注释”、“CommentReferencesSubject”、“FlowElement”  。 生成的路径应类似于 CommentReferencesSubject.Subject/!Subject。

7. 在“属性”字段值中，选择“名称” 。

8. 转换所有模板，然后生成并运行解决方案。

9. 在生成的设计器中，打开示例关系图。

10. 在图表上的注释元素和 Task1 元素之间绘制一个“注释连接器” 。

     资源管理器节点应将注释显示为“Task1”。

## <a name="hiding-nodes"></a>隐藏节点
 将节点的路径添加到“DSL 资源管理器”的“隐藏节点”节点，可以隐藏资源管理器中的节点 。 以下过程显示了如何隐藏“注释”节点。

#### <a name="to-hide-an-explorer-node"></a>隐藏资源管理器节点

1. 打开在前面的过程中创建的解决方案。

2. 在“DSL 资源管理器”中，右键单击“资源管理器行为”然后单击“添加新域路径”  。

     “域路径”节点将出现在“隐藏节点”下 。

3. 选择“域路径”，然后在“属性”窗口中，单击“路径定义”字段值  。 依次选择“FlowGraph”、“FlowGraphHasComments” 。 生成的路径应类似于 FlowGraphHasComments.Comments

4. 转换所有模板，然后生成并运行解决方案。

5. 在生成的设计器中，打开示例关系图。

     资源管理器应仅显示“参与者”节点，不应显示“注释”节点 。

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))