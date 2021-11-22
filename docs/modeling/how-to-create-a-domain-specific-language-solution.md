---
title: 如何：创建域特定语言解决方案
description: 了解如何使用专用 Visual Studio 解决方案创建域特定语言 (DSL)。
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
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: dddd3df6669ed401c6097ebd5761ed9a2c5e5660
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664164"
---
# <a name="how-to-create-a-domain-specific-language-solution"></a>如何：创建域特定语言解决方案
使用专用 Visual Studio 解决方案创建域特定语言 (DSL)。

## <a name="prerequisites"></a>先决条件

在开始此过程之前，请安装以下组件：

- Visual Studio
- Visual Studio SDK（安装为 Visual Studio 扩展开发工作负载的一部分）
- 建模 SDK（作为 Visual Studio 组件安装）

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="creating-a-domain-specific-language-solution"></a>创建域特定语言解决方案

1. 通过创建新的“特定于域的语言设计器”项目来启动 DSL 向导。

   > [!NOTE]
   > 你为项目选择的名称最好是有效的 Visual C# 标识符，因为它可能用于生成代码。

   ::: moniker range="vs-2017"

   ![“创建 DSL”对话框](../modeling/media/create_dsldialog.png)

   ::: moniker-end

2. 选择 DSL 模板。

    在“选择域特定语言选项”页上，选择一个解决方案模板，例如“最小语言”。 选择类似于要创建的 DSL 的模板。

    有关解决方案模板的详细信息，请参阅[选择域特定语言解决方案模板](../modeling/choosing-a-domain-specific-language-solution-template.md)。

3. 在“文件扩展名”页上输入文件扩展名。 它在你的计算机以及你想要安装 DSL 的任何计算机中都应该是唯一的。 应看到消息“无应用程序或 Visual Studio 编辑器使用此扩展名”。

   - 如果你在之前没有完全安装的实验性 DSL 中使用了文件扩展名，则可以使用“重置实验性实例”工具清除它们，该工具可在 Visual Studio SDK 菜单中找到。

   - 如果计算机上已完全安装使用此文件扩展名的其他 Visual Studio 扩展，请考虑将其卸载。 在“工具”菜单上，单击“扩展管理器”。

4. 检查并根据需要调整向导剩余页面中的字段。 当你对设置满意时，请单击“完成”。 有关设置的详细信息，请参阅 [DSL 设计器向导页面](#settings)。

    向导创建一个解决方案，该解决方案有两个项目，它们名为 Dsl 和 DslPackage。

   > [!NOTE]
   > 如果你看到一条消息，提示你不要从不受信任的源运行文本模板，请单击“确定”。 你可以将此消息设置为不再次显示。

## <a name="the-dsl-designer-wizard-pages"></a><a name="settings"></a> DSL 设计器向导页
 你可以保留多个字段的默认值不变。 但是，请确保设置了“文件扩展名”字段。

### <a name="solution-settings-page"></a>“解决方案设置”页
 你想使域特定语言基于哪个模板?
选择类似于要创建的 DSL 的模板。 不同的模板提供便利的起点。 选择解决方案模板时，向导会显示说明。 有关解决方案模板的详细信息，请参阅[选择域特定语言解决方案模板](../modeling/choosing-a-domain-specific-language-solution-template.md)。

 你想如何为域特定语言命名?
默认为解决方案名称。 代码是从这个值生成的。 它必须是有效的 C# 类名称。

### <a name="file-extension-page"></a>文件扩展名页
 模板文件应使用什么扩展名?
键入新的文件扩展名。

 验证此文件扩展名是否尚未注册用于此计算机，如下所示：

 在“为处理此扩展名而注册的其他工具和应用程序”下查找。 如果看到消息“无应用程序或 Visual Studio 编辑器使用此扩展名”，则可以使用此文件扩展名。

 如果看到工具或包列表，应执行以下操作之一：

- 键入不同的文件扩展名。

     \- 或 -

- 重置 Visual Studio 实验实例。 这会取消注册以前生成的所有 DSL。 在“开始”菜单上，单击“所有程序”、“Microsoft Visual Studio 2010 SDK”、“工具”，然后单击“重置 Microsoft Visual Studio 2010 实验实例”。 你可以重新生成任何其他你想要再次使用的 DSL。

     \- 或 -

- 如果计算机上已完全安装使用此文件扩展名的 Visual Studio 扩展，请将其卸载。 在“工具”菜单上，单击“扩展管理器”。

### <a name="product-settings-page"></a>产品设置页
 新的域特定语言所属的产品名是什么?
默认为 DSL 名称。

 此值在 Windows 资源管理器（或文件资源管理器）中用于描述具有此文件扩展名的文件。

 产品所属的公司名是什么?
贵公司名称。

 此值将合并到 DSL 包的 AssemblyInfo 属性中。

 此解决方案中项目的根命名空间是什么?
此值默认为由公司和产品名称组成的名称。

### <a name="signing-page"></a>签名页
 创建强名称密钥文件 默认选项是创建新密钥以对 DSL 程序集进行签名。

 使用现有强名称密钥 如果要将 DSL 与其他程序集集成，请使用此选项。

 有关强命名的更多信息，请参阅[创建和使用强命名程序集](/dotnet/standard/assembly/create-use-strong-named)。

## <a name="see-also"></a>另请参阅

- [如何定义域特定语言](../modeling/how-to-define-a-domain-specific-language.md)
- [域特定语言工具术语表](/previous-versions/bb126564(v=vs.100))