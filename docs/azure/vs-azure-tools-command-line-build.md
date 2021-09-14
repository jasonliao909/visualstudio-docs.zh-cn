---
title: 为 Azure 构建的命令行 | Microsoft Docs
description: 为 Azure 构建的命令行
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 03/05/2017
ms.author: ghogen
ms.openlocfilehash: eec0fdc1ddfbeee3ae7a23502186d7ee35d5b979
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602159"
---
# <a name="building-azure-projects-from-the-command-line"></a>通过命令行生成 Azure 项目
通过使用 Microsoft 生成引擎 (MSBuild)，可以在未安装 Visual Studio 的生成实验室环境中生成产品。 MSBuild 对可扩展且 Microsoft 完全支持的项目文件使用 XML 格式。 通过使用 MSBuild 文件格式，可以描述必须为一个或多个平台和配置生成的项目。

还可以在命令行下运行 MSBuild，本主题介绍了该方法。 通过在命令行中设置属性，可以生成项目的特定配置。 同样，还可以定义 MSBuild 将生成的目标。 有关命令行参数和 MSBuild 的详细信息，请参阅 [MSBuild 命令行参考](../msbuild/msbuild-command-line-reference.md)。

## <a name="msbuild-parameters"></a>MSBuild 参数
创建包的最简单方法是运行 MSBuild 并使用 `/t:Publish` 选项。 默认情况下，此命令将创建与项目的根文件夹相关的目录，例如 `<ProjectDirectory>\bin\Configuration\app.publish\`。 生成 Azure 项目时，将生成两个文件，即包文件本身和附带的配置文件：

* 包文件 (`project.cspkg`)
* 配置文件 (`ServiceConfiguration.TargetProfile.cscfg`)

默认情况下，每个 Azure 项目均包含两个服务配置文件，这两个文件分别针对本地（调试）生成和云（过渡或生产）生成。 但是，可以根据需要添加或删除服务配置文件。 在 Visual Studio 中生成包时，系统会询问你要将哪个服务配置文件与包一起包含。 使用 MSBuild 生成包时，默认情况下将包含本地服务配置文件。 要包含其他配置文件，请设置 MSBuild 命令 (`MSBuild /t:Publish /p:TargetProfile=ProfileName`) 的 `TargetProfile` 属性。

如果希望为存储包和配置文件使用其他目录，请使用 `/p:PublishDir=Directory\` 选项（包括末尾的反斜杠）设置路径。

## <a name="next-steps"></a>后续步骤
生成包后，即可将其部署到 Azure。
