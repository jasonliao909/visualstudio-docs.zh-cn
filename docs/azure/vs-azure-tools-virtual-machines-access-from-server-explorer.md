---
title: 从服务器资源管理器访问 Azure 虚拟机 | Microsoft Docs
description: 概述如何在 Visual Studio 的服务器资源管理器中查看、创建和管理 Azure 虚拟机 (VM)。
author: ghogen
manager: jmartens
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 8/31/2017
ms.author: ghogen
ms.openlocfilehash: ab67a81d761f2e17c82b75fb59a201188cf80986
ms.sourcegitcommit: b770b99034e65c91b29bea87bc6f5fa02348515b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2021
ms.locfileid: "112997626"
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>从服务器资源管理器访问 Azure 虚拟机

::: moniker range=">=vs-2022"
> [!Important]
> 服务器资源管理器 2022 年 1 月Visual Studio Azure 节点。 可以使用 Azure 门户或继续使用早期版本的 azure 门户服务器资源管理器 Azure Visual Studio。
>
> 此外 [，Microsoft Azure 存储资源管理器](/azure/vs-azure-tools-storage-manage-with-storage-explorer) 是 Microsoft 提供的免费独立应用。 可以通过它在 Windows、macOS 和 Linux 上直观地使用 Azure 存储数据。
>
> 有关 2022 Visual Studio，请参阅 [发行说明](/visualstudio/releases/2022/release-notes-preview/)。

::: moniker-end

::: moniker range="<=vs-2017"

如果有 Azure 托管的虚拟机，可以在服务器资源管理器中访问它们。 必须首先登录到 Azure 订阅才能查看移动服务。 若要登录，请在服务器资源管理器中打开“Azure”节点的快捷菜单，并选择“连接到 Microsoft Azure”。

1. 在 Cloud Explorer 中选择虚拟机，并选择 F4 键显示其属性窗口。

    下表显示了可用的属性，但这些属性都是只读的。 若要更改这些属性，请使用 [Azure 门户](https://portal.azure.com)。

   | 属性 | 说明 |
   | --- | --- |
   | DNS 名称 |包含虚拟机 Internet 地址的 URL。 |
   | 环境 |对于虚拟机，此属性的值始终为“生产”。 |
   | 名称 |虚拟机的名称。 |
   | 大小 |虚拟机的大小，此值反映可用的内存和磁盘空间量。 有关详细信息，请参阅 [虚拟机大小](/azure/cloud-services/cloud-services-sizes-specs)。 |
   | 状态 |值包括“正在启动”、“已启动”、“正在停止”、“已停止”和“正在检索状态”。 如果出现“正在检索状态”，则表示当前状态未知。 此属性的值不同于 [Azure 门户](https://portal.azure.com)上使用的值。 |
   | 订阅 ID |Azure 帐户的订阅 ID。 可以通过在 [Azure 门户](https://portal.azure.com)上查看订阅的属性来显示此信息。 |
2. 选择一个终结点节点，然后查看 **“属性”** 窗口。
3. 下表描述了可用的终结点属性，但这些属性都是只读的。 若要添加或编辑虚拟机的终结点，请使用 [Azure 门户](https://portal.azure.com)。

   | 属性 | 说明 |
   | --- | --- |
   | 名称 |终结点的标识符。 |
   | 专用端口 |应用程序的内部网络访问端口。 |
   | 协议 |此终结点的传输层使用的协议：TCP 或 UDP。 |
   | 公用端口 |用于公开访问应用程序的端口。 |

::: moniker-end