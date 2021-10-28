---
title: 调试 WebView 控件 (UWP) |Microsoft Docs
description: 了解如何检查和调试 Windows 运行时应用中使用的 Web 视图控件。 可使用 DOM 资源管理器和“JavaScript 控制台”窗口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 7d105907-8b39-4d07-8762-5c5ed74c7f21
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: vs-2017
ms.workload:
- uwp
ms.openlocfilehash: 3198685acc8ad33a545bf55628c99e78d104d251
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641222"
---
# <a name="debug-a-webview-control-in-a-uwp-app"></a>调试 UWP 应用中的 WebView 控件

 若要检查并调试 Windows 运行时应用中的 `WebView` 控件，可以配置 Visual Studio，使其在你启动应用时附加脚本调试器。 可通过两种方式来使用调试器与 `WebView` 控件交互：

- 打开 `WebView` 实例的 [DOM 资源管理器](../debugger/quickstart-debug-html-and-css.md)，然后检查 DOM 元素、调查 CSS 样式问题并测试动态呈现的样式的更改。

- 在 [JavaScript 控制台](../debugger/javascript-console-commands.md?view=vs-2017&preserve-view=true)窗口中选择 `WebView` 实例中显示为目标的网页或 `iFrame`，然后使用控制台命令与网页交互。 控制台提供对当前脚本执行上下文的访问。

### <a name="attach-the-debugger-c-visual-basic-c"></a>附加调试器（C#、Visual Basic、C++）

1. 在 Visual Studio 中，向 Windows 运行时应用添加 `WebView` 控件。

2. 在解决方案资源管理器中，通过从项目的快捷菜单中选择“属性”来打开项目的属性。

3. 选择“调试”。 在“应用程序进程”列表中，选择“脚本” 。

     ![附加脚本调试器](../debugger/media/js_dom_webview_script_debugger.png "JS_DOM_WebView_Script_Debugger")

4. （可选）对于不是 Express 版本的 Visual Studio，可通过选择“工具”>“选项”>“调试”>“实时”，然后禁用脚本的 JIT 调试，来禁用实时 (JIT) 调试。

    > [!NOTE]
    > 对于某些网页上发生的无法处理的异常，你可以通过禁用 JIT 调试来隐藏对话框。 在 Visual Studio Express 中，JIT 调试始终处于禁用状态。

5. 按 F5 开始调试。

### <a name="use-the-dom-explorer-to-inspect-and-debug-a-webview-control"></a>使用 DOM 资源管理器以检查并调试 WebView 控件

1. （C#、Visual Basic、C++）向你的应用附加脚本调试器。 请参见第一部分以获取说明。

2. 若没有 `WebView` 控件，请向应用添加该控件并按 F5 启动调试。

3. 导航到包含 `Webview` 控件的页面。

4. 依次选择“调试”、“窗口”、“DOM 资源管理器”来打开 `WebView` 控件的“DOM 资源管理器”窗口，然后选择要检查的 `WebView` 的 URL  。

     ![打开 DOM 资源管理器](../debugger/media/js_dom_webview.png "JS_DOM_WebView")

     与 `WebView` 关联的 DOM 资源管理器将在 Visual Studio 中显示为新选项卡。

5. 查看并修改[使用 DOM 资源管理器调试 CSS 样式](quickstart-debug-html-and-css.md)中介绍的实时 DOM 元素和 CSS 样式。

### <a name="use-the-javascript-console-window-to-inspect-and-debug-a-webview-control"></a>使用 JavaScript 控制台窗口以检查并调试 WebView 控件

1. （C#、Visual Basic、C++）向你的应用附加脚本调试器。 请参见第一部分以获取说明。

2. 若没有 `WebView` 控件，请向应用添加该控件并按 F5 启动调试。

3. 依次选择“调试”、“窗口”、“JavaScript 控制台”来打开 `WebView` 控件的“JavaScript 控制台”窗口  。

     将显示“JavaScript 控制台”窗口。

4. 导航到包含 `Webview` 控件的页面。

5. 在控制台窗口中，选择“目标”列表中 `WebView` 控件显示的网页或 `iFrame`。

     ![JavaScript 控制台窗口中的目标选择](../debugger/media/js_console_target.png "JS_Console_Target")

    > [!NOTE]
    > 通过使用控制台，可以与单个 `WebView`、`iFrame` 交互，每次还可以共享协定或 Web Worker。 每个元素都需要单独的 Web 平台主机 (WWAHost.exe) 的实例。 一次可与一个主机交互。

6. 查看并修改应用中的变量或使用控制台命令，如[快速入门：调试 JavaScript](../debugger/quickstart-debug-javascript-using-the-console.md) 和 [JavaScript 控制台命令](../debugger/javascript-console-commands.md?view=vs-2017&preserve-view=true)中所述。

## <a name="see-also"></a>请参阅

- [快速入门：调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md)