---
title: UI 文本和帮助Visual Studio |Microsoft Docs
description: 了解帮助信息中使用的 UI 文本和术语Visual Studio。
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: e8747d07-6c90-46cc-b425-55b589f7e9e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6e946715687b46f651ac301f4e95207dbde23451011e9a48d0c20ae6a200e073
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121335415"
---
# <a name="ui-text-and-help-for-visual-studio"></a>Visual Studio 的 UI 文本和帮助
## <a name="ui-text-and-terminology"></a><a name="BKMK_UITextAndTerminology"></a> UI 文本和术语
 易于理解的文本对于有效的 UI 至关重要。 软件用户倾向于先读取标签，即与完成当前任务最相关的标签。 读取静态文本的频率较低。 计划用户启动其工作会话，快速扫描整个窗口，然后按大致顺序读取 UI：

1. 中心的交互式控件

2. 提交按钮

3. 在其他地方找到的交互式控件

4. 主要说明

5. 补充说明

6. 窗口标题

7. 正文中的其他静态文本

### <a name="usage-patterns-for-ui-text"></a>UI 文本的使用模式

#### <a name="title-bar-text"></a>标题栏文本
 标题栏文本必须与生成 UI 的命令匹配。

#### <a name="instructional-text-helper-text"></a>说明文本 (帮助程序文本) 
 在某些对话框中，提供重要的主要说明来说明在窗口或页面中要执行哪些操作很有帮助。 这有时称为"帮助程序文本"。

##### <a name="writing-style-rules-for-helper-text"></a>编写帮助程序文本的样式规则

- 不要解释这一点。 除非绝对需要，否则请勿包含说明文本。

- 说明文本始终位于对话框顶部，应引用正在执行的任务。

- 向用户准确解释他们需要执行哪些工作。 避免过多的通信和冗余。

- 查看每个窗口并消除重复的单词和语句。

- 使说明文本保持简短。 如果某些用户或方案需要更多信息，请提供指向详细概念性在线主题的链接。

- 编写文本，以便每个单词都保留权重，并且是必需的。

- 按照现有 Microsoft 指南用户界面[文本](/windows/desktop/uxguide/text-ui)[、样式和音调](/windows/desktop/uxguide/text-style-tone)。

#### <a name="supplemental-instructions"></a>补充说明
 补充说明提供了有助于用户了解控件或控件分组的其他信息。 这还可以包括了解输入控件所需的格式所需的提示文本。 请谨慎使用补充说明。 对于用户可能无法完全了解他们做出的选择的影响的情况，请保留它们。

 ![屏幕截图显示了"Internet Explorer选项"按钮，其下方有说明更改选项设置的影响的补充文本。](../../extensibility/ux-guidelines/media/0601-b_supplementaltext1.png "0601-b_SupplementalText1")

 **Visual Studio 中的补充文本**

 !["选择源代码管理"对话框Visual Studio屏幕截图，其中显示了描述每个源代码管理系统选项的补充文本。](../../extensibility/ux-guidelines/media/0601-c_supplementaltext2.png "0601-c_SupplementalText2")

 **Visual Studio 中的补充文本**

#### <a name="infotips"></a>信息提示
 通常，说明文本可能过长，无法就地在 UI 中定位，或者可能仅对新用户有用，对经验丰富的用户感到混乱。 在这种情况下，说明/信息性文本应作为工具提示放置在 InfoTip 下。

 信息提示应放置在它们相关的控件附近，并且应该使用特定的 InfoTip 图标，该图标不明显，但非常明显。

 ![Visual Studio 中的信息提示](../../extensibility/ux-guidelines/media/0601-d_infotip.png "0601-d_InfoTip")

 **示例中的信息提示Visual Studio**

##### <a name="writing-style-rules-for-infotips"></a>为信息提示编写样式规则

- 将信息提示编写为完整的句子。 它们需要特定的谓词、句子大小写和结束标点。

- 使用信息提示来补充主要指令或信息。 如果只是使用不同的字词来重述主要想法，则不需要 InfoTip。

- 保持信息提示简短且简短。 使用支持和鼓励用户的小单词和普通日常语言。

- 按照现有 Microsoft 指南用户界面[文本](/windows/desktop/uxguide/text-ui)[、样式和音调](/windows/desktop/uxguide/text-style-tone)。

#### <a name="control-labels"></a>控件标签
 控件标签应简短、简洁，并遵循Windows[桌面指南](/windows/desktop/uxguide/controls)。

 有关 UI 中的控件标签格式和位置详细信息，请参阅[布局Visual Studio。](../../extensibility/ux-guidelines/layout-for-visual-studio.md)

#### <a name="help-links"></a>“帮助”链接
 帮助链接可以放置在说明文本中或 UI 的正文中。 它们可以是指向"帮助"的链接或启动内部对话。

##### <a name="visual-style-rules-for-help-links"></a>帮助链接的视觉样式规则

- 对超链接使用正确的环境颜色。 单击时，样式正确的超链接不会短暂地呈红色闪烁。 如果看到此情况，则表明未使用环境颜色。

- 仅在悬停或链接嵌入段落时使用下划线。

- 有关超链接的视觉对象和交互样式的更多详细信息，请参阅按钮和超链接。

##### <a name="writing-style-rules-for-help-links"></a>编写帮助链接的样式规则

- 启动对话时，请维护省略号的标准：没有用于导航的省略号;如果任务需要其他 UI，则省略号。

     ![Visual Studio 中的帮助链接](../../extensibility/ux-guidelines/media/0601-e_helplink.png "0601-e_HelpLink")

     **"帮助 (...) 中的省略号指示任务需要其他 UI。**

- 链接不应以"Learn"开始，因为这不是用户的意图。 用户想要回答特定问题，而不是接受常规教育。

- 短语帮助链接，以便他们提出主题将回答的问题。

     不正确："了解有关 Azure Windows定价移动服务的详细信息"

     正确："Azure 门户Windows哪些移动服务？"

- 切勿对 *链接文本使用"* 单击..."。

- 切勿仅链接单词"here"。 这给某些屏幕阅读器造成问题，这些阅读器只会发出超链接的单词。

     不正确："在此处查找有关 azure Windows移动服务 **的信息**"

     正确："Azure 门户Windows哪些移动服务？"

- 有关帮助链接的正确编写样式详细信息，请参阅帮助 Windows[桌面指南](/windows/desktop/uxguide/winenv-help)。

#### <a name="hint-text"></a>提示文本
 提示文本在 控件中或控件下方显示为水印。 将通过使用相应的 VSColors 标记应用正确的格式 `Environment.GrayText` 设置。

 它可以以多种形式显示。

- 用控件标签来表示：

     ![下拉控件的屏幕截图，其中显示了提示文本，用于保存显示"按 Ctrl+;解决方案资源管理器 (搜索") "的控件标签。](../../extensibility/ux-guidelines/media/0601-f_hinttext1.png "0601-f_HintText1")

- 使用谓词，提供说明：

     ![控件中提示文本为"输入姓名"的文本框的屏幕截图。](../../extensibility/ux-guidelines/media/0601-g_hinttext2.png "0601-g_HintText2")

- 文本指示必需条目：

     ![控件中提示文本为"必需"的文本框 \< \> 的屏幕截图。](../../extensibility/ux-guidelines/media/0601-h_hinttext3.png "0601-h_HintText3")

#### <a name="watermark-text"></a>水印文本
 在空的设计图面上，文本应指示要执行哪些工作，并提供链接以打开其他相关窗口（如果适用）：

 ![Visual Studio 中的水印文本](../../extensibility/ux-guidelines/media/0601-i_watermarktext.png "0601-i_WatermarkText")

 **中水印文本Visual Studio**

### <a name="common-terminology"></a>常用术语

|术语|说明|评论|
|----------|-----------------|-------------|
|登录/注销|谓词使用同义词将身份验证表示为 web 属性。 在客户端中，我们使用这一一次，作为用于登录和退出 IDE 用户连接的顶级概念，此类代表提供高级功能（如漫游和许可）的顶级标识，这些功能在所有其他连接中都不可用。|IDE 用户是唯一应该表示登录/注销谓词的功能，因为它表示顶级 IDE 用户。|
|连接/断开连接|在功能维护与联机服务的单一连接的位置使用。|服务器资源管理器，一次只能有一个活动的 Azure 连接，这是一个连接/Disconnect. 的示例|
|添加/删除|非破坏性。 添加或删除列表中的内容时使用。|"TFS 连接管理器服务器列表" 对话框是 "添加/删除" 的一个示例。|
|删除|破坏. 仅当要删除的元素将被永久丢弃或从磁盘中删除时使用。|如果结果是从磁盘中删除文件，"删除" 通常需要提示。|

## <a name="error-messages"></a>错误消息

### <a name="overview"></a>概述
 出现错误。 在阻止能够避免错误消息的第一步是，设置对用户可以执行的操作的限制。 但是，当发生错误时，可能会出现一条写入错误消息，以解决问题。 错误消息可能是用户看到的最重要的通知类型之一，因为它们是同步的，指出需要解决的问题。 编写不当的错误消息会让用户自行决定错误和任何可能的解决方案的原因。

 用户可能会停止关注过度滥用或混乱的错误消息，因此只需编写一些必要的消息，为用户体验带来价值。 如果消息只是一条通知，则使用替代的演示文稿。

### <a name="rules-for-creating-an-error-message"></a>用于创建错误消息的规则

- 构造错误消息时，为受众选择适当的错误级别。 旨在提供用户可执行的操作（如果适用）的简单摘要。 不要陈述用户不需要知道的任何内容。

- 提供建设性的帮助。 读取并处理包含指令的错误消息会更容易。

- 不要使用双精度型。

- 对你编写的任何错误消息同时执行自动和手动语法和拼写检查。

- 对于复杂的错误消息，请避免顺序通信。 不要将 F1 挂钩用于错误消息。 消息本身应该已经足够。

- 使用正确的图标。

- 轻松理解并使用具有清晰选择的按钮，如 "删除" 和 "取消"。

- 对于警告，请清楚了解继续操作的结果。 按钮应指示结果。

- 有关错误，请描述用户可以执行哪些操作来解决问题。 按钮应为操作或指示 "关闭"。 不要对错误消息使用 "确定" 按钮。

- 构造错误消息时需要询问自己的一些问题：

  - 用户能否确定如何解决此错误的问题？

  - 用户使用的词汇与此错误是否相同？

  - 在多种情况下不明确还是共享此错误？ 如果是这样，如何向用户指导他们所需的解决方案？

#### <a name="build-errors"></a>生成错误
 由于 Visual Studio 是软件开发工具，因此它的许多组件都有一个用于将开发人员的工作转换为二进制格式的编译、转换或编码步骤。 当编译器无法处理错误编写的文件或编译器选项设置不正确时，这些转换可能会导致错误。

 Visual Studio 用户可以花费大量的开发小时来解决生成错误。 当错误具有依赖项或错误消息编写不当时，这种解决时间会增加，这可能会导致难以发现错误源。

 最佳生成错误是第一个位置不会出现的错误，这就是 Visual Studio 提供自动完成功能和 IntelliSense 波形曲线的原因。 架构验证程序和类似工具提供了相同类型的反馈。 这些机制主动指导用户构造格式正确的代码，减少生成错误的可能性。

 Visual Studio 提供了一个工具窗口，用户可以在其中读取并浏览文档窗口中发生的错误。 提供键盘快捷方式，以便用户可以快速地浏览大量代码，并直接转到问题所在的位置。 Visual Studio 还允许将每个生成错误绑定到特定的帮助关键字/上下文 ID，以便用户可以直接前往提供有关错误的更深入信息的帮助主题。

 编写清晰、简洁的生成错误：

- **使用无** 需编译器术语说明问题的纯语言。 生成错误的文本不应太技术性。

- **概述可能的原因。** 例如，" (属性中的属性和值之间缺少冒号) ： (值) " 声明 "。

- 详细介绍潜在的修补程序。 如果没有足够的空间，则可以将其他详细信息放入相应的帮助主题。

### <a name="components-of-a-well-written-error-message"></a>编写良好的错误消息的组成部分

#### <a name="use-the-shell-dialog-service-for-error-messages"></a>使用 shell 对话框服务获取错误消息。
 使用 shell 对话框服务，可以控制消息的外观、特定字体，而不会对单个元素进行重大更改。 使用 **IErrorInfo** 机制并使用 **IVsUIShell：： SetErrorInfo/ReportErrorInfo** 报告它们。

#### <a name="choose-an-effective-and-appropriate-notification-presentation"></a>选择有效的合适通知演示。
 如果需要立即采取措施来避免丢失数据 (同步通知) ，请使用带有严重警告的模式对话框。 关键图标为关闭消息但不读取消息的情况保留，这可能会导致负面后果。 数据丢失是需要警报级别响应的一项关键情况。 过度利用关键图标 desensitizes 用户的重要性。 如果错误消息本质上是信息性的，请考虑将模式对话框 (异步通知) 的替代项。

#### <a name="provide-a-clean-succinct-explanation-of-why-the-problem-occurred-rather-than-a-technical-explanation"></a>简要说明发生此问题的原因，而不是技术说明。
 说明中的技术详细信息的负担用户将更有可能忽略错误消息。 好消息传递示例：

- "无法打开请求的文件。"

- "无法连接到 Internet"。

#### <a name="provide-information-about-how-to-fix-the-problem"></a>提供有关如何解决此问题的信息。
 为用户提供有关如何解决此问题的建议。 如果没有任何建议，请与用户诚实。 提供指向其他在线源的直接链接，例如技术支持或社区支持。 尝试将用户指向与问题相关的特定联机信息。 对于错误 ID，请考虑将用户链接到有关该特定错误的讨论线索。 好消息传递示例：

- "请确保你已连接到 Internet，然后重试此操作。"

- "请确保该文件存在并且您有权打开该文件。"

#### <a name="write-a-message-that-is-short-and-to-the-point"></a>写入短于点的消息。
 错误消息可以通知、说明和提供解决方案，但如果它太罗嗦，仍会将其忽略。 一种解决方法是使用 "详细信息" 按钮的渐进式披露。 例如，提供简短的说明/解决方案，然后在 "详细信息" 按钮下添加更多详细信息。 如果用户选择阅读有关错误的详细信息，则可以执行此操作。

 消息中的语言应为：

- **适用域。** 使用用户将了解的语言。 尽管我们的客户是开发人员，但他们通常并没有上下文和术语。

- **相关.** 避免含糊的措辞，并为所涉及的对象指定特定的名称和位置。 例如，错误消息（如 "字符无效"）不起作用。 哪个字符？ "找不到文件。" 哪个文件？

- **短暂地.** 不要让用户感到非常愚蠢。 避免恶意或冒犯性的语言 (终止、执行、终止、致命、非法) 。 避免大写文本，该文本通常被视为驯养，并不是可读的。 不要使用幽默。

- **正确。** 使用正确的拼写和语法 (甚至在 alphas) 。 打字错误是 unprofessional 和尴尬。

- **根据上下文适用。** 使用适当的按钮文本。 避免使用 "确定" 按钮，而是使用 "继续" 或 "是/否"。

### <a name="error-message-examples"></a>错误消息示例

|好|糟糕|
|----------|---------|
|"您拨打的号码不再处于服务中。 请检查号码并再次拨号，或者拨打操作员拨打0。|-"错误 (449) ：非法数字"<br />-"此未经处理的异常错误表示操作已成功完成。"<br /><br /> ![Visual Studio 中的严重错误消息](../../extensibility/ux-guidelines/media/0602-a_errordialog.png "0602-a_ErrorDialog")|

## <a name="accessing-help"></a>访问帮助

### <a name="overview"></a>概述
 除了 MSDN 中的文档外，Visual Studio 用户还具有多个访问点，可帮助用户在 UI 中使用。 为了确保这些访问点始终可用，功能团队需要利用环境提供的帮助系统。 这些访问点包括：

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

 大多数环境创建的对话框在对话框中都有 "帮助" 按钮。 显示对话框时，"帮助" 按钮会自动隐藏并且只有 **？** 按钮正常工作。 如果 **？** 在 Windows 中，按钮会被删除或更改，这种解决方案使你可以快速返回到原始的 "帮助" 按钮。

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
