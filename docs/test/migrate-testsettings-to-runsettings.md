---
title: 将 testsettings 迁移到 runsettings
description: 了解如何将 testsettings 迁移到 runsettings
ms.custom: SEO-VS-2020
ms.date: 03/18/2021
ms.topic: conceptual
f1_keywords:
- vs.UnitTest.Migrate
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- multiple
ms.openlocfilehash: 348de2d34e30c96449dcd2e4c2ba6eb83ed24c4c
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128429683"
---
# <a name="upgrade-from-testsettings-to-runsettings"></a>从 .testsettings 升级到 .runsettings

可以使用随 Visual Studio 一起安装的 SettingsMigrator 工具将测试配置文件从 .testsettings 升级到 .runsettings。 根据 Visual Studio 安装位置，可以在以下路径中找到设置迁移程序工具：
::: moniker range=">=vs-2022"
`C:\Program Files\Microsoft Visual Studio\2022\Enterprise\Common7\IDE\Extensions\TestPlatform\SettingsMigrator.exe`
::: moniker-end
::: moniker range="vs-2019"
`C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\Extensions\TestPlatform\SettingsMigrator.exe`
::: moniker-end

在正确的目录位置中，可以使用以下格式运行该工具：

```console
SettingsMigrator.exe <Full path to testsettings file to be migrated>
SettingsMigrator.exe <Full path to testsettings file to be migrated> <Full path to runsettings file to be created>
```

## <a name="examples"></a>示例
```console
SettingsMigrator.exe E:\MyTest\MyTestSettings.testsettings
SettingsMigrator.exe E:\MyTest\MyTestSettings.testsettings E:\MyTest\MyNewRunSettings.runsettings
```

如果你有兴趣阅读有关 .testsettings 选项如何转换为 .runsettings 的详细信息，则可以在 GitHub 上的[开放源代码测试平台存储库](https://github.com/microsoft/vstest-docs/blob/master/RFCs/0023-TestSettings-Deprecation.md#migration)中找到更多实现详细信息。

## <a name="see-also"></a>另请参阅

- [通过 `.runsettings` 配置测试运行](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)
- [从 MSTestv1 升级到 MSTestv2](../test/mstest-update-to-mstestv2.md)
- [单元测试代码](../test/unit-test-your-code.md)
- [使用测试资源管理器调试单元测试](../test/debug-unit-tests-with-test-explorer.md)
