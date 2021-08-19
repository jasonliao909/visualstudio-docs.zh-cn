---
title: 演练：使用 C++ 语言创建 SDK |Microsoft Docs
description: 了解如何创建本机 C++ 数学库 SDK，将 SDK 打包为 Visual Studio 扩展，然后使用此演练创建应用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 36ea793b-3832-41a1-b906-69e680ad5e1d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 8be3320976e8a51acb37be95334f609d8e4f6b3c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122049228"
---
# <a name="walkthrough-create-an-sdk-using-c"></a>演练：使用 C++ 创建 SDK
本演练演示如何创建本机 C++ 数学库 SDK，将 SDK 打包为 Visual Studio 扩展 (VSIX) ，然后使用它创建应用。 演练分为以下步骤：

- [创建本机和 Windows 运行时库](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createClassLibrary)

- [创建 NativeMathVSIX 扩展项目](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createVSIX)

- [创建使用类库的示例应用](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createSample)

## <a name="prerequisites"></a>先决条件
 要按照本演练的步骤操作，必须安装 Visual Studio SDK。 有关详细信息，请参阅 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

## <a name="to-create-the-native-and-windows-runtime-libraries"></a><a name="createClassLibrary"></a>创建本机和 Windows 运行时库

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

2. 在模板列表中，展开"Visual C++Windows  >  **通用**"，然后选择"**通用** 应用" (Windows DLL) 模板。 在" **名称** "框中，指定 `NativeMath` ，然后选择"确定 **"** 按钮。

3. 更新 *NativeMath.h* 以匹配以下代码。

     :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemath/nativemath.h" id="Snippet1":::

4. 更新 *NativeMath.cpp* 以匹配此代码：

     :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemath/nativemath.cpp" id="Snippet2":::

5. 在 **解决方案资源管理器** 中，打开解决方案 **"NativeMath"** 的快捷菜单，然后选择"添加新  >  **Project"。**

6. 在模板列表中，展开 **"Visual C++"，** 然后选择"Windows **运行时组件"** 模板。 在" **名称** "框中，指定 `NativeMathWRT` ，然后选择"确定 **"** 按钮。

7. 更新 *Class1.h* 以匹配此代码：

     :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathwrt/class1.h" id="Snippet3":::

8. 更新 *Class1.cpp* 以匹配此代码：

     :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathwrt/class1.cpp" id="Snippet4":::

9. 在菜单栏上，依次选择“生成” > “生成解决方案” 。

## <a name="to-create-the-nativemathvsix-extension-project"></a><a name="createVSIX"></a> 创建 NativeMathVSIX 扩展项目

1. 在 **解决方案资源管理器** 中，打开解决方案 **"NativeMath"** 的快捷菜单，然后选择"添加新  >  **Project"。**

2. 在模板列表中，展开 **"Visual C#**  >  **扩展性**"，然后选择 **"VSIX Project"。** 在" **名称"** 框中，指定 **"NativeMathVSIX"，** 然后选择"确定 **"** 按钮。

3. 在 **解决方案资源管理器** 中，打开 **source.extension.vsixmanifest** 的快捷菜单，然后选择"查看 **代码"。**

4. 使用以下 XML 替换现有 XML。

    ```xml
    <PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
      <Metadata>
        <Identity Id="NativeMathVSIX..c6b3cae1-e7e2-4e71-90f6-21017ea0dff7" Version="1.0" Language="en-US" Publisher="MyName" />
        <DisplayName>Native Math SDK</DisplayName>
        <Description>Native Math Library w/ Windows Runtime Additions</Description>
      </Metadata>
      <Installation Scope="Global" AllUsers="true">
        <InstallationTarget Id="Microsoft.ExtensionSDK" TargetPlatformIdentifier="Windows" TargetPlatformVersion="v8.0" SdkName="NativeMathSDK" SdkVersion="1.0" />
      </Installation>
      <Dependencies>
      </Dependencies>
      <Assets>
        <Asset Type="Microsoft.ExtensionSDK" d:Source="File" Path="SDKManifest.xml" />
      </Assets>
    </PackageManifest>
    ```

5. 在 **解决方案资源管理器** 中，打开 **NativeMathVSIX** 项目的快捷菜单，然后选择"**添加新**  >  **项"。**

6. 在 Visual **C# 项列表中**，展开"**数据**"，然后选择 **"XML 文件"。** 在" **名称** "框中，指定 `SDKManifest.xml` ，然后选择"确定 **"** 按钮。

7. 使用此 XML 替换文件的内容：

    :::code language="xml" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathvsix/sdkmanifest.xml" id="Snippet5":::

8. 在 **解决方案资源管理器** 中，在 **NativeMathVSIX** 项目下，创建此文件夹结构：

    ```xml
    \DesignTime
          \CommonConfiguration
                \Neutral
                      \Include
          \Debug
                \x86
    \Redist
          \Debug
                \x86
    \References
          \CommonConfiguration
                \Neutral
    ```

9. 在 **解决方案资源管理器** 中，打开解决方案 **"NativeMath"** 的快捷菜单，然后选择"打开"中的 **文件资源管理器。**

10. 在 **文件资源管理器** 中，复制 *$SolutionRoot$\NativeMath\NativeMath.h，* 然后在 **解决方案资源管理器** 的 **NativeMathVSIX** 项目下，将其粘贴到 *$SolutionRoot$\NativeMathVSIX\DesignTime\CommonConfiguration\Neutral\Include \\* 文件夹中。

     复制 *$SolutionRoot$\Debug\NativeMath\NativeMath.lib，* 然后将其粘贴到 *\\ $SolutionRoot$\NativeMathVSIX\DesignTime\Debug\x86* 文件夹中。

     复制 *$SolutionRoot$\Debug\NativeMath\NativeMath.dll* 并将其粘贴到 *$SolutionRoot$\NativeMathVSIX\Redist\Debug\x86 \\* 文件夹中。

     复制 *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.dll* 并将其粘贴到 *$SolutionRoot$\NativeMathVSIX\Redist\Debug\x86* 文件夹中。
     复制 *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.winmd* 并将其粘贴到 *$SolutionRoot$\NativeMathVSIX\References\CommonConfiguration\Neutral* 文件夹中。

     复制 *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.pri，* 并将其粘贴到 *$SolutionRoot$\NativeMathVSIX\References\CommonConfiguration\Neutral* 文件夹中。

11. 在 *$SolutionRoot$\NativeMathVSIX\DesignTime\Debug\x86 \\* 文件夹中，创建名为 *NativeMathSDK.props* 的文本文件，然后将以下内容粘贴到该文件中：
   
    ```xml
    <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <NativeMathSDKPath>$(FrameworkSDKRoot)\..\..\UAP\v0.8.0.0\ExtensionSDKs\NativeMathSDK\1.0\</NativeMathSDKPath>
        <IncludePath>$(NativeMathSDKPath)DesignTime\CommonConfiguration\Neutral\Include;$(IncludePath)</IncludePath>
        <LibraryPath>$(NativeMathSDKPath)DesignTime\Debug\x86;$(LibraryPath)</LibraryPath>
      </PropertyGroup>
      <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Debug|Win32'">
         <Link>
           <AdditionalDependencies>NativeMath.lib;%(AdditionalDependencies)</AdditionalDependencies>
         </Link>
      </ItemDefinitionGroup>
    </Project>
    ```

12. 在菜单栏上，选择 **"查看** 其他Windows  >    >  **属性窗口** (键盘：选择 **F4** 键) 。

13. 在 **解决方案资源管理器** 中，选择 **NativeMathWRT.winmd** 文件。 在" **属性"** 窗口中，将" **生成操作** "属性更改为 **"内容**"，然后将 **"在 VSIX 中包括"属性** 更改为 **True**。

     对 **NativeMath.h 文件重复** 此过程。

     对 **NativeMathWRT.pri** 文件重复此过程。

     对 **NativeMath.Lib 文件重复** 此过程。

     对 **NativeMathSDK.props** 文件重复此过程。

14. 在 **解决方案资源管理器** 中，选择 **NativeMath.h** 文件。 在" **属性"** 窗口中，将 **"在 VSIX 中包括"属性** 更改为 **True**。

     对文件 **重复NativeMath.dll过程** 。

     对文件 **重复NativeMathWRT.dll过程** 。

     对文件 **重复SDKManifest.xml过程** 。

15. 在菜单栏上，依次选择“生成” > “生成解决方案” 。

16. 在 **解决方案资源管理器** 中，打开 **NativeMathVSIX** 项目的快捷菜单，然后选择"打开"中的 **文件资源管理器。**

17. 在 **文件资源管理器** 中，导航到 *$SolutionRoot$\NativeMathVSIX\bin\Debug* 文件夹，然后运行 *NativeMathVSIX.vsix* 开始安装。

18. 选择"**安装**"按钮，等待安装完成，然后打开Visual Studio。

## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a> 创建使用类库的示例应用

1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

2. 在模板列表中，展开  >  **"Visual C++Windows"，** 然后选择"**空白应用"。** 在" **名称"** 框中，指定 **NativeMathSDKSample**，然后选择"确定 **"** 按钮。

3. 在 **解决方案资源管理器** 中，打开 **NativeMathSDKSample** 项目的快捷菜单，然后选择"添加 **引用**  >  **"。**

4. 在"**添加引用"** 对话框的引用类型列表中，展开"通用 **Windows"，** 然后选择"**扩展"。** 最后，选中" **本机数学 SDK"** 复选框，然后选择"确定 **"** 按钮。

5. 显示 NativeMathSDKSample 的项目属性。

    添加引用时，已应用 *NativeMathSDK.props* 中定义的属性。 可以通过检查项目的配置属性 的 VC++**目录** 属性来验证是否 **应用了这些属性**。

6. 在 **解决方案资源管理器** 中，打开 **MainPage.xaml**，然后使用以下 XAML 替换其内容：

    :::code language="xml" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml" id="Snippet1":::

7. 更新 *Mainpage.xaml.h* 以匹配此代码：

    :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml.h" id="Snippet2":::

8. 更新 *MainPage.xaml.cpp* 以匹配此代码：

    :::code language="cpp" source="../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml.cpp" id="Snippet3":::

9. 选择 **F5** 键以运行应用。

10. 在应用中，输入任意两个数字，选择一个操作，然后选择 **=** 按钮。

     将显示正确的结果。

    本演练演示了如何创建和使用扩展 SDK 来调用 [!INCLUDE[wrt](../extensibility/includes/wrt_md.md)] 库和非 [!INCLUDE[wrt](../extensibility/includes/wrt_md.md)] 库。

## <a name="next-steps"></a>后续步骤

## <a name="see-also"></a>另请参阅
- [演练：使用 C# 或 Visual Basic](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [创建软件开发工具包](../extensibility/creating-a-software-development-kit.md)
