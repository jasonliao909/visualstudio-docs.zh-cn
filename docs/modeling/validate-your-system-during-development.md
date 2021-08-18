---
title: 在开发过程中验证系统
description: 了解 Visual Studio 如何帮助使软件与用户要求和系统的体系结构保持一致。
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
ms.openlocfilehash: 4a11c41b76bff61ed5af0916f0d43aa5739da78a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122116547"
---
# <a name="validate-your-system-during-development"></a>在开发过程中验证系统

Visual Studio 有助于使你的软件与用户的要求和系统的体系结构保持一致。

若要查看支持各个功能的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/analyze-and-model-your-architecture.md#VersionSupport)。

## <a name="key-tasks"></a>关键任务

使用以下任务来验证软件：

|**任务**|**相关主题**|
|-|-|
|**请确保软件满足用户要求**：<br /><br />使用要求和体系结构模型来帮助组织系统及其组件的测试。 这种做法有助于确保你测试了对于用户和其他利益干系人而言非常重要的要求，并可帮助你在要求发生变化时快速更新测试。|- [从模型开发测试](../modeling/develop-tests-from-a-model.md)|
|**请确保你的软件与系统的预期设计保持一致：**<br /><br />依赖关系图描述了应用程序组件之间的预期依赖关系。 在开发期间，你可以验证代码中的实际依赖关系是否符合预期设计。|- [从代码创建依赖项关系图](../modeling/create-layer-diagrams-from-your-code.md)<br />- [使用依赖项关系图验证代码](../modeling/validate-code-with-layer-diagrams.md)|

## <a name="external-resources"></a>外部资源

|**类别**|**链接**|
|-|-|
|**视频**|![链接到视频 ](../data-tools/media/playvideo.gif) [频道9： Doug 7：代码理解和系统设计与 Visual Studio 2010](https://channel9.msdn.com/shows/VS2010Launch/Doug-Seven-Code-Understanding-and-Systems-Design-with-Visual-Studio-2010)<br /><br /> ![链接到视频 ](../data-tools/media/playvideo.gif) [通道9：构建应用程序](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-5-architecting-an-application)) |
|**论坛**|- [Visual Studio 可视化和建模工具](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />- [Visual Studio 扩展性](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx)|

## <a name="see-also"></a>请参阅

- [建立用户需求模型](../modeling/model-user-requirements.md)
- [对体系结构进行分析和建模](../modeling/analyze-and-model-your-architecture.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
