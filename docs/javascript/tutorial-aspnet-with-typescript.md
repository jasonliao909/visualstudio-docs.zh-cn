---
title: 使用 TypeScript 创建 ASP.NET Core 应用
description: 在本教程中，使用 ASP.NET Core 和 TypeScript 创建应用
ms.date: 03/25/2021
ms.topic: tutorial
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-javascript
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 9a4067f356f5e8beb598a3ab0366125cf2b95b35
ms.sourcegitcommit: 65a1b6aae8387735f05a83b45e1a6865e9805e1f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2021
ms.locfileid: "129339582"
---
# <a name="tutorial-create-an-aspnet-core-app-with-typescript-in-visual-studio"></a>教程：在 Visual Studio 中使用 TypeScript 创建 ASP.NET Core 应用

在本 Visual Studio 开发 ASP.NET Core 和 TypeScript 教程中，你将创建一个简单的 Web 应用程序，添加一些 TypeScript 代码，然后运行应用。

::: moniker range=">=vs-2022"

从 Visual Studio 2022 开始，如需将 Angular 或 Vue 与 ASP.NET Core 配合使用，建议使用 ASP.NET Core 单页应用程序 (SPA) 模板，以通过 TypeScript 创建 ASP.NET Core 应用。 有关详细信息，请参阅针对 [Angular](../javascript/tutorial-asp-net-core-with-angular.md) 或 [Vue](../javascript/tutorial-asp-net-core-with-vue.md) 的 Visual Studio 教程。
::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end
::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

在本教程中，你将了解：
> [!div class="checklist"]
> * 创建 ASP.NET Core 项目
> * 添加用于 TypeScript 支持的 NuGet 包
> * 添加一些 TypeScript 代码
> * 运行应用
> * 使用 npm 添加第三方库

## <a name="prerequisites"></a>先决条件

* 必须安装 Visual Studio 且具有 ASP.NET Web 开发工作负载。

    ::: moniker range="vs-2019"
    如果尚未安装 Visual Studio 2019，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页免费安装。
    ::: moniker-end
    ::: moniker range="vs-2017"
    如果尚未安装 Visual Studio 2017，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页免费安装。
    ::: moniker-end

    如果需要安装工作负载但已有 Visual Studio，请转到“工具”   > “获取工具和功能...”  ，这会打开 Visual Studio 安装程序。 选择“ASP.NET 和 web 开发”工作负载，然后选择“修改” 。

## <a name="create-a-new-aspnet-core-mvc-project"></a>创建新的 ASP.NET Core MVC 项目

Visual Studio 管理项目中的单个应用程序的文件  。 该项目包括源代码、资源和配置文件。

>[!NOTE]
> 要从空的 ASP.NET Core 项目开始并添加 TypeScript 前端，请改为参阅[含 TypeScript 的 ASP.NET Core](https://www.typescriptlang.org/docs/handbook/asp-net-core.html)。

在本教程中，将从一个包含 ASP.NET Core MVC 应用代码的简单项目开始。

1. 打开 Visual Studio。

1. 创建新项目。

    ::: moniker range="vs-2019"
    在 Visual Studio 2019 中的“启动”窗口上，选择“新建项目”。 如果开始窗口未打开，请选择“文件” > “开始窗口” 。 键入“Web 应用”，选择“C#”作为语言，然后选择“ASP.NET Core Web 应用程序(模型-视图-控制器)”，再选择“下一步”。 在下一个屏幕上，为项目命名，然后选择“下一步”。

    选择建议的目标框架 (.NET Core 3.1) 或 .NET 5，然后选择“创建”。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件”   > “新建”   > “项目”  。 在“新建项目”对话框的左侧窗格中，展开“Visual C#”，然后选择“.NET Core”  。 在中间窗格中，选择“ASP.NET Core Web 应用程序 - C#”，然后选择“确定”。

    在显示的对话框中，选择“Web 应用”之后，在选择“Web 应用(模型-视图-控制器)”，然后选择“创建”（或“确定”）  。

    ![选择 MVC 模板](../javascript/media/aspnet-core-ts-mvc-template.png)
    ::: moniker-end
    如果未显示“ASP.NET Core Web 应用程序”项目模板，必须添加“ASP.NET 和 Web 开发”工作负载。 有关详细说明，请参阅[先决条件](#prerequisites)。

    Visual Studio 创建新的解决方案并在右窗格中打开项目。

## <a name="add-some-code"></a>添加一些代码

1. 在解决方案资源管理器中（右侧窗格）。 右键单击项目节点，然后选择“管理 NuGet 包”。 在“浏览”选项卡中，搜索“Microsoft.TypeScript.MSBuild”，然后单击右侧的“安装”来安装包。

   ![添加 NuGet 包](../javascript/media/aspnet-core-ts-nuget.png)

   Visual Studio 会将 NuGet 包添加到解决方案资源管理器中的“依赖项”节点下。

1. 右键单击项目节点，然后选择“添加”>“新项”。 选择“TypeScript JSON 配置文件”，然后单击“添加”。

   Visual Studio 会将 tsconfig.json 文件添加到项目根目录中。 可以使用此文件为 TypeScript 编译器[配置选项](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)。

1. 打开 tsconfig.json，将默认代码替换为以下代码：

   ```json
   {
     "compileOnSave": true,
     "compilerOptions": {
       "noImplicitAny": false,
       "noEmitOnError": true,
       "removeComments": false,
       "sourceMap": true,
       "target": "es5",
       "outDir": "wwwroot/js"
     },
     "include": [
       "scripts/**/*"
     ]
   }
   ```

   outDir 选项指定 TypeScript 编译器转译的普通 JavaScript 文件的输出文件夹。

   此配置提供了使用 TypeScript 的基本简介。 在其他情况下，例如，在使用 [gulp 或 webpack](https://www.typescriptlang.org/docs/handbook/asp-net-core.html) 时，你可能需要为转译的 JavaScript 文件提供不同的中间位置，而不是 wwwroot/js，具体取决于你的工具和配置首选项。

1. 在解决方案资源管理器中，右键单击项目节点，然后选择“添加”>“新文件夹”。 为新文件夹使用名称“scripts”。

1. 右键单击“scripts”文件夹，然后选择“添加”>“新项”。 选择“TypeScript 文件”，键入文件名“app.config”，然后单击“添加”。

   Visual Studio 将 app.config 添加到“scripts”文件夹。

1. 打开 app.config 并添加以下 TypeScript 代码。

    ```ts
    function TSButton() {
       let name: string = "Fred";
       document.getElementById("ts-example").innerHTML = greeter(user);
    }

    class Student {
       fullName: string;
       constructor(public firstName: string, public middleInitial: string, public lastName: string) {
           this.fullName = firstName + " " + middleInitial + " " + lastName;
       }
    }

    interface Person {
       firstName: string;
       lastName: string;
    }

    function greeter(person: Person) {
       return "Hello, " + person.firstName + " " + person.lastName;
    }

    let user = new Student("Fred", "M.", "Smith");
    ```

    Visual Studio 为 TypeScript 代码提供 IntelliSense 支持。

    若要对此进行测试，请从 `greeter` 函数中删除 `.lastName`，然后重新键入“.”，将看到 IntelliSense。

    ![查看 IntelliSense](../javascript/media/aspnet-core-ts-intellisense.png)

    选择 `lastName`，将最后一个名称添加回代码。

1. 打开 Views/Home 文件夹，然后打开 Index.cshtml。

1. 在文件末尾添加以下 HTML 代码。

    ```html
    <div id="ts-example">
        <br />
        <button type="button" class="btn btn-primary btn-md" onclick="TSButton()">
            Click Me
        </button>
    </div>
    ```

1. 打开 Views/Shared 文件夹，然后打开 _Layout.cshtml 。

1. 在调用 `@RenderSection("Scripts", required: false)` 前添加以下脚本引用：

    ```js
    <script src="~/js/app.js"></script>
    ````

## <a name="build-the-application"></a>生成应用程序

1. 选择“生成”>“生成解决方案”。

   尽管应用程序会在运行时自动生成，但我们想要查看在生成过程中发生的一些事情。

1. 打开 wwwroot/js 文件夹，并找到两个新文件：app.js 和源映射文件 app.js.map  。 这些文件由 TypeScript 编译器生成。

   调试需要源映射文件。

## <a name="run-the-application"></a>运行此应用程序

1. 按 F5  （“调试”   > “启动调试”  ）来运行该应用程序。

    应用将在浏览器中打开。

    在浏览器窗口中，会看到“欢迎”标题和“单击我”按钮。

    ![含 TypeScript 的 ASP.NET Core](../javascript/media/aspnet-core-ts-running-app.png)

1. 单击该按钮可显示在 TypeScript 文件中指定的消息。

## <a name="debug-the-application"></a>调试应用程序

1. 通过在代码编辑器中单击左侧空白，在 `app.ts` 的 `greeter` 函数中设置断点。

    ![设置断点](../javascript/media/aspnet-core-ts-set-breakpoint.png)

1. 按 **F5** 运行该应用程序。

   你可能需要响应消息来启用脚本调试。

   应用程序在断点处暂停。 现在，可以检查变量并使用调试器功能。

## <a name="add-typescript-support-for-a-third-party-library"></a>为第三方库添加 TypeScript 支持

1. 按照 [npm 包管理](../javascript/npm-package-management.md#aspnet-core-projects)中的说明将 `package.json` 文件添加到项目。 此操作会向项目添加 npm 支持。

   >[!NOTE]
   > 对于 ASP.NET Core 项目，还可以使用[库管理器](/aspnet/core/client-side/libman/)或 yarn（而非 npm）来安装客户端 JavaScript 和 CSS 文件。

1. 在此示例中，将 jQuery 的 TypeScript 定义文件添加到项目。 向 package.json 文件添加以下内容。

   ```json
   "devDependencies": {
      "@types/jquery": "3.3.33"
   }
   ```

   此操作会为 jQuery 添加 TypeScript 支持。 MVC 项目模板中已包含 jQuery 库（在解决方案资源管理器中的 wwwroot/lib 下查看）。 如果使用其他模板，则可能还需要包含 jquery npm 包。

1. 如果未安装解决方案资源管理器中的包，请右键单击 npm 节点，然后选择“还原包”。

   >[!NOTE]
   > 在某些情况下，解决方案资源管理器可能会指示由于[此处](https://github.com/aspnet/Tooling/issues/479)所述的已知问题，npm 包与 package.json 不同步。 例如，在安装包时，可能会显示为未安装。 在大多数情况下，可以通过删除 package.json，重启 Visual Studio 并重新添加 package.json 文件来更新解决方案资源管理器，如本文前面所述   。

1. 在解决方案资源管理器中右键单击脚本文件夹，然后选择“添加” > “新项” 。

1. 选择“TypeScript 文件”，键入 library.ts，然后选择“添加”。

1. 在 library.ts 中，添加以下代码。

   ```ts
   var jqtest = {
      showMsg: function (): void {
         let v: any = jQuery.fn.jquery.toString();
         let content: any = $("#ts-example-2")[0].innerHTML;
         alert(content.toString() + " " + v + "!!");
         $("#ts-example-2")[0].innerHTML = content + " " + v + "!!";
      }
   };

   jqtest.showMsg();
   ```

   为简单起见，此代码使用 jQuery 显示消息和警报。

   如果添加了 jQuery 的 TypeScript 类型定义，则在 jQuery 对象后面键入“.”时，可以获得针对 jQuery 对象的 IntelliSense 支持，如下所示。

   ![jquery IntelliSense](../javascript/media/aspnet-core-ts-jquery-intellisense.png)

1. 在 _Layout.cshtml 中，更新脚本引用以包含 `library.js`。

   ```html
   <script src="~/js/app.js"></script>
   <script src="~/js/library.js"></script>
   ```

1. 在 Index.cshtml 中，将以下 HTML 代码添加到文件末尾。

   ```html
   <div>
      <p id="ts-example-2">jQuery version is:</p>
   </div>
   ```

1. 按 F5  （“调试”   > “启动调试”  ）来运行该应用程序。

    应用将在浏览器中打开。

    在警报中单击“确定”，以查看已更新为 jQuery 版本  **的页面为：** 3.3.1!! 的页面。

    ![jquery 示例](../javascript/media/aspnet-core-ts-jquery-example.png)

## <a name="next-steps"></a>后续步骤

你可能想要了解有关将 TypeScript 与 ASP.NET Core 结合使用的更多详细信息。 如果你对 Visual Studio 中的 AngularJS 编程感兴趣，可使用适用于 Visual Studio 的 [AngularJS 语言服务扩展](https://devblogs.microsoft.com/visualstudio/angular-language-service-for-visual-studio)。

> [!div class="nextstepaction"]
> [ASP.NET Core 和 TypeScript](https://www.typescriptlang.org/docs/handbook/asp-net-core.html)

> [!div class="nextstepaction"]
> [AngularJS 语言服务扩展](https://devblogs.microsoft.com/visualstudio/angular-language-service-for-visual-studio)
