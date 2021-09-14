---
title: 代码分析应用程序错误
ms.date: 11/04/2016
description: 了解托管代码分析工具在代码中生成的错误消息Visual Studio。 查看错误代码和相应的说明。
ms.custom: SEO-VS-2020
ms.topic: reference
helpviewer_keywords:
- errors [Visual Studio ALM], code analysis
- code analysis, errors
- managed code, code analysis errors
- code analysis, policy errors
ms.assetid: d8fd9475-ac9b-4085-b5a3-b0c807922cac
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 62ee5dd35eaa779292f89696f6ab18f6d1dbbeec
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601349"
---
# <a name="code-analysis-application-errors"></a>代码分析应用程序错误

本部分引用了托管代码分析工具生成的错误消息。

## <a name="in-this-section"></a>本节内容

|代码|说明|
|-|-|
|[CA0001](ca0001.md)|托管代码分析工具中引发了一个不指示预期错误条件的异常。|
|[CA0051](ca0051.md)|未选择任何规则。|
|[CA0052](ca0052.md)|未选择任何要分析的目标。|
|[CA0053](ca0053.md)|无法加载规则程序集。|
|[CA0054](ca0054.md)|自定义规则程序集具有无效的 XML 资源。|
|[CA0055](ca0055.md)|无法加载文件：\<path>|
|[CA0056](ca0056.md)|项目文件的分析工具版本不正确。|
|[CA0057](ca0057.md)|冲突无法映射到当前目标和规则集。|
|[CA0058](ca0058.md)|无法加载引用的程序集。|
|[CA0059](ca0059.md)|命令行开关错误。|
|[CA0060](ca0060.md)|无法加载间接引用的程序集。|
|[CA0061](ca0061.md)|找不到规则 *"RuleId"。*|
|[CA0062](ca0062.md)|找不到规则集 *"RuleSetName"中引用的规则"RuleId"。*|
|[CA0063](ca0063.md)|无法加载规则集文件或其依赖规则集文件之一。|
|[CA0064](ca0064.md)|未执行任何分析，因为指定的规则集不包含任何 FxCop 规则。|
|[CA0065](ca0065.md)|不支持的元数据构造：类型 *"TypeName"* 包含属性和同名 *"PropertyFieldName"的字段*|
|[CA0066](ca0066.md)|提供给 **/targetframeworkversion** 的值 *'VersionID'* 不是可识别的版本。|
|[CA0067](ca0067.md)|找不到目录。|
|[CA0068](ca0068.md)|找不到目标程序集 *"AssemblyName"的调试信息*。|
|[CA0069](ca0069.md)|使用备用平台。 *找不到 FrameworkVersion1。* 请 *改为使用 FrameworkVersion2。* 为获得最佳分析结果，请确保安装了正确的框架版本。|
|[CA0070](ca0070.md)|由于安全权限，无法加载程序集或类型。|
|[CA0501](ca0501.md)|无法读取输出报表。|
|[CA0502](ca0502.md)|不支持的语言。|
|[CA0503](ca0503.md)|属性已弃用。 使用取代属性|
|[CA0504](ca0504.md)|忽略规则目录，因为它不存在|
|[CA0505](ca0505.md)|属性已弃用。 使用取代属性|
|[FxCopCmd 错误](fxcopcmd-errors.md)|托管代码分析错误。|

## <a name="related-sections"></a>相关章节

- [Code Analysis Policy Errors](../code-quality/code-analysis-policy-errors.md)
- [分析托管代码质量](../code-quality/code-analysis-for-managed-code-overview.md)
