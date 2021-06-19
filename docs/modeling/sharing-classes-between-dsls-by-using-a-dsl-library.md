---
title: 使用 DSL 库在 DSL 之间共享类
description: 了解在可视化Visual Studio建模 SDK 中，可以创建一个不完整的 DSL 定义，该定义可以导入到另一个 DSL 中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c3729e4f386ec5a21c8f30ee3f0df6e7ffa8d891
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385495"
---
# <a name="sharing-classes-between-dsls-by-using-a-dsl-library"></a>使用 DSL 库在 DSL 之间共享类
在 Visual Studio可视化和建模 SDK 中，可以创建一个不完整的 DSL 定义，该定义可以导入到另一个 DSL 中。 这样，你可考虑相似模型的常见部分。

## <a name="creating-and-using-dsl-libraries"></a>创建和使用 DSL 库

#### <a name="to-create-a-dsl-library"></a>创建 DSL 库

1. 创建新的 DSL 项目，然后选择 DSL 库解决方案模板。

     将创建具有空模型的单个 DSL 项目。

2. 可以添加域类、关系、形状等。

     库中的元素不需要形成单个嵌入树。

     若要定义导入程序可以使用的关系，请创建两个域类并创建它们之间的关系。

     请考虑将 **域类的继承** 修饰符设置为 `Abstract` 。

3. 可以添加在 DSL 资源管理器中定义的元素，例如连接生成器。

4. 可以添加需要其他代码的自定义项，例如验证约束。

5. 单击 **"转换所有模板"。**

6. 生成项目。

7. 分发供其他人使用的 DSL 时，必须提供已编译的程序集 (DLL) 文件 `DslDefinition.dsl` 。 可以在 下的文件夹中找到已编译的程序集 `Dsl\bin\*`

#### <a name="to-import-a-dsl-library"></a>导入 DSL 库

1. 在另一个 DSL 定义中的 **DSL 资源管理器** 中，右键单击 DSL 的根类，然后单击"添加新 **DslLibrary 导入"。**

2. 在属性窗口中，设置 **库的文件** 路径。 可以使用相对路径或绝对路径。

    导入的库在 DSL 资源管理器中以只读模式显示。

3. 可以将导入的类用作基类。 在导入 DSL 中创建域类，在 属性窗口中，将"基类"设置为导入的类。

4. 单击“转换所有模板”。

5. 向 DSL 项目添加对 DSL 库项目 (DLL) 程序集的引用。

6. 生成解决方案。

   DSL 库可以导入其他库。 导入库时，其导入也会自动显示在 DSL 资源管理器中。

## <a name="see-also"></a>另请参阅

- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
