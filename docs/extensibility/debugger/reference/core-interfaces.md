---
description: 下面的接口是用于通过使用 VS SDK 扩展调试器的核心接口。
title: 核心接口 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], core interfaces
ms.assetid: 666b9116-8550-4bdd-bc15-55fc57de87df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 5dd69f5dd140118ea36ad02ff88bc36d6815616f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122127644"
---
# <a name="core-interfaces"></a>核心接口
下面的接口是用于通过使用扩展调试器的核心接口 [!INCLUDE[vsipsdk](../../../extensibility/includes/vsipsdk_md.md)] 。

## <a name="discussion"></a>讨论 (Discussion)
 这些接口主要用于创建 (DE) 的调试引擎。 它们按类别划分：

- [“断点”](#Breakpoints)

- [上下文](#Contexts)

- [核心服务器](#CoreServer)

- [调试引擎](#DebugEngines)

- 文档

- [事件](#Events)

- [表达式](#Expressions)

- [内存](#Memory)

- [模块](#Modules)

- [端口](#Ports)

- [进程](#Processes)

- Programs 

- [属性](#Properties)

- [堆栈帧](#StackFrames)

- [线程](#Threads)

- [类型可视化工具](#TypeVisualizers)

  可实现接口的实体包括：

-  (DE) 调试引擎

- 端口供应商 (PS) 

- 表达式计算器 (企业版) 

- Visual Studio (VS) 

## <a name="breakpoints"></a><a name="Breakpoints"></a> 处
 这些接口与断点的实现和跟踪相关。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)|DE|表示绑定到内存位置的断点。|
|[IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|DE|当断点绑定到内存位置时由 DE 发送。|
|[IDebugBreakpointChecksumRequest2](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2.md)|VS|表示断点请求的文档校验和。|
|[IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|DE|当断点未能绑定到内存位置时由 DE 发送。|
|[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)|DE|当到达断点时由 DE 发送。|
|[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)|VS|表示对断点的请求;用于创建挂起断点。|
|[IDebugBreakpointRequest3](../../../extensibility/debugger/reference/idebugbreakpointrequest3.md)|VS|表示对断点的请求;用于创建挂起断点。|
|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|DE|表示用于绑定断点的信息。|
|[IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|DE|当断点未绑定到内存位置时由 DE 发送。|
|[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)|DE|表示) 返回 (无效断点 `IDebugBreakpointErrorEvent2` 。|
|[IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)|DE|表示有关无效断点的解决方法信息。|
|[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|DE|表示函数中设置了断点的位置。|
|[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)|DE|表示要绑定的断点;用于创建绑定断点。|
|[IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)|DE|表示对一组绑定断点的枚举。|
|[IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)|DE|表示对一组不能绑定到内存位置的断点的枚举。|

## <a name="contexts"></a><a name="Contexts"></a> 上下文
 这些接口表示正在调试的程序中的不同类型的上下文。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|DE|表示代码指令的起始位置。|
|[IDebugCodeContext3](../../../extensibility/debugger/reference/idebugcodecontext3.md)|DE|扩展 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 接口，以便能够检索模块和进程接口。|
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS、DE|表示文档中的位置。|
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|表示要在其中计算表达式的上下文。|
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|表示字节集合的内存中的起始位置。|
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|表示断点或异常的堆栈帧上下文。|
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|表示断点或异常的堆栈帧上下文。|
|[IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)|DE|表示一组代码上下文的枚举。|

## <a name="core-server"></a><a name="CoreServer"></a> 核心服务器
 这些接口表示正在其上调试程序计算机。 这些由 实现 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ，但调试引擎可以调用它们。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)|VS|提供对端口和端口供应商的访问，以及有关计算机的信息。|
|[IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)|VS|表示支持[远程调试的 IDebugCoreServer2。](../../../extensibility/debugger/reference/idebugcoreserver2.md)|

## <a name="debug-engines"></a><a name="DebugEngines"></a> 调试引擎
 这些接口表示调试引擎及其关联的事件。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)|DE|表示自定义调试引擎。|
|[IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)|DE|表示支持加载符号、JustMyCode 和异常的自定义调试引擎。|
|[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)|DE|由 DE 的每个新实例发送，指示它已准备好处理调试任务。|
|[IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)|DE|表示支持启动程序自定义调试引擎。|
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE、PS|表示处理多个调试引擎的程序节点。|
|[IDebugQueryEngine2](../../../extensibility/debugger/reference/idebugqueryengine2.md)|DE|为 SDM 提供一种方法，用于从线程、程序或堆栈帧获取调试引擎的接口。|

## <a name="documents"></a><a name="Documents"></a> 文件
 这些接口表示源文件 (及其) 的文档。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|DE|由 DE 发送以请求打开文档。|
|[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)|DE|表示文档中的反汇编指令流。|
|[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)|VS、DE|表示 DE 提供的文档，指定 CLSID (名称和) 。|
|[IDebugDocumentChecksum2](../../../extensibility/debugger/reference/idebugdocumentchecksum2.md)|DE、企业版|表示调试文档的校验和，并启用在组件之间传递校验和。|
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS、DE|表示文档上下文，文档内与特定语句和代码上下文相对应的位置。|
|[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|VS、DE|表示文档中的常规位置。|
|[IDebugDocumentPositionOffset2](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2.md)|VS|将源文件中的位置表示为字符偏移量。|
|[IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)|VS、DE|表示 DE 文档提供的文本文档 (派生自 [IDebugDocument2) ，](../../../extensibility/debugger/reference/idebugdocument2.md) 提供实际文本。|
|[IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|DE|由 DE 发送，用于指定对内存中源文件的更改。|

## <a name="events"></a><a name="Events"></a> 事件
 这些接口表示在 DE 和会话调试管理器之间发送的所有事件 (SDM) 。

| 接口 | 实现者 | 说明 |
| - |----------------| - |
| [IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md) | DE | 由 DE 发送以请求打开文档。 |
| [IDebugBeforeSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2.md) | DE | 调试引擎 (DE) 将此接口发送到会话调试管理器 (SDM) 以在符号加载期间设置状态栏消息。 |
| [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) | DE | 当程序中的中断已完成时由 DE 发送。 |
| [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) | DE | 绑定断点时由 DE 发送。 |
| [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) | DE | 当断点绑定失败时由 DE 发送。 |
| [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) | DE | 当到达断点时由 DE 发送。 |
| [IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md) | DE | 当断点未绑定时由 DE 发送。 |
| [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md) | DE | 由 DE 发送，以确定它是否应在特定位置停止。 |
| [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md) | DE | 由 DE 发送以指定对内存中的源文件所做的更改。 |
| [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) | DE | 由每个新的 DE 实例发送以指示它已准备好处理调试任务。 |
| [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) | DE | 由 DE 发送以指示正在调试的程序已准备好执行第一个指令。 |
| [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md) | DE | 其他事件接口使用的接口，该接口可能会返回错误，以提供可读的错误消息。 |
| [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) | DE、PS | 派生所有其他事件接口的基接口。 |
| [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) | VS | 表示由 SDM 实现的接口，这些事件 (表示为实现特定事件接口) 的对象。 |
| [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) | DE | 在正在调试的程序中发生异常时由 DE 发送。 |
| [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) | DE | 异步表达式计算完成后由 DE 发送。 |
| IDebugFindSymbolEvent2 | | 已过时。 请勿使用。 |
| [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md) | DE | 当处理拦截的异常时，由 DE 发送。 |
| [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) | DE | 当程序完成加载时由 DE 发送。 |
| [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md) | DE | 由 DE 发送，使 IDE 向用户显示一条信息性消息。 |
| [IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md) | DE | 当加载或卸载模块时由 DE 发送。 |
| [IDebugNoSymbolsEvent2](../../../extensibility/debugger/reference/idebugnosymbolsevent2.md) | DE | [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]向调试器 UI 发出信号，以向用户发出警告：找不到已启动的可执行文件的符号。 |
| [IDebugOutputStringEvent2](../../../extensibility/debugger/reference/idebugoutputstringevent2.md) | DE | 由 DE 发送，使 IDE 显示任意字符串。 |
| [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) | VS、DE | 由端口发送，用于将端口事件与任何侦听器通信。 |
| [IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md) | DE、PS | 在创建进程时由 DE 或 port 发送。 |
| [IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md) | DE、PS | 当进程被销毁时由 DE 或端口发送。 |
| [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) | DE、PS | 在创建程序时由 DE 或 port 发送。 |
| [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) | DE、PS | 当程序被销毁时由 DE 或端口发送。 |
| [IDebugProgramDestroyEventFlags2](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2.md) | DE | [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]当您结束调试会话时，使调试引擎能够重写 UI 的默认行为。 |
| [IDebugProgramNameChangedEvent2](../../../extensibility/debugger/reference/idebugprogramnamechangedevent2.md) | DE | 当程序的名称更改时，从调试引擎发送 (取消) 到会话调试管理器 (SDM) 。 |
| [IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md) | DE | 当已创建由接口) 表示的新属性 (时，由 DE 发送 `IDebugProperty2` 。 |
| [IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md) | DE | 当属性被销毁时由 DE 发送。 |
| [IDebugReturnValueEvent2](../../../extensibility/debugger/reference/idebugreturnvalueevent2.md) | DE | 当跳出或超出某个函数时发送，因此返回值可以正确显示。 |
| [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md) | VS | 启用调试引擎以远程读取指标设置。 |
| [IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md) | DE | 单步执行、逐过程执行或跳出指令时由 DE 发送。 |
| [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md) | DE | 由 DE 发送，用于指示模块加载符号的成功或失败。 |
| [IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md) | DE | 在创建线程时由 DE 发送。 |
| [IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md) | DE | 当线程被销毁时由 DE 发送。 |
| [IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md) | DE | 当线程已更改其名称时由 DE 发送。 |

## <a name="expressions"></a><a name="Expressions"></a> 表达式
 这些接口表示要在特定上下文中计算的表达式。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)|DE|表示要计算表达式。 从 [IDebugExpressionContext2 接口](../../../extensibility/debugger/reference/idebugexpressioncontext2.md) 获取。|
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|表示计算表达式的上下文。 从 [IDebugStackFrame2 接口](../../../extensibility/debugger/reference/idebugstackframe2.md) 获取。|
|[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|DE|异步表达式计算完成时由 DE 发送。|

## <a name="memory"></a><a name="Memory"></a> 记忆
 这些接口表示内存中的字节序列。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)|DE|表示内存中可以读取或写入的字节序列。|
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|表示内存中的字节序列的位置。|

## <a name="modules"></a><a name="Modules"></a> 模块
 这些接口表示一个模块，该模块对应于可执行文件或.DLL文件。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)|DE|表示单个可执行文件或 DLL。|
|[IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)|DE|表示支持[符号的 IDebugModule2。](../../../extensibility/debugger/reference/idebugmodule2.md)|
|[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|DE|加载或卸载模块时由 DE 发送。|
|[IDebugSourceServerModule](../../../extensibility/debugger/reference/idebugsourceservermodule.md)|DE|表示 PDB 文件中包含的源服务器信息。|
|[IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)|DE|表示对 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)已知的一组模块的枚举。|

## <a name="ports"></a><a name="Ports"></a> 港口
 这些接口表示端口和端口供应商。

| 接口 | 实现者 | 说明 |
| - |----------------| - |
| [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md) | VS、PS | 表示本地计算机上的默认端口。 |
| [IDebugFirewallConfigurationCallback2](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2.md) | VS | 启用使用 DCOM 来请求 UI 确保防火墙不会阻止远程调试的 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 调试引擎。 |
| [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) | VS、PS | 表示端口。 |
| [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) | PS | 由端口发送，以将端口事件传达给任何侦听器。 |
| [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md) | PS | 表示可以启动和终止过程的端口。 |
| [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) | PS | 用于向端口注册和注销程序;允许端口跟踪当前正在调试的程序。 |
| [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md) | PS | 表示用于选择端口的自定义 UI。 |
| [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) | VS | 表示将创建或定位新端口的端口请求。 |
| [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) | PS | 表示端口供应商。 |
| [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md) | PS | 表示一个端口供应商，这些端口可以 (保存到磁盘) 有关创建的端口的信息。 |
| [IDebugPortSupplierDescription2](../../../extensibility/debugger/reference/idebugportsupplierdescription2.md) | PS | 使 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] UI 能够在"附加到进程"对话框的"传输信息"**部分内显示** 文本。 |
| [IDebugWindowsComputerPort2](../../../extensibility/debugger/reference/idebugwindowscomputerport2.md) | VS | 允许查询有关目标计算机的信息。 |
| [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md) | VS、PS | 表示一组端口上的枚举。 |
| [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md) | VS | 表示一组端口供应商的枚举。 |

## <a name="processes"></a><a name="Processes"></a> 过程
 这些接口表示进程，即包含一个或多个程序的单个可执行文件。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)|PS、DE|表示在计算机上运行的进程。|
|[IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)|PS、DE|表示一个进程，该进程主动支持调试 (用于在 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口上替换步骤、继续和执行方法) 。|
|[IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)|DE、PS|在创建进程时由 DE 或 port 发送。|
|[IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)|DE、PS|当进程被销毁时由 DE 或端口发送。|
|[IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)|PS|表示一个进程，该进程必须跟踪附加到的会话。|
|[IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)|PS|表示端口上的一组进程的枚举。|

## <a name="programs"></a><a name="Programs"></a> 程序
 这些接口表示不一定对应于物理可执行文件或模块的程序、执行逻辑单元。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)|DE|表示需要与同时调试的其他程序协同工作的 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 。|
|[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)|DE、PS|表示执行的逻辑单元。|
|[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|DE、PS|在创建程序时由 DE 或 port 发送。|
|[IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|DE、PS|当程序被销毁时由 DE 或端口发送。|
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE、PS|表示可由多个调试引擎处理的 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 。|
|[IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)|PS|表示必须能够跟踪附加到会话的会话的 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 。|
|[IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)|DE、PS|表示一个 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) ，它可以返回有关正在运行的进程的信息。|
|[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)|DE、PS|表示可调试的程序。|
|[IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)|DE、PS|允许程序节点通知附加到关联程序的尝试。|
|[IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)|DE|为 SDM 提供一种方法，用于查询通过该 DE 控制的程序的取消。|
|[IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)|VS|由 DEs 用来向 SDM 注册程序以显示正在调试的程序。|
|[IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)|DE、PS|表示可跨线程或进程边界封送接口的 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 。|
|[IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)|DE、PS|表示一组程序的枚举。|

## <a name="properties"></a><a name="Properties"></a> 属性
 这些接口表示属性，这是一个与特定上下文相关的值，通常是表达式计算的结果。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)|EE|表示可通过自定义方式显示其值的 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 。|
|[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)|DE|表示堆栈帧、文档或表达式计算的结果的值。|
|[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)|DE|表示支持任意长字符串的 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 。|
|[IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|DE|当已创建 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 接口) 表示的新属性 (时，由 DE 发送。|
|[IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|DE|当属性被销毁时由 DE 发送。|
|[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)|DE|表示对可存在于任何特定堆栈帧之外的属性的引用。|
|[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)|DE|表示一组 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 结构的枚举，这些结构描述变量、寄存器、参数和表达式。|
|[IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)|DE|表示一组 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 结构的枚举。|

## <a name="stack-frames"></a><a name="StackFrames"></a> 堆栈帧
 这些接口表示堆栈帧，这是发生断点或异常的上下文。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|表示在其中发生断点或异常的上下文。|
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|表示可处理被截获异常的 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) 。|
|[IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)|DE|表示一组 [CODE_PATH](../../../extensibility/debugger/reference/code-path.md) 结构，它们指定了用于到达特定堆栈帧的函数调用序列。|
|[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)|DE|表示对一组 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 结构的枚举，这些结构描述堆栈帧。|

## <a name="threads"></a><a name="Threads"></a>线程
 这些接口表示线程及其关联的事件。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|DE|表示执行线程。|
|[IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|DE|在创建线程时由 DE 发送。|
|[IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|DE|当线程被销毁时由 DE 发送。|
|[IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|DE|当线程已更改其名称时由 DE 发送。|
|[IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)|DE|表示一组线程的枚举。|

## <a name="type-visualizers"></a><a name="TypeVisualizers"></a> 类型可视化工具
 这些接口为类型可视化工具提供支持。 这些接口通常由表达式计算器实现。

|接口|实现者|说明|
|---------------|--------------------|-----------------|
|[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)|EE|表示要向类型可视化工具显示的字节数组。|
|[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)|EE|提供用于访问要传递给类型可视化工具的数据的方法。|
|[IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)|EE|表示一个属性，该属性提供对 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) 实现的访问。|

## <a name="see-also"></a>请参阅
- [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
- [创建自定义调试引擎](../../../extensibility/debugger/creating-a-custom-debug-engine.md)
