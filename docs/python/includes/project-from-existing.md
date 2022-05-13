---
ms.topic: include
ms.openlocfilehash: 5634f588255970c9b95c0ed461fad8e04a1af5cb
ms.sourcegitcommit: caf5ca17efde4dc4de8b1bdfbe7770f6d705024d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2022
ms.locfileid: "145017852"
---
1. 启动 Visual Studio，然后选择“文件” > “新建” > “项目”  。

1. 在“新建项目”对话框中，搜索“Python”，选择“从现有的 Python 代码”模板，为项目提供名称和位置，然后选择“确定”  。

1. 在出现的向导中，设置现有代码的路径，设置文件类型筛选器，并指定项目需要的任何搜索路径，然后选择“下一步”。 如果不知道搜索路径是什么，则将该字段留空。

    :::image type="content" source="../media/projects-from-existing-1.png" alt-text="“从现有代码”窗口新建Project的屏幕截图，步骤 1。":::

1. 在下一个对话框中，选择项目的启动文件，然后选择“下一步”。 如有必要，请选择环境;否则接受默认值。

    > [!Note]
    > 对话框仅显示根文件夹中的文件;如果所需的文件位于子文件夹中，请将启动文件留空，并在 **稍后解决方案资源管理器 (** 描述下一) 中设置该文件。

    :::image type="content" source="../media/projects-from-existing-2.png" alt-text="“从现有代码”窗口新建Project“步骤 2 的屏幕截图。":::

1. 选择要在其中保存项目文件（磁盘上的 `.pyproj` 文件）的位置。 如果适用，还可以包括虚拟环境的自动检测，并为不同的 Web 框架自定义项目。 如果不确定这些选项，请保持它们设置为默认值。

    :::image type="content" source="../media/projects-from-existing-3.png" alt-text="从“现有代码”窗口创建“新建Project”步骤 3 的屏幕截图。":::

1. 选择“完成”，Visual Studio 将创建项目并在解决方案资源管理器中打开该项目 。 如果要将文件移到`.pyproj`其他位置，**请在解决方案资源管理器** 中选择该文件，然后选择 **FileSave** >  As。 此操作更新项目中的文件引用，但不移动任何代码文件。

1. 若要设置其他启动文件，请在 **解决方案资源管理器** 中找到该文件，右键单击该文件，然后选择“**设置为启动文件**”。
