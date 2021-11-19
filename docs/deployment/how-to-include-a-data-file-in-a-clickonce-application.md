---
title: 将数据文件添加到 ClickOnce 应用中
description: 了解如何在 ClickOnce 应用程序中添加任何类型的数据文件，以将其存储在目标计算机本地磁盘上的数据目录中。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666952"
---
# <a name="how-to-include-a-data-file-in-a-clickonce-application"></a>如何：将数据文件包括到 ClickOnce 应用程序中
安装的每个 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序在目标计算机的本地磁盘上都分配有一个数据目录，应用程序可以在其中管理自己的数据。 数据文件可以包含任何类型的文件：文本文件、XML 文件，甚至 Microsoft Access 数据库 (.mdb) 文件。 下面的过程演示如何向 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序中添加任何类型的数据文件。

### <a name="to-include-a-data-file-by-using-mageexe"></a>使用 Mage.exe 包含数据文件

1. 将数据文件与其余的应用程序文件一起添加到应用程序目录。

    通常情况下，应用程序目录将是一个使用部署的当前版本（例如 v1.0.0.0）标记的目录。

2. 更新应用程序清单以列出数据文件。

    `mage -u v1.0.0.0\Application.manifest -FromDirectory v1.0.0.0`

    执行此任务将重新创建应用程序清单中的文件列表，并自动生成哈希签名。

3. 在你首选的文本编辑器或 XML 编辑器中打开应用程序清单，然后查找最近添加的文件的 `file` 元素。

    如果添加了一个名为 `Data.xml` 的 XML 文件，则该文件将类似于下面的代码示例。

   `<file name="Data.xml" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`

4. 将属性 `type` 添加到此元素，并为其提供值 `data`。

   `<file name="Data.xml" writeableType="applicationData" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`

5. 使用密钥对或证书对应用程序清单进行重新签名，然后对部署清单进行重新签名。

    必须对部署清单进行重新签名，因为其应用程序清单的哈希已发生更改。

    `mage -s app manifest -cf cert_file -pwd password`

    `mage -u deployment manifest -appm app manifest`

    `mage -s deployment manifest -cf certfile -pwd password`

### <a name="to-include-a-data-file-by-using-mageuiexe"></a>使用 MageUI.exe 包含数据文件

1. 将数据文件与其余的应用程序文件一起添加到应用程序目录。

2. 通常情况下，应用程序目录将是一个使用部署的当前版本（例如 v1.0.0.0）标记的目录。

3. 在“文件”菜单上，选择“打开”以打开应用程序清单 。

4. 单击“文件”选项卡。

5. 在选项卡顶部的文本框中，输入包含应用程序文件的目录，然后单击“填充”。

     数据文件将显示在网格中。

6. 设置数据文件的“文件类型”值为“数据”。

7. 保存应用程序清单，然后对文件进行重新签名。

     MageUI.exe 将提示你对该文件进行重新签名。

8. 对部署清单进行重新签名

     必须对部署清单进行重新签名，因为其应用程序清单的哈希已发生更改。

## <a name="see-also"></a>另请参阅
- [在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)