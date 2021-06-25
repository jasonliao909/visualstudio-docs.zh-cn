---
title: Visual Studio 的 UI 文本和帮助 |Microsoft Docs
description: 了解 Visual Studio 帮助信息中使用的 UI 文本和术语。
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: e8747d07-6c90-46cc-b425-55b589f7e9e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 40b128c5e95c70457d92843e620b4aa072c409ba
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899428"
---
# <a name="ui-text-and-help-for-visual-studio"></a>Visual Studio 的 UI 文本和帮助
## <a name="ui-text-and-terminology"></a><a name="BKMK_UITextAndTerminology"></a> UI 文本和术语
 易于理解文本对于有效 UI 至关重要。 软件用户倾向于首先阅读标签，即与完成任务最相关的标签。 以较低的频率读取静态文本。 计划用户使用整个窗口的快速扫描来启动其工作会话，然后按照此近似顺序读取 UI：

1. 中心的交互式控件

2. 提交按钮

3. 在其他位置找到的交互式控件

4. 主要说明

5. 补充说明

6. 窗口标题

7. 主体中的其他静态文本

### <a name="usage-patterns-for-ui-text"></a>UI 文本的使用模式

#### <a name="title-bar-text"></a>标题栏文本
 标题栏文本必须与产生 UI 的命令匹配。

#### <a name="instructional-text-helper-text"></a>说明文本 (帮助器文本) 
 在某些对话框中，提供重要的主要说明来说明要在窗口或页面中执行的操作非常有用。 这有时称为 "帮助器文本"。

##### <a name="writing-style-rules-for-helper-text"></a>为帮助器文本编写样式规则

- 不要清楚地说明这一点。 除非绝对需要，否则不要包含说明文本。

- 说明文本始终置于对话框顶部，并且应引用正在执行的任务。

- 向用户准确说明他们需要执行的操作。 避免过多的通信和冗余。

- 查看每个窗口并消除重复的单词和语句。

- 简短说明文本。 如果某些用户或方案需要更多的信息，请提供详细的概念联机主题的链接。

- 编写文本，使每个单词都具有权重，并且是必需的。

- 遵循适用于 [用户界面文本](/windows/desktop/uxguide/text-ui) 和 [样式和音调](/windows/desktop/uxguide/text-style-tone)的现有 Microsoft 指导。

#### <a name="supplemental-instructions"></a>补充说明
 补充说明提供有助于用户理解控件或控制分组的其他信息。 这还可能包括必要的提示文本，以了解输入控件所需的格式。 请慎用补充说明。 如果用户可能不会完全了解所做选择的后果，请保留它们。

 ![屏幕截图：显示带有下面补充文本的 Internet Explorer 选项按钮，用于描述更改选项设置的影响。](../../extensibility/ux-guidelines/media/0601-b_supplementaltext1.png "0601-b_SupplementalText1")

 **Visual Studio 中的补充文本**

 ![Visual Studio 中的 "选择源代码管理" 对话框的屏幕截图，显示描述每个源代码管理系统选项的补充文本。](../../extensibility/ux-guidelines/media/0601-c_supplementaltext2.png "0601-c_SupplementalText2")

 **Visual Studio 中的补充文本**

#### <a name="infotips"></a>信息提示
 通常，说明文本可能会太长，无法在用户界面中就地放置，或者仅对新用户很有用，觉得对于经验丰富的用户感觉很混乱。 在这种情况下，应将说明/信息性文本作为工具提示放置在信息提示下。

 信息提示应放置在与其相关的控件附近，并应使用特定的信息提示图标，但这种情况并不明显。

 ![Visual Studio 中的信息提示](../../extensibility/ux-guidelines/media/0601-d_infotip.png "0601-d_InfoTip")

 **Visual Studio 中的信息提示示例**

##### <a name="writing-style-rules-for-infotips"></a>编写信息提示的样式规则

- 编写信息提示作为完整句子。 它们需要特定的谓词、句子大小写和结束标点。

- 使用信息提示来补充你的主要说明或信息。 如果只是使用不同的单词来重述，则不需要信息提示。

- 让信息提示简短明了。 使用支持和鼓励用户的小词和普通、日常语言。

- 遵循适用于 [用户界面文本](/windows/desktop/uxguide/text-ui) 和 [样式和音调](/windows/desktop/uxguide/text-style-tone)的现有 Microsoft 指导。

#### <a name="control-labels"></a>控件标签
 控件标签应简短、简洁，并遵循 [Windows 桌面的控件指南](/windows/desktop/uxguide/controls)。

 有关 UI 中控件标签格式和位置的详细信息，请参阅 [Visual Studio 的布局](../../extensibility/ux-guidelines/layout-for-visual-studio.md)。

#### <a name="help-links"></a>“帮助”链接
 可将帮助链接置于说明文本或 UI 正文中。 它们可以是帮助或启动内部对话框的链接。

##### <a name="visual-style-rules-for-help-links"></a>帮助链接的视觉样式规则

- 为超链接使用正确的环境颜色。 当单击正确的带样式的超链接时，将不会短暂地闪烁红色。 如果出现这种情况，则表明环境颜色未被使用。

- 下划线只应在悬停时使用或在段落中嵌入链接时使用。

- 有关超链接的视觉和交互样式的详细信息，请参阅按钮和超链接。

##### <a name="writing-style-rules-for-help-links"></a>为帮助链接编写样式规则

- 启动对话框时，请保留省略号的标准：没有用于导航的省略号，如果任务需要其他 UI，则为省略号。

     ![Visual Studio 中的帮助链接](../../extensibility/ux-guidelines/media/0601-e_helplink.png "0601-e_HelpLink")

     **"帮助" 链接中的省略号 ( ... ) 指示任务将需要其他 UI。**

- 链接不应以 "学习" 开头，因为这不是用户的意图。 用户希望回答特定问题，而不是获得一般教育。

- 短语帮助链接，让他们提出主题将回答的问题。

     错误： "了解有关 Microsoft Azure 移动服务定价的详细信息"

     正确： "适用于 Windows Azure 移动服务的哪些定价选项？"

- 永远不要对链接文本使用 *"单击 ...* "。

- 决不要链接 "此处" 一词。 这对于某些屏幕读取器是有问题的，它只会语音显示超链接字。

     错误： "在 **此处** 查找有关 Microsoft Azure 移动服务的信息"

     正确： "适用于 Windows Azure 移动服务的哪些定价选项？"

- 有关帮助链接的正确写入样式的详细信息，请参阅 [Windows 桌面指南以获得帮助](/windows/desktop/uxguide/winenv-help)。

#### <a name="hint-text"></a>提示文本
 提示文本作为水印显示在控件内或控件的下方。 将使用相应的 VSColors 标记来应用正确的格式设置 `Environment.GrayText` 。

 它可以出现在多个窗体中。

- 代替控件标签：

     ![带有提示文本的下拉控件屏幕截图，用于显示 "Search 解决方案资源管理器 (Ctrl +; ) " 的控件标签。](../../extensibility/ux-guidelines/media/0601-f_hinttext1.png "0601-f_HintText1")

- 对于谓词，提供说明：

     ![文本框中的屏幕截图，其中显示了控件中的提示文本 "输入您的姓名"。](../../extensibility/ux-guidelines/media/0601-g_hinttext2.png "0601-g_HintText2")

- 带有指示必需条目的文本：

     ![控件中的提示文本显示为 "Required" 的文本框屏幕截图 \< \> 。](../../extensibility/ux-guidelines/media/0601-h_hinttext3.png "0601-h_HintText3")

#### <a name="watermark-text"></a>水印文本
 在空设计图面上，文本应指示要执行的操作，并提供用于打开其他相关窗口的链接（如果适用）：

 ![Visual Studio 中的水印文本](../../extensibility/ux-guidelines/media/0601-i_watermarktext.png "0601-i_WatermarkText")

 **Visual Studio 中水印文本的示例**

### <a name="common-terminology"></a>常见术语

|术语|说明|评论|
|----------|-----------------|-------------|
|登录/注销|谓词与 Web 同义，用于表示 Web 属性的身份验证。 在客户端中，我们将这一次用作一个顶级概念，用于登录和退出 IDE 用户连接，这表示一个顶级标识，它提供高级功能，例如漫游和许可，但所有其他连接都不可用。|IDE 用户是唯一应表示登录/注销谓词的功能，因为它表示顶级 IDE 用户。|
|连接/断开连接|在功能维护与联机服务的单个连接的位置使用 。|服务器资源管理器连接（一次只能有一个活动 Azure 连接）是连接/断开连接的示例。|
|添加/删除|非破坏性。 在从列表中添加或删除内容时使用 。|"TFS 连接管理器服务器列表"对话框是添加/删除的示例。|
|删除|破坏性。 仅在要删除的元素将被永久丢弃或从磁盘中删除时使用。|如果结果是从磁盘中删除文件，则"删除"通常需要提示。|

## <a name="error-messages"></a>Error messages

### <a name="overview"></a>概述
 发生错误。 设置用户可以执行哪些操作的限制是防止出现可避免的错误消息的一个合理第一步。 但是，发生错误时，编写良好的错误消息对于缓解问题可能会大有作为。 错误消息可能是用户看到的最重要的通知类型之一，因为它们是同步的，表示需要解决的问题。 编写错误的错误消息让用户自行确定错误的原因和任何可能的解决方案。

 用户可能会不再关注过度使用或令人困惑的错误消息，因此只编写必要的消息来为用户体验增加价值。 如果消息只是一个通知，则使用备用演示文稿。

### <a name="rules-for-creating-an-error-message"></a>用于创建错误消息的规则

- 构造错误消息时，为受众选择适当的错误级别。 旨在提供用户可采取操作（如果适用）的直观摘要。 不要说明用户不需要知道任何内容。

- 提供积极协助。 可以更轻松地读取并处理包含指令的错误消息。

- 请勿使用双负值。

- 对写入的任何错误消息执行自动和手动语法和拼写检查。

- 对于复杂的错误消息，请避免顺序通信。 切勿对错误消息使用 F1 挂钩。 消息本身应已足够。

- 使用正确的图标。

- 使问题易于理解并使用具有明确选项的按钮，例如"删除"和"取消"。

- 对于警告，请清楚地了解继续操作的结果。 按钮应指示结果。

- 对于错误，请描述用户可以执行哪些操作来解决问题。 按钮应为操作，或显示"关闭"。 请勿对错误消息使用"确定"按钮。

- 构造错误消息时要询问的一些问题：

  - 用户能否单独确定如何解决此错误的问题？

  - 用户是否使用与此错误相同的词汇？

  - 此错误在多个情况下是令人怀疑还是共享？ 如果是，如何指导用户找到所需的解决方案？

#### <a name="build-errors"></a>生成错误
 由于Visual Studio是一种软件开发工具，因此它的许多组件都有编译、转换或编码步骤，可将开发人员的工作转换为二进制形式。 当编译器无法正确处理创作的文件或编译器选项未正确设置时，这些转换可能会导致错误。

 Visual Studio用户可能会花费大量开发时间来解决生成错误。 当错误具有依赖关系或错误消息编写不佳时，此解决时间会增加，这会使发现错误的来源很困难。

 最佳生成错误是一开始不会发生的错误，这就是Visual Studio AutoComplete 和 IntelliSense 的一些问题。 架构验证程序或类似工具提供相同类型的反馈。 这些机制会主动指导用户构造格式良好的代码，从而降低生成错误的可能性。

 Visual Studio提供了一个工具窗口，用户可以在该工具窗口中读取和导航其文档窗口中发生的错误。 提供了键盘快捷方式，以便用户可以快速导航大量代码并直接转到问题的位置。 Visual Studio还允许将每个生成错误绑定到特定的 Help 关键字/上下文 ID，以便用户可以直接转到提供有关错误的更深入信息的帮助主题。

 编写清晰简洁的生成错误：

- **使用纯语言** ，以很少或没有编译器术语来解释问题。 生成错误的文本不应过于技术。

- **概述可能的原因。** 例如，"' (属性中的 属性和值之间缺少冒号) ： (值) '声明。"

- 提供有关潜在修复的详细信息。 如果没有足够的空间，则其他详细信息可能会放入相应的帮助主题中。

### <a name="components-of-a-well-written-error-message"></a>编写良好的错误消息的组件

#### <a name="use-the-shell-dialog-service-for-error-messages"></a>对错误消息使用 shell 对话服务。
 使用 shell 对话服务可以控制消息的外观，特别是字体，而无需对单个元素进行重大更改。 使用 **IErrorInfo** 机制并使用 **IVsUIShell：：SetErrorInfo/ReportErrorInfo 报告它们**。

#### <a name="choose-an-effective-and-appropriate-notification-presentation"></a>选择有效且适当的通知演示文稿。
 如果需要立即采取措施，则使用具有严重警告的模式对话框，以避免在同步通知 (数据丢失) 。 关键图标保留用于关闭消息而不读取消息可能导致负面后果的情况。 数据丢失是需要警报级别响应的一种严重情况。 过度使用关键图标会让用户了解其重要性。 如果错误消息本质上是信息性的，请考虑使用异步通知模式对话框 (替代) 。

#### <a name="provide-a-clean-succinct-explanation-of-why-the-problem-occurred-rather-than-a-technical-explanation"></a>提供问题发生原因的简洁简洁说明，而不是技术说明。
 如果用户在解释中具有技术详细信息，则其负担过于重将更有可能忽略错误消息。 良好的消息传送示例：

- "无法打开请求的文件。"

- "无法连接到 Internet。"

#### <a name="provide-information-about-how-to-fix-the-problem"></a>提供如何解决此问题的信息。
 提供用户建议，了解如何解决问题。 如果没有建议，则与用户合作。 提供指向备用联机源的直接链接，例如技术支持或社区支持。 尝试将用户指向与问题相关的特定联机信息。 对于错误 ID，请考虑将用户链接到有关该特定错误的讨论线程。 良好的消息传送示例：

- "请确保已连接到 Internet，然后重试此操作。"

- "请确保该文件存在，并且你有权打开它。"

#### <a name="write-a-message-that-is-short-and-to-the-point"></a>编写一条简短且指向该点的消息。
 错误消息可以通知、解释和提供解决方案，但如果过于字词，则仍然会被忽略。 一种解决方案是使用带详细信息按钮的渐进式披露。 例如，提供简短说明/解决方案，然后将更多详细信息放在详细信息按钮下。 如果用户选择阅读有关错误的详细信息，他们可以这样做。

 消息中的语言应为：

- **域适用。** 使用用户将理解的语言。 即使我们的客户是开发人员，他们通常没有我们的上下文和术语。

- **特定。** 避免使用模糊的词句，并给出涉及的对象的特定名称和位置。 例如，错误消息（如 "字符无效"）不起作用。 哪个字符？ "找不到文件。" 哪个文件？

- **短暂地.** 不要让用户感到非常愚蠢。 避免恶意或冒犯性的语言 (终止、执行、终止、致命、非法) 。 避免大写文本，该文本通常被视为驯养，并不是可读的。 不要使用幽默。

- **正确。** 使用正确的拼写和语法 (甚至在 alphas) 。 打字错误是 unprofessional 和尴尬。

- **根据上下文适用。** 使用适当的按钮文本。 避免使用 "确定" 按钮，而是使用 "继续" 或 "是/否"。

### <a name="error-message-examples"></a>错误消息示例

|好|糟糕|
|----------|---------|
|"您拨打的号码不再处于服务中。 请检查号码并再次拨号，或者拨打操作员拨打0。|-"错误 (449) ：非法数字"<br />-"此未经处理的异常错误表示操作已成功完成。"<br /><br /> ![Visual Studio 中的严重错误消息](../../extensibility/ux-guidelines/media/0602-a_errordialog.png "0602-a_ErrorDialog")|

## <a name="accessing-help"></a>访问帮助

### <a name="overview"></a>概述
 除了 MSDN 中的文档外，Visual Studio 用户还具有多个访问点，可帮助用户在用户界面中使用。 为了确保这些访问点始终可用，功能团队需要利用环境提供的帮助系统。 这些访问点包括：

- **对话框中的说明文本和补充文本。** 提供方向或说明的静态文本，可以在 UI 表面上，也可以在悬停图标上悬停时使用。

- **F1 帮助** (编辑器仅) 。 在 Visual Studio 编辑器中，用户可以随时相信，按 F1 将显示特定于当前所选内容的帮助主题。 确保与 F1 关联的主题正确并提供信息。

- **帮助主题的超链接。** 对话框、工具窗口或设计图面中的超链接，用于启动主题，以帮助用户了解有关技术、功能或如何完成任务的信息。

- **帮助器 UI 机制，如智能标记和生成对话框。** 这些机制有助于用户了解 UI 元素，或促进任务，如智能标记或生成器对话框。

- **UI 帮助按钮** (弃用) 。 标题栏中的可见指示器，可用于访问相关的 F1 帮助主题。

### <a name="text"></a>文本

#### <a name="instructional-and-supplemental-text-in-dialogs"></a>对话框中的说明文本和补充文本
 在支持复杂任务的对话中，可能需要在 UI （通常是在对话框顶部或接近复杂控件）中提供说明性文本。 有关编写样式的详细信息，请参阅 [UI 文本和术语](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology) 。

#### <a name="infotips"></a>信息提示
 通常情况下，说明性文本可能太长，无法在用户界面中就地放置，或者仅对新用户很有用，觉得对经验丰富的用户感到杂乱。 在这种情况下，应将说明/信息性文本作为工具提示放置在信息提示下。

 信息提示应放置在与其相关的控件附近，并应使用特定的信息提示图标，但这种情况并不明显。

 ![Visual Studio 中的信息提示](../../extensibility/ux-guidelines/media/0601-d_infotip.png "0601-d_InfoTip")

 **Visual Studio 中的信息提示示例**

### <a name="interactive-help-mechanisms"></a>交互式帮助机制

#### <a name="f1-help"></a>F1 帮助
 需要在编辑器或设计图面中提供 F1 帮助，但不能在 Visual Studio 环境中的其他位置使用。

#### <a name="hyperlinks-to-help-topics"></a>帮助主题的超链接
 超链接可用于执行操作，在 IDE 中导航，或在浏览器中启动帮助。 请参阅 [UI 文本和术语](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology) ，详细了解语言和07.10.01 的按钮以及用于视觉对象和布局准则的超链接。

#### <a name="help--buttons-in-dialog-title-bars-deprecated"></a>在 (弃用) 的对话框标题栏中的 "帮助 [？]" 按钮
 大多数情况下，对话框的标题栏中的 "帮助 [？]" 按钮已被弃用。 UI 主题不再是我们的文档模型的一部分，因此可能没有链接到的相关主题。 实质上，标题栏按钮与 F1 帮助相同，并且对话框中不再需要该按钮。 在某些情况下，仍可将其用作指示提供更多概念或过程信息的指示符，尽管超链接更常用于较新的 UI。

##### <a name="dialogs-created-through-the-environment"></a>通过环境创建的对话框
 许多 shell 对话框是通过 **VBDialogBoxParam** 函数创建的。 已更新此共享函数，以帮助你将 " **帮助** " 按钮从对话框移动到 **？** 按钮，同时保留向后兼容并可扩展的体系结构。

 具体来说， **VBDialogBoxParam** 函数会查看 ID 为 **IDHELP** (9) 或标签为 **help** 或 **&帮助** 的按钮的对话框模板。 如果找到了 "帮助" 按钮，则会将其隐藏并将 **WS_EX_CONTEXTHELP** 样式添加到对话框中，这会将 **？** 对话框的标题栏中的按钮。

 创建对话框时，它会将对话进程推送到堆栈上，并使用名为 **DialogPreProc** 的预处理对话框过程调用该对话框。 当 **？** 按钮后，它会将 SC_CONTEXTHELP **WM_SYSCOMMAND** 发送到该对话框。 **DialogPreProc** 捕获此命令并将其更改为传递到原始对话过程的 **WM_HELP** 消息。

 大多数环境创建的对话框在对话框中都有 "帮助" 按钮。 显示对话框时，"帮助" 按钮会自动隐藏并且只有 **？** 按钮正常工作。 如果 **？** 按钮在 Windows 中被删除或更改，则此解决方案使你可以快速返回到原始的 "帮助" 按钮。

 此解决方案提出了可能导致 bug 的四个假设：

- 该对话框的 "帮助" 按钮是 **IDHELP** (9) 。

- "帮助" 按钮处于隐藏状态时，对话框看起来是正确的。

- 此对话框不会替换它的 winproc。

- 此对话框未嵌入到另一个对话框中。

  如果对话框位于 msenv 中，并且不使用 **VBDialogBoxParam**，请在实现自己的处理程序之前调查使用 **VBDialogBoxParam** 。

##### <a name="dialogs-created-through-other-packages"></a>通过其他包创建的对话框
 您可以为驻留在 msenv 外部的对话框实现自己的解决方案。 对于 VSPackage 中的共享对话框类，请考虑将按钮移动到标题栏，或在每个对话框上实现处理程序。 下面的代码是实现的主干，旨在帮助你入门：

```
struct DLGPROCITEM
{
    FARPROC proc; // The info used to create the dialog.
    DLGPROCITEM* procPrev;
};

DLGPROCITEM* g_dlgProcStack = NULL;

// A dialog starter/wrapper function is used to push the new
// dialog proc to the top of our dialog proc stack.

int SomeDialogStarterFunction(hinst, id, proc, etc)
{
    if (g_dlgProcStack == NULL)
    {
        g_dlgProcStack = new DLGPROCITEM;
        g_dlgProcStack->procPrev = NULL;
    }
    else
    {
        DLGPROCITEM* procItem = new DLGPROCITEM;
        g_dlgProcStack->procPrev = g_dlgProcStack;
        g_dlgProcStack = procItem;
    }
}

// Pop this dialog proc off the dialog proc stack.

DialogBoxIndirectParam...(...)
{
    DLGPROCITEM* procItem = g_dlgProcStack->procPrev;
    delete g_dlgProcStack;
    g_dlgProcStack = procItem;
}

// A wrapper dialog procedure will allow us to capture the
// SC_CONTEXTHELP button on the title bar from Windows and
// forward it as a simple WM_HELP message back to the dialog.

INT_PTR CALLBACK DialogPreProc(HWND hwndDlg, UINT uMsg,
    WPARAM wParam, LPARAM lParam)
{
    if (uMsg == WM_SYSCOMMAND && wParam == SC_CONTEXTHELP)
    {
        uMsg = WM_HELP;
        wParam = 0;
        lParam = 0;
    }
    return CallWindowProc((WNDPROC)g_dlgProcStack->proc,
        hwndDlg, uMsg, wParam, lParam);
}
```

##### <a name="help-buttons-in-managed-code"></a>托管代码中的帮助按钮
 在托管代码中，重写窗口标题栏 "帮助" 按钮的默认行为很简单。 下面是一个演示此行为的完整演示应用程序。 实质上，你需要重写窗体的 **WndProc** 方法，然后在 **SC_CONTEXTHELP** 消息被截获时激发 F1 帮助请求。

```
using System;
using System.Windows.Forms;

public class HelpForm : Form
{
    private const int SC_CONTEXTHELP = 0xF180;
    private const int WM_SYSCOMMAND = 0x0112;

    public HelpForm()
    {
        this.ClientSize = new System.Drawing.Size(300, 250);
        this.HelpButton = true;
        this.MaximizeBox = false;
        this.MinimizeBox = false;
        this.Name = "HelpForm";
        this.Text = "Help Form";
    }

    protected override void WndProc(ref Message m)
    {
        if (m.Msg == WM_SYSCOMMAND && SC_CONTEXTHELP == (int)m.WParam)
            ShowHelp();
        else
            base.WndProc(ref m);
    }

    private void ShowHelp()
    {
        MessageBox.Show("F1 Help goes here.");
    }

     [STAThread]
    static void Main()
    {
        Application.EnableVisualStyles();
        Application.EnableRTLMirroring();
        Application.Run(new HelpForm());
    }
}
```

## <a name="see-also"></a>另请参阅
- [Visual Studio 的字体和格式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)
- [Visual Studio 的布局](../../extensibility/ux-guidelines/layout-for-visual-studio.md)
- [Visual Studio 的通知和进度](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)
