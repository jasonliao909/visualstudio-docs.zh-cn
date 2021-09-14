---
title: 错误代码|Microsoft Docs
description: 本文包含源代码管理插件 API 函数的错误代码、值和说明的列表。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- error codes, source control plug-ins
- source control plug-ins, error codes
- errors [Visual Studio SDK]
ms.assetid: d9cbd1c4-719b-467a-8100-333c1e146d3b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 7e7af991cc00b482dae3475fdc9a36a9b9fde032
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665340"
---
# <a name="error-codes"></a>错误代码
当源代码管理插件 API 函数返回错误时，它应该是以下错误代码之一。 所有错误都是负面的，警告或信息性错误代码为正，成功为 0。

|错误代码|值|说明|
|----------------|-----------|-----------------|
|`SCC_I_SHARESUBPROJOK`|7|插件支持通过两个步骤从源代码管理添加文件。 有关详细信息，请参阅 [SccSetOption](../extensibility/sccsetoption-function.md)。|
|`SCC_I_FILEDIFFERS`|6|本地文件不同于源代码管理数据库中的文件，例如 ([SccDiff](../extensibility/sccdiff-function.md) 可能会返回此值) 。|
|`SCC_I_RELOADFILE`|5|本地文件在源代码管理操作期间已更改;如果可能，IDE 应重新加载文件。|
|`SCC_I_FILENOTAFFECTED`|4|文件不受影响。|
|`SCC_I_PROJECTCREATED`|3|此Project是在源代码管理操作期间创建的， (例如，在调用[SccOpenProject](../extensibility/sccopenproject-function.md)时指定了 标志 `SCC_OP_CREATEIFNEW`) 。|
|`SCC_I_OPERATIONCANCELED`|2|已取消操作。|
|`SCC_I_ADV_SUPPORT`|1|插件支持指定命令的高级选项。 有关详细信息，请参阅 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)。|
|`SCC_OK`|0|成功。|
|`SCC_E_INITIALIZEFAILED`|-1|错误：初始化失败。|
|`SCC_E_UNKNOWNPROJECT`|-2|错误：项目未知。|
|`SCC_E_COULDNOTCREATEPROJECT`|-3|错误：无法创建项目。|
|`SCC_E_NOTCHECKEDOUT`|-4|错误：文件未签出。|
|`SCC_E_ALREADYCHECKEDOUT`|-5|错误：文件已签出。|
|`SCC_E_FILEISLOCKED`|-6|错误：文件已锁定。|
|`SCC_E_FILEOUTEXCLUSIVE`|-7|错误：以独占方式签出文件。|
|`SCC_E_ACCESSFAILURE`|-8|访问源代码管理系统时出现问题，原因可能是网络或争用问题。 建议重试。|
|`SCC_E_CHECKINCONFLICT`|-9|错误：签入期间发生冲突。|
|`SCC_E_FILEALREADYEXISTS`|-10|错误：该文件已存在。|
|`SCC_E_FILENOTCONTROLLED`|-11|错误：文件不在源代码管理下。|
|`SCC_E_FILEISCHECKEDOUT`|-12|错误：文件已签出。|
|`SCC_E_NOSPECIFIEDVERSION`|-13|错误：没有指定的版本。|
|`SCC_E_OPNOTSUPPORTED`|-14|错误：不支持该操作。|
|`SCC_E_NONSPECIFICERROR`|-15|非特定错误。|
|`SCC_E_OPNOTPERFORMED`|-16|错误，操作未执行。|
|`SCC_E_TYPENOTSUPPORTED`|-17|错误：源代码管理系统不支持文件类型，例如 binary。|
|`SCC_E_VERIFYMERGE`|-18|文件已自动合并，但尚未检查，因为它正在等待用户验证。|
|`SCC_E_FIXMERGE`|-19|文件已自动合并，但由于必须手动解决的合并冲突而未签入。|
|`SCC_E_SHELLFAILURE`|-20|Shell 故障导致的错误。|
|`SCC_E_INVALIDUSER`|-21|错误：用户无效。|
|`SCC_E_PROJECTALREADYOPEN`|-22|错误：项目已打开。|
|`SCC_E_PROJSYNTAXERR`|-23|Project语法错误。|
|`SCC_E_INVALIDFILEPATH`|-24|错误：文件路径无效。|
|`SCC_E_PROJNOTOPEN`|-25|错误：项目未打开。|
|`SCC_E_NOTAUTHORIZED`|-26|错误：用户无权执行此操作。|
|`SCC_E_FILESYNTAXERR`|-27|文件语法错误。|
|`SCC_E_FILENOTEXIST`|-28|错误，本地文件不存在。|
|`SCC_E_CONNECTIONFAILURE`|-29|错误：连接失败。|
|`SCC_E_UNKNOWNERROR`|-30|未知错误。|
|`SCC_E_BACKGROUNDGETINPROGRESS`|-31|后台获取操作当前正在进行。|

## <a name="macros-provided-for-quick-checking"></a>用于快速检查的宏

```cpp
IS_SCC_ERROR(rtn) (((rtn) < 0) ? TRUE : FALSE)
IS_SCC_SUCCESS(rtn) (((rtn) == SCC_OK) ? TRUE : FALSE)
IS_SCC_WARNING(rtn) (((rtn) > 0) ? TRUE : FALSE)
```

## <a name="remarks"></a>备注
 当作为参数传递的本地文件不存在于工作文件夹中时，除[SccAdd、SccCheckin](../extensibility/sccadd-function.md)和[SccDiff](../extensibility/sccdiff-function.md)) 之外的所有源代码管理插件 (API 函数都预期会成功。 [](../extensibility/scccheckin-function.md) 例如，IDE 可能会对工作文件夹中不存在但存在于源代码管理系统中的文件发出 [对 SccCheckout](../extensibility/scccheckout-function.md) 或 [SccUncheckout](../extensibility/sccuncheckout-function.md) 的调用。 此调用将成功。 只有在工作文件夹或源代码管理系统中没有任何文件时，函数才应失败。

 当工作文件夹中的文件不存在时，某些函数（如 和 ） `SccAdd` `SccCheckin` `SCC_E_FILENOTEXIST` 应专门返回 。 如果函数对源代码管理系统中的有效文件名进行操作，则其他函数预期在工作文件不存在时成功。

 源代码管理插件不应对工作文件夹中的文件的权限做出任何假设，即使插件在某些操作期间将文件标记为只读。 可以在插件的 控件之外移动、删除和更改工作文件夹中的文件。

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
