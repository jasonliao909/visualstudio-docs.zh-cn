---
description: Dia2dump 示例演示如何使用 Microsoft 调试接口访问软件开发工具包 (DIA SDK) 在 PDB 文件中查询信息。
title: Dia2dump 示例 |Microsoft Docs
ms.date: 07/24/2018
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- sample applications [DIA SDK]
- Dia2dump sample [DIA SDK]
ms.assetid: 492c0893-7043-452f-a020-890a47230d20
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: cdf5e84eaeace022d733d7f8521aecdbc2cd58d1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832383"
---
# <a name="dia2dump-sample"></a>Dia2dump 示例

Dia2dump 示例演示如何使用 Microsoft 调试接口访问软件开发工具包 (DIA SDK) 在 PDB 文件中查询信息。

Dia2dump 示例随 Visual Studio 一起安装，包含解决方案和源文件。 编译的可执行文件从命令行运行。 它可以显示整个程序数据库 ( .pdb) 文件的内容，也可以只显示你感兴趣的部分。

## <a name="install-the-sample"></a>安装示例

在 Visual Studio 安装程序中选择 " **c + + 的桌面开发**" 工作负载时，会安装该示例。 有关如何安装 Visual Studio 并选择特定工作负载和单个组件的信息，请参阅[安装 Visual Studio](../../install/install-visual-studio.md)。

安装后，该示例位于名为 \DIA SDK\Samples\DIA2Dump. 的子目录中的 Visual Studio 安装目录中。

## <a name="build-the-sample"></a>生成示例

默认情况下，安装目录是受保护的目录。 这意味着，必须使用提升的开发人员命令提示或 Visual Studio 的实例在此位置生成和编辑示例解决方案。 为了简化生成，我们建议首先将示例目录中的文件复制到另一个目录，例如文档文件夹中的文件夹，然后生成示例。

### <a name="to-build-the-dia2dump-sample-in-visual-studio"></a>在 Visual Studio 中生成 Dia2Dump 示例

1. 在 Visual Studio 中打开 DIA2Dump 文件。 如果你没有将解决方案复制到其他目录，则系统可能会提示你重新启动具有提升权限的 Visual Studio。

1. 在 **解决方案资源管理器** 中，选择 "Dia2Dump" 项目 ("解决方案) "。

1. 打开项目的“属性页”  对话框。 有关详细信息，请参阅[使用项目属性](/cpp/build/working-with-project-properties)。

1. 打开 "**配置属性**" "  >  **c/c + +**  >  **常规**" 属性页。

1. 在 " **附加包含目录** " 属性中，选择下拉控件，然后选择 " **编辑**"。

1. 在 " **附加包含目录** " 对话框中的 "编辑" 字段中，输入 `$(VSInstallDir)DIA SDK\include` 目录。 添加此目录可保证编译器可以找到 dia2 文件。 选择“确定”以保存更改  。

1. 选择 **"确定"** 以保存对项目属性所做的更改。

1. 在 " **生成** " 菜单上，选择 " **重新生成解决方案**"。 默认情况下，Visual Studio 生成示例的调试版本，该版本位于解决方案目录的调试子目录中。

1. 关闭 Visual Studio。

### <a name="to-build-the-dia2dump-sample-at-the-command-line"></a>在命令行上生成 Dia2Dump 示例

1. 在 "开发人员命令提示" 窗口中，切换到在其中复制了示例文件的目录。 如果未将该示例复制到其他目录，则必须使用提升的 (以管理员身份运行) 开发人员命令提示窗口。

1. 输入 `nmake makefile` 用于生成 dia2dump.exe 默认调试配置的命令。

## <a name="run-the-dia2dump-sample"></a>运行 Dia2Dump 示例

Dia2Dump.exe 依赖于.dll COM 服务器的 msdia) *版本* 来提供其服务。 从 Visual Studio 2015 开始，msdia140.dll 版本。 如果未初始化 msdia) *版本*.dll COM 服务器，则必须先注册它，然后 dia2dump.exe 才能工作。 DIA SDK 目录包含一个 bin 子目录，其中包含 x86 版本的 DLL。 X64 体系结构计算机的版本位于 bin\amd64 中，ARM 的版本在 bin\arm. 中。 若要注册 dll，请打开提升的 "开发人员命令提示符" 窗口，并更改为包含计算机体系结构的版本的目录。 输入 `regsvr32 msdia140.dll` 用于注册 COM 服务器的命令。

### <a name="to-run-the-sample"></a>运行示例

1. 打开命令提示符并切换到包含您生成的 dia2dump.exe 的目录。

1. 输入命令 `dia2dump filename` ，其中 *filename* 是要检查的 PDB 文件的名称。 如果 PDB 文件位于另一个目录中，则使用该文件的完整路径作为 *文件名*。 此命令列出 PDB 文件中的所有数据。

1. Dia2Dump 有其他选项可仅显示选定的信息。 使用 `dia2dump -?` 命令列出所有可用选项。

## <a name="see-also"></a>请参阅

- [移植、迁移和升级 Visual Studio 项目](../../porting/port-migrate-and-upgrade-visual-studio-projects.md)
