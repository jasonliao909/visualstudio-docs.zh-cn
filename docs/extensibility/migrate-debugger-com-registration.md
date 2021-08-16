---
title: 迁移 64 位调试器 COM 类注册|Microsoft Docs
description: 了解如何将 COM 类注册到 msvsmon 以用于调试器扩展，而无需HKEY_CLASSES_ROOT。
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
ms.openlocfilehash: cd02fe3e8df0372a2a5503c455c706c0006fcef1d14b1ccacfb1695036646415
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121375151"
---
# <a name="migrate-64-bit-debugger-com-class-registration"></a>迁移 64 位调试器 COM 类注册

对于使用 regasm、regsvr32 或直接写入注册表并加载到msvsmon.exe *(* 远程调试器) 中的 com 类在 HKEY_CLASSES_ROOT 中注册 COM 类的调试器扩展，现在无需写入 HKEY_CLASSES_ROOT 即可向 msvsmon 提供此注册。 这会影响配置为在进程内加载的旧版 .NET 调试器表达式 *msvsmon.exe引擎。*

## <a name="msvsmon-comclass-def"></a>msvsmon-comclass-def

若要使用此技术，请.msvsmon-comclass-def.js *msvsmon (InstallDir：\Common7\IDE\Remote* Debugger\x64*) 。

下面是一个示例 msvsmon-comclass-def 文件，该文件注册了一个托管类和一个本机类：

FileName：MyCompany.MyExample.msvsmon-comclass-def.js *on*

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
