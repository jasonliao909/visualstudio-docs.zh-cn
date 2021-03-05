---
ms.openlocfilehash: a33871a9a80dfcb6260f57e504c72ae2f72077bd
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/03/2021
ms.locfileid: "101750796"
---
## <a name="prerequisites"></a>先决条件

::: moniker range=">=vs-2019"

* 安装有 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) 并具有所选语言相应的工作负载：
  * ASP.NET：ASP.NET 和 Web 开发
  * Python：Python 开发
  * Node.js：Node.js 开发
::: moniker-end
::: moniker range="vs-2017"
* 安装有 [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)并具有所选语言相应的工作负荷：
  * ASP.NET：ASP.NET 和 Web 开发
  * Python：Python 开发
  * Node.js：Node.js 开发
::: moniker-end

* ASP.NET、ASP.NET Core、Python 或 Node.js 项目。 如果还没有项目，请选择下方选项：
  * ASP.NET Core：按照[快速入门：使用 Visual Studio 创建第一个 ASP.NET Core Web 应用](../../ide/quickstart-aspnet-core.md)的说明操作，或者使用以下步骤：
    ::: moniker range=">=vs-2019"
    在 Visual Studio 2019 中的“启动”窗口上，选择“新建项目”。 如果开始窗口未打开，请选择“文件” > “开始窗口” 。 在搜索框中键入“Web 应用”，选择“C#”作为语言，然后选择“ASP.NET Core Web 应用程序(模型-视图-控制器)”，再选择“下一步”。 在下一个屏幕上，将项目命名为“MyASPApp”，然后选择“下一步”。

    选择建议的目标框架 (.NET Core 3.1) 或 .NET 5，然后选择“创建”。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在 Visual Studio 2017 中，选择“文件” > “新建项目”，然后选择“Visual C#” > “.NET Core”，再选择“ASP.NET Core Web 应用程序”    。 系统出现提示时，请选择“Web 应用程序(模型-视图-控制器)”模板，确保选中“无身份验证”，然后选择“确定”。
    ::: moniker-end
  * Python：请遵照[快速入门：使用 Visual Studio 创建首个 Python Web 应用](../../ide/quickstart-python.md)进行操作，或使用“文件” > “新建项目”，选择“Python”，然后选择“Flask Web 项目”。
  * Node.js：请遵照[快速入门：使用 Visual Studio 创建首个 Node.js 应用](../../ide/quickstart-nodejs.md)进行操作，或使用“文件” > “新建文件”，选择“JavaScript”，然后选择“空白 Node.js Web 应用程序”。

* 请确保在执行部署步骤之前，使用“生成”>“生成解决方案”菜单命令生成项目。