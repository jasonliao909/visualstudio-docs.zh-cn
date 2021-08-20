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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122105816"
---
# <a name="code-analysis-policy-errors"></a>Code Analysis Policy Errors

如果签入时未满足代码分析策略，则会发生以下错误：

**一个或多个项目的 Code Analysis 设置与 Code Analysis 策略不兼容。**

对于一个或多个代码项目，代码分析要求签入到项目源代码管理中。 此错误可能是由以下一种或多种情况引起的：

- 未对解决方案中所有项目的生成版本启用代码分析。

- Visual Studio 中的项目的本地规则集的 **操作** 设置限制低于项目规则集，例如，服务器上设置为 **操作** = **错误** 的规则将其 **操作** 设置为 "**警告**" 或 "**无**" （在 Visual Studio) 运行的规则集中。

- Visual Studio 中指定的规则集不包含项目的 Code Analysis 签入策略中指定的规则集中指定的所有规则。

**Code Analysis 策略失败。项目中存在错误， {0} 或生成不是最新的。**

生成包含错误或修复了错误，但修复后未执行代码分析。

**签入失败。Code Analysis 策略要求你通过打开的解决方案在 Visual Studio 中签入。**

代码分析策略要求签入的所有文件必须位于当前打开的解决方案中。 若要更正此错误，请打开包含要签入的文件的解决方案。

**并非挂起签入中的所有文件都在当前打开的解决方案中。**

代码分析策略要求签入的所有文件必须位于当前打开的解决方案中。 当存在打开的解决方案，但 "挂起签入" 视图中的某些文件不是当前打开的解决方案的一部分时，将引发此错误。 若要更正此错误，请打开包含要签入的文件的解决方案。

**"" 的版本 {0} 不正确。策略中指定的强名称为 " {1} "。**

此错误适用于 .NET 项目。 代码分析策略所需的规则 .dll 存在于本地计算机上，但版本/公钥不匹配。 若要更正此错误，策略创建者必须在其计算机上更新 *C:\Program Files \ Microsoft Visual Studio 8 \ Team Tools\Static Analysis \\ Tools\FxCop\Rules* 目录中的 .dll。

**{0}策略中指定的 "" 程序集不存在。**

此错误适用于 .NET 项目。 代码分析策略所需的规则未在客户端计算机上安装相应的 dll。 若要更正此错误，策略创建者必须在其计算机上更新 *C:\Program Files \ Microsoft Visual Studio 8 \ Team Tools\Static \\ Analysis Tools\FxCop\Rules* 目录中的 dll。

**Project {0}规则设置与 Code Analysis 策略不一致。**

此错误适用于 .NET 项目。 托管代码规则设置与策略要求并不严格。 若要更正此错误，客户端设置必须与服务器上的策略要求相同或更严格。

**未在活动配置上启用 Code Analysis。签入之前，切换到 "配置" {0} 和 "生成项目 {1} "。**

在中 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ，活动配置未启用代码分析，但至少启用了一个代码分析。

**签入之前，必须在项目属性中启用托管二进制文件的 Code Analysis {0} ，然后生成。**

此错误适用于 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] .net 应用程序。 策略需要执行托管代码分析，但不会在客户端上的当前项目中启用它。

**签入之前，必须在项目 {0} 属性和生成中启用 Code Analysis。**

此错误应用于 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 项目和 web 项目。 策略需要执行托管代码分析，但不会在客户端上的当前项目中启用它。

**签入之前，必须在项目属性和生成中启用 c/c + + Code Analysis {0} 。**

此错误适用于非托管项目。 代码分析策略需要适用于 C/c + + 的 Code Analysis，但在客户端上的当前项目中未启用该策略。

## <a name="see-also"></a>请参阅

- [Code Analysis应用程序错误](../code-quality/code-analysis-application-errors.md)
