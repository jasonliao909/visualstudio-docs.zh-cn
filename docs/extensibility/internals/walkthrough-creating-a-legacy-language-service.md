---
title: 演练：创建旧版语言服务|Microsoft Docs
description: 了解如何使用托管包框架语言类在 Visual C# 中实现语言服务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- language services [managed package framework], creating
ms.assetid: 6a5dd2c2-261b-4efd-a3f4-8fb90b73dc82
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a0f3e497368047cec2ce1518e7b01f59a8895fbc
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110444"
---
# <a name="walkthrough-creating-a-legacy-language-service"></a>演练：创建旧版语言服务
使用托管包框架 (MPF) 语言类在 中实现语言服务 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 非常简单。 需要 VSPackage 来托管语言服务、语言服务本身和语言分析器。

## <a name="prerequisites"></a>先决条件
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅 [Visual Studio SDK](../../extensibility/visual-studio-sdk.md)。

## <a name="locations-for-the-visual-studio-package-project-template"></a>Visual Studio 包项目模板的位置
 "Visual Studio包Project模板"位于"新建模板"对话框中的三 **Project位置：**

1. 在“Visual Basic 扩展性”之下。 项目的默认语言为 Visual Basic。

2. 在“C# 扩展性”之下。 项目的默认语言为 C#。

3. 在“其他项目类型扩展性”之下。 项目的默认语言为 C++。

### <a name="create-a-vspackage"></a>创建 VSPackage

1. 使用"包"项目模板Visual Studio VSPackage。

    如果要将语言服务添加到现有 VSPackage，请跳过以下步骤并直接转到"创建语言服务类"过程。

2. 输入 MyLanguagePackage 作为项目名称，然后单击"确定 **"。**

    可以使用所需的任何名称。 此处详述的这些过程假定 MyLanguagePackage 作为名称。

3. 选择 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 作为语言和用于生成新密钥文件的选项。 单击“下一步”。

4. 输入相应的公司信息和包信息。 单击“下一步”。

5. 选择 **"菜单命令"。** 单击“下一步”。

    如果不打算支持代码片段，可以单击"完成"并忽略下一步。

6. 输入 **"插入代码****片段"作为命令名称，输入** `cmdidInsertSnippet` 作为 **命令 ID**。 单击“完成”。

    命令 **名称和** 命令 **ID** 可以是所需的任何名称，这些只是示例。

### <a name="create-the-language-service-class"></a>创建语言服务类

1. 在 **解决方案资源管理器** 中，右键单击"MyLanguagePackage"项目，选择"**添加**"和"引用"，然后选择"添加新 **引用"** 按钮。

2. 在"**添加引用"** 对话框中，选择 **".NET"** 选项卡中的 **"Microsoft.VisualStudio.Package.LanguageService"，** 然后单击"确定 **"。**

     只需为语言包项目执行一次此操作。

3. 在 **解决方案资源管理器** 中，右键单击 VSPackage 项目，然后选择"**添加"和**"**类"。**

4. 请确保 **在** 模板列表中选择"类"。

5. 输入 **MyLanguageService.cs** 作为类文件的名称，然后单击"添加 **"。**

     可以使用所需的任何名称。 此处详细介绍的这些过程 `MyLanguageService` 假定为名称。

6. 在 MyLanguageService.cs 文件中，添加以下 `using` 指令。

     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mylanguageservice.cs" id="Snippet1":::
     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mylanguageservice.vb" id="Snippet1":::

7. 修改 `MyLanguageService` 类以从 类 <xref:Microsoft.VisualStudio.Package.LanguageService> 派生：

     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mylanguageservice.cs" id="Snippet2":::
     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mylanguageservice.vb" id="Snippet2":::

8. 将光标置于"LanguageService"上，然后从"编辑 **"、"IntelliSense"** 菜单中选择"**实现抽象类"。** 这会添加实现语言服务类所需的最少方法。

9. 实现抽象方法，如实现旧版 [语言服务 中所述](../../extensibility/internals/implementing-a-legacy-language-service2.md)。

### <a name="register-the-language-service"></a>注册语言服务

1. 打开 MyLanguagePackagePackage.cs 文件并添加以下 `using` 指令：

     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mylanguagepackagepackage.vb" id="Snippet3":::
     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mylanguagepackagepackage.cs" id="Snippet3":::

2. 如注册旧版语言服务 中所述 [注册语言服务类](../../extensibility/internals/registering-a-legacy-language-service1.md)。 这包括 ProvideXX 属性和"提供语言服务"部分。 使用 MyLanguageService，其中本主题使用 TestLanguageService。

### <a name="the-parser-and-scanner"></a>分析器与扫描程序

1. 为语言实现分析和扫描程序，如旧版语言服务 [分析器与扫描程序中所述](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)。

     实现分析和扫描程序完全由你决定，超出了本主题的范围。

## <a name="language-service-features"></a>语言服务功能
 若要在语言服务中实现每个功能，通常从相应的 MPF 语言服务类派生一个类，并在必要时实现任何抽象方法，并重写相应的方法。 创建和/或派生自的类取决于要支持的功能。 旧版语言服务功能 中 [详细介绍了这些功能](../../extensibility/internals/legacy-language-service-features1.md)。 以下过程是从 MPF 类派生类的常规方法。

#### <a name="deriving-from-an-mpf-class"></a>从 MPF 类派生

1. 在 **解决方案资源管理器** 中，右键单击 VSPackage 项目，然后选择"**添加"和**"**类"。**

2. 请确保 **在** 模板列表中选择"类"。

     为类文件输入适当的名称，然后单击"添加 **"。**

3. 在新的类文件中，添加以下 `using` 指令。

     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mysource.cs" id="Snippet4":::
     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mysource.vb" id="Snippet4":::

4. 修改 类以从所需的 MPF 类派生。

5. 添加一个类构造函数，该构造函数采用的参数至少与基类的构造函数相同，并且将 构造函数参数传递给基类构造函数。

     例如，派生自 类的类的构造函数 <xref:Microsoft.VisualStudio.Package.Source> 可能如下所示：

     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mysource.cs" id="Snippet5":::
     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mysource.vb" id="Snippet5":::

6. 如果基 **类** 具有必须实现的任何抽象方法，请从"编辑 **"、IntelliSense** 菜单中选择"实现抽象类"。

7. 否则，将 caret 定位在 类中，并输入要重写的方法。

     例如，键入 `public override` 以查看可在该类中重写的所有方法的列表。

## <a name="see-also"></a>请参阅
- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)
