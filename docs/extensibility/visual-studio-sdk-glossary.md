---
title: Visual Studio SDK 术语表|Microsoft Docs
description: 此术语表提供在 Visual Studio SDK 文档中使用的术语的定义。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- glossary [Visual Studio SDK]
ms.assetid: b64d432b-c39b-4904-ad18-3c3218b6e3aa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 78a66998e18ef68afe71e51f8d7ce99c7a75fc3a
ms.sourcegitcommit: 1c0eda2db1b1fff9595ca644503f467bf3e223e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/20/2022
ms.locfileid: "137094906"
---
# <a name="visual-studio-sdk-glossary"></a>Visual Studio SDK 术语表
此术语表提供文档中使用的术语 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] 的定义。

## <a name="terms"></a>术语

**Add-in — 外接程序**  
添加到主应用程序的实用工具应用程序、驱动程序或其他软件。 在 Visual Studio IDE (集成开发) 中，外接程序是基于自动化的应用程序，可扩展 IDE 的功能。

**自动化模型**  
自动化模型（在早期版本的 Visual Studio称为扩展性模型）是一个编程接口，可让你访问驱动 IDE 的基础例程。 外接程序、向导和宏使用自动化模型中的对象来控制或扩展 IDE 的功能。

**命令 UI 上下文**  
GUID 与 UI 命令或元素（如工具栏）的可见性的关联。 命令 UI 上下文与选择上下文不同，因为它未附加到窗口。

命令 UI 上下文可用于：
- 将 GUID 分配给激活特定窗口时显示的工具栏。
- 将 GUID 分配给命令的可用性，而无需加载或运行 VSPackage。
- 分配 GUID 以影响活动键绑定。
- 分配 GUID 以打开宏录制。
- 分配 GUID 以激活调试模式或在编辑器中的设计模式和运行模式之间进行切换。

**component**  
一段软件，可成为应用程序功能的一部分，无需该应用程序具有有关软件实现的任何预先存在的信息。 组件与应用程序之间的通信仅通过 OLE 样式接口进行。

**组件管理器**  
一项 `SOleComponentManager` 服务，它为顶级组件提供非用户界面协调服务。 `SOleComponentManager`服务实现 `IOleComponentManager` 接口。

**组件 UI 管理器**  
一个服务 `SOleComponentUIManager` ，它提供用户界面协调服务。 `SOleComponentUIManager`服务实现 和 `IOleComponentUIManager` `IOleInPlaceComponentUIManager` 接口。

**上下文包**  
附加到 `IVsUserContext` (组件的 COM) 对象的对象。 此对象保存查找关键字 **、F1** 关键字和与组件相关的属性。 上下文包还指向链接到它们的任何子文本包。

**上下文提供程序**  
IDE 中具有与之关联的上下文包的组件。 此类组件包括工具窗口、编辑器或项目层次结构。

**设计师**  
一个编程接口，允许用户操作 UI 元素 (窗体、按钮和其他控件) 。

**DocData**  
在存在文档/视图分隔的情况下封装文档基础数据的 COM 对象 (例如，在文本编辑器中，这是所有文本编辑器视图的基础文本缓冲区) 。 如果 EditorFactory 不提供此对象，则 IDE 将代表它制造一个。 此对象的职责是管理数据持久性以及针对同一 上的多个视图的共享语义 `DocData` 。 如果 `DocData` 对象支持 `IOleCommandTarget` 接口，它将包含在 UIShell 的命令路由中。

**DocObject**  
用于在主机提供的帧内托管 UI 的技术。 更具体地说，此术语是指支持 和相关接口 `IOleDocument` 的任何嵌入。 此技术具有许多潜在应用程序，例如 COM 文档的实现详细信息、Visual Basic 5.0 中的工具窗口、Visual Basic 6.0 中的 ActiveX 设计器等。

**document**  
用于以一般方式将文档作为一个整体引用 - 和 `DocData` `DocView` 。 例如，DocumentFrame 包含 ，但它还保留对 的引用 `DocView` `DocData` 以处理持久性。

**DocView**  
用户与之交互以查看和操作基础 的 DocObject/嵌入/WindowPane。 `DocData` 用户不会利用作为界面设计的一部分的文档/视图 `DocObject` 分隔。 用户使用整个 DocObject 作为视图，而不是使用更抽象 (不太正式) 称为 的基础数据的概念 `DocData` 。 `DocView` 对象始终嵌入在 IDE 的 MDI (窗口) 文档框架对象。

**DTE**  
 (开发工具扩展性) 对象是 Visual Studio 自动化模型中最顶层的访问点，可用于以编程方式自动执行和扩展 `DTE` IDE。

**“动态帮助”窗口**  
由 IDE 实现的工具窗口，显示查找关键字或 **F1 帮助主题** 的列表。

**编辑 器**  
代码 (类，CLSID) 实现 `DocView` 。 如果支持 `DocData` 视图和数据分离，则它还实现 。

**extension**  
修改、自定义或添加到 IDE 的功能。 使用自动化模型或 VSPackage 创建扩展。

**外部编辑器**  
不特定于 IDE 的编辑器，例如Microsoft Word。 它已通过其自己的机制注册，可在 IDE 外部使用。 如果可以嵌入此编辑器，则它将显示在 IDE 中的窗口中。 如果无法嵌入，将创建一个单独的顶级窗口。

**层次结构**  
节点树，每个与一组属性关联的节点。

**独立顶级组件**  
一个组件，它使用无模式顶级窗口，并且可以有效地作为独立应用程序窗口运行，但作为进程内对象实现。 因此，独立的顶级组件必须与 IDE 协调形式和消息循环服务。 进程内对象没有其自己的消息循环。

**信息提供程序**  
信息提供程序是一个模块，可以查找关键字并返回对象形式的主题 `IVsUserContextItem` 列表。 若要为信息提供程序提供 **F1** 和 lookup 关键字项，请在 中注册已编译的帮助 *(。HxS*) 与系统一起运行。 这些文件中的帮助主题提供动态帮助窗口中显示的主题列表，并显示用户是否按 **F1**。

**就地组件**  
一个 VSPackage 对象，该对象实现 接口以管理一个窗口，该窗口以可视方式包含在 `IOleInPlaceComponent` IDE 拥有的文档窗口中。 就地组件不参与标准 OLE 菜单合并;而是将其用户界面元素集成到 IDE 中。

有两种类型的就地组件：硬连接就地组件和组件控件。

硬连接就地组件具有菜单、工具栏和命令，这些菜单、工具栏和命令紧密集成到 IDE 的用户界面中，就像它们直接内置到 IDE 中一样。

组件控件没有任何其自己的用户界面元素集成到 IDE 中;而是使用 IDE 的菜单、命令和工具栏。 例如，Bold 命令可用于在窗体中嵌入的富文本控件中将所选单词加粗。 但是，组件控件可以请求显示动态安装的特定于组件的 UI 元素。

**语言服务**  
一组 对象，允许 VSPackage 开发人员实现计算机语言代码编辑器的功能，例如文本标记和着色。

**杂项文件项目**  
Project用于存储未在任何项目中打开的文件。 此项目中的项列表不会持久保存。

**project**  
项目由层次结构对象或实现 接口的 COM `IVsHierarchy` 对象共同完成。

**特定于项目的设计器或编辑器**  
不能独立于项目类型使用的设计器。 所有特定于项目的设计器都必须在注册表中输入其编辑器工厂信息。 然后，每当特定项目中打开特定文件类型时，IDE 都可以实例化设计器。

**project-type 窗口**  
一个窗口，该窗口持续跟踪全局选择上下文中当前活动的项目层次结构和项。 Project类型的窗口使用 服务来提醒 `SVsTrackSelectionEx` IDE 更改，以及向用户显示反馈。 解决方案资源管理器是项目类型窗口的示例。

**属性窗口**  
以前为属性浏览器。

**基于引用的项目**  
Project不需要项目的文件在同一目录中。 相反，对来自其他不相关目录的文件的引用由项目本身存储和维护。

**运行文档表**  
内部结构，IDE 通过该结构维护所有当前打开的文档的列表。 该列表包括内存中所有打开的文档，而不考虑当前是否正在编辑文档。 文档是保存的任何项，包括在编辑器中打开存储过程、项目中的文件或主项目文件 (例如 *.vcproj 文件) 。

**选择上下文**  
数据是 IDE 中每个窗口详细信息的一部分，用于跟踪活动选择。 选择上下文包括：

- 指向 `IVsHierarchy` 项目层次结构的接口的指针
- 项目项的项标识符。
- 指向接口 `ISelectionContainer` 的指针，该接口提供对活动对象属性的访问。
- 元素值的数组。

**服务**  
驻留在单个 COM 对象中的一组 COM 接口的协定。 创建由 GUID 标识的服务时，可定义执行该服务的 COM 接口集。 COM 对象使用服务相互通信。

**解决方案**  
用户使用的相关项目组。

**标准设计器**  
一个可以独立于项目类型使用的设计器。 所有标准设计器都必须在注册表中输入其编辑器工厂信息。 然后，只要打开具有特定扩展名的文件，IDE 就可以实例化设计器。 数据必须持久保留到文件中。

**标准编辑器**  
可以独立于任何特定项目类型使用的编辑器。 此类编辑器在注册表中注册了 EditorFactories。 这允许 IDE 查找并调用编辑器。

**标准 OS 编辑器**  
不特定于Visual Studio嵌入。 它使用已知的 Win32 密钥注册 (例如，Win32 资源管理器知道如何调用) 。 如果可以嵌入此类编辑器，编辑器仍显示在 IDE 中的位置。 否则，会为此类编辑器创建单独的顶级窗口。

**subcontext 包**  
链接到 `IVsUserContext` 上下文包的对象。 对象保存查找关键字 **、F1** 关键字和 IDE 组件中所选内容的属性。 子文本的示例包括工具窗口中的命令或编辑器中的关键字。

**任务列表**  
由 IDE 实现并显示活动任务列表的工具窗口。

**文本缓冲区**  
对象的公用名 `VSTextBuffer` 。

**文本视图**  
对象的公用名 `VSTextView` 。

**工具顶级组件**  
作为无模式弹出窗口运行的组件，与 IDE 的用户界面紧密协调。 与独立的顶级组件一样，工具顶级组件还必须与 IDE 协调形式和消息循环服务。

**顶级组件**  
VSPackage 对象，用于管理无模式顶级窗口，而不是 IDE 窗口的工作区。 顶级组件实现 `IOleComponent` 接口以利用消息循环服务，例如对空闲时间的访问。

**UI 活动**  
可见且当前具有焦点的 VSPackage 对象。

**UI 层次结构**  
实现 接口以允许显示层次结构的 COM `IVsUIHierarchy` 对象。 UI 层次结构窗口实现 接口以更新 `ISelectionContainer` 属性窗口;其他项目类型窗口可使用此实现（如果需要）。

**VSCT**  
Visual Studio命令表。 .vsct 文件包含有关 XML 格式的菜单、工具栏和命令的位置和行为的信息。

**VSPackage**  
一个可安装的软件，Visual Studio以下一项或多个项扩展 IDE：用户界面、服务、项目类型或编辑器/设计器。 VSPackage 由实现 接口的 COM 对象以及一个或多个其他 COM 对象组成，这些 COM 对象实现其他接口以支持 `IVsPackage` 选择和其他功能。 此外，VSPackage 具有特定的注册要求。
