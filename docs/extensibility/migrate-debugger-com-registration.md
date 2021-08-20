---
title: 迁移64位调试器 COM 类注册 |Microsoft Docs
description: 了解如何在不写入 HKEY_CLASSES_ROOT 的情况下，将 COM 类注册到无需调试器扩展的 msvsmon。
ms.custom: SEO-VS-2020
ms.date: 11/10/2016
ms.topic: conceptual
ms.assetid: 45cfcee6-7a68-4d4f-b3f6-e2d8a0fa066a
author: gregg-miskelly
ms.author: greggm
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- greggm
ms.openlocfilehash: a9b569f78720d59bf6321ff972bd7f2668ca6729
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122152115"
---
# <a name="migrate-64-bit-debugger-com-class-registration"></a>迁移64位调试器 COM 类注册

对于通过使用 regasm、regsvr32 或直接写入注册表并加载到 *msvsmon.exe* (远程调试器) 来注册 HKEY_CLASSES_ROOT 中的 COM 类的调试器扩展，现在可以向 msvsmon 提供此注册，而无需写入 HKEY_CLASSES_ROOT。 这会影响配置为在 *msvsmon.exe* 进程中加载的旧版 .net 调试器表达式计算器或调试引擎。

## <a name="msvsmon-comclass-def"></a>msvsmon-comclass

若要使用此方法，请 **在* msvsmon (InstallDir：* \Common7\IDE\Remote Debugger\x64 * ) 旁边的文件上添加.msvsmon-comclass-def.js。

下面是一个示例 comclass .def 文件，用于注册一个托管和一个本机类：

文件名： *MyCompany.MyExample.msvsmon-comclass-def.js*

```json
{
  "managedCOMClasses": [
    {
      "clsid": "{C9F48B25-36ED-4B22-8210-98BC5BE4D1E7}",
      "assemblyName": "MyCompany.MyAssembly",
      "className": "MyCompany.MyNamespace.MyClass"
    }
  ],
  "nativeCOMClasses": [
    {
      "clsid": "{42A476E9-8FA7-44D5-ADFE-216AD371EEC9}",
      "dllPath": "MyExample.dll"
    }
  ]
}
```
