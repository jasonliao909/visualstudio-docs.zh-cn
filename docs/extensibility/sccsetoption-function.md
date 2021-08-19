---
description: 此函数设置控制源代码管理插件行为的选项。
title: SccSetOption 函数|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccSetOption
helpviewer_keywords:
- SccSetOption function
ms.assetid: 4b5e6666-c24c-438a-a9df-9c52f58f8175
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a918dad74fe777842fa22395d80535113792e119
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122158328"
---
# <a name="sccsetoption-function"></a>SccSetOption 函数
此函数设置控制源代码管理插件行为的选项。

## <a name="syntax"></a>语法

```cpp
SCCRTN SccSetOption(
   LPVOID pvContext,
   LONG   nOption,
   LONG   dwVal
);
```

#### <a name="parameters"></a>参数
 pvContext

[in]源代码管理插件上下文结构。

 nOption

[in]正在设置的选项。

 dwVal

[in]设置选项。

## <a name="return-value"></a>返回值
 此函数的源代码管理插件实现应返回以下值之一：

|值|说明|
|-----------|-----------------|
|SCC_OK|选项已成功设置。|
|SCC_I_SHARESUBPROJOK|如果 为 `nOption` ，则返回 ，并且源代码管理 `SCC_OPT_SHARESUBPROJ` 插件允许 IDE 设置目标文件夹。|
|SCC_E_OPNOTSUPPORTED|选项未设置，不应依赖。|

## <a name="remarks"></a>备注
 IDE 调用此函数来控制源代码管理插件的行为。 第一个参数 指示要设置的值，而第二个参数 指示 `nOption` `dwVal` 对该值执行什么操作。 插件存储与 关联的此信息，因此 IDE 必须在调用 `pvContext``,` [SccInitialize](../extensibility/sccinitialize-function.md) (之后调用此函数，但不一定在调用 [SccOpenProject](../extensibility/sccopenproject-function.md)) 。

 选项及其值的摘要：

|`nOption`|`dwValue`|说明|
|---------------|---------------|-----------------|
|`SCC_OPT_EVENTQUEUE`|`SCC_OPT_EQ_DISABLE`<br /><br /> `SCC_OPT_EQ_ENABLE`|启用/禁用后台事件队列。|
|`SCC_OPT_USERDATA`|任意值|指定要传递给 [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md) 回调函数的用户值。|
|`SCC_OPT_HASCANCELMODE`|`SCC_OPT_HCM_NO`<br /><br /> `SCC_OPT_HCM_YES`|指示 IDE 当前是否支持取消操作。|
|`SCC_OPT_NAMECHANGEPFN`|指向 [OPTNAMECHANGEPFN 回调](../extensibility/optnamechangepfn.md) 函数的指针|设置指向名称更改回调函数的指针。|
|`SCC_OPT_SCCCHECKOUTONLY`|`SCC_OPT_SCO_NO`<br /><br /> `SCC_OPT_SCO_YES`|指示 IDE 是否允许通过源代码管理用户界面 (手动签出其) 或者是否必须通过源代码管理插件签出这些文件。|
|`SCC_OPT_SHARESUBPROJ`|不适用|如果源代码管理插件允许 IDE 指定本地项目文件夹，该插件将返回 `SCC_I_SHARESUBPROJOK` 。|

## <a name="scc_opt_eventqueue"></a>SCC_OPT_EVENTQUEUE
 如果 `nOption` `SCC_OPT_EVENTQUEUE` 为 ，则 IDE 正在禁用 (或重新启用) 后台处理。 例如，在编译期间，IDE 可能会指示源代码管理插件停止任何类型的空闲处理。 编译后，它会重新启用后台处理，使插件的事件队列保持最新。 与 `SCC_OPT_EVENTQUEUE` 的值相对应 `nOption` ， 有两个可能的值 `dwVal` ， 即 和 `SCC_OPT_EQ_ENABLE` `SCC_OPT_EQ_DISABLE` 。

## <a name="scc_opt_hascancelmode"></a>SCC_OPT_HASCANCELMODE
 如果 的值为 `nOption` `SCC_OPT_HASCANCELMODE` ，则 IDE 允许用户取消长时间操作。 设置为 `dwVal` `SCC_OPT_HCM_NO` (默认) 表示 IDE 没有取消模式。 如果源代码管理插件希望用户能够取消，则必须提供其自己的"取消"按钮。 `SCC_OPT_HCM_YES` 指示 IDE 提供取消操作的能力，因此 SCC 插件无需显示自己的"取消"按钮。 如果 IDE 将 设置为 ，则它已准备好响应 和发送到回调函数的消息 `dwVal` `SCC_OPT_HCM_YES` `SCC_MSG_STATUS` `DOCANCEL` `lpTextOutProc` (请参阅 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)) 。 如果 IDE 未设置此变量，插件不应发送这两条消息。

## <a name="scc_opt_namechangepfn"></a>SCC_OPT_NAMECHANGEPFN
 如果 nOption 设置为 ，并且源代码管理插件和 IDE 都允许，则插件实际上可以在源代码管理操作期间重命名或 `SCC_OPT_NAMECHANGEPFN` 移动文件。 `dwVal`将设置为[OPTNAMECHANGEPFN 类型的函数指针](../extensibility/optnamechangepfn.md)。 在源代码管理操作期间，插件可以调用此函数，并传递三个参数。 这些是具有 (完全限定路径) 的旧名称，具有该文件的完全限定路径) 的新名称 (，以及指向与 IDE 相关的信息的指针。 IDE 通过调用 ，并将 设置为 并指向数据，在此最后一个指针 `SccSetOption` `nOption` `SCC_OPT_USERDATA` `dwVal` 中发送 。 对此函数的支持是可选的。 使用此功能的 VSSCI 插件必须将其函数指针和用户数据变量初始化为 ，并且除非已提供重命名函数，否则不得调用重命名 `NULL` 函数。 它还应准备好保存它给定的值，或者更改该值以响应对 的新调用 `SccSetOption` 。 这不会在源代码管理命令操作过程中发生，但可能在命令之间发生。

## <a name="scc_opt_scccheckoutonly"></a>SCC_OPT_SCCCHECKOUTONLY
 如果 nOption 设置为 ，则 IDE 指示永远不应通过源代码管理系统的用户界面手动签出当前打开的项目 `SCC_OPT_SCCCHECKOUTONLY` 中的文件。 相反，应仅通过 IDE 控件下的源代码管理插件签出文件。 如果 设置为 ，则意味着文件应该由插件正常处理，并且 `dwValue` `SCC_OPT_SCO_NO` 可以通过源代码管理 UI 签出。 如果 设置为 ，则仅允许插件签出文件，并且不应调用源代码 `dwValue` `SCC_OPT_SCO_YES` 管理系统的 UI。 这适用于 IDE 可能包含仅通过 IDE 签出的"伪文件"的情况。

## <a name="scc_opt_sharesubproj"></a>SCC_OPT_SHARESUBPROJ
 如果 设置为 ，则 IDE 正在测试从源代码管理添加文件时，源代码管理插件 `nOption` `SCC_OPT_SHARESUBPROJ` 是否可以使用指定的本地文件夹。 在这种情况下， `dwVal` 参数的值并不重要。 如果插件允许 IDE 在调用 [SccAddFromScc](../extensibility/sccaddfromscc-function.md) 时指定从源代码管理中添加文件的本地目标文件夹，则调用函数时该插件必须 `SCC_I_SHARESUBPROJOK` `SccSetOption` 返回。 然后，IDE `lplpFileNames` 使用 函数 `SccAddFromScc` 的 参数来传递目标文件夹。 插件使用该目标文件夹放置从源代码管理添加的文件。 如果设置 选项时插件未返回，则 IDE 假定该插件只能在当前本地 `SCC_I_SHARESUBPROJOK` `SCC_OPT_SHARESUBPROJ` 文件夹中添加文件。

## <a name="see-also"></a>请参阅
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [SccAddFromScc](../extensibility/sccaddfromscc-function.md)
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)
- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)
