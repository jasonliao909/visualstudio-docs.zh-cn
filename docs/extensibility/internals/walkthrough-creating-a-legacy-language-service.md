---
title: 演练：创建旧版语言服务 |Microsoft Docs
description: '了解如何使用托管包框架语言类在 Visual c # 中实现语言服务。'
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664295"
---
# <a name="walkthrough-creating-a-legacy-language-service"></a>演练：创建旧版语言服务
使用托管包框架 (MPF) 语言类实现中的语言服务 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 非常简单。 你需要一个 VSPackage 来托管语言服务、语言服务本身和语言分析器。

## <a name="prerequisites"></a>先决条件
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅 [Visual Studio SDK](../../extensibility/visual-studio-sdk.md)。

## <a name="locations-for-the-visual-studio-package-project-template"></a>Visual Studio 包项目模板的位置
 可以在 "**新建 Project** " 对话框中的三个不同模板位置找到 Visual Studio 包 Project 模板：

1. 在“Visual Basic 扩展性”之下。 项目的默认语言为 Visual Basic。

2. 在“C# 扩展性”之下。 项目的默认语言为 C#。

3. 在“其他项目类型扩展性”之下。 项目的默认语言为 C++。

### <a name="create-a-vspackage"></a>创建 VSPackage

1. 使用 Visual Studio 包项目模板创建新的 VSPackage。

    如果要将语言服务添加到现有 VSPackage，请跳过以下步骤，直接转到 "创建语言服务类" 过程。

2. 输入 MyLanguagePackage 作为项目名称，然后单击 **"确定"**。

    您可以使用任何所需的名称。 此处详述的这些过程假定 MyLanguagePackage 为名称。

3. 选择 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 作为语言和选项以生成新的密钥文件。 单击“下一步”。 

4. 输入相应的公司和包信息。 单击“下一步”。

5. 选择 " **菜单命令**"。 单击“下一步”。

    如果不打算支持代码片段，只需单击 "完成"，然后忽略下一步。

6. 输入 " **插入代码片段** " 作为 **命令名称** ，并输入 `cmdidInsertSnippet` **命令 ID**。 单击“完成”  。

    **命令名称** 和 **命令 ID** 可以是你想要的任何内容，只是示例。

### <a name="create-the-language-service-class"></a>创建语言服务类

1. 在 **解决方案资源管理器** 中，右键单击 MyLanguagePackage 项目，选择 " **添加**"、" **引用**"，然后选择 " **添加新引用** " 按钮。

2. 在 "**添加引用**" 对话框的 " **.net** " 选项卡中，选择 " **VisualStudio** "，然后单击 **"确定"**。

     对于语言包项目，仅需执行一次此操作。

3. 在 **解决方案资源管理器** 中，右键单击 VSPackage 项目，然后选择 " **添加**"、" **类**"。

4. 确保在 "模板" 列表中选择 " **类** "。

5. 输入 **MyLanguageService** 类文件的名称，然后单击 " **添加**"。

     您可以使用任何所需的名称。 此处详述的这些过程假定 `MyLanguageService` 为名称。

6. 在 MyLanguageService 文件中，添加以下 `using` 指令。

     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mylanguageservice.cs" id="Snippet1":::
     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mylanguageservice.vb" id="Snippet1":::

7. 将 `MyLanguageService` 类修改为从类派生 <xref:Microsoft.VisualStudio.Package.LanguageService> ：

     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mylanguageservice.cs" id="Snippet2":::
     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mylanguageservice.vb" id="Snippet2":::

8. 将光标放置在 "LanguageService" 上，然后在 " **编辑**" " **IntelliSense** " 菜单中选择 " **实现抽象类**"。 这将添加实现语言服务类所必需的最低方法。

9. 如 [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service2.md)中所述，实现抽象方法。

### <a name="register-the-language-service"></a>注册语言服务

1. 打开 MyLanguagePackagePackage 文件并添加以下 `using` 指令：

     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mylanguagepackagepackage.vb" id="Snippet3":::
     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mylanguagepackagepackage.cs" id="Snippet3":::

2. 注册语言服务类，如 [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)中所述。 这包括 ProvideXX 属性和 "Proffering 语言服务" 部分。 使用 MyLanguageService，其中本主题使用 TestLanguageService。

### <a name="the-parser-and-scanner"></a>分析器和扫描程序

1. 按照 [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)中所述，为你的语言实现分析器和扫描程序。

     你如何实现分析器和扫描程序完全由你完成，并超出了本主题的范围。

## <a name="language-service-features"></a>语言服务功能
 若要实现语言服务中的每个功能，通常从相应的 MPF 语言服务类派生一个类，根据需要实现任何抽象方法，并重写适当的方法。 您创建和/或派生的类取决于您要支持的功能。 [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)中详细讨论了这些功能。 下面的过程是从多功能进纸器类派生类的一般方法。

#### <a name="deriving-from-an-mpf-class"></a>从 MPF 类派生

1. 在 **解决方案资源管理器** 中，右键单击 VSPackage 项目，然后选择 " **添加**"、" **类**"。

2. 确保在 "模板" 列表中选择 " **类** "。

     为该类文件输入合适的名称，然后单击 " **添加**"。

3. 在新的类文件中，添加以下 `using` 指令。

     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mysource.cs" id="Snippet4":::
     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mysource.vb" id="Snippet4":::

4. 将类修改为从所需的 MPF 类派生。

5. 添加一个类构造函数，该构造函数至少使用与基类的构造函数相同的参数，并将构造函数参数传递到基类构造函数。

     例如，从类派生的类的构造函数 <xref:Microsoft.VisualStudio.Package.Source> 可能如下所示：

     :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/cs/mysource.cs" id="Snippet5":::
     :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/creatingalanguageservice(managedpackageframework)/vb/mysource.vb" id="Snippet5":::

6. 在 " **编辑**" " **IntelliSense** " 菜单中，如果基类具有必须实现的任何抽象方法，请选择 " **实现抽象类** "。

7. 否则，将插入符号放置在类中，并输入要重写的方法。

     例如，键入 `public override` 可以查看可在该类中重写的所有方法的列表。

## <a name="see-also"></a>另请参阅
- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)
