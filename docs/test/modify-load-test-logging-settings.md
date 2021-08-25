---
title: 负载测试日志记录设置
description: 了解如何修改负载测试日志记录设置，从而控制收集的性能数据量，这可能会导致结果文件非常大。
ms.custom: SEO-VS-2020
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- load tests, logging, modifying
ms.assetid: 9649226a-857d-41ef-8ec7-047b6e498033
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.openlocfilehash: 6a5ecba31faca0594ec1705054222b17f366263c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122032909"
---
# <a name="modify-load-test-logging-settings"></a>修改负载测试日志记录设置

已完成的负载测试的负载测试结果包含从受测计算机的日志中定期收集的性能计数器样本和错误信息。 可以在负载测试运行过程中收集大量性能计数器样本。 所收集到的性能数据量取决于运行的长度、采样间隔、受测计算机的数量以及要收集的计数器的数量。 对于大型负载测试，所收集的性能数据量很容易就能达到数千兆字节；因此，您可能需要考虑修改将数据保存到日志的频率。 请参阅[测试控制器和测试代理](configure-test-agents-and-controllers-for-load-tests.md)。

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

测试控制器会在测试运行期间将收集的所有负载测试样本数据后台处理到一个数据库日志中。 其他数据（如计时详细信息和错误详细信息）会在测试完成时加载到该数据库中。

|任务|关联主题|
|-|-----------------------|
|**在负载测试未通过时保存日志：** 可以指定是否每当负载测试未通过就保存测试日志。|-   [如何：指定是否将测试失败保存到测试日志中](../test/how-to-specify-if-test-failures-are-saved-to-test-logs.md)|
|**为日志文件设置最大文件大小：** 可以编辑与测试控制器服务关联的 XML 配置文件，以指定要用于日志文件的最大文件大小。|修改 QTCcontroller.exe.config XML 配置文件中的 `<add key="LogSizeLimitInMegs" value="20"/>`。|

## <a name="see-also"></a>另请参阅

- [配置负载测试运行设置](../test/configure-load-test-run-settings.md)
