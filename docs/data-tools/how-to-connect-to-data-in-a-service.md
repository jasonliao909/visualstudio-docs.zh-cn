---
title: 如何：连接 WCF 服务中的数据
description: 通过运行 "数据源配置向导" 并在 "选择数据源类型" 页上选择 "服务"，将应用程序连接 Windows Communication Foundation 从 (WCF) 服务返回的数据。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data [Visual Studio], connecting to web services
- data sources, creating from web services
- data [Visual Studio], reading from web services
- reading data, from web services
- web services, reading data
- web services, as data sources
- web services, connecting
ms.assetid: a6b54353-05fe-4e5c-8631-90231fc95504
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 6a480224e8e27c8997f98bbb434a7ce404e6bb5a
ms.sourcegitcommit: 1ed233bb3afc5ae1f52aff8e41f7e650342033ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2022
ms.locfileid: "141275182"
---
# <a name="how-to-connect-to-data-in-a-wcf-service"></a>如何：连接 WCF 服务中的数据

通过运行 "[数据源配置向导](../data-tools/media/data-source-configuration-wizard.png)" 并在 "**选择数据源类型**" 页上选择 "**服务**"，将 .NET Framework 应用程序连接到 Windows Communication Foundation (WCF) 服务返回的数据。

完成向导后，服务引用将添加到项目，并立即出现在[“数据源”窗口](add-new-data-sources.md#data-sources-window)中。

> [!NOTE]
> “数据源”窗口中显示的项取决于该服务返回的信息。 某些服务可能没有为“数据源配置”向导创建可绑定的对象提供足够的信息。 例如，如果该服务返回一个非类型化数据集，则在完成该向导时“数据源”窗口中不会显示任何项。 这是因为非类型化数据集不提供架构，因此向导没有足够的信息来创建数据源。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="prerequisites"></a>先决条件

WCF 工具不随 .NET 工作负荷一起安装;使用 Visual Studio 安装程序修改安装。 在安装程序中，选择 "单个组件" 下的 **Windows Communication Foundation** 。 请参阅[修改 Visual Studio](../install/modify-visual-studio.md)。

## <a name="to-connect-your-application-to-a-service"></a>将应用程序连接到服务

1. 在 **“数据”** 菜单上，单击 **“添加新数据源”**。

2. 在“选择数据源类型”页上选择“服务”，然后单击“下一步”  。

3. 输入要使用的服务的地址，或单击“发现”在当前解决方案中查找服务，然后单击“转到” 。

4. 可以选择键入新的命名空间来代替默认值。

    > [!NOTE]
    > 单击“高级”以打开[“配置服务引用”对话框](../data-tools/configure-service-reference-dialog-box.md)。

5. 单击“确定”以向项目添加服务引用。

6. 单击“完成”  。

     数据源随即添加到“数据源”窗口中。

## <a name="next-steps"></a>后续步骤

若要向应用程序添加功能，可以在“数据源”窗口选择一个项，然后将其拖动到窗体中来创建绑定控件。 有关详细信息，请参阅[将控件绑定到 Visual Studio 中的数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。

## <a name="see-also"></a>另请参阅

- [将 WPF 控件绑定到 WCF 数据服务](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)
- [Visual Studio 中的 Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
