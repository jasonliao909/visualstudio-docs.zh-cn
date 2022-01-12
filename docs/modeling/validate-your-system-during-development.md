---
title: 在开发过程中验证系统
description: 了解 Visual Studio 如何帮助使你的软件与用户要求和系统的体系结构保持一致。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- dependency diagrams
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: a5e4186af249d44f908d3af10c84e5eedabf5eb8
ms.sourcegitcommit: fc874be3fe4637a23997b4ef2d99a2ee9a499581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2021
ms.locfileid: "135517404"
---
# <a name="validate-your-system-during-development"></a>在开发过程中验证系统

Visual Studio 可帮助使你的软件与用户要求和系统的体系结构保持一致。

若要查看支持各个功能的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/analyze-and-model-your-architecture.md#VersionSupport)。

## <a name="key-tasks"></a>关键任务

使用以下任务来验证软件：

|**任务**|**相关主题**|
|-|-|
|**请确保软件满足用户要求**：<br /><br />使用要求模型和体系结构模型来帮助组织系统及其组件的测试。 这种做法有助于确保你测试了对于用户和其他利益干系人而言非常重要的要求，并可帮助你在要求发生变化时快速更新测试。|- [基于模型开发测试](../modeling/develop-tests-from-a-model.md)|
|**请确保你的软件与系统的预期设计保持一致：**<br /><br />依赖项关系图描述了应用程序组件之间的预期依赖关系。 在开发期间，你可以验证代码中的实际依赖关系是否符合预期设计。|- [从代码创建依赖项关系图](../modeling/create-layer-diagrams-from-your-code.md)<br />- [使用依赖项关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)|

## <a name="external-resources"></a>外部资源

**论坛**  - [Visual Studio 可视化 & 建模工具](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />- [Visual Studio 扩展性](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx)

## <a name="see-also"></a>另请参阅

- [建立用户需求模型](../modeling/model-user-requirements.md)
- [对体系结构进行分析和建模](../modeling/analyze-and-model-your-architecture.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
