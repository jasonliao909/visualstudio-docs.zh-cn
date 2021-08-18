---
title: 结构和联合|Microsoft Docs
description: 本文链接到调试 SDK 中结构和联合Visual Studio说明。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- structures [Visual Studio SDK]
ms.assetid: 9ff0a8f8-1ee6-4fdd-8b80-206436ff589b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: fd727409541d7b4935fcf676bf17319ae25b3a04b67bded0a14b548ade213f08
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121377061"
---
# <a name="structures-and-unions"></a>结构和联合
以下是调试 SDK 中的Visual Studio和联合。

- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 指定进程 ID，可以是系统 ID 或 GUID。

- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) 描述将发射断点的条件。

- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) 描述错误断点（包括位置、程序、线程）的解决方法。

- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 指定用于描述断点位置的结构类型。

- [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md) 定义描述断点在代码中的地址位置的组件。

- [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md) 描述直接绑定到正在调试的程序中的地址的断点的位置。

- [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md) 描述代码源文件中行处断点的位置。

- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md) 描述断点在代码中的函数的偏移位置。

- [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md) 用于基于用户可从 IDE 输入的字符串设置代码断点。

- [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md) 用于设置基于用户可从 IDE 输入的字符串的数据断点。

- [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md) 描述特定位置的断点解析。

- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) 描述在之前传递断点后将触发断点的计数和条件。

- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 包含实现断点所需的信息。

- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 包含实现断点结构 (结构 [BP_REQUEST_INFO的信息，](../../../extensibility/debugger/reference/bp-request-info.md) 但包含供应商 GUID、约束和跟踪点) 。

- [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md) 描述代码断点的位置。

- [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md) 描述绑定数据断点的结果。

- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) 描述代码断点或数据断点的绑定断点信息。

- [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md) 指定断点解析位置的结构。

- [BSTR_ARRAY](../../../extensibility/debugger/reference/bstr-array.md) 描述字符串的数组。

- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md) 指定有关从元数据获取的字段类型的信息。

- [CODE_PATH](../../../extensibility/debugger/reference/code-path.md) 描述对函数或方法的调用。

- [COMPUTER_INFO](../../../extensibility/debugger/reference/computer-info.md) 描述运行调试器的计算机。

- [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md) 描述 GUID 的列表。

- [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md) 描述内存上下文或代码上下文。

- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 描述正在调试的程序中的地址。

- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) 表示多种不同类型的地址之一。

- [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) 标识自定义查看器或类型可视化工具。

- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 描述一个调试属性，该属性又描述具有名称、类型和值的分层特性的对象。

- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 描述引用。

- [反汇编数据](../../../extensibility/debugger/reference/disassemblydata.md) 描述对 IDE 进行反汇编以进行显示。

- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 描述正在调试的程序引发的异常或运行时错误。

- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md) 描述局部变量、参数或其他字段。

- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 描述堆栈帧。

- [GUID_ARRAY](../../../extensibility/debugger/reference/guid-array.md) 描述可用调试引擎的唯一标识符数组。

- [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md) 用于设置模块的 JustMyCode 信息。

- [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md) 描述特定计算机。

- [METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md) 描述数组中的数组元素。

- [METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md) 描述类或结构的字段的地址。

- [METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md) 描述作用域内局部变量的地址 (函数或方法) 。

- [METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md) 描述类的方法的地址。

- [METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md) 描述方法或函数的参数。

- [METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md) 描述方法或函数的返回值。

- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md) 描述从元数据取的字段类型。

- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) 描述 DLL、EXE (程序集的特定模块) 。

- [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md) 描述已搜索的符号搜索路径的状态信息。

- [NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md) 描述本机地址。

- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md) 描述从 PDB 符号取的字段类型。

- [PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md) 描述已准备好绑定到代码位置的断点的状态。

- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) 描述进程。

- [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md) 描述表示程序节点 [的 IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 对象的列表。

- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md) 描述计算机上运行的进程。

- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 描述给定文本中的行和列位置。

- [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md) 描述线程的属性。

- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) 描述字段的类型。

- [UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md) 描述物理地址。

- [UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md)描述一个地址，该地址相对于 (`this` `Me` 中的指针Visual Basic) 。

## <a name="requirements"></a>要求
 标头：msdbg.h、sh.h 或 ee.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
