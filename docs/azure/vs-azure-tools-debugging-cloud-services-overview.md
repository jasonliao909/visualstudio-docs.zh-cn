---
title: 调试 Azure 云服务的选项 | Microsoft Docs
description: 调试 Azure 云服务
author: mikejo5000
manager: jmartens
ms.topic: conceptual
ms.workload: azure-vs
ms.date: 03/18/2017
ms.author: mikejo
ms.technology: vs-ide-debug
ms.openlocfilehash: 417718e519686039ef7f027a4e2d76e7a74065dc2d177236dc2a9a74ecf191cc
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121363929"
---
# <a name="learn-the-various-ways-to-debug-an-azure-cloud-service"></a>了解调试 Azure 云服务的各种方法
本文提供了调试 Azure 云服务的各种方法的链接。

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>在 Visual Studio 中调试 Azure 云服务
可以使用 Azure 计算 Emulator 在本地计算机上调试云服务，从而节省时间和金钱。 部署某个服务之前在本地对其进行调试可以提高可靠性和性能，且不会产生计算时间的相关费用。 但是，仅在 Azure 中运行云服务时，某些错误才可能会出现。 仅在 Azure 中运行云服务时才会发生的错误可以通过在发布服务时启用远程调试，然后将调试器附加到角色实例来进行调试。 有关详细信息，请参阅 [Debug your cloud service on your local computer](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer)（在本地计算机上调试云服务）。

## <a name="using-intellitrace"></a>使用 IntelliTrace
如果使用 Visual Studio Enterprise 来编写以 .NET Framework 4.5 为目标的角色，从 Visual Studio 部署 Azure 云服务时，可以启用 IntelliTrace。 IntelliTrace 提供一个日志，可将该日志与 Visual Studio 一起使用以调试应用程序，就如同应用程序在 Azure 中运行一样。 有关详细信息，请参阅 [Debugging a published cloud service with IntelliTrace and Visual Studio](vs-azure-tools-intellitrace-debug-published-cloud-services.md)（使用 IntelliTrace 和 Visual Studio 调试已发布的云服务）。

## <a name="remote-debugging"></a>远程调试
从 Visual Studio 部署云服务时，可以在云服务上启用远程调试。 如果选择为部署的项目启用远程调试，会在运行每个角色实例的虚拟机上安装远程调试服务。 这些服务（如 `msvsmon.exe`）不影响性能，也不额外收费。 有关详细信息，请参阅 [Debug a cloud service in Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure)（调试 Azure 中的云服务）。

## <a name="next-steps"></a>后续步骤
- [在 Visual Studio 中调试 Azure 云服务或 VM](./vs-azure-tools-debug-cloud-services-virtual-machines.md) - 了解如何调试 Azure 云服务的详细信息。
