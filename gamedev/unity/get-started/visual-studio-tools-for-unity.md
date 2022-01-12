---
title: Visual Studio Tools for Unity | Microsoft Docs
description: 阅读有关 Visual Studio Tools for Unity 的概述，这是一个免费的 Visual Studio 扩展，可帮助你使用 Unity 开发跨平台游戏和应用。
ms.date: 12/10/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: overview
ms.assetid: 6cabc626-5310-4622-a743-210a9abb5535
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
zone_pivot_groups: platform
ms.openlocfilehash: 6512154e53c1ac1e77071e1aac01e09e90cbc120
ms.sourcegitcommit: 2a4744fb312396d36086dd59fd55ab741ae8e106
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/28/2021
ms.locfileid: "135575915"
---
# <a name="visual-studio-tools-for-unity"></a>Visual Studio Tools for Unity
![用于游戏播放的计算机、游戏控制器和图标的屏幕截图。](../media/hero.png)

## <a name="overview"></a>概述
Visual Studio Tools for Unity包含一组丰富的功能，可增强 Unity C# 脚本的编写和调试以及 Unity 项目的使用。

* 使用针对 Unity 项目优化的调试器对代码进行故障排除、检查和浏览。
* 使用特定于 Unity 的 IntelliSense 代码完成功能快速发现和编写 Unity 脚本。
* 通过快速访问 Unity 文档详细了解编写的代码。
* 使用符合 Unity 脚本最佳做法的重构选项编写更好的代码。
* 确定 Unity 引擎如何使用消息函数和资产使用情况的 CodeLens 提示调用代码。
* 更多。 [](#features)

## <a name="available-for-windows-and-macos"></a>适用于 Windows 和 macOS
:::zone pivot="windows"
Visual Studio Tools for Unity免费，并支持 Visual Studio 2017 Community、Professional 和 Enterprise 及更高版本。 我们建议[下载和使用最新版本的 Visual Studio。](https://visualstudio.microsoft.com/downloads/)
:::zone-end
:::zone pivot="macos"
Visual Studio Tools for Unity 2017 及更高版本的每次安装中都Visual Studio for Mac免费版。 我们建议[下载和使用最新版本的 Visual Studio for Mac。](https://visualstudio.microsoft.com/downloads/)
:::zone-end

访问 Visual Studio Tools for Unity Tools [for Unity 入门。](getting-started-with-visual-studio-tools-for-unity.md) 有关安装和设置详细信息。

### <a name="supported-unity-versions"></a>支持的 Unity 版本
#### <a name="visual-studio-editor-unity-package"></a>Visual Studio编辑器 Unity 包
Unity 2020.1 及更高版本需要适用于外部编辑器工具（如 Visual Studio 和 Visual Studio for Mac） 的 Unity 包。 [有关这些更改的更多文档，请参阅 Unity 博客文章](https://unity.com/releases/2020-1/programmer-tools#verified-ide-packages-now-include-visual-studio)。

入门[部分](getting-started-with-visual-studio-tools-for-unity.md)包含有关编辑器包配置Visual Studio详细信息。

建议使用最新版本的 Visual Studio 编辑器包。

:::zone pivot="windows"

|Visual Studio  |最低 Unity 版本|最低包版本|
|---------------|---------------------|-----------------------|
|2022           |Unity 2019.4         |Visual Studio编辑器 2.0.11|
|2019           |Unity 2017.4         |Visual Studio编辑器 2.0.0|
|2017           |不推荐      |空值
:::zone-end
:::zone pivot="macos"

|Visual Studio for Mac |最低 Unity 版本|最低包版本|
|---------------|---------------------|-----------------------|
|2022           |Unity 2019.4         |Visual Studio编辑器 2.0.11|
|2019           |Unity 2017.4         |Visual Studio编辑器 2.0.0|
|2017           |不推荐      |空值
:::zone-end

## <a name="features"></a>功能
### <a name="unity-event-functions"></a>Unity 事件函数
使用 `Start` 由 IntelliSense 支持自动完成的建议，通过几次击键快速准确地将 Unity 事件函数（如 、 和 ）添加到 `Update` `OnCollisionEnter` C# 脚本。 

:::zone pivot="windows"
![显示 OnCollisionEnter 的 IntelliSense 对话框的屏幕截图。](../media/vs/intellisense-example.png)
:::zone-end
:::zone pivot="macos"
使用 ⌘+Shift+M 为多个 Unity 事件函数及其注释生成代码。
:::zone-end

快速修复事件函数中通过快速修复建议手动添加的任何参数错误。

:::zone pivot="windows"
:::zone-end
:::zone pivot="macos"
:::zone-end

### <a name="high-performance-debugger"></a>高性能调试器
Visual Studio Tools for Unity 支持用户期望从 Visual Studio 中获得的可靠[调试](using-visual-studio-tools-for-unity.md#unity-debugging)功能：

* 设置断点，包括条件断点。
* 计算“监视”窗口中的复杂表达式。
* 检查和修改变量和参数的值。
* 深化到复杂的对象和数据结构。

![检查变量Visual Studio断点上停止的屏幕截图。](../media/vs/debugging-inspecting.png)

### <a name="quick-fixes-and-refactoring-suggestions"></a>快速修复和重构建议
通过 Visual Studio 对 Unity 项目的深刻理解编写更好的代码，以获得最佳做法。

![与 CompareTag Visual Studio字符串比较的屏幕截图。](../media/vs/unity-diagnostics.png)

:::zone pivot="windows"
### <a name="codelens-hints"></a>CodeLens 提示
使用显示来自 Unity 资产的隐式调用的 CodeLens 提示确定从何处调用代码。 选择提示以查看隐式调用的列表。 选择特定调用将直接导航到 Unity 编辑器中的 对象。

通过每个 Unity 事件函数的提示快速区分代码与 Unity 方法。

 ![显示 Unity 脚本和 Unity 消息的 CodeLens 提示的新脚本的屏幕截图。](../media/vs/codelens-support.png)
:::zone-end

:::zone pivot="windows"
### <a name="unity-project-explorer"></a>Unity 项目资源管理器
以与 Unity 编辑器中的层次结构窗口匹配的方式显示项目文件。

![Unity Project资源管理器的屏幕截图。](../media/vs/unity-project-explorer.png)
:::zone-end
:::zone pivot="macos"
### <a name="unity-project-view"></a>Unity 项目视图
Visual Studio for Mac以与 Unity 编辑器中的层次结构窗口匹配的方式自动显示项目文件。

:::zone-end

### <a name="unity-documentation"></a>Unity 文档
检查代码时，请直接在工具提示中查看 Unity 文档。

:::zone pivot="windows"
![工具提示中显示了 Unity 文档的屏幕截图。](../media/vs/visual-studio-tools-unity-documentation-tooltips.png)
:::zone-end
:::zone pivot="macos"

:::zone-end

通过突出显示类或方法名称，然后选择"帮助"> Unity API 参考"菜单项，快速搜索 Unity 文档。

### <a name="support-for-shaders"></a>支持着色器
着色器文件的语法突出显示和自动完成。 

### <a name="support-for-assembly-definition-files"></a>支持程序集定义文件
使用关键字着色和完成 (在) 中直接编辑 Unity 汇编定义 Visual Studio.asmdef 文件。

:::zone pivot="macos"
### <a name="run-and-debug-unit-tests"></a>运行和调试单元测试
直接在 Visual Studio for Mac 中编写、运行和调试单元测试。

:::zone-end

### <a name="automatically-refresh-unity-assets"></a>自动刷新 Unity 资产
在 Unity 和 Visual Studio 之间来回切换Visual Studio。 保存文件时，Unity 中会自动更新对代码的更改。
