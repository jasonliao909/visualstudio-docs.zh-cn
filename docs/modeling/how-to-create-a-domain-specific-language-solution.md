---
title: 如何：创建域特定语言解决方案
description: 了解如何使用专用化解决方案 (DSL) 域Visual Studio语言。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.designerwizard
helpviewer_keywords:
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools], creating domain-specific language
- Domain-Specific Language Tools, creating solutions
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ce03349a5179e8dd78220fffd1ff6b21d1a3b495
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387315"
---
# <a name="how-to-create-a-domain-specific-language-solution"></a>如何：创建域特定语言解决方案
DSL (域) 是使用专用化 Visual Studio 解决方案创建的。

## <a name="prerequisites"></a>先决条件

在开始此过程之前，请安装以下组件：

- Visual Studio
- Visual Studio扩展 (工作负荷中安装的 Visual Studio **SDK**) 
- 建模 SDK (安装为Visual Studio组件) 

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="creating-a-domain-specific-language-solution"></a>创建 Domain-Specific 语言解决方案

1. 通过创建新的 DSL 项目来启动 **DSL 特定于域的语言设计器** 向导。

   > [!NOTE]
   > 最好为项目选择的名称应该是有效的 Visual C# 标识符，因为它可用于生成代码。

   ::: moniker range="vs-2017"

   ![“创建 DSL”对话框](../modeling/media/create_dsldialog.png)

   ::: moniker-end

2. 选择 DSL 模板。

    在"**选择Domain-Specific选项**"页上，选择一个解决方案模板，例如"最小 **语言"。** 选择与要创建的 DSL 类似的模板。

    有关解决方案模板详细信息，请参阅 [选择Domain-Specific语言解决方案模板](../modeling/choosing-a-domain-specific-language-solution-template.md)。

3. 在"文件扩展名"页上 **输入文件扩展** 名。 它在计算机中以及要安装 DSL 的任何计算机中应是唯一的。 应会看到消息"没有 **应用程序或Visual Studio编辑器使用此扩展。**

   - 如果在尚未完全安装的实验性 DSL 中使用过文件扩展名，可以使用"重置实验实例"工具将其清除，该工具可在Visual Studio SDK 菜单中找到。

   - 如果Visual Studio扩展名的另一个扩展名已完全安装在计算机上，请考虑卸载它。 在"**工具"菜单** 上，单击"**扩展管理器"。**

4. 检查向导其余页中的字段，并在必要时进行调整。 如果对设置满意，请单击"完成 **"。** 有关设置详细信息，请参阅向导DSL 设计器 [页](#settings)。

    向导创建一个解决方案，该解决方案有两个项目，它们名为 **Dsl** 和 **DslPackage**。

   > [!NOTE]
   > 如果看到一条消息，提醒你不要从不受信任的源运行文本模板，请单击"确定 **"。** 可以将此消息设置为不再次显示。

## <a name="the-dsl-designer-wizard-pages"></a><a name="settings"></a> "DSL 设计器向导"页
 可以将多个字段保留其默认值不变。 但是，请确保设置"文件扩展名"字段。

### <a name="solution-settings-page"></a>"解决方案设置"页
 **希望将域特定语言基于哪个模板？**
选择与要创建的 DSL 类似的模板。 不同的模板提供了方便的起始点。 选择解决方案模板时，向导将显示说明。 有关解决方案模板详细信息，请参阅 [选择Domain-Specific语言解决方案模板](../modeling/choosing-a-domain-specific-language-solution-template.md)。

 **想要为域特定语言命名什么？**
默认为解决方案名称。 从此值生成代码。 它必须作为 C# 类名有效。

### <a name="file-extension-page"></a>"文件扩展名"页
 **模型文件应该使用什么扩展名？**
键入新的文件扩展名。

 验证此文件扩展名是否尚未注册以用于此计算机，如下所示：

 在" **已注册以处理此扩展的其他工具和应用程序"下查看**。 如果看到消息"没有应用程序或 **Visual Studio编辑器使用此扩展名**，可以使用此文件扩展名。

 如果看到工具或包的列表，应执行以下操作之一：

- 键入其他文件扩展名。

     \- 或 -

- 重置Visual Studio实例。 这会取消注册之前生成的所有 DSL。 在"**开始"** 菜单上，单击"所有程序 **"，Microsoft Visual Studio 2010 SDK** **、"工具**"，然后单击"重置 Microsoft Visual Studio **2010 试验实例"。** 可以重新生成想要再次使用的其他任何 DSL。

     \- 或 -

- 如果Visual Studio扩展名的扩展名已完全安装在计算机上，请将其卸载。 在"**工具"菜单** 上，单击"**扩展管理器"。**

### <a name="product-settings-page"></a>"产品设置"页
 **新域特定语言所属的产品的名称是什么？**
默认为 DSL 名称。

 此值在 Windows 资源管理器 (或 文件资源管理器) 用于描述具有此文件扩展名的文件。

 **产品所属的公司的名称是什么？**
公司名称。

 此值将合并到 DSL 包的 AssemblyInfo 属性中。

 **此解决方案中项目的根命名空间是什么？**
这默认为由你的公司和产品名称构成的名称。

### <a name="signing-page"></a>"签名"页
 **创建强名称密钥文件** 默认选项是创建新密钥以对 DSL 程序集进行签名。

 **使用现有的强名称密钥** 如果要将 DSL 与其他程序集集成，请使用此选项。

 有关强命名详细信息，请参阅 [创建和使用Strong-Named程序集](/dotnet/standard/assembly/create-use-strong-named)。

## <a name="see-also"></a>另请参阅

- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)
- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))