---
title: 安装后必须运行的命令|Microsoft Docs
description: 了解必须在安装扩展过程中运行的命令，该扩展插件是通过 .msi 文件部署的Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- post-install commands
ms.assetid: c9601f2e-2c6e-4da9-9a6e-e707319b39e2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 5659c2adbe3b7d8f74ccf0a3a28feefdd7d9421c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664396"
---
# <a name="commands-that-must-be-run-after-installation"></a>安装后必须运行的命令
如果通过.msi文件部署扩展，则必须在安装过程中运行 **devenv /setup，Visual Studio** 发现扩展。

> [!NOTE]
> 本主题中的信息适用于查找 2008 *devenv.exe及Visual Studio* 版本。 若要了解如何使用更高版本 *devenv.exe* 发现Visual Studio，请参阅 [检测系统要求](../../extensibility/internals/detecting-system-requirements.md)。

## <a name="find-devenvexe"></a>查找devenv.exe
 可以使用 RegLocator 表devenv.exeAppSearch 表将注册表值存储为属性，从安装程序写入的注册表值中查找每个版本的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 注册表值。 有关详细信息，请参阅 [检测系统要求](../../extensibility/internals/detecting-system-requirements.md)。

### <a name="reglocator-table-rows-to-locate-devenvexe-from-different-versions-of-visual-studio"></a>RegLocator 表行，用于devenv.exe不同版本的表Visual Studio

|签名|Root|键|名称|类型|
|-----------------|----------|---------|----------|----------|
|RL_DevenvExe_2002|2|SOFTWARE\Microsoft\VisualStudio\7.0\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2003|2|SOFTWARE\Microsoft\VisualStudio\7.1\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2005|2|SOFTWARE\Microsoft\VisualStudio\8.0\Setup\VS|EnvironmentPath|2|
|RL_DevenvExe_2008|2|SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS|EnvironmentPath|2|

### <a name="appsearch-table-rows-for-corresponding-reglocator-table-rows"></a>对应 RegLocator 表行的 AppSearch 表行

|Property|签名|
|--------------|-----------------|
|DEVENV_EXE_2002|RL_DevenvExe_2002|
|DEVENV_EXE_2003|RL_DevenvExe_2003|
|DEVENV_EXE_2005|RL_DevenvExe_2005|
|DEVENV_EXE_2008|RL_DevenvExe_2008|

 例如，Visual Studio安装程序将HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0\Setup\VS\EnvironmentPath注册表值作为C:\VS2008\Common7\IDE\devenv.exe写入，这是安装程序必须运行的可执行文件的完整路径。

> [!NOTE]
> 由于 RegLocator 表的 Type 列为 2，因此无需在 Signature 表中指定其他版本信息。

## <a name="run-devenvexe"></a>运行devenv.exe
 在安装程序中运行 AppSearch 标准操作后，AppSearch 表中的每个属性都有一个值，该值指向 *相应* 版本的devenv.exe文件Visual Studio。 如果指定的注册表值不存在（因为未安装该版本的 Visual Studio）则指定的 属性设置为 null。

 Windows安装程序支持运行属性通过自定义操作类型 50 指向的可执行文件。 自定义操作应包括脚本内执行选项 `msidbCustomActionTypeInScript` (1024) 和 `msidbCustomActionTypeCommit` (512) ，以确保 VSPackage 在集成到 之前已成功安装 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 有关详细信息，请参阅[CustomAction 表和](/windows/desktop/msi/customaction-table)[脚本内自定义操作执行选项](/windows/desktop/msi/custom-action-in-script-execution-options)。

 类型为 50 的自定义操作将包含可执行文件的 属性指定为"目标"列中"源"列和命令行参数的值。

### <a name="customaction-table-rows-to-run-devenvexe"></a>要运行查询的 CustomAction 表devenv.exe

|操作|类型|源|目标|
|------------|----------|------------|------------|
|CA_RunDevenv2002|1586|DEVENV_EXE_2002|/setup|
|CA_RunDevenv2003|1586|DEVENV_EXE_2003|/setup|
|CA_RunDevenv2005|1586|DEVENV_EXE_2005|/setup|
|CA_RunDevenv2008|1586|DEVENV_EXE_2008|/setup|

 必须将自定义操作创作到 InstallExecuteSequence 表中，以安排在安装过程中执行这些操作。 使用"条件"列的每一行中的相应属性，以防止在系统未安装该版本的 时运行 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 自定义操作。

> [!NOTE]
> 在条件中使用时，Null `False` 值属性计算结果为 。

 每个自定义操作"序列"列的值取决于安装程序包Windows序列值。 序列值应使自定义devenv.exe操作在 InstallFinalize 标准操作之前尽可能接近运行。

### <a name="installexecutesequence-table-to-schedule-the-devenvexe-custom-actions"></a>InstallExecuteSequence 表，用于devenv.exe自定义操作

|操作|条件|序列|
|------------|---------------|--------------|
|CA_RunDevenv2002|DEVENV_EXE_2002|6602|
|CA_RunDevenv2003|DEVENV_EXE_2003|6603|
|CA_RunDevenv2005|DEVENV_EXE_2005|6605|
|CA_RunDevenv2008|DEVENV_EXE_2008|6608|

## <a name="see-also"></a>另请参阅
- [使用 Windows 安装程序安装 VSPackage](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
