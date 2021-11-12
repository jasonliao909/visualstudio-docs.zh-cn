---
title: 代码分析签入策略的版本兼容性
ms.date: 11/04/2016
description: 了解 Team System 2008 Team Foundation Server 和 Team Foundation Server 2010 如何通过不同的方式评估 Visual Studio 签入策略。
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- version compatibility, code analysis check-in policy
- check-in policies, version compatibility for code analysis
ms.assetid: 1af376e3-3be7-4445-803b-76a858567a5b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 1cd049a8e2aea94e6dc3b581c5b6ca8ccf3ab4e8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601253"
---
# <a name="version-compatibility-for-code-analysis-check-in-policies"></a>代码分析签入策略的版本兼容性

如果必须使用不同版本的 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 来评估和创作代码分析签入策略，那么你必须了解 [!INCLUDE[vstsTfsOrcasLong](../code-quality/includes/vststfsorcaslong_md.md)] 和 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 评估签入策略的方式差异。

## <a name="version-compatibility-for-evaluating-check-in-policies"></a>评估签入策略的版本兼容性

- 在 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 中评估代码分析签入策略时，存在于 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 但 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 中不存在的任何规则都将被忽略。

- 在 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 中评估代码分析签入策略时，[!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 独有的所有新规则都将被忽略。

- 如果代码分析签入策略指定了规则程序集，则 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 将忽略其无法识别的程序集指定的所有规则。

- 如果代码分析签入策略指定了 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 无法识别的规则程序集，系统将显示一条消息。

## <a name="version-compatibility-for-authoring-check-in-policies"></a>创作签入策略的版本兼容性

- 如果使用 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 的 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 版本创建了代码分析签入策略，则不能使用 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 的 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 版本对其进行修改。 此外，[!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 无法评估策略。

- 如果使用 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 中的 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 创建了代码分析签入策略，则可以使用 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 中的 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 对其进行修改，也可通过 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 评估该策略。 使用 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 中的 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 修改策略之后，就不能再使用 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 中的 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 来编辑该策略。 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 可以评估策略，而不会出现因不匹配的强名称而引起的问题。

- 若要使用适用于 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 和 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 的规则设置创建代码分析签入策略，必须在 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 中创建该策略，进行所有所需的更改，然后保存该策略。 如果对规则所做的更改仅存在于 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 中，则可以修改并保存 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 中的策略。

   在 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 中保存策略后，就无法再更改仅存在于 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 中的规则设置。
