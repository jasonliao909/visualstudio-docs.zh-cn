---
title: 单元测试面向 .NET Framework 的早期版本
description: 了解如何创建面向 .NET Framework 的特定版本的单元测试项目。 所面向的版本必须为 3.5 或更高版本，并且不能为客户端版本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- dotnet
author: mikejo5000
ms.openlocfilehash: 19c0300cf8549b01b36f911bfb287bbdc3a22f1e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122123029"
---
# <a name="how-to-configure-unit-tests-to-target-an-earlier-version-of-the-net-framework"></a>如何：配置单元测试以面向 .NET Framework 的早期版本

在 Microsoft Visual Studio 中创建测试项目时，默认将 .NET Framework 的最新版本设为要面向的版本。 此外，如果从 Visual Studio 的早期版本升级测试项目，那么它们将被升级为面向 .NET Framework 的最新版本。 通过编辑项目属性，可以显式使项目重新面向 .NET Framework 的早期版本。

可以创建面向 .NET Framework 的特定版本的单元测试项目。 所面向的版本必须为 3.5 或更高版本，并且不能为客户端版本。 Visual Studio 为面向特定版本的单元测试启用了以下基本支持：

- 可以创建单元测试项目，并使它们面向 .NET Framework 的特定版本。

- 可以在本地计算机上的 Visual Studio 中运行面向特定版本的 .NET Framework 的单元测试。

- 可以使用 MSTest.exe 从命令提示符处运行面向特定版本的 .NET Framework 的单元测试。

- 作为生成的一部分，可以在生成代理上运行单元测试。

**测试 SharePoint 应用程序**

上面列出的功能还支持使用 Visual Studio 为 SharePoint 应用程序编写单元测试和集成测试。 有关如何使用 Visual Studio 开发 SharePoint 应用程序的详细信息，请参阅[创建 SharePoint 解决方案](../sharepoint/create-sharepoint-solutions.md)、[生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)以及[验证和调试 SharePoint 代码](../sharepoint/verifying-and-debugging-sharepoint-code.md)。

**限制**

将测试项目重新面向为使用早期版本的 .NET Framework 时，存在以下限制：

- 在 .NET Framework 3.5 中，只包含单元测试的测试项目支持多面向。 .NET Framework 3.5 不支持任何其他测试类型，如编码的 UI 测试或负载测试。 除了单元测试，其他测试类型均不支持重新面向。

- 仅默认的主机适配器支持面向 .NET Framework 的早期版本的测试的执行。 ASP.NET 主机适配器不支持。 需要在 ASP.NET 开发服务器环境中运行的 ASP.NET 应用程序必须与 .NET Framework 的当前版本兼容。

- 运行支持 .NET Framework 3.5 多面向的测试时，将禁用数据收集支持。 可以使用 Visual Studio 命令行工具来运行代码覆盖率。

- 无法在远程计算机上运行使用 .NET Framework 3.5 的单元测试。

- 无法使单元测试面向早期客户端版本的框架。

## <a name="retargeting-for-visual-basic-unit-test-projects"></a>重定向 Visual Basic 单元测试项目

1. 创建新的 Visual Basic“单元测试项目”项目。

2. 在“解决方案资源管理器”中，从新的 Visual Basic 测试项目的右键单击菜单中选择“属性” 。

     随即显示 Visual Basic 测试项目的属性。

3. 在“编译”选项卡上，选择“高级编译选项”，如下面的插图中所示。

     ![高级编译选项](../test/media/howtoconfigureunittest35frameworka.png)

4. 使用“目标框架 (所有配置)”下拉列表，将目标框架更改为 **.NET Framework 3.5** 或更高版本，如下图中的标注 B 所示。 不应指定客户端版本。

     ![“高级编译器设置”对话框的屏幕截图。 其中突出显示了“目标框架”下拉列表，并且值设置为“.NET Frameowrk 3.5”。](../test/media/howtoconfigureunitest35frameworkstepb.png)

## <a name="retargeting-for-c-unit-test-projects"></a>重定向 C# 单元测试项目

1. 创建新的 C#“单元测试项目”项目。

2. 在“解决方案资源管理器”中，从新的 C# 测试项目的右键单击菜单中选择“属性” 。

   随即显示 C# 测试项目的属性。

3. 在“应用程序”选项卡上，选择“目标框架”。 从下拉列表中，选择“.NET Framework 3.5”或更高版本，如下图中所示。 不应指定客户端版本。

   ![解决方案资源管理器“属性”窗格中“应用程序”选项卡的插图，其中突出显示了“目标框架”下拉列表的位置。](../test/media/howtoconfigureunittest35frameworkcsharp.png)

## <a name="retargeting-for-ccli-unit-test-projects"></a>重定向 C++/CLI 单元测试项目

1. 创建新的 C++“单元测试项目”项目。

   > [!WARNING]
   > 若要为以前版本的适用于 Visual C++ 的 .NET Framework 生成 C++/CLI 单元测试，则必须使用相应版本的 Visual Studio。

2. 在“解决方案资源管理器”中，从新的 C++ 测试项目中选择“卸载项目” 。

3. 在“解决方案资源管理器”中，依次选择已卸载的 C++ 测试项目和“编辑 \<project name>.vcxproj”。

   即可在编辑器中打开 .vcxproj 文件。

4. 在标记为`"Globals"`的 `PropertyGroup` 中将 `TargetFrameworkVersion` 设为版本 3.5 或更高版本。 不应指定客户端版本：

    ```xml
    <PropertyGroup Label="Globals">
        <TargetName>DefaultTest</TargetName>
        <ProjectTypes>{3AC096D0-A1C2-E12C-1390-A8335801FDAB};{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}</ProjectTypes>
        <ProjectGUID>{CE16D77A-E364-4ACD-948B-1EB6218B0EA3}</ProjectGUID>
        <TargetFrameworkVersion>3.5</TargetFrameworkVersion>
        <Keyword>ManagedCProj</Keyword>
        <RootNamespace>CPP_Test</RootNamespace>
      </PropertyGroup>
    ```

5. 保存并关闭 .vcxproj 文件。

6. 在“解决方案资源管理器”中，从新的 C++ 测试项目的右键单击菜单中选择“重载项目” 。

## <a name="see-also"></a>请参阅

- [创建 SharePoint 解决方案](../sharepoint/create-sharepoint-solutions.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [“高级编译器设置”对话框 (Visual Basic)](../ide/reference/advanced-compiler-settings-dialog-box-visual-basic.md)
