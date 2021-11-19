---
title: 在图表上设置背景图像
description: 了解在可视化Visual Studio建模 SDK 中，可以使用自定义代码为生成的设计器设置背景图像。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: b0e96a74b56226818c96e049df93dba8b1fa721a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663894"
---
# <a name="setting-a-background-image-on-a-diagram"></a>在图表上设置背景图像
在Visual Studio可视化和建模 SDK 中，可以使用自定义代码为生成的设计器设置背景图像。

## <a name="setting-the-background-image"></a>设置背景图像

#### <a name="to-set-a-background-image-for-a-generated-designer"></a>为生成的设计器设置背景图像

1. 将要用作关系图的背景的图像文件复制到当前项目的 Dsl\Resources 目录中。

2. 在 **解决方案资源管理器** 中，右键单击 Dsl\Resources 文件夹，指向"**添加**"，然后单击"现有 **项"。**

3. 在" **添加现有项** "对话框中，浏览到 Dsl\Resources 文件夹。

4. 在"**文件类型"列表中**，单击"**图像文件"。**

5. 单击复制到目录的图像文件，然后单击"添加 **"。**

6. 右键单击 Dsl，然后单击" **属性** "打开 Dsl 项目的属性。

7. 在" **资源** "选项卡 **上，单击"此项目不包含默认资源文件"。单击此处创建一个。**

8. 将图片从资源窗口拖动到资源窗口中，解决方案资源管理器 **文件添加到** 资源文件。

9. 打开“文件”菜单，然后单击该选项以保存项目属性。

10. 验证文件 Dsl\Properties\Resources.resx 是否存在，以及该文件下面是否具有文件 Resources.Designer.cs。

11. 如果缺少 Resources.Designer.cs，请单击中的文件 Resources.resx **解决方案资源管理器。**

12. 在“属性”  窗口中，将 `Custom Tool` 属性设置为 `ResXFileCodeGenerator`。

13. 在 **解决方案资源管理器** 中，右键单击 Dsl 项目，指向"**添加**"，然后单击"新建 **文件夹"。**

14. 将文件夹命名为 **"自定义"。**

15. 右键单击"自定义"文件夹，指向"**添加"，** 然后单击"**新建项"。**

16. 在"**添加新项"对话框** 的"**模板"** 列表中，单击"**代码文件"。**

17. 在"**名称"** 框中，键入 `BackgroundImage.cs` ，然后单击"添加 **"。**

18. 将以下代码复制到 BackgroundImage.cs 文件，从而调整命名空间、关系图类名以及图像文件资源名称。

     将“MyDiagramClass”替换为在 Dsl\GeneratedCode\Diagrams.cs 中定义的关系图分部类的名称。 还可以从文件 Dsl\GeneratedCode\Diagrams.cs 中检索正确的命名空间。

    ```csharp
    using System;
    using Microsoft.VisualStudio.Modeling.Diagrams;

    // Fix the namespace:
    namespace Fabrikam.MyLanguage
    {
      // Fix the Diagram Class name - get it from GeneratedCode\Diagram.cs

      public partial class Language29Diagram
      {
        protected override void InitializeInstanceResources()
        {
          // Fix the Resources namespace and the Image resource name:
          ImageField backgroundField = new ImageField("background",
              Fabrikam.MyLanguage.Properties.Resources.MyPicture);

          backgroundField.DefaultFocusable = false;
          backgroundField.DefaultSelectable = false;
          backgroundField.DefaultVisibility = true;
          backgroundField.DefaultUnscaled = false;

          shapeFields.Add(backgroundField);

          backgroundField.AnchoringBehavior
            .SetTopAnchor(AnchoringBehavior.Edge.Top, 0.01);
          backgroundField.AnchoringBehavior
            .SetLeftAnchor(AnchoringBehavior.Edge.Left, 0.01);
          backgroundField.AnchoringBehavior
            .SetRightAnchor(AnchoringBehavior.Edge.Right, 0.01);
          backgroundField.AnchoringBehavior
            .SetBottomAnchor(AnchoringBehavior.Edge.Bottom, 0.01);

          base.InitializeInstanceResources();
        }
      }
    }
    ```

     有关使用程序代码自定义模型的信息，请参阅在程序代码中导航和更新 [模型](../modeling/navigating-and-updating-a-model-in-program-code.md)。

## <a name="see-also"></a>另请参阅

- [定义形状和连接线](../modeling/defining-shapes-and-connectors.md)
- [自定义文本和图像字段](../modeling/customizing-text-and-image-fields.md)
- [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [编写代码以自定义域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
