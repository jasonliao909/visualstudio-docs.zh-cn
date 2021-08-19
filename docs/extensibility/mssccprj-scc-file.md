---
title: MSSCCPRJ。SCC 文件|Microsoft Docs
description: 了解 MSSCCPRJ。SCC 文件，它是源代码管理插件使用的本地客户端文件，适用于 Visual Studio SDK。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- source control plug-ins, MSSCCPRJ.SCC file
- MSSCCPRJ.SCC file
ms.assetid: 6f2e39d6-b79d-407e-976f-b62a3cedd378
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 74a83ff3160ebe12fd16a811b6580061c0572f75
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122158536"
---
# <a name="mssccprjscc-file"></a>MSSCCPRJ。SCC 文件
使用 IDE 将Visual Studio或项目放在源代码管理下时，IDE 会收到两个关键信息片段。 信息来自字符串形式的源代码管理插件。 这些字符串"AuxPath"和"ProjName"对 IDE 是不透明的，但插件使用这些字符串在版本控制中查找解决方案或项目。 IDE 通常第一次通过调用 [SccGetProjPath](../extensibility/sccgetprojpath-function.md)获取这些字符串，然后将这些字符串保存在解决方案或项目文件中，供将来调用 [SccOpenProject](../extensibility/sccopenproject-function.md)。 嵌入到解决方案和项目文件中时，当用户分支、分支或复制版本控制中的解决方案和项目文件时，不会自动更新"AuxPath"和"ProjName"字符串。 若要确保解决方案和项目文件指向其版本控制中的正确位置，用户必须手动更新字符串。 由于字符串是不透明的，因此可能并不总是清楚地了解如何更新它们。

 源代码管理插件可以通过将"AuxPath"和"ProjName"字符串存储在名为 *MSSCCPRJ.SCC* 文件的特殊文件中来避免此问题。 它是插件拥有和维护的本地客户端文件。 此文件永远不会置于源代码管理下，而是由插件针对包含源代码管理文件的每一个目录生成。 若要确定哪些文件Visual Studio和项目文件中，源代码管理插件可以将文件扩展名与标准列表或用户提供的列表进行比较。 一旦 IDE 检测到插件支持 *MSSCCPRJ.SCC* 文件，它将停止将"AuxPath"和"ProjName"字符串嵌入到解决方案和项目文件中，而是从 *MSSCCPRJ.SCC* 文件中读取这些字符串。

 支持 *MSSCCPRJ.SCC* 文件的源代码管理插件必须遵循以下准则：

- 每个目录只能有 *一个 MSSCCPRJ.SCC* 文件。

- 对于 *给定目录中受源代码管理的多个文件，MSSCCPRJ.SCC* 文件可以包含"AuxPath"和"ProjName"。

- "AuxPath"字符串内不得包含引号。 允许将引号括起来作为分隔符 (例如，一对双引号可用于指示空字符串) 。 从 *MSSCCPRJ.SCC* 文件中读取时，IDE 会从"AuxPath"字符串中去除所有引号。

- *MSSCCPRJ 中的"ProjName"字符串。SCC* 文件必须与函数返回的字符串 `SccGetProjPath` 完全匹配。 如果函数返回的字符串周围有引号， *则 MSSCCPRJ.SCC* 文件的字符串周围必须有引号，反之亦然。

- 每当将文件置于源代码管理下时，就会创建或更新 *MSSCCPRJ.SCC* 文件。

- 如果 *删除了 MSSCCPRJ.SCC* 文件，则提供程序应在下次执行有关该目录的源代码管理操作时重新生成该文件。

- *MSSCCPRJ.SCC* 文件必须严格遵循定义的格式。

## <a name="an-illustration-of-the-mssccprjscc-file-format"></a>MSSCCPRJ 的插图。SCC 文件格式
 下面是 *MSSCCPRJ.SCC* 文件格式的示例 (行号仅作为指南提供，不应包含在文件正文) ：

- [第 1 行] `SCC = This is a Source Code Control file`

- [第 2 行]

- [第 3 行] `[TestApp.sln]`

- [第 4 行] `SCC_Aux_Path = "\\server\vss\"`

- [第 5 行] `SCC_Project_Name = "$/TestApp"`

- [第 6 行]

- [第 7 行] `[TestApp.csproj]`

- [第 8 行] `SCC_Aux_Path = "\\server\vss\"`

- [第 9 行] `SCC_Project_Name = "$/TestApp"`

 第一行说明文件的用途，并充当此类型的所有文件的签名。 在所有 *MSSCCPRJ.SCC* 文件中，此行应如下所示：

 `SCC = This is a Source Code Control file`

 以下部分详细介绍了每个文件的设置，用方括号中的文件名进行标记。 对于要跟踪的每个文件，将重复此部分。 此行是文件名的示例，即 `[TestApp.csproj]` 。 IDE 需要以下两行。 但是，它不会定义定义的值的样式。 变量为 `SCC_Aux_Path` 和 `SCC_Project_Name` 。

 `SCC_Aux_Path = "\\server\vss\"`

 `SCC_Project_Name = "$/TestApp"`

 本部分没有结束分隔符。 文件的名称以及文件内显示的所有文本在 scc.h 头文件中定义。 有关详细信息，请参阅 [用作查找源代码管理插件的键的字符串](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)。

## <a name="see-also"></a>请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [用作查找源代码管理插件的键的字符串](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)
