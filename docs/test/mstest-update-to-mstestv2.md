---
title: 更新到 MSTestV2
description: 了解如何从 MSTestV1 更新到 MSTestV2
ms.custom: SEO-VS-2020
ms.date: 02/26/2021
ms.topic: conceptual
f1_keywords:
- vs.UnitTest.Migrate
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- multiple
ms.openlocfilehash: 68ca8dbe123fd0585a321fbefd49fd61713f4329
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122038443"
---
# <a name="upgrade-from-mstestv1-to-mstestv2"></a>从 MSTestV1 升级到 MSTestV2

可以通过将 .csproj 中引用的 MSTest 版本从 MSTestV1 重定目标到 MSTestV2 来升级测试项目。 并非 MSTestV1 中的所有功能都引入了 MSTestV2，因此可能需要进行一些更改以解决错误。 请参阅 [MSTestV2 中不支持的 MSTestV1 功能](#mstestv1-features-that-are-not-supported-in-mstestv2)，以了解哪些功能将会失效。 可能需要从测试中删除其中一些功能。

1. 从单元测试项目中删除对 Microsoft.VisualStudio.QualityTools.UnitTestFramework 的程序集引用。
2. 在 nuget.org 上添加对 MSTestV2 的 NuGet 包引用，包括 [MSTest.TestFramework](https://www.nuget.org/packages/MSTest.TestFramework) 和 [MSTest.TestAdapter](https://www.nuget.org/packages/MSTest.TestAdapter/) 包。可在 NuGet 包管理器控制台中使用以下命令来安装包：

    ```console
    PM> Install-Package MSTest.TestAdapter -Version 2.1.2
    PM> Install-Package MSTest.TestFramework -Version 2.1.2
    ```

### <a name="old-style-csproj-example"></a>旧式 csproj 示例

示例 .csproj 面向 MSTestV1：

```xml
<Reference Include="Microsoft.VisualStudio.QualityTools.UnitTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
  <Private>False</Private>
</Reference>
```

示例 .csproj 现在面向 MSTestV2：

```xml
<Reference Include="Microsoft.VisualStudio.TestPlatform.TestFramework, Version=14.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
  <HintPath>..\packages\MSTest.TestFramework.2.1.2\lib\net45\Microsoft.VisualStudio.TestPlatform.TestFramework.dll</HintPath>
</Reference>
```

> [!NOTE]
> 作为编码 UI 测试或 Web 负载测试的测试项目与 MSTestV2 不兼容。 已弃用这些项目类型。 详细了解[编码 UI 测试弃用](https://devblogs.microsoft.com/devops/changes-to-coded-ui-test-in-visual-studio-2019/)和 [Web 负载测试弃用](https://devblogs.microsoft.com/devops/cloud-based-load-testing-service-eol/)。

### <a name="sdk-style-csproj-net-core-and-net-5"></a>SDK 样式的 csproj（.NET Core 和 .NET 5）

如果 .csproj 是较新的 SDK 样式 .csproj ，则很可能已在使用 MSTestV2。  可在 NuGet 上查找 [MSTestV2](https://www.nuget.org/packages/MSTest.TestFramework) 和 [MSTestV2 适配器](https://www.nuget.org/packages/MSTest.TestAdapter/)的 NuGet 包。

示例：

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.NET.Test.Sdk" Version="16.7.1" />
  <PackageReference Include="MSTest.TestAdapter" Version="2.1.1" />
  <PackageReference Include="MSTest.TestFramework" Version="2.1.1" />
</ItemGroup>
```

## <a name="why-upgrade-to-mstestv2"></a>为什么要升级到 MSTestV2？

2016 年，我们发布了通过 MSTestV2 改进 MSTest 框架的下一步计划。 可在公告[博客文章](https://devblogs.microsoft.com/devops/taking-the-mstest-framework-forward-with-mstest-v2/)中了解有关此更改的详细信息。

* MSTestV2 更易于获取和更新，因为它以 [NuGet 包](https://www.nuget.org/packages/MSTest.TestFramework/)的形式提供。
* MSTestV2 [开放源代码](https://github.com/microsoft/testfx)。
* 统一的应用-平台支持 – MSTestV2 是一个聚合实现，可在 .NET Framework、.NET Core、ASP.NET Core 和 UWP 之间提供统一的应用-平台支持。 [了解详细信息](https://blogs.msdn.microsoft.com/devops/2016/09/01/announcing-mstest-v2-framework-support-for-net-core-1-0-rtm/)。
* 该实现是完全跨平台的（Windows、Linux、Mac）。 [了解详细信息](https://blogs.msdn.microsoft.com/devops/2017/04/05/mstest-v2-is-open-source/)。
* MSTestV2 支持面向 .NET Framework 4.5.0 和更高版本，.NET Core 1.0 和更高版本（通用 Windows 应用 10+）、ASP.NET Core 1.0 和更高版本，以及 .NET 5 和更高版本。
* 提供统一的单一最终用户扩展性机制。 [了解详细信息](https://blogs.msdn.microsoft.com/devops/2017/07/18/extending-mstest-v2/)。
* 为所有基于 MSTest 的测试项目提供统一的 `DataRow` 支持。 [了解详细信息](https://blogs.msdn.microsoft.com/devops/2017/02/25/mstest-v2-now-and-ahead/)。
* 允许将 `TestCategory` 属性置于类或程序集级别。 [了解详细信息](https://blogs.msdn.microsoft.com/devops/2017/02/25/mstest-v2-now-and-ahead/)。
* 现在，从派生的测试类发现并运行来自另一个程序集中定义的基类的测试方法。 此更改引入了与派生测试类类型一致的行为。 如果出于兼容性原因不需要此行为，可以使用以下运行设置将其改回原有行为：

    ```xml
    <RunSettings>    
    <MSTest> 
      <EnableBaseClassTestMethodsFromOtherAssemblies>false</EnableBaseClassTestMethodsFromOtherAssemblies> 
    </MSTest> 
    </RunSettings>
    ```

* 通过[程序集内并行执行](https://github.com/Microsoft/testfx-docs/blob/master/RFCs/004-In-Assembly-Parallel-Execution.md)测试，提供对并行执行的更精细的控制。 这样就可以在程序集中并行运行测试。
* 即使其相应的 `TestInitialize` 方法失败，也会调用 `TestClass` 上的 `TestCleanup` 方法。 [问题详细信息](https://github.com/Microsoft/testfx/issues/250)。
* `AssemblyInitialize` 和 `ClassInitialize` 所花费的时间不计入测试持续时间。 此更改限制了其对测试超时的影响。
* 可通过 `MapNotRunnableToFailed` 标记（它属于 `.runsettings` 文件中的适配器节点）配置无法运行的测试以将其标记为失败。

    ```xml
    <RunSettings>    
    <MSTest> 
      <MapNotRunnableToFailed>true</MapNotRunnableToFailed> 
    </MSTest> 
    </RunSettings>
    ```

## <a name="mstestv1-features-that-are-not-supported-in-mstestv2"></a>MSTestV2 中不支持的 MSTestV1 功能

*   测试不能包含在“顺序测试”中。
*   适配器不支持通过 .testsettings 文件进行配置。 将新的 [.runsettings](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md) 文件用于测试运行配置。
*   适配器不支持指定为 .vsmdi 文件的测试列表。
*   不支持“编码 UI 测试项目”和“Web 性能和负载测试项目”类型。 详细了解[编码 UI 测试弃用](https://devblogs.microsoft.com/devops/changes-to-coded-ui-test-in-visual-studio-2019/)和 [Web 负载测试弃用](https://devblogs.microsoft.com/devops/cloud-based-load-testing-service-eol/)。

## <a name="see-also"></a>另请参阅

- [通过 `.runsettings` 配置测试运行](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)
- [单元测试代码](../test/unit-test-your-code.md)
- [使用测试资源管理器调试单元测试](../test/debug-unit-tests-with-test-explorer.md)
