---
title: 使用 npm 编译和生成 TypeScript 代码
description: 了解如何使用节点包管理器 (npm) 向 Visual Studio 项目添加 TypeScript 支持。
ms.date: 01/10/2022
ms.topic: conceptual
ms.custom: devdivchpfy22
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-javascript
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: c556a8ad167a4e37508dea2864da17a6b785a519
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139549579"
---
# <a name="compile-typescript-code-nodejs"></a>编译 TypeScript 代码 (Node.js)

可以使用 TypeScript SDK 或 npm 将 TypeScript 支持添加到项目。 默认情况下TypeScript SDK安装程序中提供Visual Studio。

对于在 Visual Studio 2019 中开发的项目，建议使用 TypeScript npm 包，以实现跨不同平台和环境的更高可移植性。

对于 ASP.NET Core，建议改为使用 NuGet [包](../javascript/compile-typescript-code-nuget.md)。

## <a name="add-typescript-support-using-npm"></a>使用 npm 添加 TypeScript 支持

[TypeScript npm 包](https://www.npmjs.com/package/typescript)添加 TypeScript 支持。 当 TypeScript 2.1 或更高版本的 npm 包安装到项目中时，将在编辑器中加载相应版本的 TypeScript 语言服务。

1. [按照说明](./tutorial-nodejs.md?toc=%252fvisualstudio%252fjavascript%252ftoc.json)安装 Node.js 开发工作负载和 Node.js 运行时。

   若要实现Visual Studio集成，请通过以下 TypeScript Node.js之一创建项目，例如"Node.js Web 应用程序"模板。 否则，请使用 Node.js中包含的 JavaScript 模板Visual Studio并按照此处的说明进行操作。 或者，使用" [打开文件夹"](../javascript/develop-javascript-code-without-solutions-projects.md) 项目。

1. 如果你的项目尚未包含它，则安装 [TypeScript npm 包](https://www.npmjs.com/package/typescript)。

   在解决方案资源管理器（右窗格）中，打开项目根目录中的 package.json。 列出的包对应于解决方案资源管理器中 npm 节点下的包。 有关详细信息，请参阅[管理 npm 包](../javascript/npm-package-management.md)。

   对于 Node.js 项目，可以使用命令行或 IDE 安装 TypeScript npm 包。 若要使用 IDE 安装，请在解决方案资源管理器中右键单击“npm”节点，选择“安装新的 npm 包”，搜索“TypeScript”，然后安装包。

   选中“输出”窗口中的“npm”选项，以查看包安装进度。 安装的包显示在解决方案资源管理器的“npm”节点下。

1. 如果项目尚未包含该文件，请向项目根目录添加 *tsconfig.json* 文件。 若要添加文件，右键单击项目节点，然后选择“添加”>“新项”。 选择“TypeScript JSON 配置文件”，然后单击“添加”。

   Visual Studio 会将 tsconfig.json 文件添加到项目根目录中。 可以使用此文件为 TypeScript 编译器[配置选项](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)。

1. 打开 tsconfig.json 并更新，以设置所需的编译器选项。

   以下是简单 *tsconfig.json 文件* 的示例。

   ```json
   {
     "compilerOptions": {
       "noImplicitAny": false,
       "noEmitOnError": true,
       "removeComments": false,
       "sourceMap": true,
       "target": "es5",
       "outDir": "dist"
     },
     "include": [
       "scripts/**/*"
     ]
   }
   ```

   在此示例中：
   - include 告诉编译器在何处查找 TypeScript (*.ts) 文件。
   - outDir 选项指定 TypeScript 编译器转译的普通 JavaScript 文件的输出文件夹。
   - “sourceMap”选项指示编译器是否生成 sourceMap 文件。

   以前的配置仅提供配置 TypeScript 的基本简介。 有关其他选项的信息，请参阅 [tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)。

## <a name="build-the-application"></a>生成应用程序

1. 将 TypeScript (.ts) 或 TypeScript JSX (.tsx) 文件添加到项目，然后添加 TypeScript 代码。 以下是 TypeScript 的简单示例：

   ```typescript
   let message: string = 'Hello World';
   console.log(message);
   ```

1. 在 package.json 中，使用以下脚本添加对 Visual Studio build 和 clean 命令的支持。

   ```json
   "scripts": {
     "build": "tsc --build",
     "clean": "tsc --build --clean"
   },
   ```

   若要使用 webpack 等第三方工具进行生成，可以将命令行生成脚本添加到 *package.json* 文件：

   ```json
   "scripts": {
      "build": "webpack-cli app.tsx --config webpack-config.js"
   }
   ```

   有关将 webpack 与 React 和 webpack 配置文件结合使用的示例，请参阅[使用 Node.js 和 React 创建 Web 应用](../javascript/tutorial-nodejs-with-react-and-jsx.md)。

   有关将 Vue.js 与 TypeScript 结合使用的示例，请参阅[创建 Vue.js 应用程序](create-application-with-vuejs.md)。

1. 如果需要配置选项（如启动页、Node.js 运行时路径、应用程序端口或运行时参数），请右键单击解决方案资源管理器中的项目节点，然后选择“属性”。

   >[!NOTE]
   > 配置第三方工具 > 时，Node.js项目不使用在"工具 **"** >  > "选项""项目和解决方案""Web 包管理""外部 **Web 工具"下配置** > **的路径**。 这些设置用于其他项目类型。

1. 选择“生成”>“生成解决方案”。

   应用在运行时自动生成。 但是，在生成过程中可能会发生以下情况：

   如果生成了源映射，请打开在“outDir”选项中指定的文件夹，并找到生成的 \*.js 文件以及生成的 \*js.map 文件。

   [调试](../javascript/debug-nodejs.md)需要源映射文件。

### <a name="run-the-application"></a>运行应用程序

有关编译应用后运行应用的说明，请参阅 [创建 Node.js 和 Express 应用](./tutorial-nodejs.md?toc=%252fvisualstudio%252fjavascript%252ftoc.json#run-the-app)。

## <a name="automate-build-tasks"></a>自动化生成任务

可以使用 Visual Studio 中的任务运行程序资源管理器来帮助自动执行第三方工具（例如 npm 和 webpack）的任务。

- [NPM 任务运行程序](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.NPMTaskRunner) - 添加对 package. json 中定义的 npm 脚本的支持。 支持 yarn。
- [Webpack 任务运行程序](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.WebPackTaskRunner) - 添加对 webpack 的支持。