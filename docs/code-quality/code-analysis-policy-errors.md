---
title: Code Analysis Policy Errors
ms.date: 11/04/2016
description: 了解代码中的代码分析策略Visual Studio。 查看在签入代码时不满足策略时发生的错误的说明。
ms.custom: SEO-VS-2020
ms.topic: reference
f1_keywords:
- vs.codeanalysis.policyfailures
helpviewer_keywords:
- policy errors, code analysis
ms.assetid: d1f221cd-68c0-4277-9397-b76ad0dbae77
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: da597933d187ea8d3b433901c322679ec5edbab2b9144e0f27ce54bd080c5537
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121328678"
---
# <a name="code-analysis-policy-errors"></a>Code Analysis Policy Errors

如果在签入时未满足代码分析策略，则会发生以下错误：

**一Code Analysis项目的设置与项目策略Code Analysis兼容。**

一个或多个代码项目未满足签入到项目源代码管理的代码分析要求。 此错误可能是由以下一种或多种情况引起的：

- 未对解决方案中所有项目的生成版本启用代码分析。

- Visual Studio 中项目的本地规则集具有比项目规则集限制较少的操作设置，例如，在服务器上设置为"操作错误"的规则在 Visual Studio) 中运行的规则集的" = 操作"设置为"警告"或"无"。

- 在 Visual Studio 中指定的规则集不包含在项目签入策略Code Analysis规则集内指定的所有规则。

**策略Code Analysis失败。项目中出现错误 {0} ，或者生成不是最新的。**

生成包含错误或错误已修复，但在修复后未执行代码分析。

**签入失败。Code Analysis策略要求使用打开Visual Studio签入。**

代码分析策略要求签入的所有文件都必须处于当前打开的解决方案中。 若要更正此错误，请打开包含要签入的文件的解决方案。

**并非所有挂起签入中的文件都位于当前打开的解决方案中。**

代码分析策略要求签入的所有文件都必须处于当前打开的解决方案中。 存在打开的解决方案，但"待签入"视图中的一些文件不是当前打开的解决方案的一部分时，将引发此错误。 若要更正此错误，请打开包含要签入的文件的解决方案。

**"" {0} 的版本不正确。策略中指定的强名称为 {1} ''。**

此错误适用于 .NET 项目。 代码.dll策略所需的规则存在于本地计算机上，但版本/公钥不匹配。 若要更正此错误，策略创建者必须更新其计算机上 *C：\Program Files\Microsoft Visual Studio 8\Team Tools\Static Analysis Tools\FxCop\Rules \\* 目录中的 .dll。

**策略 {0} 中指定的''程序集不存在。**

此错误适用于 .NET 项目。 代码分析策略所需的规则未在客户端计算机上安装相应的 dll。 若要更正此错误，策略创建者必须更新其计算机上 *C：\Program Files\Microsoft Visual Studio 8\Team Tools\Static Analysis Tools\FxCop\Rules \\* 目录中的 dll。

**{0}Project规则设置与策略Code Analysis一致。**

此错误适用于 .NET 项目。 托管代码规则设置没有策略要求严格。 若要更正此错误，客户端设置必须与服务器上策略要求相同或更严格。

**Code Analysis未在活动配置上启用。签入之前 {0} 切换到配置 {1} 和生成项目。**

在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中，活动配置未启用代码分析，但至少启用了一个代码分析。

**必须在签入Code Analysis属性和生成中为托管二进制文件 {0} 启用托管二进制文件。**

此错误适用于 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] .NET 应用程序。 策略需要执行托管代码分析，但在客户端上的当前项目中未启用。

**在签入Code Analysis必须在项目属性 {0} 和生成中启用属性。**

此错误应用于项目和 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] Web 项目。 策略需要执行托管代码分析，但在客户端上的当前项目中未启用。

**在签入之前，Code Analysis属性和生成中启用 C/C++ {0} 属性。**

此错误适用于非托管项目。 代码分析策略要求Code Analysis C/C++，但它未在客户端的当前项目中启用。

## <a name="see-also"></a>另请参阅

- [Code Analysis应用程序错误](../code-quality/code-analysis-application-errors.md)
