---
title: 对 JavaScript 和 TypeScript 代码进行单元测试
description: Visual Studio 支持使用针对 Visual Studio 的 Node.js 工具对 JavaScript 和 TypeScript 代码进行单元测试
ms.date: 09/20/2021
ms.topic: how-to
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-javascript
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: dd1f130d8cc63ad86ca0ae93dfd551edf871311f
ms.sourcegitcommit: 8b44ba7864f67afa476708d5092729345e689f93
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2021
ms.locfileid: "132861492"
---
# <a name="unit-testing-javascript-and-typescript-in-visual-studio"></a>在 Visual Studio 中对 JavaScript 和 TypeScript 代码进行单元测试

使用更受欢迎的 JavaScript 框架，无需切换到命令提示符，即可在 Visual Studio 中写入和运行单元测试。 支持 Node.js 和 ASP.NET Core 项目。

支持的框架：
* Mocha ([mochajs.org](https://mochajs.org/))
* Jasmine ([Jasmine.github.io](https://jasmine.github.io/))
* Tape ([github.com/substack/tape](https://github.com/substack/tape))
* Jest ([jestjs.io](https://jestjs.io/))
* 导出运行程序（此框架特定于针对 Visual Studio 的 Node.js 工具）

有关 ASP.NET Core 和 JavaScript 或 TypeScript，请参阅[编写 ASP.NET Core 单元测试](#write-unit-tests-for-aspnet-core)。

如果你常用的框架不受支持，请参阅[添加对单元测试框架的支持](#addingFramework)，获取有关添加支持的信息。

::: moniker range=">=vs-2022"
## <a name="write-unit-tests-for-a-cli-based-project-esproj"></a>为基于 CLI 的项目 (.esproj) 编写单元测试

Visual Studio 2022 中支持的[基于 CLI 的项目](../javascript/javascript-in-vs-2022.md#project-templates)可使用测试资源管理器。 Jest 是用于 React 和 Vue 项目的内置测试框架，Karma 和 Jasmine 用于 Angular 项目。 默认情况下，你将能够运行每个框架提供的默认测试以及你编写的任何其他测试。  只需在测试资源管理器中点击“运行”按钮即可。 如果尚未打开测试资源管理器，请在菜单栏中选择“测试” > “测试资源管理器”以找到它。

需要 Node.js 开发工作负载才能为基于 CLI 的项目支持单元测试。

还支持 Mocha 和 Tape 测试库。 若要使用其中一种测试库，只需将 package.json 中的默认测试库更改为相应的测试库的包即可。
::: moniker-end

## <a name="write-unit-tests-in-a-nodejs-project-njsproj"></a>在 Node.js 项目 (.njsproj) 中编写单元测试

对于 Node.js 项目，在将单元测试添加到项目之前，请确保要使用的框架已本地安装在项目中。 使用 [npm 包安装窗口](npm-package-management.md#npmInstallWindow)可以轻松完成此操作。

向项目添加单元测试的首选方法是在项目中创建“测试”文件夹并将其设置为项目属性中的测试根。 还需要选择想要使用的测试框架。

![设置测试根和测试框架](../javascript/media/unit-test-project-properties.png)

可以使用“添加新项”对话框，将简单的空白测试添加到项目。 同一项目中同时支持 JavaScript 和 TypeScript。

![添加新单元测试](../javascript/media/unit-test-add-new-item.png)

对于 Mocha 单元测试，请使用以下代码：

```javascript
var assert = require('assert');

describe('Test Suite 1', function() {
    it('Test 1', function() {
        assert.ok(true, "This shouldn't fail");
    })

    it('Test 2', function() {
        assert.ok(1 === 1, "This shouldn't fail");
        assert.ok(false, "This should fail");
    })
})
```

如果尚未在项目属性中设置单元测试选项，则必须确保“属性”窗口中的“测试框架”属性设为适用于单元测试文件的正确测试框架 。 这通过单元测试文件模板自动完成。

![测试框架](../javascript/media/UnitTestsFrameworkMocha.png)

> [!Note]
> 单元测试选项将优先于单个文件的设置。

打开测试资源管理器（选择“测试” > “Windows” > “测试资源管理器”）后，Visual Studio 发现并显示测试  。 如果开始未显示测试，则重新生成项目以刷新列表。

![测试资源管理器](../javascript/media/UnitTestsDiscoveryMocha.png)

> [!NOTE]
> 对于 TypeScript，请勿在 tsconfig.json 中使用 `outdir` 或 `outfile` 选项，因为测试资源管理器没法找到你的单元测试。

## <a name="run-tests-nodejs"></a>运行测试 (Node.js)

可在 Visual Studio 中运行测试，也从命令行运行。

### <a name="run-tests-in-visual-studio"></a>在 Visual Studio 中运行测试

::: moniker range=">=vs-2019"
可以通过在测试资源管理器中单击“全部运行”链接运行测试。 或者，可选择一个或多个测试或组，右键单击并从快捷菜单选择“运行”来运行测试。 后台运行测试，测试资源管理器自动更新并显示结果。 此外，还可右键单击并选择“调试”来调试所选测试。
::: moniker-end
::: moniker range="vs-2017"
可以通过在测试资源管理器中单击“全部运行”链接运行测试。 或者，可以选择一个或多个测试或组，右键单击并从快捷菜单选择“运行所选测试”，从而运行测试。 后台运行测试，测试资源管理器自动更新并显示结果。 此外，还可以通过选择“调试所选测试”调试所选测试。
::: moniker-end

对于 TypeScript，针对生成的 JavaScript 代码运行单元测试。

> [!NOTE]
> 在大多数 TypeScript 场景中，你可在 TypeScript 代码中设置断点，在测试资源管理器中右键单击一个测试，然后选择“调试”来调试单元测试。 在更复杂的场景中，例如在某些使用源映射的场景中，可能很难在 TypeScript 代码中命中断点。 一种变通方法是尝试使用 `debugger` 关键字。

> [!NOTE]
> 我们当前不支持分析测试或代码覆盖率。

### <a name="run-tests-from-the-command-line"></a>从命令行运行测试

可使用以下命令从 [Visual Studio 的开发人员命令提示](../ide/reference/command-prompt-powershell.md)中运行测试：

```
vstest.console.exe <path to project file>\NodejsConsoleApp23.njsproj /TestAdapterPath:<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter
```

该命令显示如下所示的输出：

```
Microsoft (R) Test Execution Command Line Tool Version 15.5.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
Processing: NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js
  Creating TestCase:NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js::Test Suite 1 Test 1::mocha
  Creating TestCase:NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js::Test Suite 1 Test 2::mocha
Processing finished for framework of Mocha
Passed   Test Suite 1 Test 1
Standard Output Messages:
 Using default Mocha settings
 1..2
 ok 1 Test Suite 1 Test 1

Failed   Test Suite 1 Test 2
Standard Output Messages:
 not ok 1 Test Suite 1 Test 2
   AssertionError [ERR_ASSERTION]: This should fail
       at Context.<anonymous> (NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js:10:16)

Total tests: 2. Passed: 1. Failed: 1. Skipped: 0.
Test Run Failed.
Test execution time: 1.5731 Seconds
```

> [!NOTE]
> 如果收到指示无法找到 vstest.console.exe 的错误，请确保已打开开发人员命令提示，而不是常规的命令提示符。

## <a name="write-unit-tests-for-aspnet-core"></a>编写 ASP.NET Core 单元测试

1. 创建 ASP.NET Core 项目并添加 TypeScript 支持。

   有关示例项目，请参阅[使用 TypeScript 创建 ASP.NET Core 应用](../javascript/tutorial-aspnet-with-typescript.md)。 如需单元测试支持，建议从标准 ASP.NET Core 项目模板开始。

   使用 NuGet 包（而不是 npm TypeScript 包）来添加 TypeScript 支持。

1. 安装 NuGet 包 [Microsoft.JavaScript.UnitTest](https://www.nuget.org/packages/Microsoft.JavaScript.UnitTest/)

1. 在解决方案资源管理器中，右键单击项目节点，并选择“卸载项目”。

   .csproj文件应在 Visual Studio 中打开。

1. 将以下元素添加到元素中的 .csproj 文件中的 `PropertyGroup` 元素。

   此示例将 Mocha 指定为测试框架。 可以改为指定 Jest、Tape 或 Jasmine。

   ```xml
   <PropertyGroup>
      ...
      <JavaScriptTestRoot>tests\</JavaScriptTestRoot>
      <JavaScriptTestFramework>Mocha</JavaScriptTestFramework>
      <GenerateProgramFile>false</GenerateProgramFile>
   </PropertyGroup>
   ```

   `JavaScriptTestRoot` 元素指定单元测试将位于项目根目录的 tests 文件夹中。

1. 在解决方案资源管理器中，右键单击项目节点，并选择“重新加载项目”。

1. 添加 npm 支持，如“npm 包管理”一文中的 [ASP.NET Core 项目](../javascript/npm-package-management.md#aspnet-core-projects)下所述。

   这需要安装 Node.js 运行时以实现 npm 支持，并在项目根目录中添加 package.json。

1. 在 package.json 中，在依赖项下添加所需的 npm 包。

   例如，对于 mocha，可使用以下命令：

   ```json
   "dependencies": {
     "mocha": "8.3.0",
   ```

   某些单元测试框架（如 Jest）需要额外的 npm 包。 对于 Jest，请使用以下 JSON：

   ```json
   "dependencies": {
     "jest": "26.6.3",
     "jest-editor-support": "28.1.0"
   ```

   >[!NOTE]
   > 在某些情况下，由于[此处](https://github.com/aspnet/Tooling/issues/479)所述的已知问题，解决方案资源管理器可能无法正确显示 npm 节点。 如果需要查看 npm 节点，可以卸载项目（右键单击该项目，并选择“卸载项目”）然后重新加载该项目，以使 npm 节点重新显示出来。

1. 向测试添加代码。

   如果使用[通过 TypeScript 创建 ASP.NET Core 应用](tutorial-aspnet-with-typescript.md)中所述的示例，请在 scripts 文件夹中的库 library.ts 文件末尾添加以下代码。 

   ```typescript
   function getData(value) {
      if (value > 1) {
         return true;
      }
   }
    
   module.exports = getData;
   ```

   对于 TypeScript，针对生成的 JavaScript 代码运行单元测试。

1. 将单元测试添加到项目根目录中的 tests 文件夹。

   例如，你可以通过选择与测试框架（在此示例中即 Mocha 或 Jest）匹配的正确文档选项卡来使用以下代码。 此代码会测试一个名为 `getData` 的函数。

   # <a name="mocha"></a>[穆哈咖啡](#tab/mocha)

   ```typescript
   const getData = require('../wwwroot/js/library.js');
   var assert = require('assert');
    
   describe('Test Suite 1', function () {
      it('getData', function () {
         assert.ok(true, getData(2));
      })
   })
   ```

   # <a name="jest"></a>[Jest](#tab/jest)

   ```typescript
   const getData = require('../wwwroot/js/library.js');
    
   test('should return true', () => {
      expect(getData(2)).toBe(true);
   });
   ```

1. 打开测试资源管理器（选择“测试” > “Windows” > “测试资源管理器”），Visual Studio 将发现并显示测试。 如果开始未显示测试，则重新生成项目以刷新列表。

   ![测试资源管理器测试发现](../javascript/media/unit-tests-aspnet-core-discovery.png)

   > [!NOTE]
   > 对于 TypeScript，请勿在 tsconfig.json 中使用 `outfile` 选项，因为测试资源管理器没法找到你的单元测试。 可以使用 `outdir` 选项，但请确保配置文件（如 `package.json` 和 `tsconfig.json`）位于项目根目录中。

## <a name="run-tests-aspnet-core"></a>运行测试 (ASP.NET Core)

::: moniker range=">=vs-2019"
可以通过在测试资源管理器中单击“全部运行”链接运行测试。 或者，可选择一个或多个测试或组，右键单击并从快捷菜单选择“运行”来运行测试。 后台运行测试，测试资源管理器自动更新并显示结果。 此外，还可右键单击并选择“调试”来调试所选测试。
::: moniker-end
::: moniker range="vs-2017"
可以通过在测试资源管理器中单击“全部运行”链接运行测试。 或者，可以选择一个或多个测试或组，右键单击并从快捷菜单选择“运行所选测试”，从而运行测试。 后台运行测试，测试资源管理器自动更新并显示结果。 此外，还可以通过选择“调试所选测试”调试所选测试。
::: moniker-end

对于 TypeScript，针对生成的 JavaScript 代码运行单元测试。

![测试资源管理器结果](../javascript/media/unit-tests-aspnet-core-run.png)

> [!NOTE]
> 在大多数 TypeScript 场景中，你可在 TypeScript 代码中设置断点，在测试资源管理器中右键单击一个测试，然后选择“调试”来调试单元测试。 在更复杂的场景中，例如在某些使用源映射的场景中，可能很难在 TypeScript 代码中命中断点。 一种变通方法是尝试使用 `debugger` 关键字。

> [!NOTE]
> 我们当前不支持分析测试或代码覆盖率。

## <a name="add-support-for-a-unit-test-framework"></a><a name="addingFramework"></a>添加对单元测试框架的支持

可以通过使用 JavaScript 实现发现和执行逻辑添加对其他测试框架的支持。

> [!NOTE]
> 对于 ASP.NET Core，将 NuGet 包 [Microsoft.JavaScript.UnitTest](https://www.nuget.org/packages/Microsoft.JavaScript.UnitTest/) 添加到你的项目以添加支持。

可以通过在以下位置添加名为测试框架的文件夹执行此操作：

`<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter\TestFrameworks`

如果在 ASP.NET Core 项目中没有看到 `NodeJsTools` 文件夹，请使用 Visual Studio 安装程序添加 Node.js 开发工作负载。 此工作负载包括对 JavaScript 和 TypeScript 进行单元测试的支持。

此文件夹必须包含与导出以下两个函数的文件名称相同的 JavaScript 文件：

* `find_tests`
* `run_tests`

有关 `find_tests` 和 `run_tests` 实现的示例，请参阅 Mocha 单元测试框架实现：

`<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter\TestFrameworks\mocha\mocha.js`

Visual Studio 启动时开始发现可用测试框架。 如果在 Visual Studio 运行时添加框架，请重启 Visual Studio 检测框架。 但是，对实现做出更改时无需重启。

## <a name="unit-tests-in-net-framework"></a>.NET Framework 中的单元测试

并不局限于在 Node.js 和 ASP.NET Core 项目中编写单元测试。 将 TestFramework 和 TestRoot 属性添加到任何 C# 或 Visual Basic 项目时，将枚举这些测试，并且可使用“测试资源管理器”窗口运行它们。

为实现此操作，请在解决方案资源管理器中右键单击项目节点，选择“卸载项目”，然后选择“编辑项目”。 然后在项目文件中，将以下两个元素添加到属性组中。

> [!IMPORTANT]
> 确保未对要添加元素的属性组指定条件。
> 这可能会导致意外行为。

```xml
<PropertyGroup>
    <JavaScriptTestRoot>tests\</JavaScriptTestRoot>
    <JavaScriptTestFramework>Tape</JavaScriptTestFramework>
</PropertyGroup>
```

接下来，将测试添加到指定的测试根文件夹，它们将可以在“测试资源管理器”窗口中运行。 如果最初未显示它们，可能需要重新生成项目。

## <a name="unit-test-net-core-and-net-standard"></a>对 .NET Core 和 .NET Standard 进行单元测试

除了上述属性之外，你还需要安装 NuGet 包[Microsoft.JavaScript.UnitTest](https://www.nuget.org/packages/Microsoft.JavaScript.UnitTest/) 并设置以下属性：

```xml
<PropertyGroup>
    <GenerateProgramFile>false</GenerateProgramFile>
</PropertyGroup>
```

一些测试框架可能需要额外的 npm 包来进行测试检测。 例如，jest 需要 jest-editor-support npm 包。 如果需要，请查看特定框架的文档。
