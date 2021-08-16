---
title: 代码分析签入策略的版本兼容性
ms.date: 11/04/2016
description: 了解 Team System 2008 Team Foundation Server 2010 Team Foundation Server如何以Visual Studio方式评估签入策略。
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
ms.openlocfilehash: d1ab46216ac2955e6629d5a577659f938e9aa741659309a12c2ee98b527d5915
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121348458"
---
# <a name="version-compatibility-for-code-analysis-check-in-policies"></a>代码分析签入策略的版本兼容性

如果必须使用不同版本的 评估和创作代码分析签入策略，则必须了解签入策略方式 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] [!INCLUDE[vstsTfsOrcasLong](../code-quality/includes/vststfsorcaslong_md.md)] [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 和评估方式的差异。

## <a name="version-compatibility-for-evaluating-check-in-policies"></a>用于评估策略的版本Check-In兼容性

- 在 中评估代码分析签入策略时，将忽略 存在于 中但 不存在 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 的任何规则。

- 在 中评估代码分析签入策略时 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] ，将忽略所有排除 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 的新规则。

- 如果代码分析签入策略指定规则程序集， 将忽略它无法识别的程序集 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 指定的所有规则。

- 如果代码分析签入策略指定无法识别的规则 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 程序集，则会显示一条消息。

## <a name="version-compatibility-for-authoring-check-in-policies"></a>创作策略的版本Check-In兼容性

- 如果使用 版本创建了代码分析签入策略，则 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 不能使用 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 的版本 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 对其进行修改。 此外， [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 无法评估策略。

- 如果在 中使用 创建了代码分析签入策略，可以使用 在 中对其进行修改，并且该策略也可 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 通过 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 进行评估 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 。 在 中使用 修改策略后，无法再使用 中的 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 编辑 [!INCLUDE[esprtfc](../code-quality/includes/esprtfc_md.md)] 策略 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 。 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 可以评估策略，而不会遇到与强名称不匹配的问题。

- 若要使用适用于 和 的规则设置创建代码分析签入策略，必须在 中创建策略， [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 进行所有所需的更改，并 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 保存策略。 如果对规则所做的更改仅存在于 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 中，则修改策略并将其保存在 中 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] 。

   在 中保存策略后 [!INCLUDE[vstsTfsOrcasShort](../code-quality/includes/vststfsorcasshort_md.md)] ，无法再更改仅存在于 中的规则的 [!INCLUDE[vstsTfsRosarioShort](../code-quality/includes/vststfsrosarioshort_md.md)] 设置。
