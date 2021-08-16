---
title: 调试 Azure 云服务或虚拟机
description: 在 Visual Studio 中调试云服务或虚拟机
author: mikejo5000
manager: jmartens
ms.topic: how-to
ms.workload: azure-vs
ms.date: 11/11/2016
ms.author: mikejo
ms.technology: vs-ide-debug
ms.openlocfilehash: aeaa6bf6230833a350fb2fe8d55178d6c838a5f1d014a5dcdbe959daf6d01838
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121364036"
---
# <a name="debugging-an-azure-cloud-service-or-virtual-machine-in-visual-studio"></a>在 Visual Studio 中调试云服务或虚拟机

Visual Studio 提供了不同的选项来调试 Azure 云服务和虚拟机。

## <a name="debug-your-cloud-service-on-your-local-computer"></a>在本地计算机上调试云服务

可以通过在本地计算机上使用 Azure 计算 Emulator调试云服务来节省时间和资金。 部署某个服务之前在本地对其进行调试可以提高可靠性和性能，且不会产生计算时间的相关费用。 但是，仅在 Azure 自身中运行云服务时，某些错误才可能会出现。 如果在发布服务时启用远程调试，然后将调试器附加到角色实例，则可以调试这些错误。

该模拟器模拟 Azure 计算服务并在本地环境中运行，使你可以在部署云服务之前对其进行测试和调试。 该模拟器将处理角色实例的生命周期，并提供对所模拟资源（如本地存储）的访问。 从 Visual Studio 调试或运行服务时，Visual Studio 会自动将模拟器作为后台应用程序启动，然后将服务部署到模拟器。 当模拟器在本地环境中运行时，可以使用它来查看服务。 可以运行完整版或速成版的模拟器。  (Azure 2.3 开始，模拟器的 express 版本为默认值。) 请参阅使用[Emulator Express](vs-azure-tools-emulator-express-debug-run.md)在本地运行和调试云服务。

### <a name="to-debug-your-cloud-service-on-your-local-computer"></a>在本地计算机上调试云服务

1. 在菜单栏上，选择 **"调试**  >  **""开始调试**"以运行 Azure 云服务项目。 或者，可以按 F5。 会看到一条消息，计算模拟器正在启动。 当该模拟器启动时，系统托盘图标会对其进行确认。

    ![系统托盘中的 Azure 模拟器](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC783828.png)

2. 打开通知区域中的 Azure 图标快捷菜单，并选择“显示计算模拟器 UI”，从而显示计算模拟器的用户界面。

    UI 的左窗格显示了当前部署到计算模拟器的服务以及每项服务正在运行的角色实例。 可选择服务或角色，以便在右窗格中显示生命周期、日志记录和诊断信息。 如果将焦点置于包括窗口的上边距中，则该窗口将展开以填写右侧窗格。

3. 在"调试"菜单上选择命令，在代码中设置断点，逐步执行应用程序。 在调试器中单步执行应用程序时，窗格会随着应用程序的当前状态而更新。 当停止调试时，将删除应用程序部署。 如果应用程序包含 Web 角色，并且已将启动操作属性设置为启动 Web 浏览器，Visual Studio 会在浏览器中启动 Web 应用程序。 如果更改服务配置中某个角色的实例数，则必须停止云服务，然后重新启动调试，以便可以调试该角色的这些新实例。

    > [!NOTE]
    > 停止运行或调试服务时，不会停止本地计算模拟器和存储模拟器。 必须从通知区域显式将其停止。

## <a name="debug-a-cloud-service-in-azure"></a>在 Azure 中调试云服务

若要从远程计算机调试云服务，必须在部署云服务时显式启用该功能，以便在运行角色实例的虚拟机上安装所需的服务（例如 msvsmon.exe）。 如果在发布服务时未启用远程调试，则必须在启用远程调试的情况下重新发布该服务。

为云服务启用远程调试不会导致性能下降或费用增加。 请勿在生产服务上使用远程调试，因为使用该服务的客户端可能会受到不利影响。

> [!NOTE]
> 当从 Visual Studio 中发布云服务时，可以为该服务中所有以 .NET Framework 4 或 .NET Framework 4.5 为目标的角色启用 **IntelliTrace**。 使用 **IntelliTrace** 可以检查过去发生在某个角色实例中的事件，并重现当时的上下文。 请参阅[使用 IntelliTrace 和 Visual Studio 调试已发布的云服务](vs-azure-tools-IntelliTrace-debug-published-cloud-services.md)和[使用 IntelliTrace 进行调试](../debugger/intellitrace.md)。

### <a name="to-enable-remote-debugging-for-a-cloud-service"></a>为云服务启用远程调试

1. 打开 Azure 项目的快捷菜单，并选择“发布”。

2. 选择“过渡”环境和“调试”配置。

    这些内容仅供指导。 可以选择在生产环境中运行测试环境。 但是，如果在生产环境中启用远程调试，则可能会对用户造成不利影响。 可以选择“发布”配置，但是，“调试”配置能使调试变得更轻松。

    ![选择调试配置](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746717.gif)

3. 请按照一般步骤进行操作，但在“高级设置”选项卡上选中“为所有角色启用远程调试器”复选框。

    ![调试配置](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746718.gif)

### <a name="to-attach-the-debugger-to-a-cloud-service-in-azure"></a>将调试器附加到 Azure 中的云服务

1. 在“服务器资源管理器”中，展开云服务的节点。

2. 打开要附加的角色或角色实例的快捷菜单，并选择“附加调试器”。

    如果要调试某个角色，Visual Studio 调试器将附加到该角色的每个实例中。 对于运行某个断点所在的代码行并符合该断点的所有条件的第一个角色实例，调试器会在该断点位置中断。 如果调试某个实例，调试器将只附加到该实例，并且仅当该特定实例运行某个断点所在的代码行并符合该断点的条件时，调试器才在该断点位置中断。

    ![附加调试器](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746719.gif)

3. 将调试器附加到实例后，像往常一样进行调试。 调试器会自动附加到角色的相应主机进程。 根据具体的角色，调试器将附加到 w3wp.exe、WaWorkerHost.exe 或 WaIISHost.exe。 若要确认调试器附加到的进程，请展开“服务器资源管理器”中的实例节点。 有关 Azure 进程的详细信息，请参阅 [Azure 角色体系结构](/archive/blogs/kwill/windows-azure-role-architecture)。

    ![选择代码类型对话框](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)

4. 若要标识调试器附加到的进程，请在菜单栏上选择"调试Windows进程  >    >  **"，** 然后打开"进程 **"** 对话框。 （键盘操作：Ctrl+Alt+Z）要分离特定的进程，请打开其快捷菜单，然后选择“分离进程”。 或者，在“服务器资源管理器”中找到实例节点，找到该进程，打开其快捷菜单，并选择“分离进程”。

    ![调试进程](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC690787.gif)

> [!WARNING]
> 远程调试时避免长时间停止在断点处。 Azure 会将停止时间超过数分钟的进程视为无响应，并停止向相应的实例发送流量。 如果停止时间太长，msvsmon.exe 将与进程分离。

要将调试器与实例或角色中的所有进程分离，请打开要调试的角色或实例的快捷菜单，然后选择“分离调试器”。

## <a name="limitations-of-remote-debugging-in-azure"></a>在 Azure 中进行远程调试的限制

从 Azure SDK 2.3 开始，远程调试存在以下限制：

* 启用远程调试后，无法发布其中的任一角色包含 25 个以上实例的云服务。
* 调试器使用端口 30400 至 30424、端口 31400 至 31424 以及端口 32400 至 32424。 如果尝试使用其中的任一端口，将无法发布服务，并且 Azure 的活动日志中会显示以下错误消息之一：

  * 根据 .csdef 文件验证 .cscfg 文件时出错。
    角色 “role” 的终结点 Microsoft.WindowsAzure.Plugins.RemoteDebugger.Connector 的保留端口范围 “range” 与已定义的端口或范围重叠。
  * 分配失败。 请稍后重试，尝试减少 VM 大小或角色实例数目，或者尝试部署到其他区域。

## <a name="debugging-azure-virtual-machines"></a>调试 Azure 虚拟机

可以在 Visual Studio 中使用“服务器资源管理器”调试 Azure 虚拟机上运行的程序。 在 Azure 虚拟机上启用远程调试时，Azure 会在该虚拟机上安装远程调试扩展。 然后，你可以附加到虚拟机上的进程中，并像平时一样进行调试。

> [!NOTE]
> 可使用 Visual Studio 2015 中的“云 Resource Manager ”对通过 Azure Resource Manager 堆栈创建的虚拟机进行远程调试。 有关详细信息，请参阅[使用云资源管理器管理 Azure 资源](vs-azure-tools-resources-managing-with-cloud-explorer.md)。

### <a name="to-debug-an-azure-virtual-machine"></a>调试 Azure 虚拟机

1. 在“服务器资源管理器”中，展开“虚拟机”节点并选择要调试的虚拟机的节点。

2. 打开上下文菜单，并选择“启用调试”。 当系统询问是否确定要在虚拟机上启用调试时，请选择“是”。

    Azure 会在该虚拟机上安装远程调试扩展以启用调试。

    ![虚拟机启用调试命令](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Azure 活动日志](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)

3. 远程调试扩展安装完毕后，打开虚拟机的上下文菜单，并选择“附加调试器...”

    Azure 将获取虚拟机上的进程的列表，并在 **“附加到进程”** 对话框中显示这些进程。

    ![附加调试器命令](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)

4. 在“附加到进程”对话框中，选择“选择”以将结果列表限制为仅显示要调试的代码类型。 可以调试 32 位或 64 位托管代码和/或本机代码。

    ![选择代码类型对话框](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)

5. 选择要在虚拟机上调试的进程，然后选择"附加 **"。** 例如，如果要调试虚拟机上的某个 Web 应用，则可以选择 w3wp.exe 进程。 有关详细信息，请参阅[在 Visual Studio 中调试一个或多个进程](../debugger/debug-multiple-processes.md)和 [Azure 角色体系结构](/archive/blogs/kwill/windows-azure-role-architecture)。

## <a name="create-a-web-project-and-a-virtual-machine-for-debugging"></a>创建用于调试的 Web 项目和虚拟机

在发布 Azure 项目之前，你可能会发现，在支持调试和测试方案并且可以在其中安装测试和监视程序的受控环境中对项目进行测试会很有用。 运行这类测试的方法之一是远程调试虚拟机上的应用。

Visual Studio ASP.NET 项目提供了一个选项，可创建用于应用程序测试且易于操作的虚拟机。 该虚拟机包含通常需要的终结点，例如 PowerShell、远程桌面和 WebDeploy。

### <a name="to-create-a-web-project-and-a-virtual-machine-for-debugging"></a>创建用于调试的 Web 项目和虚拟机

1. 在 Visual Studio 中创建一个新的 ASP.NET Web 应用程序。

2. 在 "新建 ASP.NET Project" 对话框中的 "Azure" 部分，在下拉列表框中选择 "**虚拟机**"。 保留 **“创建远程资源”** 复选框的选中状态。 选择“确定”以继续。

    此时将出现 **“在 Azure 上创建虚拟机”** 对话框。

    ![“创建 ASP.NET Web 项目”对话框](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746723.png)

    > [!NOTE]
    > 如果尚未登录到 Azure 帐户，系统将要求登录。

3. 选择虚拟机的各种设置，然后选择 **"确定"**。 有关详细信息，请参阅[虚拟机](/azure/virtual-machines/)。

    为 DNS 名称输入的名称也就是虚拟机的名称。

    ![在 Azure 对话框上创建虚拟机](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746724.png)

    Azure 会创建虚拟机，然后设置和配置终结点，例如远程桌面和 Web 部署。

4. 完全配置好虚拟机后，请在“服务器资源管理器”中选择该虚拟机的节点。

5. 打开上下文菜单，并选择“启用调试”。 当系统询问是否确定要在虚拟机上启用调试时，请选择“是”。

    Azure 会在该虚拟机上安装远程调试扩展以启用调试。

    ![虚拟机启用调试命令](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Azure 活动日志](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)

6. 根据[如何：在 Visual Studio 中使用一键式发布来部署 Web 项目](/previous-versions/aspnet/dd465337(v=vs.110))中所述的方法发布项目。 由于你想要在虚拟机上进行调试，因此，请在 **“发布 Web”** 向导的 **“设置”** 页上选择 **“调试”** 作为配置。 这可以确保在调试时代码符号可用。

    ![发布设置](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718349.png)

7. 如果以前已经部署了该项目，请在 **“文件发布选项”** 中，选择 **“删除目标位置的其他文件”**。

8. 发布项目之后，在服务器资源管理器中该虚拟机的上下文菜单上，选择“附加调试器...”

    Azure 将获取虚拟机上的进程的列表，并在 **“附加到进程”** 对话框中显示这些进程。

    ![附加调试器命令](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)

9. 在“附加到进程”对话框中，选择“选择”以将结果列表限制为仅显示要调试的代码类型。 可以调试 32 位或 64 位托管代码和/或本机代码。

    ![选择代码类型对话框](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)

10. 选择要在虚拟机上调试的进程，然后选择 " **附加**"。 例如，如果要调试虚拟机上的某个 Web 应用，则可以选择 w3wp.exe 进程。 有关详细信息，请参阅[在 Visual Studio 中调试一个或多个进程](../debugger/debug-multiple-processes.md)。

## <a name="next-steps"></a>后续步骤

* 使用 **IntelliTrace** 从发布服务器中收集调用和事件的日志。 请参阅[使用 IntelliTrace 和 Visual Studio 调试已发布的云服务](vs-azure-tools-IntelliTrace-debug-published-cloud-services.md)。

* 使用“Azure 诊断”以记录在角色内运行的代码的详细信息，角色是否在开发环境或 Azure 中运行。 请参阅[使用 Azure 诊断收集日志记录数据](/azure/cloud-services/cloud-services-dotnet-diagnostics)。
