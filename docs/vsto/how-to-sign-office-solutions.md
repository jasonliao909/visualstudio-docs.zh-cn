---
title: 如何：对Office签名
description: 了解如何使用证书作为Microsoft Office向解决方案授予信任。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- certificates [Office development in Visual Studio], Office solutions
- security [Office development in Visual Studio], signing Office solutions
- signing manifests [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: ab1fa5de20975b3c08d95906cef1288ebe8f4ec5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665245"
---
# <a name="how-to-sign-office-solutions"></a>如何：对Office签名
  如果对解决方案进行签名，可以使用证书作为证据授予对解决方案的信任。 可以将同一证书用于多个解决方案，所有解决方案都将受信任，无需其他安全策略更新。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 如果使用 清单生成和编辑工具 (mage.exe和mageui.exe) 手动编辑应用程序和部署清单，则必须对清单重新签名，然后才能使用它们。 有关详细信息，请参阅[如何：对应用程序和部署清单重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)。

## <a name="sign-by-using-a-certificate"></a>使用证书签名
 证书是包含唯一密钥和解决方案发布者标识的文件。 可以从证书颁发机构购买证书，也可以创建自己的证书，然后由证书颁发机构对证书进行签名。

 Visual Studio使用Office证书对解决方案进行签名以启用调试。 不应将已部署解决方案中的临时证书用作证据。

### <a name="to-sign-an-office-solution-by-using-a-certificate"></a>使用证书Office解决方案签名

1. 在 **"Project"** 菜单上，单击"_解决方案""名称属性_**"。**

2. 单击“签名”选项卡。 

3. 选择 **"为ClickOnce签名"。**

4. 通过单击"从存储中选择 **"** 或 **"从文件中** 选择"并导航到证书找到证书。

5. 若要验证是否使用了正确的证书，请单击 **"更多详细信息** "以查看证书信息。

## <a name="see-also"></a>另请参阅

- [安全Office解决方案](../vsto/securing-office-solutions.md)
- [向解决方案Office信任](../vsto/granting-trust-to-office-solutions.md)
- [“项目设计器”-&gt;“签名”页](../ide/reference/signing-page-project-designer.md)
