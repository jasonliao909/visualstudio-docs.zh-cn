---
title: 实现源代码管理插件 - 最佳做法
description: 查看这些技术详细信息，以帮助你可靠地在 Visual Studio 中实现源代码管理插件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, best practices
- best practices, source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: 85e73b73-29dc-464f-8734-ed308742c435
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 8333179533bec73379944cead37e359ecf8ae609
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664630"
---
# <a name="best-practices-for-implementing-a-source-control-plug-in"></a>实现源代码管理插件的最佳实践
以下技术详细信息可帮助你可靠地在 中实现源代码管理插件 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

## <a name="memory-management-issues"></a>内存管理问题
 在大多数情况下，集成开发环境 (IDE) （调用方）释放和分配内存。 源代码管理插件返回调用方分配的缓冲区中的字符串和其他项。 异常在出现异常的特定函数的说明中进行说明。

## <a name="arrays-of-file-names"></a>文件名数组
 传递文件数组时，不会将文件作为连续的文件名数组传递。 它作为指向文件名的指针数组传递。 例如，在 [SccGet](../extensibility/sccget-function.md)中，文件名由 参数传递， `lpFileNames` 其中 `lpFileNames` 实际上是指向 的指针 `char **` 。 `lpFileNames`[0] 是指向名字的指针 `lpFileNames` ，[1] 是指向第二个名称的指针，等等。

## <a name="large-model"></a>大型模型
 所有指针都是 32 位，即使在 16 位操作系统上也是。

## <a name="fully-qualified-paths"></a>完全限定的路径
 如果文件名或目录指定为参数，则它们必须是完全限定的路径或 UNC 路径，而不使用结尾反杠。 如果这是基础源代码管理系统的要求，源代码管理插件负责将这些路径转换为相对路径。

## <a name="specify-a-fully-qualified-path-for-the-registered-dll"></a>指定已注册 DLL 的完全限定路径
 IDE 不再从相对路径加载 DLL (例如 *.\NewProvider.dll) 。* 必须指定 DLL 的完整路径 (例如 *，C:\Providers\NewProvider.dll) 。* 此要求通过防止加载未经授权的或模拟的源代码管理 DLL 来增强 IDE 的安全性。

## <a name="check-for-an-existing-vssci-plug-in-when-you-install-your-source-control-plug-in"></a>安装源代码管理插件时检查现有 VSSCI 插件
 计划安装源代码管理插件的用户可能已在计算机上安装了现有的源代码管理插件。 为 (插件) 安装程序安装程序应确定相关注册表项是否有现有值。 如果已设置这些密钥，则安装程序应询问用户是否将插件注册为默认源代码管理插件，并替换已安装的插件。

## <a name="error-result-codes-and-reporting"></a>错误结果代码和报告
 `SCC_OK`源代码管理函数的返回代码指示操作已成功处理所有文件。 如果操作失败，应返回遇到的最后一个错误代码。

 报告规则是，如果 IDE 中发生错误，则 IDE 负责报告该错误。 如果源代码管理系统中发生错误，源代码管理插件将负责报告它。 例如 **，IDE 当前不** 报告任何文件，而此文件已签出，插件将报告此文件。

## <a name="the-context-structure"></a>上下文结构
 在调用 [SccInitialize](../extensibility/sccinitialize-function.md)期间，调用方将 参数（未 `ppvContext` 初始化的句柄）传递给 void。 源代码管理插件可以忽略此参数，也可以分配任何类型的结构，将指向该结构的指针放入传递的指针中。 IDE 不了解此结构，但它将指向此结构的指针传递给插件中的所有其他调用。 这会为插件提供有价值的上下文缓存信息，该插件可用于维护跨函数调用保留的全局状态信息，而无需使用全局变量。 插件负责在调用 [SccUninitialize](../extensibility/sccuninitialize-function.md)时释放 结构。

 具体而言，如果插件在 `SCC_CAP_REENTRANT` [SccInitialize](../extensibility/sccinitialize-function.md) (中设置位，则参数) 中将使用多个上下文结构来跟踪打开的所有 `lpSccCaps` 项目。

## <a name="bitflags-and-other-command-options"></a>位标志和其他命令选项
 对于每个命令（如 [SccGet），IDE](../extensibility/sccget-function.md)可以指定更改命令行为的许多选项。

 API 支持 IDE 通过 参数设置某些 `fOptions` 选项。 这些选项在由特定命令使用的 [Bitflags](../extensibility/bitflags-used-by-specific-commands.md) 以及它们影响的命令中进行了说明。 一般情况下，这些选项不会提示用户。

 大多数用户可配置的设置选项未按此方式定义，因为它们在源代码管理插件之间差异很大。因此，建议的机制是"高级 **"** 按钮。 例如，在"**获取**"对话框中，IDE 仅显示它理解的信息，但如果插件具有此命令的选项，则它还会显示"高级"按钮。 当用户单击"高级"按钮时，IDE 将调用[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)以使源代码管理插件能够提示用户输入信息，例如位标志或日期/时间。 插件在 命令期间传递回的 结构中返回 `SccGet` 此信息。

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md)
