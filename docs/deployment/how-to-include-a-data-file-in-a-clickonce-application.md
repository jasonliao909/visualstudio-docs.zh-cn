---
title: 在应用程序应用ClickOnce数据文件
description: 了解如何将任何类型的数据文件添加到 ClickOnce应用程序，以存储在目标计算机本地磁盘上的数据目录中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, data
- deploying applications [ClickOnce], data files
- data access, ClickOnce applications
ms.assetid: 89ee46ef-bc8c-4ab0-a2ac-1220f9da06fc
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 225c24e4bb743b26a137b68e206a5937963f6e28
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122080593"
---
# <a name="how-to-include-a-data-file-in-a-clickonce-application"></a>如何：将数据文件包括到 ClickOnce 应用程序中
安装的每个应用程序在目标计算机的本地磁盘上分配有一个数据目录 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ，应用程序可以在其中管理自己的数据。 数据文件可以包含任何类型的文件：文本文件、XML 文件，甚至 Microsoft Access 数据库 (*.mdb*) 文件。 以下过程显示如何将任何类型的数据文件添加到 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序中。

### <a name="to-include-a-data-file-by-using-mageexe"></a>使用数据包含数据文件Mage.exe

1. 使用应用程序的其他文件将数据文件添加到应用程序目录。

    通常，应用程序目录将是一个标有部署当前版本的目录，例如 v1.0.0.0。

2. 更新应用程序清单以列出数据文件。

    `mage -u v1.0.0.0\Application.manifest -FromDirectory v1.0.0.0`

    执行此任务会重新创建应用程序清单中的文件列表，并自动生成哈希签名。

3. 在首选文本或 XML 编辑器中打开应用程序清单，找到 `file` 最近添加的文件的 元素。

    如果添加了名为 的 XML 文件 `Data.xml` ，该文件将类似于以下代码示例。

   `<file name="Data.xml" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`

4. 将 属性 `type` 添加到此元素，并为此元素提供值 `data` 。

   `<file name="Data.xml" writeableType="applicationData" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`

5. 使用密钥对或证书对应用程序清单重新签名，然后对部署清单重新签名。

    必须重新对部署清单进行签名，因为它的应用程序清单哈希已更改。

    `mage -s app manifest -cf cert_file -pwd password`

    `mage -u deployment manifest -appm app manifest`

    `mage -s deployment manifest -cf certfile -pwd password`

### <a name="to-include-a-data-file-by-using-mageuiexe"></a>使用数据包含数据文件MageUI.exe

1. 使用应用程序的其他文件将数据文件添加到应用程序目录。

2. 通常，应用程序目录将是一个标有部署当前版本的目录，例如 v1.0.0.0。

3. 在" **文件"** 菜单上，单击 **"打开** "以打开应用程序清单。

4. 选择" **文件"** 选项卡。

5. 在选项卡顶部的文本框中，输入包含应用程序文件的目录，然后单击"填充 **"。**

     数据文件将显示在网格中。

6. 将 **数据文件的"文件类型**"值设置为"**数据"。**

7. 保存应用程序清单，然后重新对文件进行签名。

     *MageUI.exe* 将提示你重新对文件进行签名。

8. 对部署清单重新签名

     必须重新对部署清单进行签名，因为它的应用程序清单哈希已更改。

## <a name="see-also"></a>请参阅
- [在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)