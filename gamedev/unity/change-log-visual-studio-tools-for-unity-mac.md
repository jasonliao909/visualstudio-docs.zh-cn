---
title: 更改日志（Visual Studio Tools for Unity、Mac）| Microsoft Docs
description: 查看 Visual Studio Tools for Unity、Mac 的更改日志。 查看版本 1.0.0.0 到 2.7.0.0 及更高版本的版本变化。
ms.custom: ''
ms.date: 6/3/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: conceptual
ms.assetid: 33a6ac54-d997-4308-b5a0-af7387460849
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: 5ab2a8e5e3a4ef49999c2e986353f15684508a53306284e5832ea4d71a57fc0e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121439999"
---
# <a name="change-log-visual-studio-tools-for-unity-mac"></a>更改日志（Visual Studio Tools for Unity、Mac）

Visual Studio Tools for Unity 更改日志。

## <a name="21020"></a>2.10.2.0
发布时间：2021 年 6 月 2 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了 [`UNT0024`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0024.md) 诊断。 优先使用标量计算，而不要考虑矢量计算。

- **评估版：**

  - 添加了对使用可移植 pdb 符号正确筛选可见局部区域的支持。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 固定播放器宣布使用最新的 Unity 版本进行分析。

## <a name="21010"></a>2.10.1.0
发布时间：2021 年 5 月 11 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了快速修复 [`UNT0008`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0008.md) 的稳定性问题。

  - 修复了线程的性能问题。

  - 修复了错误列表中禁止的警告和错误的筛选。

  - 修复了筛选 Unity 后台进程的问题。

## <a name="21000"></a>2.10.0.0
发布时间：2021 年 4 月 13 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了 [`UNT0019`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0019.md) 诊断。 不必要的间接调用 `GameObject.gameObject` 。

  - 添加了 [`UNT0020`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0020.md) 诊断。 `MenuItem` 在非静态方法中使用的 特性。

  - 添加了 [`UNT0021`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0021.md) 诊断。 应保护 Unity 消息 (选择加入) 。

  - 添加了 [`UNT0022`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0022.md) 诊断。 设置位置和旋转的低效方法。

  - 添加了 [`UNT0023`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0023.md) 诊断。 Unity 对象上的联合赋值。

  - 为 `IDE0074` 添加了 [`USP0017`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0017.md) 抑制器。 Unity 对象不应使用联合赋值。

## <a name="2940"></a>2.9.4.0
发布时间：2021 年 4 月 6 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复测试枚举的问题

## <a name="2930"></a>2.9.3.0
发布时间：2021 年 3 月 30 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复测试运行程序的问题 

## <a name="2920"></a>2.9.2.0
发布时间：2021 年 3 月 2 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了 Unity 消息对话框中的搜索突出显示。

  - 修复了 Unity 项目树视图的稳定性问题。

- **调试：**

  - 修复了对条件断点的处理。

## <a name="2910"></a>2.9.1.0
发布时间：2021 年 2 月 9 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对从 IDE 运行和调试 Unity 测试的支持

- **评估版：**

  - 向局部变量添加了 `Active Scene`，同时显示根游戏对象。

  - 向局部变量添加了 `this.gameObject`，鉴于它广泛用于 Unity 项目。

  - 向所有 `GameObject` 实例添加了 `Children` 和 `Components` 组，这样就可以轻松地显示所有对象层次结构。

  - 向所有 `GameObject` 实例添加了 `Scene Path`，以显示场景中的位置。

  - 新增了对 `JobEntityBatch`/Lambdas 的支持，便于将实体用于源生成器。

  - 改进了对（使用索引桶）显示大型数组的支持。

  - 添加了 2019.4 API 缺少的 Unity 消息。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了 Unity 消息对话框的稳定性问题

  - 修复了非 ENU 语言的各种 UI 问题。

  - 修复了与 [`UNT0018`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0018.md) 诊断有关的稳定性问题。

- **调试：**

  - 修复了使用 `Trace` 方法时的 VM 断开连接问题。

- **评估版：**

  - 修复了对抛出异常的过时属性的筛选。

## <a name="2900"></a>2.9.0.0
发布时间：2021 年 1 月 20 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 新增了对 `raytrace shaders`、`UXML` 和 `USS` 文件的支持。

  - 更新了 Unity 消息 API（用于所有用作协同例程的方法）。

  - 更新了 Android SDK 检测。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了对协同例程和 `AssetPostprocessor.OnAssignMaterialModel` 发出错误警告的 [`UNT0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0006.md) 诊断。

## <a name="2840"></a>2.8.4.0
发布时间：2020 年 12 月 15 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了关闭 Unity 事件创建向导时的可靠性问题。

## <a name="2830"></a>2.8.3.0
发布时间：2020 年 11 月 10 日

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了即使解决方案中没有任何 VSTU 项目，也附加到 Unity 的问题。

## <a name="2820"></a>2.8.2.0
发布时间：2020 年 10 月 27 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 改进了 [`UNT0010`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0010.md) 诊断以应用于从 继承的所有内容 `Component` ，而不只是 `MonoBehaviour` 。

## <a name="2810"></a>2.8.1.0
发布时间：2020 年 10 月 13 日

### <a name="new-features"></a>新增功能

- **评估版：**

  - 添加了对使用调用进行隐式转换的支持。 以前，评估程序强制实施严格的类型检查，从而导致 `Failed to find a match for method([parameters...])` 警告消息。

- **集成：**

  - 添加了 [`UNT0018`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0018.md) 诊断。 不应在性能 `System.Reflection` 关键型消息（如 `Update` `FixedUpdate` 、、 或 ） `LateUpdate` 中使用功能 `OnGUI` 。

  - 改进了 [`USP0003`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0003.md) 和 [`USP0005`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0005.md) 抑制器，支持所有 `AssetPostprocessor` 静态方法。

  - 为 `CS8618` 添加了 [`USP0016`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0016.md) 抑制器。 `C# 8.0` 引入了可为空引用类型和不可为 null 的引用类型。 不支持从 继承的类型的初始化 `UnityEngine.Object` 检测，将导致错误。

  - 现在，对 Unity 2019.x 和 2020.x+ 使用相同的播放器和 asmdef 项目生成机制。
  
  - 改进了使用向导生成 Unity 消息时的体验。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了注释中消息意外完成的问题。

## <a name="2800"></a>2.8.0.0 
发布时间：2020 年 9 月 14 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了 Unity 2019.x 的播放器项目生成问题。

## <a name="2710"></a>2.7.1.0
发布日期：2020 年 8 月 5 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 已将 Unity 消息 API 更新为 2019.4。

  - 为 `CA1823` 添加了 [`USP0013`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0013.md) 抑制器。 不应将具有 `SerializeField` 或 `SerializeReference` 属性的专用字段标记为未使用 (FxCop)。
  
  - 为 `CA1822` 添加了 [`USP0014`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0014.md) 抑制器。 不应将 Unity 消息标记为 `static` 修饰符的候选项 (FxCop)。

  - 为 `CA1801` 添加了 [`USP0015`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0015.md) 抑制器。 不应从 Unity 消息中删除未使用的参数 (FxCop)。
  
  - 添加了对 [`USP0009`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0009.md) 抑制器的 `MenuItem` 支持。  

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了 [`USP0001`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0001.md) 和 [`USP0002`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0002.md) 抑制器不能使用额外的括号或方法参数的问题。
  
  - 修复了即使在 Unity 设置中禁用自动刷新时也必须刷新资产数据库的问题。

## <a name="2700"></a>2.7.0.0
发布日期：2020 年 6 月 23 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了在 Unity 重新生成解决方案和项目时对持久性解决方案文件夹的支持。

  - 添加了 [`UNT0015`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0015.md) 诊断。 使用 `InitializeOnLoadMethod` 或 `RuntimeInitializeOnLoadMethod` 属性检测不正确的方法签名。

  - 添加了 [`UNT0016`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0016.md) 诊断。 使用 `Invoke`、`InvokeRepeating`、`StartCoroutine` 或 `StopCoroutine` 时，如果第一个参数是字符串文本，那么就不是类型安全的。

  - 添加了 [`UNT0017`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0017.md) 诊断。 `SetPixels` 调用速度缓慢。

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了当游戏在旧的 Mono 运行时上运行时创建断点的问题（尝试在创建断点时立即绑定断点）。 
  
- **集成：**

  - 在 Unity 消息向导中筛选消息时，不要重置选择。
  
  - 修复了 [`USP0004`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0004.md)、[`USP0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0006.md) 和 [`USP0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0007.md) 抑制器的以下规则：为所有使用 SerializeField 属性装饰的字段禁止 `IDE0044`（只读），`IDE0051`（未使用）、`CS0649`（从未指定）。 为扩展 `Unity.Object` 的所有类型的公共字段禁止 `CS0649`（从未指定）。

  - 修复了 [`UNT0014`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0014.md) 的泛型类型参数检查。

- **评估版：**

  - 修复了与枚举的相等比较。

## <a name="2610"></a>2.6.1.0
发布日期：2020 年 5 月 19 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 如果无法在 Unity 端创建消息服务器，则会发出警告。

  - 在轻量级编译期间正确运行分析器。

  - 修复了与 Unity 中心安装相关的 API 文档。
  
  - 修复了调试器可视化工具故障。

## <a name="2600"></a>2.6.0.0
发布时间：2020 年 4 月 14 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了 [`UNT0012`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0012.md) 诊断。 在 `StartCoroutine()` 中检测并包装对协同例程的调用。

  - 添加了 [`UNT0013`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0013.md) 诊断。 检测并删除无效或冗余的 `SerializeField` 属性。

  - 添加了 [`UNT0014`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0014.md) 诊断。 检测用非组件或非接口类型调用的 `GetComponent()`。

  - 为 `IDE0051` 添加了 [`USP0009`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0009.md) 抑制器。 请勿将具有 `ContextMenu` 属性的方法或由具有 `ContextMenuItem` 属性的字段引用的方法标记为未使用。

  - 为 `IDE0051` 添加了 [`USP0010`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0010.md) 抑制器。 请勿将具有 `ContextMenuItem` 属性的字段标记为未使用。

  - 为 `IDE0044` 添加了 [`USP0011`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0011.md) 抑制器。 请勿将具有 `ContextMenuItem` 属性的字段设为只读字段。

  - [`USP0004`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0004.md)、[`USP0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0006.md) 和 [`USP0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0007.md) 现在都适用于 `SerializeReference` 和 `SerializeField` 属性。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 当编辑器能够进行通信时，才向 Unity 发送启动/停止命令。

  - 修复了与继承消息相关的 QuickInfo 文档。

  - 修复了 `CreateInspectorGUI` 消息的消息范围。

  - 请勿报告与具有多态修饰符的方法相关的 [`UNT0001`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0001.md)。

- **评估版：**

  - 修复了别名为 using 的处理。
  
  - 修复了 null 值的处理。  

## <a name="2520"></a>2.5.2.0

发布日期：2020 年 3 月 23 日

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了附加时的线程注册问题。

## <a name="2510"></a>2.5.1.0

发布日期：2020 年 3 月 3 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 为 `IDE0051` 添加了 [`USP0008`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0008.md) 抑制器。 与 Invoke、InvokeRepeating、StartCoroutine 或 StopCoroutine 一起使用的专用方法不应标记为未使用。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了 OnDrawGizmos/OnDrawGizmosSelected 文档。

- **评估版：**

  - 修复了 Lambda 参数检查。

## <a name="2501"></a>2.5.0.1

发布日期：2020 年 2 月 19 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了针对错误的消息签名的 [`UNT0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0006.md) 诊断检查。 当检查具有多个继承级别的类型时，此诊断可能会失败，并显示以下消息：`warning AD0001: Analyzer 'Microsoft.Unity.Analyzers.MessageSignatureAnalyzer' threw an exception of type 'System.ArgumentException' with message 'An item with the same key has already been added`。

## <a name="2500"></a>2.5.0.0

发布日期：2020 年 1 月 22 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对 HLS 文件的支持。
  
  - 切换到“新建文件夹”对话框用户界面。
  
  - 切换到新的可访问属性网格以进行设置。

  - 为 `IDE0051` 添加了 [`USP0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0006.md) 抑制器。 具有 `SerializeField` 属性的专用字段不应标记为未使用。

  - 为 `CS0649` 添加了 [`USP0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0007.md) 抑制器。 具有 `SerializeField` 属性的字段不应标记为未分配。  

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了项目生成问题（无法始终正确找到 `GenerateTargetFrameworkMonikerAttribute` 目标）。

- **评估版：**

  - 修复了字符串评估问题（不使用 ToString() 调用）

## <a name="2420"></a>2.4.2.0

发布时间：2019 年 12 月 3 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了使用用户定义的接口进行的诊断。

  - 修复了表达式格式错误的快速工具提示。
  
## <a name="2410"></a>2.4.1.0

发布时间：2019 年 11 月 6 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对 Unity 后台进程的支持。 （调试程序能够自动连接到主进程，而不是子进程）。

  - 为 Unity 消息添加了快速工具提示，可显示关联的文档。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 使用高级二进制和 invocation 表达式修复了标签比较分析器 `UNT0002`。

### <a name="deprecated-features"></a>弃用的功能

- **集成：**

  - 展望未来，Visual Studio Tools for Unity 将仅支持 Visual Studio 2017+。

## <a name="2400"></a>2.4.0.0

发布时间：2019 年 10 月 15 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 为所有 Unity 消息的 `IDE0060`（未使用的参数）添加了 [`USP0005`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0005.md) 抑制器。

  - 为标有 `TooltipAttribute` 的字段添加了快速工具提示。 （这也适用于使用此字段的简单 get 访问器）。

## <a name="2330"></a>2.3.3.0

发布日期：2019 年 9 月 23 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 为 IDE0060 添加了新的抑制器，防止 IDE 显示针对删除未使用参数的快速修复。
    - `USP0005` 对于 `IDE0060`：Unity 消息由 Unity 运行时调用。

## <a name="2320"></a>2.3.2.0

发布日期：2019 年 9 月 16 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 通过添加特定于 Unity 的新诊断，深化了 Visual Studio 对 Unity 项目的理解。 还通过取消不适用于 Unity 项目的一般 C# 诊断，使 IDE 更智能。 例如，IDE 不会显示将检查器变量更改为 `readonly` 的快速修复，因此这会阻止你修改 Unity 编辑器中的变量。
    - `UNT0001`：即使 Unity 消息为空，运行时也会调用它们，请勿声明它们，以避免 Unity 运行时进行不必要的处理。
    - `UNT0002`：使用字符串相等比较标记的速度比内置的 CompareTag 方法慢。
    - `UNT0003`：为了获得类型安全性，最好使用 GetComponent 的通用形式。
    - `UNT0004`：更新消息依赖于帧速率，应使用 Time.deltaTime 而不是 Time.fixedDeltaTime。
    - `UNT0005`：固定更新消息与帧速率无关，应使用 Time.fixedDeltaTime 而不是 Time.deltaTime。
    - `UNT0006`：检测到此 Unity 消息的方法签名不正确。
    - `UNT0007`：Unity 重写与 null 合并不兼容的 Unity 对象的 null 比较运算符。
    - `UNT0008`：Unity 重写与 null 传播不兼容的 Unity 对象的 null 比较运算符。
    - `UNT0009`：将 InitializeOnLoad 特性应用于类时，需要提供静态构造函数。 InitializeOnLoad 特性可确保在编辑器启动时调用该函数。
    - `UNT0010`：应只使用 AddComponent() 创建 MonoBehaviours。 MonoBehaviour 是一个组件，需要附加到 GameObject。
    - `UNT0011`：应只使用 CreateInstance() 创建 ScriptableObject。 ScriptableObject 需要由 Unity 引擎创建，才能处理 Unity 消息方法。
    - `USP0001` 对于 `IDE0029`：Unity 对象不应使用 Null 合并。
    - `USP0002` 对于 `IDE0031`：Unity 对象不应使用 Null 传播。
    - `USP0003` 对于 `IDE0051`：Unity 消息由 Unity 运行时调用。
    - `USP0004` 对于 `IDE0044`：不应将具有 SerializeField 特性的字段设为只读。

## <a name="2310"></a>2.3.1.0

发布日期：2019 年 9 月 4 日

### <a name="new-features"></a>新增功能

- **评估版：**

  - 添加了对更佳类型显示的支持，即 `List<object>`，而不是 `List'1[[System.Object, <corlib...>]]`。

  - 添加了对指针成员访问的支持，即 `p->data->member`。

  - 添加了对数组初始值设定项中的隐式转换的支持，即 `new byte [] {1,2,3,4}`。

  - 添加了检查字节数组和字符串时对十六进制编辑器的支持。

## <a name="2300"></a>2.3.0.0

发布日期：2019 年 8 月 13 日

### <a name="bug-fixes"></a>Bug 修复

- **评估版：**

  - 修复了出现异常的单步执行问题。

  - 修复了伪标识符（如 $exception）计算问题。

  - 防止在取消引用无效地址时出现故障。  

  - 修复了已卸载的 appdomains 的问题。

## <a name="2200"></a>2.2.0.0

发布时间：2019 年 7 月 25 日

### <a name="bug-fixes"></a>Bug 修复

- **评估版：**

  - 修复了 IntPtr 类型的检测。

- **调试器：**

  - 修复了捕获点和函数断点的处理。

## <a name="2130"></a>2.1.3.0

发布时间：2019 年 7 月 9 日

### <a name="new-features"></a>新增功能

- **调试器：**

  - 增加了对捕获异常子类的支持。

  - 增加了对 MDS 协议 2.51 的支持。

- **集成：**

  - 增加了对 asmdef 文件的支持。

  - 从模板添加文件时切换到重命名模式（模仿 Unity 编辑器的行为）。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了与 Unity 播放器通信时格式错误消息的处理。

- **评估版：**

  - 修复了表达式中命名空间的处理。

## <a name="2120"></a>2.1.2.0

发布时间：2019 年 7 月 2 日

### <a name="bug-fixes"></a>Bug 修复

- **评估版：**

  - 修复了包含不可解析表达式的错误报告。

## <a name="2110"></a>2.1.1.0

发布时间：2019 年 6 月 27 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 已将 MonoBehaviour API 更新到 2019.1。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了 Unity 项目资源管理器的性能。

  - 启用轻型生成时，修复了要输出的报告警告和错误。

  - 修复了轻型生成性能。

## <a name="2100"></a>2.1.0.0

发布时间：2019 年 6 月 20 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 禁用了 Unity 项目的完整生成，取而代之的是使用 IntelliSense 错误和警告。 事实上，Unity 使用表示 Unity 内部所执行操作的类库项目创建 Visual Studio 解决方案。 尽管如此，Visual Studio 中的生成结果从未由 Unity 使用或选取，因为其编译管道已关闭。 在 Visual Studio 中生成只是使用资源。 如果由于你具有工具或具有依赖于完整生成的安装程序而需要完整生成，则可以禁用此优化（设置/Tools for Unity/禁用项目的完整生成）。
  
  - 添加了对 UPE 中的 Unity 包的支持。 只有引用包（使用 `Packages` 文件夹中的 manifest.json）和本地包（嵌入在 `Packages` 文件夹中）是可见的。

## <a name="2021"></a>2.0.2.1

发布时间：2019 年 5 月 30 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 增加了 Unity 执行目标的自定义图标。

## <a name="2020"></a>2.0.2.0

发布时间：2019 年 4 月 2 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对保存时自动刷新 Unity 资产数据库的支持。 这在默认情况下处于启用状态，当在 Visual Studio 中保存脚本时，将在 Unity 端触发重新编译。 保存时可以在“工具\选项\适用于 Unity 的工具\刷新 Unity 的 AssetDatabase”中禁用此功能。

  - 添加了对脱机文档设置首选 unity 安装的支持。

  - 添加了适用于新编辑器的上下文菜单。

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了空帧的程序集筛选和帧检查。

## <a name="2011"></a>2.0.1.1
 
 发布日期：2019 年 3 月 26 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 暂时将 Mono 设置为此特定版本的默认且唯一可用的调试器。

## <a name="2006"></a>2.0.0.6

发布日期：2019 年 3 月 26 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对“附加到 Unity 并播放”的支持。

## <a name="2005"></a>2.0.0.5

发布日期：2019 年 3 月 20 日

### <a name="new-features"></a>新增功能

- **Project Generation:**

  - 处理解决方案文件时，请保留外部属性。
  
- **评估版：**

  - 添加了对别名限定名称的支持（目前仅支持全局命名空间）。 因此，表达式计算器现在正在使用 global::namespace.type 窗体接受类型。

  - 添加了对 `pointer[index]` 窗体的支持，在语义上等同于指针取消引用 `*(pointer+index)` 窗体。

## <a name="2004"></a>2.0.0.4

发布日期：2019 年 3 月 5 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 更新了 `ScriptableObject` API。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 从模板中删除了命名空间。

## <a name="2003"></a>2.0.0.3
 
 发布日期：2019 年 3 月 5 日

### <a name="new-features"></a>新增功能

- **Project Generation:**

  - 公共字段和序列化字段将不再引发警告。 在创建这些消息的 Unity 项目中，我们自动禁止了 `CS0649` 和 `IDE0051` 编译器警告。

- **集成：**

  - 如果运行多个 Unity 进程，系统将提示附加到特定实例。

- **评估版：**

  - 增加了对本地函数的支持。

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了在使用旧协议版本时读取命名参数的自定义属性。

## <a name="2002"></a>2.0.0.2

发布时间：2019 年 2 月 4 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 更新了 MonoBehaviour API。

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了在调试器中设置基元值。

## <a name="2001"></a>2.0.0.1

发布时间：2018 年 12 月 4 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了安装包的自包含。

## <a name="2000"></a>2.0.0.0
 发布时间：2018 年 12 月 4 日

### <a name="new-features"></a>新增功能

- **调试器：**

  - 用 Windows 上的同核心 Unity 调试程序替换了 Mac 上的 Unity 调试程序。

  - 将 NRefactory 替换为 Roslyn 以进行表达式计算。

  - 添加了对指针的支持：取消引用、强制转换和指针算法（为此同时需要 Unity 2018.2+ 和新运行时）。

  - 添加了对数组指针视图（例如在 C++ 中）的支持。 需要一个指针表达式，然后追加一个逗号和要查看的元素数。

  - 添加了对异步构造的支持。

  - 增加了对伪变量（异常和对象标识符）的支持。

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了表达式格式不正确或不受支持的表达式计算。

## <a name="1700"></a>1.7.0.0

发布时间：2018 年 11 月 13 日

### <a name="new-features"></a>新增功能

- **调试器：**

  - 在“附加”对话框中添加了更多客户端信息（IP、计算机名称）。

### <a name="bug-fixes"></a>Bug 修复

- **调试器：**

  - 修复了用于与 Unity 调试器引擎进行通信的库中的死锁，此死锁会导致 Visual Studio 或 Unity 冻结，尤其是在用户点击“附加到 Unity”或重启游戏时。

- **集成：**

  - 修复了选中另一个默认编辑器时 Unity 插件的激活。

  - 修复了 Unity 文件模板创建。

## <a name="1602"></a>1.6.0.2

发布时间：2018 年 7 月 24 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 回滚了针对 Unity 性能缺陷的解决方案（此缺陷已由 Unity 修复）。

## <a name="1601"></a>1.6.0.1

发布时间：2018 年 7 月 10 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 支持固定着色器代码着色。

## <a name="1600"></a>1.6.0.0

发布时间：2018 年 6 月 26 日

### <a name="bug-fixes"></a>Bug 修复

- **向导：**

  - 修复了 OnApplicationFocus 消息拼写错误。

- **Project Generation:**

  - Unity 性能 Bug 的暂时解决方法：生成项目时缓存 MonoIsland。

  - 使用新版 Unity 运行时，不要再将可移植 pdb 转换为 mdb。

## <a name="1502"></a>1.5.0.2

发布时间：2018 年 4 月 18 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对基本着色器代码补全的支持。

  - 添加了对在着色器文件中切换注释的支持。

## <a name="1501"></a>1.5.0.1

发布时间：2018 年 3 月 28 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对 Unity 项目资源管理器中的额外模板的支持。

## <a name="1500"></a>1.5.0.0

发布时间：2018 年 3 月 21 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对检测并附加到通过 USB 连接的 Android 播放器的支持。

## <a name="1403"></a>1.4.0.3

发布时间：2018 年 3 月 5 日

### <a name="new-features"></a>新增功能

- **Project Generation:**

  - 添加了对 Unity 2018.1 中新项目生成器的支持。

- **集成：**

  - 为专用设置添加了选项面板。

## <a name="1402"></a>1.4.0.2

发布时间：2018 年 1 月 24 日

### <a name="bug-fixes"></a>Bug 修复

- **Project Generation:**

  - 修复了 Mono 版本检测的问题。

- **集成：**

  - 修复了 2018.1 和插件激活的计时问题。

  - 修复了检测新播放器时的通知。

## <a name="1401"></a>1.4.0.1

发布时间：2018 年 1 月 23 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了双击展开/折叠文件夹

## <a name="1400"></a>1.4.0.0

发布时间：2017 年 12 月 13 日

### <a name="new-features"></a>新增功能

- **Project Generation:**

  - 添加了对 .NET Standard 的支持。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 固定自动 pdb 到 mdb 调试符号转换。

## <a name="1301"></a>1.3.0.1

发布时间：2017 年 12 月 12 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了在尝试更改数组大小时对 EditorPrefs.GetBool 的间接调用影响检查器的问题。

- **向导：**

  - 在插入方法前刷新 roslyn 上下文。

## <a name="1300"></a>1.3.0.0

发布时间：2017 年 11 月 20 日

### <a name="new-features"></a>新增功能

- **向导：**

  - 添加了“实现 Unity 消息”向导。

  - 添加了对 Mac 7.4 的 VS 中 API 新完成的支持。

## <a name="1200"></a>1.2.0.0

发布时间：2017 年 10 月 23 日

### <a name="new-features"></a>新增功能

- **调试器：**

  - 增加了对可移植调试符号文件的支持。

### <a name="bug-fixes"></a>Bug 修复

- **Project Generation:**

  - 修复了额外 .dll 扩展名错误添加到程序集文件问题。

  - 不强制 AllowAttachedDebuggingOfEditor Unity，因为现在默认为“true”。

## <a name="1103"></a>1.1.0.3

发布时间：2017 年 10 月 23 日

### <a name="new-features"></a>新增功能

- **Project Generation:**

  - 添加了对 .NET 4.6 配置文件的支持。

## <a name="1102"></a>1.1.0.2

发布时间：2017 年 8 月 8 日

### <a name="new-features"></a>新增功能

- **调试器：**

  - 如果不确定附加到哪个 Unity，启动“附加到进程”对话框。

- **Project Generation:**

  - 使用 Unity 5.6 时，始终启用不安全编译开关。

## <a name="1101"></a>1.1.0.1

发布时间：2017 年 7 月 20 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对本地化资源的支持。

## <a name="1100"></a>1.1.0.0

发布时间：2017 年 7 月 12 日

### <a name="new-features"></a>新增功能

- **集成：**

  - 添加了对通过“附加到进程”窗口附加到播放器和编辑器的支持。

- **Project Generation:**

  - 修复了使用 mcs.rsp 文件的程序集名称引用。

  - 添加了对 assembly.json 编译单元的支持。

  - 修复了通过 API 级别进行定义的问题。

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了编译时的着色器错误消息。

## <a name="1001"></a>1.0.0.1

发布时间：2017 年 5 月 4 日

### <a name="bug-fixes"></a>Bug 修复

- **集成：**

  - 修复了混合和常规项目的活动文档跟踪。

## <a name="1000"></a>1.0.0.0

发布时间：2017 年 5 月 3 日
