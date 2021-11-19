---
title: Code Analysis Policy Errors
ms.date: 11/04/2016
description: 了解 Visual Studio 中的代码分析策略错误。 查看在签入代码时不满足策略时发生的错误的说明。
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
ms.openlocfilehash: 9ca28097058c0f9c7722aacd806f00af3ef263a1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601341"
---
# <a name="code-analysis-policy-errors"></a>Code Analysis Policy Errors

签入时未满足代码分析策略会出现以下错误：

**一个或多个项目的 Code Analysis 设置与 Code Analysis 策略不兼容。**

对于一个或多个代码项目，签入到项目源代码管理中的代码分析需求没有得到满足。 此错误可能是由以下一种或多种情况引起的：

- 未对解决方案中所有项目的生成版本启用代码分析。

- 与项目规则集相比，Visual Studio 中项目的本地规则集具有限制性较低的“操作”设置（例如，某一在服务器上设置为“操作”=“错误”的规则，在 Visual Studio 中运行的规则集中将其“操作”设置为“警告”或“无”）     。

- 在 Visual Studio 指定的规则集不包含在项目代码分析签入策略中指定的规则集中指定的所有规则。

**Code Analysis 策略失败。项目 {0} 中有错误或生成不是最新的。**

生成包含错误或错误已修复，但在修复后未执行代码分析。

**签入失败。Code Analysis 策略要求通过 Visual Studio 使用一个打开的解决方案来执行签入。**

代码分析策略要求签入的所有文件都必须位于当前打开的解决方案中。 若要更正此错误，请打开包含要签入的文件的解决方案。

**并非所有挂起签入中的文件都位于当前打开的解决方案中。**

代码分析策略要求签入的所有文件都必须位于当前打开的解决方案中。 存在打开的解决方案，但“挂起签入”视图中的一些文件不是当前打开的解决方案的一部分时，将引发此错误。 若要更正此错误，请打开包含要签入的文件的解决方案。

**{0} 的版本不正确。策略中指定的强名称是 {1}** 。

此错误适用于 .NET 项目。 本地计算机上存在代码分析策略所需的规则 .dll，但版本/公钥不匹配。 若要更正此错误，策略创建者必须更新其计算机上 C:\Program Files\Microsoft Visual Studio 8\Team Tools\Static Analysis Tools\FxCop\Rules\\ 目录中的 .dll。

**策略中指定的 {0} 的程序集不存在。**

此错误适用于 .NET 项目。 代码分析策略所需的规则未在客户端计算机上安装相应的 dll。 若要更正此错误，策略创建者必须更新其计算机上 C:\Program Files\Microsoft Visual Studio 8\Team Tools\Static Analysis Tools\FxCop\Rules\\ 目录中的 dll。

**项目 {0} 规则设置不符合 Code Analysis 策略。**

此错误适用于 .NET 项目。 托管代码规则设置没有策略要求严格。 若要更正此错误，客户端设置必须与服务器上策略要求相同或更严格。

**在活动配置中未启用 Code Analysis。在签入之前，切换到配置 {0} 并生成项目{1}。**

在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中，活动配置未启用代码分析，但至少启用了一个代码分析。

**在签入之前，必须对项目 {0} 属性和生成中的托管二进制文件启用代码分析。**

此错误适用于 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] .NET 应用程序。 策略需要执行托管代码分析，但在客户端上的当前项目中未启用该策略。

**在签入之前，必须在项目 {0} 属性和生成中启用代码分析。**

此错误应用于 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 项目和 Web 项目。 策略需要执行托管代码分析，但在客户端上的当前项目中未启用该策略。

**在签入之前，必须在项目 {0} 属性和生成中启用 C/C++ 代码分析。**

此错误适用于非托管项目。 代码分析策略要求 C/C++ 的代码分析，但在客户端的当前项目中未启用。

## <a name="see-also"></a>另请参阅

- [代码分析应用程序错误](../code-quality/code-analysis-application-errors.md)
