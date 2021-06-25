---
title: Visual Studio 的通知和进度 |Microsoft Docs
description: 了解如何通过多种方式来通知用户在 Visual Studio 中发生了哪些有关软件开发任务的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: f0ef65e9-0f1f-45f4-9f25-6e2398691168
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 994a315d04b06d1998a8c8e0c4291b6a4c54cb61
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902236"
---
# <a name="notifications-and-progress-for-visual-studio"></a>Visual Studio 的通知和进度
## <a name="notification-systems"></a><a name="BKMK_NotificationSystems"></a> 通知系统

### <a name="overview"></a>概述
 有多种方法可通知用户 Visual Studio 中发生的关于其软件开发任务的内容。

 实现任何类型的通知时：

- **将通知数保持为最小** 有效数字。 通知消息应该适用于大多数 Visual Studio 用户或特定功能/功能区域的用户。 过多地使用通知可能会 sidetrack 用户或降低系统的易用性。

- **确保显示清晰、可操作的消息** ，用户可以使用这些消息来调用适当的上下文，以便进行更复杂的选择并采取进一步的操作。

- **适当地显示同步和异步消息。** 同步通知指示需要立即关注的内容，例如当 web 服务崩溃或引发代码异常时。 应该立即向用户通知这种情况，要求用户输入，例如在模式对话框中。 异步通知是指用户应该知道但不需要立即采取措施的通知，例如在生成操作完成或网站部署完成时。 这些消息应该更环境，而且不会中断用户的任务流。

- **仅在必要时使用模式对话框，以防止用户** 在确认消息或做出对话框中显示的决策之前采取进一步操作。

- **删除不再有效的环境通知。** 如果用户已经采取操作来解决通知他们的问题，则不要求用户关闭通知。

- **请注意，通知可能导致错误相关性。** 用户可能会相信，其中一个或多个操作触发了通知，但实际上没有因果关系。 请在通知消息中清除有关上下文、触发器和通知的源的信息。

### <a name="choosing-the-right-method"></a>选择正确的方法
 使用此表可帮助你选择正确的方法来通知用户消息。

|方法|使用|请勿使用|
|------------|---------|----------------|
|[模式错误消息对话框](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ModalErrorMessageDialogs)|在需要用户响应时使用，然后继续。|不需要阻止用户并中断其流时，请不要使用。 如果可以用另一种不太入侵的方式显示消息，则应避免使用模式对话框。|
|[IDE 状态栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_IDEStatusBar)|当存在有关进程状态的环境文本信息时，请使用。|不要单独使用。 最好与其他反馈机制结合使用。|
|[嵌入式信息栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedInfobar)|在工具窗口或文档窗口中，使用来通知进度、错误状态、结果和/或可操作的信息。|如果信息与信息栏所在的位置无关，请不要使用。<br /><br /> 不要在文档/工具窗口之外使用。|
|[鼠标光标更改](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_MouseCursorChanges)|可用于通知进程正在进行。 还用于通知鼠标发生了状态变化，例如当拖/放正在进行或鼠标光标处于特定模式（如绘图模式）时。|不要使用进行较短的进度更改，或者如果游标的 fluttering 可能 (例如，绑定到较长运行进程的一部分，而不是与整个进程) 相关联。|
|[进度指示器](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotSysProgressIndicators)|需要 ("确定性" 或 "不确定") 报告进度时使用。 每种类型都有多种进度指示器类型和特定用法。 请参阅 [进度指示器](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators)。||
|[Visual Studio“通知”窗口](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_VSNotificationsToolWindow)|"通知" 窗口不能公开扩展。 但是，它用于传达有关 Visual Studio 的一系列消息，包括你的许可证的重要问题，以及对 Visual Studio 或到包的更新的信息性通知。|请勿用于其他类型的通知。|
|[错误列表](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ErrorList)|如果问题与用户当前打开的解决方案直接相关，出现 (错误/警告/信息) 的问题，则他们可能需要对代码采取措施。<br /><br /> 这包括：<br /><br /> -编译器消息 (错误/警告/信息) <br /><br /> -代码分析器/代码的诊断消息<br /><br /> -生成消息<br /><br /> 可能适用于与项目或解决方案文件相关的问题，但请首先考虑解决方案资源管理器指示。|对于与用户的开放式解决方案代码不具有任何关系的项，请不要使用。|
|编辑器通知：灯泡|如果有可用于解决打开文件中存在的问题的修补程序，请使用。<br /><br /> 请注意，灯泡还应该用于托管按需在用户的代码上执行的快速操作，例如重构，但在这种情况下，将不会显示 "通知样式"。|不要将用于不与打开的文件进行任何关系的项。|
|编辑器通知：波形曲线|用于向用户发出警报，提醒用户解决其开放代码的特定范围 (例如，) 的错误的红色波形曲线。|不要将用于不与其打开代码的特定范围相关的项。|
|[嵌入式状态栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedStatusBars)|用于提供与特定工具窗口、文档窗口或对话框窗口上下文内的内容或流程相关的状态。|请勿用于常规产品通知、进程或与特定窗口内的内容不相关的项目。|
|[Windows 任务栏通知](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_WindowsTray)|用于显示进程外进程或配套应用程序的通知。|不要将用于与 IDE 相关的通知。|
|[通知气泡](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotificationBubbles)|用于在 IDE **外部** 通知远程进程或更改。|不要将作为向用户通知 IDE **内** 进程的方法。|

### <a name="notification-methods"></a>通知方法

#### <a name="modal-error-message-dialogs"></a><a name="BKMK_ModalErrorMessageDialogs"></a> 模式错误消息对话框
 模式错误消息对话框用于显示需要用户确认或操作的错误消息。

 ![模式错误消息](../../extensibility/ux-guidelines/media/0901-01_modalerrormessage.png "0901-01_ModalErrorMessage")

 **一个模式错误消息对话框，用于对数据库的无效连接字符串进行用户警报**

#### <a name="ide-status-bar"></a><a name="BKMK_IDEStatusBar"></a> IDE 状态栏
 用户注意到状态栏文本与他们的所有计算机体验和 Windows 平台特定体验相关的可能性。 Visual Studio 客户群在这两个方面都很有经验，即使是知识丰富的 Windows 用户可能会错过状态栏中的更改。 因此，状态栏最适合用于信息性目的或作为冗余的提示来提供其他位置提供的信息。 用户必须立即解决的任何类型的关键信息都应该在对话或通知工具窗口中提供。

 Visual Studio 状态栏旨在允许显示多种类型的信息。 它划分为多个区域，用于反馈、设计器、进度栏、动画和客户端。

 反馈区域和设计器区域始终可见。 进度栏和动画区域始终是动态的，并且基于用户上下文。 设计器区域具有一个静态宽度，由从该文本消息的伴随资源中提取的字符串长度决定。 这允许本地化调整宽度大小，而无需更改代码。 对于英语，此字符串的宽度约为220像素。 设计器区域将正常运行，并且反馈区域会吸收剩余的空间。

 状态栏也着色通过传达各种 IDE 状态更改（例如 IDE 处于调试模式时）来添加视觉对象和功能值。

 ![IDE 状态栏颜色更改](../../extensibility/ux-guidelines/media/0901-02_idestatusbar.png "0901-02_IDEStatusBar")

 **IDE 状态栏颜色**

#### <a name="embedded-infobar"></a><a name="BKMK_EmbeddedInfobar"></a> 嵌入的信息栏
 可在文档窗口或工具窗口顶部使用信息栏来通知用户状态或条件。 它还可以提供命令，使用户能够轻松地采取措施。 "信息栏" 是标准 shell 控件。 避免创建您自己的，这将会起作用，并与 IDE 中的其他内容不一致。 有关实现的详细信息和使用指南，请参阅 [信息栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars) 。

 ![嵌入式信息栏](../../extensibility/ux-guidelines/media/0901-03_embeddedinfobar.png "0901-03_EmbeddedInfobar")

 **在文档窗口中嵌入的信息栏，提醒用户 IDE 处于历史调试模式，并且编辑器在标准调试模式下的响应方式不会相同。**

#### <a name="mouse-cursor-changes"></a><a name="BKMK_MouseCursorChanges"></a> 鼠标光标更改
 更改鼠标光标时，请使用绑定到 VSColor 服务的颜色，并且已与光标关联。 游标更改可用于指示正在进行的操作，还可用于指示正在进行的操作，以及在用户将鼠标悬停在可拖放到其上或用于选择对象的目标上的命中区域。

 仅当必须为某个操作保留所有可用的 CPU 时间，以防止用户表示任何进一步的输入时，才使用忙/wait 鼠标光标。 在大多数情况下，如果使用多线程编写编写良好的应用程序，则阻止用户执行其他操作的时间应很少。

 请记住，对于其他位置提供的信息，游标更改会很有用。 不要依赖于游标更改，这是与用户进行通信的唯一方式，尤其是在尝试传达用户必须解决的关键内容时。

#### <a name="progress-indicators"></a><a name="BKMK_NotSysProgressIndicators"></a> 进度指示器
 进度指示器对于在需要超过几秒钟才能完成的过程中给予用户反馈非常重要。 在正在进行的操作的开始点附近) 、嵌入的状态栏、模式对话框或 Visual Studio 状态栏中，可以就地显示进度指示器 (。 请按照有关其使用和实现的 [进度指示器](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators) 中的指导进行操作。

#### <a name="visual-studio-notifications-window"></a><a name="BKMK_VSNotificationsToolWindow"></a> Visual Studio 通知窗口
 Visual Studio "通知" 窗口通知开发人员有关许可、环境 (Visual Studio) 、扩展和更新的信息。 用户可以关闭单个通知，也可以选择忽略某些类型的通知。 已忽略通知的列表在 **工具 > 选项** 页中进行管理。

 "通知" 窗口当前不可扩展。

 ![Visual Studio“通知”窗口](../../extensibility/ux-guidelines/media/0901-06_vsnotificationswindow.png "0901-06_VSNotificationsWindow")

 **Visual Studio 通知工具窗口**

#### <a name="error-list"></a><a name="BKMK_ErrorList"></a> 错误列表
 "错误列表" 中的通知指示在编译和或生成过程中发生的错误和警告，并允许用户在代码中导航到特定代码错误。

 ![错误列表](../../extensibility/ux-guidelines/media/0901-08_errorlist.png "0901-08_ErrorList")

 **Visual Studio 中的错误列表**

#### <a name="embedded-status-bars"></a><a name="BKMK_EmbeddedStatusBars"></a> 嵌入式状态栏
 由于 IDE 状态栏是动态的，其 "客户端区域" 上下文设置为 "活动文档" 窗口，并且在用户的上下文和/或系统响应中进行更新，因此很难维护连续显示的信息，也不会提供长期异步处理的状态。 例如，对于多个运行和/或立即可操作的项选择，IDE 状态栏不适合测试运行结果的通知。 在用户进行选择或启动进程的文档或工具窗口的上下文中保留此类状态信息非常重要。

 ![嵌入式状态栏](../../extensibility/ux-guidelines/media/0901-09_embeddedstatusbar.png "0901-09_EmbeddedStatusBar")

 **Visual Studio 中的嵌入式状态栏**

#### <a name="windows-tray-notifications"></a><a name="BKMK_WindowsTray"></a> Windows 任务栏通知
 Windows 通知区域位于 Windows 任务栏上的系统时钟旁边。 许多实用工具和软件组件都提供此区域中的图标，以便用户可以为系统范围的任务（例如更改屏幕分辨率或获取软件更新）获取上下文菜单。

 环境级通知应显示在 Visual Studio 通知中心，而不是 Windows 通知区域。

#### <a name="notification-bubbles"></a><a name="BKMK_NotificationBubbles"></a> 通知气泡
 通知气泡可以在编辑器/设计器中显示为信息性，也可以作为 Windows 通知区域的一部分出现。 用户将这些气泡视为以后可以解决的问题，这是不重要通知的优点。 冒泡不适用于用户必须立即解决的重要信息。 如果确实要在 Visual Studio 中使用通知气泡，请遵循 [适用于通知气泡的 Windows 桌面指南](/windows/desktop/uxguide/mess-notif)。

 ![通知气泡](../../extensibility/ux-guidelines/media/0901-07_notificationbubbles.png "0901-07_NotificationBubbles")

 **用于 Visual Studio 的 Windows 通知区域中的通知冒泡**

## <a name="progress-indicators"></a><a name="BKMK_ProgressIndicators"></a> 进度指示器

### <a name="overview"></a>概述
 进度指示器是通知系统的重要组成部分，用于向用户提供反馈。 当进程和操作完成时，它们会告诉用户。 熟悉的指示器类型包括进度栏、旋转光标和动画图标。 进度指示器的类型和位置取决于上下文，包括所报告的内容以及完成操作所需的时间。

#### <a name="factors"></a>因素
 若要确定哪些指示器类型合适，需要确定下列因素。

1. **计时：** 操作需要的时间长度

2. **模态：** 操作是否对环境模式 (锁定 UI，直到完成此过程) 

3. **永久性/暂时性：** 是否需要报告和/或以后查看进度的最终结果

4. **确定性/不确定：** 是否可以计算操作结束时间和进度

5. **图形/文本位置：** 是以内联方式捕获进度或过程、在消息的正文中还是在特定控件（如树控件）中捕获。

6. **邻近性：** 进度是否应与相关联的 UI 接近。 例如， (可以位于状态栏中，它可能会远离远处，或者是否需要在启动过程的按钮附近？ ) 

#### <a name="determinate-progress"></a>确定性进度

|进度类型|何时以及如何使用|说明|
|-------------------|-------------------------|-----------|
|进度栏 (确定性) |预期持续时间为 >5 秒。<br /><br /> 可能包括进程详细信息的文本说明。|**不要** 将文本嵌入动画。|
|信息栏|与上下文 UI 关联的消息。 请参阅 [信息栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)。<br /><br /> 可能包括进程详细信息的文本说明。|如果需要指出多个进程，请 **不要** 使用多个信息栏。 请改用堆积进度栏。|
|输出窗口|暂时性通知：用户在完成后要 **查看** 其详细信息的应用程序级进程。|如果用户稍后需要引用数据，请 **不要** 使用。|
|日志文件|当完成后 **保存** 详细信息很重要时，与 intransient 通知配对。||
|状态栏|暂时性通知：用户在完成后 **不需要** 详细信息的应用程序级进程。<br /><br /> 包括嵌入的进度栏。<br /><br /> 可能包括进程详细信息的文本说明。||

#### <a name="indeterminate-progress"></a>不确定进度

|进度类型|何时以及如何使用|说明|
|-------------------|-------------------------|-----------|
|进度栏 (不确定) |预期持续时间为 >5 秒。<br /><br /> 可能包括进程详细信息的文本说明。|**不要** 将文本嵌入动画。|
|蚂蚁 (动态水平点) |到服务器的往返。<br /><br /> 放置在父容器顶部的上下文附近。|如果不是整个容器的父级，请 **不要** 使用。|
|微调 (进度环形) |与上下文 UI 相关联的进程，或者需要考虑空间的进程。<br /><br /> 可能包括进程详细信息的文本说明。||
|信息栏|与上下文 UI 关联的消息。 请参阅 [信息栏](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)。|如果需要指出多个进程，请 **不要** 使用多个信息栏。 请改为使用堆积进度条。|
|输出窗口|暂时性通知：用户将在完成后查看其 **详细信息** 的应用级进程。|**请勿用于** 需要跨会话保留的信息。|
|日志文件|与在完成后保存详细信息非常重要的情况下与 **不内向** 通知配对。||
|状态栏|暂时性通知：完成后用户 **不需要其详细信息** 的应用级进程。<br /><br /> 包括嵌入的进度栏。<br /><br /> 可能包括进程详细信息的文本说明。||

### <a name="progress-indicator-types"></a>进度指示器类型

#### <a name="progress-bars"></a>进度栏

##### <a name="indeterminate"></a>定
 ![不确定的进度栏](../../extensibility/ux-guidelines/media/0901-04_indeterminate.png "0901-04_Indeterminate")

 **不确定的进度栏**

 "不确定"表示无法确定操作或进程的总体进度。 对于需要无限时间或访问未知数量的对象的操作，请使用不确定的进度条。 使用文本说明来伴随发生的情况。 使用超时为基于时间的操作提供限制。 不确定的进度条使用动画来显示正在进行进度，但不提供其他信息。 不要仅根据可能缺少准确性的原因选择不确定的进度栏。

##### <a name="determinate"></a>确定
 ![确定进度栏](../../extensibility/ux-guidelines/media/0901-05_determinate.png "0901-05_Determinate")

 **确定进度栏**

 "确定"意味着操作或进程需要有限的时间，即使无法准确预测该时间量。 清楚地指示完成。 除非操作已完成，否则不要让进度栏达到 100%。 确定进度栏动画从左到右从 0 移动到 100%。

 在操作期间，切勿将进度指示器向后移动。 当操作开始时，条形应稳定向前移动，在结束时应达到 100%。 进度栏的要点是让用户了解整个操作需要的时间，而不考虑涉及多少个步骤。

##### <a name="concurrent-reporting-stacked-progress-bars"></a>并发报告 (堆积进度条) 
 如果操作需要很长时间（可能几分钟），则可能会使用两个进度条，一个显示操作的总体进度，另一个显示当前步骤的进度。 例如，如果安装程序正在复制多个文件，则一个进度栏可用于指示整个过程需要的时间，而第二个进度栏可以指示复制当前文件或目录的百分比。 请勿使用堆积进度条报告超过五个并发操作或进程。 如果要报告超过五个并发操作或进程，请使用包含"取消"按钮的模式对话框，并报告进度输出窗口。

##### <a name="textual-descriptions"></a>文本说明
 使用文本说明来伴随发生的情况和估计的完成时间。 如果无法确定操作需要多久，则提供反馈的更好选择可能是动画图标，而不是进度栏。

 Visual Studio状态栏中提供标准进度栏，任何集成到状态栏中的产品都可以Visual Studio。 有关对进度栏进行动画处理时发生的情况的文本说明，可以更新状态栏文本。

#### <a name="other-progress-indicators"></a>其他进度指示器

##### <a name="ants-animated-horizontal-dots"></a>Ants (动画水平点) 
 ![进度 ant](../../extensibility/ux-guidelines/media/0903-01_ants.png "0903-01_Ants")

 "Ants"（动画水平点）为不确定的往返服务器进程提供视觉参考。

##### <a name="spinner-progress-ring"></a>旋转 (进度环) 
 ![进度微调框](../../extensibility/ux-guidelines/media/0903-02_spinner.png "0903-02_Spinner")

 旋转 (也称为"进度环") 是一个不确定的进度指示器，主要用于上下文 UI。 在靠近其相关内容（如文本类别标头、消息传送或控件）的位置显示旋转图标。

##### <a name="cursor-feedback"></a>游标反馈
 对于需要 2-7 秒的操作，请提供游标反馈。 通常，这意味着使用操作系统提供的等待游标。 有关指导，请参阅 MSDN 文章 [Cursors.Wait 属性](/dotnet/api/system.windows.input.cursors.wait)。

#### <a name="progress-indicator-locations"></a>进度指示器位置

##### <a name="status-bar"></a>状态栏
 状态栏为应用程序提供了一个向用户显示消息和有用信息的位置，而不会中断用户的工作。 通常显示在窗口底部，进度状态将是一个工具提示窗格，其中包含有关进度度量值的消息以及进度栏指示器。

 ![具有进度栏的状态栏](../../extensibility/ux-guidelines/media/0903-03_statusbarprogressbar.png "0903-03_StatusBarProgressBar")

 **具有进度栏的状态栏**

 ![具有消息传递的状态栏](../../extensibility/ux-guidelines/media/0903-04_statusbarmessage.png "0903-04_StatusBarMessage")

 **包含文本说明的状态栏**

##### <a name="infobar"></a>信息栏
 与状态栏类似，信息栏提供上下文通知和消息传送，也可与不确定的进度指示器（如进度栏或旋转按钮）配对。 信息栏不应提供粒度级别进度或确定进度指示。 请参阅 [Infobars](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)。

 ![具有进度栏和消息传送的信息栏](../../extensibility/ux-guidelines/media/0903-05_infobar.png "0903-05_InfoBar")

 **包含进度栏和文本说明的信息栏**

 ![窗口中的信息栏](../../extensibility/ux-guidelines/media/0903-06_infobarinwindow.png "0903-06_InfoBarInWindow")

##### <a name="inline"></a>内联
 任何进度加载程序类型都可以表示内联进度指示。 通常，进度指示器与消息传送配对，但这不是一项要求。

 ![内联进度微调框](../../extensibility/ux-guidelines/media/0903-07_inlinespinner.png "0903-07_InlineSpinner")

 **将旋转器与文本说明结合使用**

 ![内联堆积进度栏](../../extensibility/ux-guidelines/media/0903-08_inlinestackedprogress.png "0903-08_InlineStackedProgress")

 **确定堆积进度条**

 ![内联进度消息传递](../../extensibility/ux-guidelines/media/0903-09_inlinetext.png "0903-09_InlineText")

 **服务器资源管理器内联文本：正在刷新...**

##### <a name="tool-windows"></a>工具窗口
 全局进度指示由位于工具栏正下方的不确定进度栏表示。

 ![全局不确定的进度栏](../../extensibility/ux-guidelines/media/0903-23_globalindeterminate.png "0903-23_GlobalIndeterminate")

 **团队资源管理器全局不确定进度栏**

##### <a name="dialogs"></a>对话框
 对话框可以包含任何进度加载程序类型。 进度指示器可以与消息传送配对，也可以与多个进度指示级别结合使用，以表示粒度和子进程。

 ![具有多个进度指示器类型的对话框](../../extensibility/ux-guidelines/media/0903-11_dialog.png "0903-11_Dialog")

 **Visual Studio并发进程和多个进度指示器类型的对话框**

 ![具有进度加载器和消息传递的对话框](../../extensibility/ux-guidelines/media/0903-12_dialog2.png "0903-12_Dialog2")

 **Visual Studio加载程序以及内联命令传送的对话框**

##### <a name="document-well"></a>文档井
 文档井可以与控件一起显示多个进度加载程序类型。

 ![文档井中的进度消息传递](../../extensibility/ux-guidelines/media/0903-13_documentwell.png "0903-13_DocumentWell")

 **工具栏下面的不确定进度栏**

##### <a name="output-window"></a>输出窗口
 "输出"窗口适用于通过内联文本消息传送处理进程进度和正在进行的进度状态。 应该将状态栏与任何"输出"窗口进度报告一起使用。

 ![输出窗口中的进度消息传递](../../extensibility/ux-guidelines/media/0903-14_outputwindow.png "0903-14_OutputWindow")

 **输出窗口进程状态和等待消息传送**

## <a name="infobars"></a><a name="BKMK_Infobars"></a> 信息栏

### <a name="overview"></a>概述
 信息栏为用户提供接近其焦点的指示器，使用共享信息栏控件可确保视觉外观和交互的一致性。

 ![Infobar](../../extensibility/ux-guidelines/media/0904-01_infobar.png "0904-01_Infobar")

 **信息栏中Visual Studio**

#### <a name="appropriate-uses-for-an-infobar"></a>信息栏的适当用法

- 为用户提供与当前上下文相关的非阻塞但重要的消息

- 指示 UI 的状态或条件具有一些交互影响，例如历史调试

- 通知用户系统检测到问题，例如当扩展导致性能问题时

- 为用户提供一种轻松采取措施的方法，例如当编辑器检测到文件包含混合制表符和空格时

##### <a name="do"></a>应做事项：

- 将 infobar 消息文本保持简短并指向点。

- 使链接和按钮上的文本保持简洁。

- 确保为用户提供的"操作"选项最少，只显示所需的操作。

##### <a name="dont"></a>不要：

- 使用信息栏提供应放置在工具栏中的标准命令。

- 使用信息栏来表示模式对话。

- 在窗口外部创建浮动消息。

- 在同一窗口中的多个位置使用多个信息栏。

#### <a name="can-multiple-infobars-show-at-the-same-time"></a>多个信息栏可以同时显示吗？
 是的，可以同时显示多个信息栏。 它们以先到先得的顺序显示，第一个信息栏显示在顶部，其他信息栏如下所示。

 用户一次最多看到三个信息栏，之后，如果更多信息栏可用，信息栏区域将变为可滚动。

### <a name="creating-an-infobar"></a>创建信息栏
 信息栏包含四个部分，从左到右：

- **图标：** 这是需要为信息栏显示的任何图标（如警告图标）的地方。

- **文本：** 如果需要，可以添加文本来描述用户的情况，以及文本中的链接。 请记得保持文本简洁。

- **操作：** 本部分应包含用户可在 infobar 中执行的操作的链接和按钮。

- **关闭按钮：** 右侧最后一部分可以有一个关闭按钮。

#### <a name="creating-a-standard-infobar-in-managed-code"></a>在托管代码中创建标准信息栏
 InfoBarModel 类可用于为 infobar 创建数据源。 使用以下四个构造函数之一：

```
public InfoBarModel(IEnumerable<IVsInfoBarTextSpan> textSpans, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);

```

```
public InfoBarModel(string text, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);

```

```
public InfoBarModel(IEnumerable<IVsInfoBarTextSpan> textSpans, IEnumerable<IVsInfoBarActionItem> actionItems, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);

```

```
public InfoBarModel(string text, IEnumerable<IVsInfoBarActionItem> actionItems, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);
```

 以下示例创建 InfoBarModel，其中某些文本包含超链接、操作按钮和图标。

 ![具有超链接的信息栏](../../extensibility/ux-guidelines/media/0904-02_infobarhyperlink.png "0904-02_InfobarHyperlink")

```
var infoBar = new InfoBarModel(
    textSpans: new[]
    {
        new InfoBarTextSpan("This is a "),
        new InfoBarHyperlink("hyperlink"),
        new InfoBarTextSpan(" InfoBar.")
    },
    actionItems: new[]
    {
        new InfoBarButton("Click Me")
    },
    image: KnownMonikers.StatusInformation,
    isCloseButtonVisible: true);

```

#### <a name="creating-a-standard-infobar-in-native-code"></a>在本机代码中创建标准信息栏
 实现 IVsInfoBar 接口，以便从本机代码提供信息栏。

```
public interface IVsInfoBar
{
    IVsInfoBarActionItemCollection ActionItems { get; }
    ImageMoniker Image { get; }
    bool IsCloseButtonVisible { get; }
    IVsInfoBarTextSpanCollection TextSpans { get; }
}

```

#### <a name="getting-an-infobar-uielement-from-an-infobar"></a>从信息栏获取信息栏 UIElement
 InfoBarModel 或 IVsInfoBar 实现是必须转换为 UIElement 才能在 UI 中显示的数据模型。 可以使用 SVsInfoBarUIFactory/IVsInfoBarUIFactory 服务检索 UIElement。

```
private bool TryCreateInfoBarUI(IVsInfoBar infoBar, out IVsInfoBarUIElement uiElement)
{
    IVsInfoBarUIFactory infoBarUIFactory = serviceProvider.GetService(typeof(SVsInfoBarUIFactory)) as IVsInfoBarUIFactory;
    if (infoBarUIFactory == null)
    {
        uiElement = null;
        return false;
    }

    uiElement = infoBarUIFactory.CreateInfoBar(infoBar);
    return uiElement != null;
}
```

### <a name="placement"></a>放置
 信息栏可以显示在以下一个或多个位置：

- 工具窗口

- 在文档选项卡中

> [!IMPORTANT]
> 可以定位信息栏，以发出有关全局上下文的消息。 这将显示在工具栏和文档之间。 不建议这样做，因为它会导致 IDE 的"跳转和跳跃"问题，除非绝对必要且适当，否则应避免这样做。

#### <a name="placing-an-infobar-in-a-toolwindowpane"></a>在 ToolWindowPane 中放置信息栏
 ToolWindowPane.AddInfoBar (IVsInfoBar) 方法可用于将信息栏添加到工具窗口。 此 API 可以添加 IVsInfoBar (InfoBarModel 是默认实现) 或 IVsUIElement。

#### <a name="placing-an-infobar-in-a-document-or-non-toolwindowpane"></a>将信息栏放置在文档或非 ToolWindowPane 中
 若要将信息栏放入任何 IVsWindowFrame，请使用 VSFPROPID_InfoBarHost 属性获取帧的 IVsInfoBarHost，然后添加信息栏 UIElement。

```
private void AddInfoBar(IVsWindowFrame frame, IVsUIElement uiElement)
{
    IVsInfoBarHost infoBarHost;
    if (TryGetInfoBarHost(frame, out infoBarHost))
    {
        infoBarHost.AddInfoBar(uiElement);
    }
}
private bool TryGetInfoBarHost(IVsWindowFrame frame, out IVsInfoBarHost infoBarHost)
{
    object infoBarHostObj;
    if (ErrorHandler.Failed(frame.GetProperty((int)__VSFPROPID7.VSFPROPID_InfoBarHost, out infoBarHostObj)))
    {
        infoBarHost = null;
        return false;
    }

    infoBarHost = infoBarHostObj as IVsInfoBarHost;
    return infoBarHost != null;
}

```

#### <a name="placing-an-infobar-in-the-main-window"></a>在主窗口中放置信息栏
 若要将信息栏放在主窗口中，请使用 IVsShell 服务的 VSSPROPID_MainWindowInfoBarHost 获取主窗口的 IVsInfoBarHost，然后将信息栏 UIElement 添加到其中。

### <a name="will-i-know-when-the-user-takes-action-in-my-infobar"></a>是否知道用户何时在我的信息栏中采取措施？
 是的，我们会将每个事件操作返回给 infobar 作者。 然后，由信息栏作者根据信息栏中的用户选择在 IDE 中采取措施。 信息栏将自动从单击了"关闭"按钮的主机中删除，但如果关闭后需要删除其他信息栏，则需要执行其他工作。 遥测还需要由每个信息栏独立记录。

#### <a name="receiving-infobar-events-in-a-toolwindowpane"></a>在 ToolWindowPane 中接收信息栏事件
 ToolWindowPane 有两个 infobar 事件。 当 ToolWindowPane 中的信息栏关闭时，将引发 InfoBarClosed 事件。 单击信息栏中的超链接或按钮时，将引发 InfoBarActionItemClicked 事件。

#### <a name="receiving-infobar-events-directly-from-the-uielement"></a>直接从 UIElement 接收 infobar 事件
 IVsInfoBarUIElement.Advise 可用于直接从信息栏的 UIElement 订阅事件。 实现 IVsInfoBarUIEvents 将允许作者接收关闭和单击事件。

```
public interface IVsInfoBarUIEvents
{
    void OnActionItemClicked(IVsInfoBarUIElement infoBarUIElement, IVsInfoBarActionItem actionItem);
    void OnClosed(IVsInfoBarUIElement infoBarUIElement);
}

```

## <a name="error-validation"></a><a name="BKMK_ErrorValidation"></a> 错误验证
 当用户输入不可接受的信息时（例如跳过必填字段或以错误格式输入数据时）时，最好在控件附近使用控制验证或反馈，而不是使用阻止弹出错误对话框。

### <a name="field-validation"></a>字段验证
 窗体和字段验证由三个组件组成：控件、图标和工具提示。 虽然多种类型的控件可以使用此功能，但文本框将用作示例。

 ![字段验证&#40;空白&#41;](../../extensibility/ux-guidelines/media/0905-01_fieldvalidation.png "0905-01_FieldValidation")

 如果需要该字段，应显示水印文本，并且字段背景应为浅黄色 **\<Required>** (VSColor：) ，并且前景应为灰色 (`Environment.ControlEditRequiredBackground` VSColor： `Environment.ControlEditRequiredHintText`) ：

 ![具有“必须”标签的字段验证](../../extensibility/ux-guidelines/media/0905-02_fieldvalidationrequired.png "0905-02_FieldValidationRequired")

 程序可以确定控件在焦点移到另一个控件或用户单击 [确定] 提交按钮或用户保存文档或窗体时，是否进入无效内容的状态。

 确定无效的内容状态后，控件内或控件旁边会显示一个图标。 在鼠标悬停在图标或控件上时，应会出现描述错误的工具提示。 此外，1 像素边框应出现在正在创建无效状态控件的周围。

 ![字段验证布局规范](../../extensibility/ux-guidelines/media/0905-03_layoutspecs.png "0905-03_LayoutSpecs")

 **字段验证的布局规范**

#### <a name="acceptable-variations-for-icon-location"></a>图标位置的可接受变体
 在数十个唯一情况下，需要通知用户验证错误。 考虑 UI 的控件类型和配置，选择适合你的情况的图标位置。

 ![图标位置的可接受位置](../../extensibility/ux-guidelines/media/0905-04_iconlocation.png "0905-04_IconLocation")

 **字段验证图标位置的可接受变体**

#### <a name="validation-requiring-a-round-trip-to-a-server-or-network-connection"></a>需要往返服务器或网络连接的验证
 在某些情况下，需要往返服务器来验证内容，并且必须显示用户进度、已验证状态和错误状态。 下图显示了这种情况的示例以及建议的 UI。

 ![涉及到服务器的往返行程的验证](../../extensibility/ux-guidelines/media/0905-05_roundtrip.png "0905-05_RoundTrip")

 **涉及到服务器的往返行程的验证**

 请注意，必须提供控件右侧足够的可用空间才能容纳"正在验证..."和"重试"文本。

#### <a name="in-place-warning-text"></a>就地警告文本
 当有空间将错误消息置于错误状态时，最好单独使用工具提示。

 ![在&#45;放置警告](../../extensibility/ux-guidelines/media/0905-06_inplacewarning.png "0905-06_InPlaceWarning")

 **就地警告文本**

#### <a name="watermarks"></a>水印
 有时，整个控件或窗口都为错误状态。 在这种情况下，请使用水印来指示错误。

 ![水印](../../extensibility/ux-guidelines/media/0905-07_watermark.png "0905-07_Watermark")

 **水印字段验证**
