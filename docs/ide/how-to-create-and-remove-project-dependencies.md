---
title: 如何：创建和删除项目依赖项
description: 了解如何使用 Visual Studio 创建和删除项目在其他项目的代码上的依赖项。
ms.custom: SEO-VS-2020
ms.date: 05/09/2022
ms.topic: how-to
f1_keywords:
- VS.ProjectDependenciesDlg
helpviewer_keywords:
- vs.build.projectdependencies
- project dependencies
- builds [Visual Studio], setting up
- project build configurations, dependencies
- dependencies, project
- projects [Visual Studio], dependencies
ms.assetid: e2a0a8ff-dae7-40a8-b774-b88aa5235183
ms.technology: vs-ide-compile
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a39b4f1f06461b409f1261b413498dce1088415e
ms.sourcegitcommit: 8e829a5358a0ce32a81a0f97060237be3c9ab074
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2022
ms.locfileid: "145045183"
---
# <a name="how-to-create-and-remove-project-dependencies"></a>如何：创建和删除项目依赖项

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

生成包含多个项目的解决方案时，可能需要首先生成某些项目，然后才能生成由其他项目使用的代码。 当一个项目使用另一个项目生成的可执行代码时，生成代码的项目则称为使用代码的项目的项目依赖项。 可在“项目依赖项”对话框中定义此类依赖关系。

将项目到项目引用从一个项目添加到另一个项目时，会自动创建项目依赖项。 在执行这些步骤之前，请考虑是否应改为创建项目到项目引用，除了在项目之间创建依赖关系外，还可以创建一个引用，该引用可用于生成使用来自其他项目的类、接口和其他代码实体的代码。 请参阅[管理项目中的引用](managing-references-in-a-project.md#project-to-project-references)。

## <a name="to-assign-dependencies-to-projects"></a>将依赖项分配给项目

1. 在“解决方案资源管理器”中，选择一个项目。

2. 在“项目”菜单上，选择“项目依赖项”。

    “项目依赖项”对话框随即打开。

    ![“Project依赖项”对话框的屏幕截图。](media/vs-2022/project-dependencies.png)

3. 从“依赖项”选项卡上的“项目”下拉菜单中选择一个项目。

4. 在“依赖对象”字段中，选中必须在此项目生成前生成的任何其他项目的复选框。

   解决方案必须包含多个项目才能创建项目依赖项。

## <a name="to-remove-dependencies-from-projects"></a>删除项目中的依赖项

1. 在“解决方案资源管理器”中，选择一个项目。

2. 在“项目”菜单上，选择“项目依赖项”。

     “项目依赖项”对话框随即打开。

3. 从“依赖项”选项卡上的“项目”下拉菜单中选择一个项目。

4. 在“依赖对象”字段中，清除不再属于此项目依赖项的任何其他项目的复选框。

## <a name="to-view-the-build-order"></a>查看生成顺序

在 **“Project依赖项**”对话框中，可以切换到“**生成顺序**”选项卡，以查看解决方案的生成顺序。

若要随时在解决方案中查看生成顺序，请右键单击解决方案节点并选择 **Project生成顺序**。

可以使用 **“生成顺序** ”选项卡查看项目将生成的顺序，但无法直接从此选项卡中更改订单。

列出的顺序是所需的逻辑生成顺序，但在实践中，Visual Studio通过并行生成多个项目进一步优化生成过程。 但是，只要你指定了项目依赖项，任何依赖项目在依赖项完成后才会开始生成。

![“生成顺序”选项卡的屏幕截图。](media/vs-2022/project-build-order.png)

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中生成和清理项目和解决方案](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
- [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
- [了解生成配置](../ide/understanding-build-configurations.md)
- [管理项目和解决方案属性](managing-project-and-solution-properties.md)
