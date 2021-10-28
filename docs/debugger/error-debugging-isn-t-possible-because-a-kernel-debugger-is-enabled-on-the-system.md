---
title: 无法进行调试，因为系统上已启用内核调试程序 | Microsoft Docs
description: 当你尝试在已在调试模式下启动的 Windows 7 或 Windows Vista 系统上调试托管代码时，如果应用程序使用 CLR 版本 CLR 2.0、3.0 或 3.5，则会出现此消息。
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.kernel_dbg_enabled
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- kernel debugger
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 8a09e47641ac8b94a3c7a60b39c4260bdd6ea5af
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126737166"
---
# <a name="error-debugging-isn39t-possible-because-a-kernel-debugger-is-enabled-on-the-system"></a>错误：无法进行调试，因为系统上已启用内核调试程序
调试托管代码时，你可能会收到以下错误消息：

```cmd
Debugging isn't possible because a kernel debugger is enabled on the system
```

 在你尝试调试托管代码时，将出现此消息：

- 在已在调试模式下启动的 [!INCLUDE[win7](../debugger/includes/win7_md.md)] 或 [!INCLUDE[wiprlhext](../debugger/includes/wiprlhext_md.md)] 系统上。

- 应用程序使用 CLR 版本 2.0、3.0 或 3.5。

## <a name="solution"></a>解决方案

#### <a name="to-fix-this-problem"></a>修复此问题

- 将应用程序升级为使用 CLR 版本 4.0 或 4.5

   \- 或 -

- 禁用内核调试，并在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中进行调试。

   \- 或 -

- 使用内核调试器而不是 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 进行调试。

   \- 或 -

- 在内核调试器中，禁用用户模式异常。

#### <a name="to-disable-kernel-debugging-in-the-current-session"></a>在当前会话中禁用内核调试

- 在命令提示符处，键入：

    ```cmd
    Kdbgctrl.exe -d
    ```

#### <a name="to-disable-kernel-debugging-for-all-sessions-windows-vista-and-windows-7"></a>对所有会话禁用内核调试（Windows Vista 和 Windows 7）

1. 在命令提示符处，键入：

    ```cmd
    bcdedit /debug off
    ```

2. 重新启动计算机。

#### <a name="to-disable-kernel-debugging-for-all-sessions-other-windows-operating-systems"></a>对所有会话禁用内核调试（其他 Windows 操作系统）

1. 在系统驱动器（通常为 C:\\）上查找 boot.ini。 boot.ini 文件可能是隐藏文件并且是只读的。 因此，您必须使用以下命令才能看到它：

    ```cmd
    dir /ASH
    ```

2. 用记事本打开 boot.ini 并移除下列选项：

    ```cmd
    /debug
    /debugport
    /baudrate
    ```

3. 重新启动计算机。

#### <a name="to-debug-with-the-kernel-debugger"></a>使用内核调试器进行调试

1. 如果内核调试器已挂钩，则将显示一条消息，询问您是否要继续调试。 单击此按钮以继续。

2. 您也许会收到 `User break exception(Int 3).`。如果出现此情况，请键入以下内核调试器命令以继续调试：

     `gn`

## <a name="see-also"></a>请参阅
- [调试器安全](../debugger/debugger-security.md)
- [调试托管代码](../debugger/debugging-managed-code.md)
