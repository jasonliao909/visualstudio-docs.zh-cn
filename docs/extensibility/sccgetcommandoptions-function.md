---
description: 此函数会提示用户输入给定命令的高级选项。
title: SccGetCommandOptions 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGetCommandOptions
helpviewer_keywords:
- SccGetCommandOptions function
ms.assetid: bbe4aa4e-b4b0-403e-b7a0-5dd6eb24e5a9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7972d874668649b8bb86adc15008880c5fc4152e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903926"
---
# <a name="sccgetcommandoptions-function"></a>SccGetCommandOptions 函数
此函数会提示用户输入给定命令的高级选项。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccGetCommandOptions(
   LPVOID pvContext,
   HWND hWnd,
   enum SCCCOMMAND iCommand,
   LPCMDOPTS* ppvOptions
);
```

### <a name="parameters"></a>参数
 pvContext

[in]源代码管理插件上下文结构。

 hWnd

[in]IDE 窗口的句柄，源代码管理插件可以将该窗口用作它提供的任何对话框的父级。

 iCommand

[in]请求高级选项的命令 ([命令代码，](../extensibility/command-code-enumerator.md) 了解可能) 。

 ppvOptions

[in]还可以 (选项结构 `NULL`) 。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|描述|
|-----------|-----------------|
|SCC_OK|成功。|
|SCC_I_ADV_SUPPORT|源代码管理插件支持命令的高级选项。|
|SCC_I_OPERATIONCANCELED|用户取消了源代码管理插件的"选项 **"** 对话框。|
|SCC_E_OPTNOTSUPPORTED|源代码管理插件不支持此操作。|
|SCC_E_ISCHECKEDOUT|无法对当前签出的文件执行此操作。|
|SCC_E_ACCESSFAILURE|访问源代码管理系统时出现问题，原因可能是网络或争用问题。 建议重试。|
|SCC_E_NONSPECIFICERROR|非特定故障。|

## <a name="remarks"></a>备注
 IDE 首次使用 调用此函数，以确定源代码管理插件是否支持指定命令 `ppvOptions` = `NULL` 的高级选项功能。 如果插件确实支持该命令的功能，则当用户请求高级选项时，IDE 将再次调用此函数 (通常作为对话框) 中的"高级"按钮实现，并为此指向指针的 指针提供非 NULL 指针。 `ppvOptions` `NULL` 插件将用户指定的任何高级选项存储在私有 结构中，并返回指向 中该结构的指针 `ppvOptions` 。 然后，此结构将传递给需要知道它的所有其他源代码管理插件 API 函数，包括对函数的后续 `SccGetCommandOptions` 调用。

 一个示例有助于阐明这种情况。

 用户选择"获取 **"** 命令，IDE 将显示" **获取"** 对话框。 IDE 调用 函数 `SccGetCommandOptions` ， `iCommand` 将 设置为 `SCC_COMMAND_GET` `ppvOptions` ，将 设置为 `NULL` 。 源代码管理插件将此问题解释为"你是否有此命令的高级选项？" 如果插件返回 `SCC_I_ADV_SUPPORT` ，则 IDE 在其"获取 **"** 对话框中显示" **高级"** 按钮。

 用户首次单击"高级 **"** 按钮时，IDE 会再次调用 函数，这次使用指向指针 `SccGetCommandOptions` 的非 `NULL``ppvOptions` `NULL` 。 该插件显示其自己的"获取选项"对话框，提示用户输入信息，将该信息放入其自己的 结构中，并返回指向 中的该结构的指针 `ppvOptions` 。

 如果用户在同 **一对话框中** 再次单击"高级"，IDE 将再次调用函数而不更改 ，以便结构传递回 `SccGetCommandOptions` `ppvOptions` 插件。 这使插件能够将其对话框重新初始化为用户之前设置的值。 插件在返回之前就地修改结构。

 最后，当用户在 IDE 的"获取"对话框中单击"确定"时，IDE 将调用[SccGet，](../extensibility/sccget-function.md)并传递中返回的结构，其中包含 `ppvOptions` 高级选项。

> [!NOTE]
> 当 IDE 显示"选项"对话框时，使用 命令，该对话框允许用户设置 `SCC_COMMAND_OPTIONS` 控制集成工作方式的首选项。  如果源代码管理插件想要提供自己的首选项对话框，它可以从 IDE 首选项对话框中的"高级"按钮显示它。 插件只负责获取和保留此信息;IDE 不使用它或修改它。

## <a name="see-also"></a>另请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [命令代码](../extensibility/command-code-enumerator.md)
