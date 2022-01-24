---
title: JIT 优化和调试 | Microsoft Docs
description: 已优化的代码比未优化的代码更难调试。 了解 JIT 优化，以及何时、如何取消该优化。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], optimized code
- optimized code, debugging
ms.assetid: 19bfabf3-1a2e-49dc-8819-a813982e86fd
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: be8a0b57bc009d776f20ca2bebae94627f4a4909
ms.sourcegitcommit: 7d319435c35075d4cec021b7b667666a81c02435
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2022
ms.locfileid: "137650290"
---
# <a name="jit-optimization-and-debugging"></a>JIT 优化和调试
如果尝试调试代码，则在该代码未优化时更易调试。 优化代码时，编译器和运行时会对发出的 CPU 代码进行更改，使其运行速度更快，但与原始源代码的映射不太直接。 如果映射不太直接，则调试器通常无法告诉你局部变量的值，代码步进和断点也可能无法按预期要求工作。

> [!NOTE]
> 有关 JIT（实时）调试的详细信息，请阅读[此文档](../debugger/debug-using-the-just-in-time-debugger.md)。

## <a name="how-optimizations-work-in-net"></a>.NET 中的优化如何工作 
通常，“发布”生成配置会创建优化的代码，“调试”生成配置则不会。 `Optimize` MSBuild 属性控制是否指示编译器优化代码。

在 .NET 生态系统中，代码通过一个两步过程从源代码转换为 CPU 指令：首先，C# 编译器将键入的文本转换为称为 MSIL 的中间二进制格式，并将 MSIL 写入 .dll 文件。 随后，.NET 运行时将此 MSIL 转换为 CPU 指令。 这两个步骤都可以优化到一定程度，但 .NET 运行时执行的第二个步骤将执行更重要的优化。

## <a name="the-suppress-jit-optimization-on-module-load-managed-only-option"></a>“在模块加载时取消 JIT 优化(仅限托管)”选项
调试器提供了一个选项，该选项控制在启用优化的情况下编译的 DLL 加载到目标进程内部时所发生的情况。 如果未选中此选项（默认状态），则当 .NET 运行时将 MSIL 代码编译为 CPU 代码时，它会保留优化的启用状态。 如果选中该选项，则调试器将请求禁用优化。

若要找到“在模块加载时取消 JIT 优化(仅限托管)”选项，请选择“工具” > “选项”，然后选择“调试”节点下的“常规”页 。

![取消 JIT 优化](../debugger/media/suppress-jit-tool-options.png "取消 JIT 优化")

## <a name="when-should-you-check-the-suppress-jit-optimization-option"></a>何时应选中“取消 JIT 优化”选项？
从另一个源（例如 nuget 包）下载 DLL 并要​​调试此 DLL 中的代码时，请选中此选项。 为了使取消生效，还必须找到此 DLL 的符号 (.pdb) 文件。

如果只想调试本地生成的代码，最好将此选项保留为未选中状态，因为在某些情况下，启用此选项会大大减慢调试速度。 造成减速的原因有两个：

* 经过优化的代码运行速度更快。 如果为大量代码关闭优化，则可能会增加性能影响。
* 如果启用“仅我的代码”，则调试器甚至不会尝试为经过优化的 DLL 加载符号。 查找符号可能需要很长时间。

## <a name="limitations-of-the-suppress-jit-optimization-option"></a>“取消 JIT 优化”选项的局限性 
在两种情况下，启用此选项不起作用：

1. 在将调试器附加到已在运行的进程的情况下，此选项对附加调试器时已加载的模块无效。
2. 此选项对已预编译（也称为 ngen'ed）为本机代码的 DLL 无效。 但是，可以通过以下方式禁用预编译的代码：通过将环境变量“COMPlus_ReadyToRun”设置为“0”来启动进程。 这将指示 .NET Core 运行时禁用预编译的映像，从而迫使运行时实时编译框架代码。 

   如果要将目标设置为 .NET Framework，请添加环境变量 **"COMPlus_ZapDisable"，** 将其设置为 **"1"。** 
   
通过将 `"COMPlus_ReadyToRun": "0"`  配置文件添加到 *Properties\launchSettings.json* 文件的每个配置文件进行设置：

```json
{
  "iisSettings": {
    "windowsAuthentication": false,
    "anonymousAuthentication": true,
    "iisExpress": {
      "applicationUrl": "http://localhost:59694/",
      "sslPort": 44320
    }
  },
  "profiles": {
    "IIS Express": {
      "commandName": "IISExpress",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development",
        "COMPlus_ReadyToRun": "0"
      }
    },
    "HttpLoggingSample": {
      "commandName": "Project",
      "launchBrowser": true,
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development",
        "COMPlus_ReadyToRun": "0"
      },
      "applicationUrl": "https://localhost:5001;http://localhost:5000"
    }
  }
}
```


## <a name="see-also"></a>请参阅
- [如何调试 .NET Framework 源代码](../debugger/how-to-debug-dotnet-framework-source.md)
- [调试托管代码](../debugger/debugging-managed-code.md)
- [使用调试器浏览代码](../debugger/navigating-through-code-with-the-debugger.md)
- [附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [托管执行过程](/dotnet/standard/managed-execution-process)
