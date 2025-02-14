---
title: 客户体验改善计划
description: 了解如何在 Visual Studio 中管理隐私设置，并了解 Visual Studio 系统生成的日志、收集的数据类型，以及如何使用该日志来解决问题并提高产品质量。
ms.date: 10/28/2021
ms.topic: conceptual
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: b5f8991deec8543cd0ce6bf1d134318996bdfc22
ms.sourcegitcommit: 7a820b7698a8dcf076eb36e3d766fb0751f56bb1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2021
ms.locfileid: "131127620"
---
# <a name="visual-studio-customer-experience-improvement-program"></a>Visual Studio 客户体验改善计划

Visual Studio 客户体验改善计划 (VSCEIP) 旨在随着时间推移帮助 Microsoft 改进 Visual Studio。 此程序[收集有关错误的信息](../ide/visual-studio-experience-improvement-program.md#types-of-collected-data)、计算机硬件以及 Visual Studio 的使用方式，而不中断用户在计算机中的任务。 收集的信息帮助 Microsoft 确定要改善的功能。 本文档介绍如何[选择加入或选择退出](../ide/visual-studio-experience-improvement-program.md#opt-in-or-out) VSCEIP，并介绍我们收集的数据类型以及使用数据的方式。 还为扩展作者提供一些关于如何避免个人信息或敏感信息意外泄露的提示。

## <a name="opt-out-of-diagnostic-data-collection"></a>选择退出诊断数据收集
鉴于我们收集数据的目的以及数据访问和保留的相关约束，建议使用 Visual Studio 和 Windows 的默认隐私设置。 不过你可以[选择退出](../ide/visual-studio-experience-improvement-program.md#opt-in-or-out) Visual Studio 体验改善计划。 选择退出时，将选择退出可选诊断数据收集。 需要完成一些诊断数据收集，才能确保 Visual Studio 是安全的、最新的且正常运行。 所需的诊断数据收集不会因选择退出 VSCEIP 而受到影响。

[!INCLUDE [gdpr-hybrid-note](../misc/includes/gdpr-hybrid-note.md)]
> [!NOTE]
> VSCEIP 遥测选择加入或退出设置不适用于 Visual Studio 中的“报告问题”。 报告问题时，仅当你通过单击“提交”提供权限时，才会收集日志并发送给 Microsoft。 如果你有兴趣在提交到“报告问题”之前管理日志，请参阅[反馈数据隐私](./developer-community-privacy.md)了解更多详细信息。

### <a name="opt-in-or-out"></a>选择加入或退出

VSCEIP 默认开启。 可以按照以下步骤将其关闭或者再次打开：

::: moniker range="vs-2017"

1. 在 Visual Studio 中，选择“帮助”>“发送反馈”，然后选择“设置” 。

   “Visual Studio 体验改善计划”对话框随即打开。

1. 若要选择退出，请选择“否，我不想参加”，然后选择“确定”。 若要选择加入，请选择“是，我愿意参加”，然后选择“确定”。

   ![“Visual Studio 体验改善计划”对话框](media/experience-improvement-program.png)

::: moniker-end

::: moniker range=">=vs-2019"

1. 在 Visual Studio 中，选择“帮助”>“隐私”>“隐私设置”  。

   “Visual Studio 体验改善计划”对话框随即打开。

1. 若要选择退出，请选择“否，我不想参加”，然后选择“确定”。 若要选择加入，请选择“是，我愿意参加(建议)”，然后选择“确定” 。

   ![“Visual Studio 体验改善计划”对话框](media/vs-2022/experience-improvement-program.png)

::: moniker-end

#### <a name="registry-settings"></a>注册表设置

如果安装 [Visual Studio 生成工具](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2017)，必须更新注册表来配置 VSCEIP。 企业客户可以设置基于注册表的策略，利用这种方式构造选择加入或不加入 VSCEIP 的组策略。

相关注册表项和设置如下所示：

::: moniker range="vs-2017"

- 在 64 位操作系统上，Key = HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSCommon\15.0\SQM
- 在 32 位操作系统上，Key = HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSCommon\15.0\SQM
- 启用“组策略”时，Key = HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM

::: moniker-end

::: moniker range="vs-2019"

- 在 64 位操作系统上，Key = HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSCommon\16.0\SQM
- 在 32 位操作系统上，Key = HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSCommon\16.0\SQM
- 启用“组策略”时，Key = HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM

::: moniker-end

::: moniker range=">=vs-2022"

- 在 64 位操作系统上，Key = HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VSCommon\17.0\SQM
- 在 32 位操作系统上，Key = HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VSCommon\17.0\SQM
- 启用“组策略”时，Key = HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM

::: moniker-end

Entry = OptIn

值 = (DWORD)

- “0”为选择退出（关闭 VSCEIP）
- “1”为选择加入（开启 VSCEIP）

> [!CAUTION]
> 不正确地编辑注册表可能会对系统造成严重损坏。 在更改注册表之前，应备份计算机上任何有价值的数据。 如果在应用手动更改之后遇到问题，也可以使用“最近一次的正确配置”启动选项。

有关 VSCEIP 收集、处理或传输的信息的详情，请参阅 [Microsoft 隐私声明](https://privacy.microsoft.com/privacystatement)。

## <a name="system-generated-logs-collected-by-visual-studio"></a>由 Visual Studio 收集的系统生成的日志

Visual Studio 收集系统生成的日志以修复问题并提升产品的质量。 本文介绍我们收集的数据类型以及使用数据的方式。 还为扩展作者提供一些关于如何避免个人信息或敏感信息意外泄露的提示。

### <a name="types-of-collected-data"></a>收集的数据类型

Visual Studio 收集崩溃、UI 无响应以及 CPU 或内存使用率偏高等方面的系统生成的日志。 我们还会收集产品安装或使用期间遇到的错误的相关信息。 收集的数据会基于错误而有所不同，且会包括堆栈跟踪、内存转储和异常信息：

- 对于很高的 CPU 使用率和无响应的情况，会收集相关 Visual Studio 线程的堆栈跟踪信息。

- 如果部分线程的堆栈跟踪信息不足以确定问题的根本原因（例如崩溃、无响应还是内存使用率偏高），我们会收集内存转储。 转储代表出现错误时的进程状态。

- 对于意外的错误情况，例如在尝试向文件或磁盘写入内容时出现的异常，我们会收集该异常的相关信息。 此信息包括异常的名称、出现异常的线程的堆栈跟踪、异常的相关消息以及此特定异常的其他相关信息。

   下面是所收集数据的一个示例，显示了异常名称、堆栈跟踪以及异常消息：

   ```text
   "Reserved.DataModel.Fault.Exception.TypeString": "System.IO.IOException",
   "Reserved.DataModel.Fault.Exception.StackTrace": "System.IO.__Error.WinIOError(Int32,String)\r\n
   System.IO.FileStream.Init(String,FileMode,FileAccess,Int32,Boolean,FileShare,Int32,FileOptions,SECURITY_ATTRIBUTES,String,Boolean,Boolean,Boolean)\r\n
   System.IO.FileStream..ctor(String,FileMode,FileAccess,FileShare,Int32,FileOptions,String,Boolean,Boolean,Boolean)\r\nSystem.IO.StreamWriter.CreateFile(String,Boolean,Boolean)\r\n
   System.IO.StreamWriter..ctor(String,Boolean,Encoding,Int32,Boolean)\r\n
   System.IO.StreamWriter..ctor(String,Boolean)\r\n
   System.IO.File.CreateText(String)\r\n
   Microsoft.VisualStudio.Setup.Services.FileSystem.CreateText(String,Boolean)\r\n
   Microsoft.VisualStudio.Setup.Cache.ChannelManifestRepository.WriteChannelManifest(IChannelManifest,String,String)\r\n
   Microsoft.VisualStudio.Setup.Cache.ChannelManifestRepository.AddChannel(ChannelManifestPair,Boolean)\r\n
   Microsoft.VisualStudio.Setup.Cache.CacheManager.AddChannel(ChannelManifestPair,Boolean)\r\n
   Microsoft.VisualStudio.Setup.ChannelManager.\<UpdateAsync>d__37.MoveNext()\r\n”,
   "Reserved.DataModel.Fault.Exception.Message": " The process cannot access the file 'C:\\Users\\[UserName]\\AppData\\Local\\Microsoft\\VisualStudio\\Packages\\_Channels\\4CB340F5\\channelManifest.json' because it is being used by another process."
   ```

### <a name="how-we-use-system-generated-logs"></a>我们如何使用系统生成的日志

判定错误的根本原因的工作流会各不相同，具体取决于错误的类型和严重性。

#### <a name="error-classification"></a>错误分类

基于日志对错误进行了分类和计数，以确定调查的优先顺序。 例如，我们可能会发现，在产品的版本 \<x> 中，“System.IO.FileStream.Init”处的“System.IO.\__Error.WinIOError”出现了 500 次，并且在该版本中的出现率是最高的。

#### <a name="work-items-for-tracking"></a>用于跟踪的工作项

为按优先级排列的各个错误创建工作项并分配给工程师以进行调查。 这些工作项通常包含分类、优先级以及与错误类型相关的诊断信息。 此信息派生自收集的系统生成的错误日志。 例如，某次崩溃的工作项可能包含出现崩溃的堆栈跟踪。

#### <a name="error-investigation"></a>错误调查

工程师们使用工作项中的可用信息来确定错误的根本原因。 在某些情况下，他们需要比工作项中的内容更多的信息，他们这时候会参考收集到的原始的系统生成的日志。 例如，工程师可能会检查内存转储，以了解产品的崩溃情况。

### <a name="tips-for-extension-authors"></a>对扩展作者的提示

扩展作者应避免在模块、类型和方法名称中使用个人信息或其他敏感信息，从而限制个人信息的公开程度。 如果堆栈上的代码出现崩溃或类似的错误，此信息会被收集为系统生成的日志的一部分。

## <a name="see-also"></a>请参阅

* [如何报告 Visual Studio 的问题](../ide/how-to-report-a-problem-with-visual-studio.md)
* [Visual Studio 开发者社区](https://developercommunity.visualstudio.com/home)
* [Microsoft 隐私声明](https://privacy.microsoft.com/privacystatement)
* [Windows 10 中的诊断、反馈和隐私](https://privacy.microsoft.com/windows-10-feedback-diagnostics-and-privacy)
