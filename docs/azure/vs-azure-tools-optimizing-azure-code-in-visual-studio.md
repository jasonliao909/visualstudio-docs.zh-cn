---
title: 优化 Azure 代码
description: 了解 Visual Studio 中的 Azure 代码优化工具如何帮助提高代码的可靠性和性能。
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.topic: conceptual
ms.workload: azure-vs
ms.date: 11/11/2016
ms.author: ghogen
ms.openlocfilehash: 9836f13ac97641876746e0c514f11efc297d2975
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602130"
---
# <a name="optimizing-your-azure-code"></a>优化 Azure 代码
对使用 Microsoft Azure 的应用程序进行编程时，应遵循某些编码做法，以免在云环境中应用程序的伸缩性、行为和性能出现问题。 Microsoft 提供了 Azure 代码分析工具，该工具可识别并确定部分常见问题并帮助你解决这些问题。 可以通过 NuGet 在 Visual Studio 中下载该工具。

## <a name="azure-code-analysis-rules"></a>Azure 代码分析规则
当 Azure 代码分析工具发现已知的影响性能的问题时，它使用以下规则来自动标记 Azure 代码。 检测到的问题显示为警告或编译器错误。 用于解决警告或错误的代码修复或建议通常通过灯泡图标提供。

## <a name="avoid-using-default-in-process-session-state-mode"></a>避免使用默认的（进程内）会话状态模式
### <a name="id"></a>ID
AP0000

### <a name="description"></a>说明
如果对云应用程序使用默认（进程内）会话状态模式，可能丢失会话状态。

请通过 [Azure 代码分析反馈](https://social.msdn.microsoft.com/Forums/en-US/home)来分享看法和意见。

### <a name="reason"></a>原因
默认情况下，在 web.config 文件中指定的会话状态模式为进程内。 此外，如果配置文件中没有指定任何条目，会话状态模式默认为进程内。 进程内模式会话状态存储在 Web 服务器的内存中。 当重新启动某个实例或使用新实例来支持负载均衡或故障转移时，存储在 Web 服务器内存中的会话状态并不保存。 这种情况会导致应用程序无法在云上缩放。

ASP.NET 会话状态支持多种不同的会话状态数据存储选项：InProc、StateServer、SQLServer、Custom 和 Off。 建议使用 Custom 模式在外部会话状态存储（例如，[适用于 Redis 的 Azure 会话状态提供程序](https://devblogs.microsoft.com/aspnet/announcing-asp-net-session-state-provider-for-redis-preview-release/)）中托管数据。

### <a name="solution"></a>解决方案
建议的解决方案之一是在托管缓存服务中存储会话状态。 了解如何使用[适用于 Redis 的 Azure 会话状态提供程序](https://devblogs.microsoft.com/aspnet/announcing-asp-net-session-state-provider-for-redis-preview-release/)来存储会话状态。 也可以在其他位置存储会话状态，以确保应用程序可在云上缩放。 若要详细了解替代解决方案，请阅读[会话状态模式](/previous-versions/ms178586(v=vs.140))。

## <a name="run-method-should-not-be-async"></a>运行方法不应是异步的
### <a name="id"></a>ID
AP1000

### <a name="description"></a>说明
在 [Run()](/previous-versions/azure/reference/ee772746(v=azure.100)) 方法外部创建异步方法（例如 [await](/dotnet/csharp/language-reference/operators/await)），并从 [Run()](/previous-versions/azure/reference/ee772746(v=azure.100)) 调用异步方法。 将 [[Run()](/previous-versions/azure/reference/ee772746(v=azure.100))](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) 方法声明为异步方法会导致辅助角色进入重新启动循环。

请通过 [Azure 代码分析反馈](https://social.msdn.microsoft.com/Forums/en-US/home)来分享看法和意见。

### <a name="reason"></a>原因
在 [Run()](/previous-versions/azure/reference/ee772746(v=azure.100)) 方法内部调用异步方法会导致云服务运行时回收辅助角色。 当辅助角色启动时，所有程序执行会在 [Run()](/previous-versions/azure/reference/ee772746(v=azure.100)) 方法内发生。 退出 Run 方法会导致辅助角色重启。 当辅助角色运行时调用异步方法时，会在异步方法之后调度所有操作，然后返回。 这会导致辅助角色从 Run 方法退出并重启。 在下一轮执行时，辅助角色再次调用异步方法并重新启动，导致辅助角色再次回收。

### <a name="solution"></a>解决方案
将所有异步操作放在 [Run()](/previous-versions/azure/reference/ee772746(v=azure.100)) 方法的外部。 然后从 Run 方法内部调用重构的异步方法，例如 RunAsync().wait。 Azure 代码分析工具可帮助解决此问题。

以下代码段演示了此问题的代码修复过程：

```csharp
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("https://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a>使用服务总线共享访问签名身份验证
### <a name="id"></a>ID
AP2000

### <a name="description"></a>说明
使用共享访问签名 (SAS) 进行身份验证。 用于服务总线身份验证的访问控制服务 (ACS) 会被弃用。

请通过 [Azure 代码分析反馈](https://social.msdn.microsoft.com/Forums/en-US/home)来分享看法和意见。

### <a name="reason"></a>原因
为了增强安全性，Azure Active Directory 会将 ACS 身份验证替换为 SAS 身份验证。 有关过渡计划的信息，请参阅 [Azure Active Directory is the future of ACS](https://cloudblogs.microsoft.com/enterprisemobility/2013/06/22/azure-active-directory-is-the-future-of-acs/)（Azure Active Directory 是 ACS 的未来）。

### <a name="solution"></a>解决方案
在应用中使用 SAS 身份验证。 以下示例说明如何使用现有 SAS 令牌访问服务总线命名空间或实体。

```csharp
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

有关更多信息，请参阅以下主题。

* 有关概述，请参阅[服务总线的共享访问签名身份验证](/azure/service-bus-messaging/service-bus-sas)
* [如何使用服务总线的共享访问签名身份验证](/azure/service-bus-messaging/service-bus-sas)

## <a name="consider-using-onmessage-method-to-avoid-receive-loop"></a>考虑使用 OnMessage 方法来避免“receive 循环”
### <a name="id"></a>ID
AP2002

### <a name="description"></a>说明
为了避免陷入“receive 循环”，接收消息时调用 **OnMessage** 方法是比调用 **Receive** 方法更适合的解决方案。 但是，如果必须使用 **Receive** 方法并指定了非默认的服务器等待时间，请确保服务器等待时间超过一分钟。

请通过 [Azure 代码分析反馈](https://social.msdn.microsoft.com/Forums/en-US/home)来分享看法和意见。

### <a name="reason"></a>原因
当调用 **OnMessage** 时，客户端将启动一个内部消息泵，该消息泵不断轮询队列或订阅。 此消息泵包含发出消息接收调用的无限循环。 如果调用超时，它将发出新的调用。 超时间隔由所用的 [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) 的 [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings) 属性值确定。

相比于 **Receive**，使用 **OnMessage** 的优点是用户不必手动轮询消息、处理异常、并行处理多个消息和完成消息。

如果调用 **Receive** 时而未使用其默认值，请确保 *ServerWaitTime* 值大于一分钟。 将 *ServerWaitTime* 设置为大于一分钟可防止服务器在未接收完消息时就已超时。

### <a name="solution"></a>解决方案
请参阅以下代码示例了解建议用法。 有关详细信息，请参阅 [QueueClient.OnMessage 方法 (Microsoft.ServiceBus.Messaging)](/dotnet/api/microsoft.servicebus.messaging.queueclient) 和 [QueueClient.Receive 方法 (Microsoft.ServiceBus.Messaging)](/dotnet/api/microsoft.servicebus.messaging.queueclient)。

若要提高 Azure 消息传送基础结构的性能，请参阅设计模式 [Asynchronous Messaging Primer](/previous-versions/msp-n-p/dn589781(v=pandp.10))（异步消息传送入门）。

下面是使用 **OnMessage** 接收消息的示例。

```csharp
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if the message-pump should call complete on messages after the callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates the maximum number of concurrent calls to the callback the pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you to get notified of any errors encountered by the message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates the message pump and callback is invoked for each message that is received, calling close on the client will stop the pump.
    {
        // Process the message.
    }, options);
    Console.WriteLine("Press any key to exit.");
    Console.ReadKey();
```

下面是使用 **Receive** 和默认服务器等待时间的示例。

```csharp
string connectionString =
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)
{
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

下面是使用 **Receive** 和非默认服务器等待时间的示例。

```csharp
while (true)
{
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```

## <a name="consider-using-asynchronous-service-bus-methods"></a>考虑使用异步服务总线方法
### <a name="id"></a>ID
AP2003

### <a name="description"></a>说明
使用异步服务总线方法可改善中转消息传送的性能。

请通过 [Azure 代码分析反馈](https://social.msdn.microsoft.com/Forums/en-US/home)来分享看法和意见。

### <a name="reason"></a>原因
使用异步方法可实现应用程序并行性效果，因为在执行每个调用时不会阻塞主线程。 使用服务总线消息传送方法时，执行某项操作（发送、接收、删除等）需要花费一定的时间。 这一时间包括服务总线服务处理该操作的时间，外加延迟处理请求和答复的时间。 若要增加每次操作的数目，操作必须同时执行。 有关详细信息，请参阅 [Best Practices for Performance Improvements Using Service Bus Brokered Messaging](/previous-versions/azure/hh528527(v=azure.100))（使用服务总线中转消息传送改善性能的最佳实践）。

### <a name="solution"></a>解决方案
有关如何使用建议的异步方法的信息，请参阅 [QueueClient 类 (Microsoft.ServiceBus.Messaging)](/dotnet/api/microsoft.servicebus.messaging.queueclient)。

若要提高 Azure 消息传送基础结构的性能，请参阅设计模式 [Asynchronous Messaging Primer](/previous-versions/msp-n-p/dn589781(v=pandp.10))（异步消息传送入门）。

## <a name="consider-partitioning-service-bus-queues-and-topics"></a>考虑将对服务总线队列和主题进行分区
### <a name="id"></a>ID
AP2004

### <a name="description"></a>说明
对服务总线队列和主题进行分区以提高服务总线消息传送的性能。

请通过 [Azure 代码分析反馈](https://social.msdn.microsoft.com/Forums/en-US/home)来分享看法和意见。

### <a name="reason"></a>原因
对服务总线队列和主题进行分区可以提高性能吞吐量和服务可用性，因为分区后的队列或主题的总体吞吐量不再受限于单个消息代理或消息存储的性能。 此外，消息存储的临时中断不会导致分区的队列或主题不可用。 有关详细信息，请参阅[对消息实体进行分区](/previous-versions/azure/dn520246(v=azure.100))。

### <a name="solution"></a>解决方案
以下代码段演示了如何将消息实体分区。

```csharp
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

有关详细信息，请参阅 [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/)（分区的服务总线队列和主题 | Microsoft Azure 博客）并检查 [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f)（Microsoft Azure 服务总线分区队列）示例。

## <a name="do-not-set-sharedaccessstarttime"></a>不要设置 SharedAccessStartTime
### <a name="id"></a>ID
AP3001

### <a name="description"></a>说明
应避免使用设置为当前时间的 SharedAccessStartTimeset，以立即启动共享访问策略。 仅想要在以后启动共享访问策略时，才需要设置此属性。

请通过 [Azure 代码分析反馈](https://social.msdn.microsoft.com/Forums/en-US/home)来分享看法和意见。

### <a name="reason"></a>原因
时钟同步会导致各数据中心的时间略有不同。 例如，你可能会使用 DateTime.Now 或类似方法将存储 SAS 策略的开始时间设为当前时间，以使 SAS 策略立即生效。 但是，数据中心之间的轻微时间差可能会导致问题，因为某些数据中心可能会略迟于开始时间，而其他数据中心则可能会早于开始时间。 因此，如果策略生存时间设置得太短，则 SAS 策略可能很快（或者甚至立即）过期。

有关在 Azure 存储中使用共享访问签名的更多指导，请参阅 [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS](https://blogs.msdn.microsoft.com/windowsazurestorage/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas/)（表 SAS（共享访问签名）、队列 SAS 简介及 Blob SAS 更新），访问路径为“Microsoft Azure 存储团队博客”-“站点首页”-“MSDN 博客”。

### <a name="solution"></a>解决方案
删除用于设置共享访问策略开始时间的语句。 Azure 代码分析工具为此问题提供了修复方法。 有关安全管理的详细信息，请参阅设计模式 [Valet Key Pattern](/previous-versions/msp-n-p/dn568102(v=pandp.10))（辅助密钥模式）。

以下代码段演示了此问题的代码修复过程。

```csharp
// The shared access policy provides
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a>共享访问策略的过期时间必须超过五分钟
### <a name="id"></a>ID
AP3002

### <a name="description"></a>说明
由于存在所谓“时钟偏差”的情况，位于不同位置的数据中心之间最多可能有五分钟的时间差。 为了防止 SAS 策略令牌早于预计时间过期，请将过期时间设置为五分钟以上。

请通过 [Azure 代码分析反馈](https://social.msdn.microsoft.com/Forums/en-US/home)来分享看法和意见。

### <a name="reason"></a>原因
位于全球不同位置的数据中心以时钟信号来同步。 由于时钟信号需要花费时间来传送到不同位置，因此尽管理论上各地的时间都同步，但位于不同地理位置的数据中心之间还是有时间差。 这种时间差可能会影响共享访问策略的开始时间和过期间隔。 因此，为了确保共享访问策略能立即生效，请不要指定开始时间。 此外，请确保过期时间为 5 分钟以上，以防止提前超时。

有关在 Azure 存储中使用共享访问签名的详细信息，请参阅 [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS](https://blogs.msdn.microsoft.com/windowsazurestorage/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas/)（表 SAS（共享访问签名）、队列 SAS 简介及 Blob SAS 更新），访问路径为“Microsoft Azure 存储团队博客”-“站点首页”-“MSDN 博客”。

### <a name="solution"></a>解决方案
有关安全管理的详细信息，请参阅设计模式 [Valet Key Pattern](/previous-versions/msp-n-p/dn568102(v=pandp.10))（辅助密钥模式）。

下面是不指定共享访问策略开始时间的示例。

```csharp
// The shared access policy provides
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

下面是指定共享访问策略开始时间，且策略过期期限超过五分钟的示例。

```csharp
// The shared access policy provides
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

有关详细信息，请参阅[配置对容器和 Blob 的匿名公共读取访问](/azure/storage/blobs/anonymous-read-access-configure?tabs=portal)。

## <a name="use-cloudconfigurationmanager"></a>使用 CloudConfigurationManager
### <a name="id"></a>ID
AP4000

### <a name="description"></a>说明
对 Azure 网站和 Azure 移动服务等项目使用 [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) 类不会造成运行时问题。 但是，最佳做法是使用 Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) 作为所有 Azure 云应用程序配置的统一管理方式。

请通过 [Azure 代码分析反馈](https://social.msdn.microsoft.com/Forums/en-US/home)来分享看法和意见。

### <a name="reason"></a>原因
CloudConfigurationManager 读取适合应用程序环境使用的配置文件。

[CloudConfigurationManager](/previous-versions/azure/)

### <a name="solution"></a>解决方案
重构代码以使用 [CloudConfigurationManager Class](/previous-versions/azure/reference/mt634650(v=azure.100))。 Azure 代码分析工具针对此问题提供了代码修复。

以下代码段演示了此问题的代码修复过程。 Replace

`var settings = ConfigurationManager.AppSettings["mySettings"];`

替换为

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

下面是有关如何在 App.config 或 Web.config 文件中存储配置设置的示例。 请将设置添加到配置文件的 appSettings 节。 下面是上一代码示例的 Web.config 文件。

```xml
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>
```

## <a name="avoid-using-hard-coded-connection-strings"></a>避免使用硬编码的连接字符串
### <a name="id"></a>ID
AP4001

### <a name="description"></a>说明
如果使用硬编码的连接字符串并且以后需要更新，则必须对源代码进行更改并重新编译应用程序。 但是，如果将连接字符串存储在配置文件中，以后只需更新配置文件就能更改连接字符串。

请通过 [Azure 代码分析反馈](https://social.msdn.microsoft.com/Forums/en-US/home)来分享看法和意见。

### <a name="reason"></a>原因
将连接字符串硬编码不是个好办法，因为这种方式在需要快速更改连接字符串时会引发问题。 此外，如果需要将项目签入源代码管理，硬编码的连接字符串将引发安全漏洞，因为在源代码中就能查看字符串。

### <a name="solution"></a>解决方案
将连接字符串存储在配置文件或 Azure 环境中。

* 对于独立的应用程序，请使用 app.config 来存储连接字符串设置。
* 对于 IIS 托管的 Web 应用程序，请使用 web.config 来存储连接字符串。
* 对于 ASP.NET vNext 应用程序，请使用 configuration.json 来存储连接字符串。

有关使用 web.config 或 app.config 等配置文件的相关信息，请参阅[ASP.NET Web 配置指南](/aspnet/web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations)。 有关 Azure 环境变量工作原理的信息，请参阅 [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)（Azure 网站：应用程序字符串和连接字符串的工作原理）。 有关在源代码管理中存储连接字符串的信息，请参阅[避免将敏感信息（如连接字符串）放置在源代码存储库中存储的文件内](/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)。

## <a name="use-diagnostics-configuration-file"></a>使用诊断配置文件
### <a name="id"></a>ID
AP5000

### <a name="description"></a>说明
不要在代码中配置诊断设置（例如使用 Microsoft.WindowsAzure.Diagnostics 编程 API），而应该在 diagnostics.wadcfg 文件中配置诊断设置。 （或者，如果使用 Azure SDK 2.5，请使用 diagnostics.wadcfgx）。 这样，就可以更改诊断设置而无需重新编译代码。

请通过 [Azure 代码分析反馈](https://social.msdn.microsoft.com/Forums/en-US/home)来分享看法和意见。

### <a name="reason"></a>原因
在 Azure SDK 2.5（使用 Azure 诊断 1.3）之前，可使用几种不同的方法来配置 Azure 诊断 (WAD)：将它添加到存储中的配置 Blob，或者使用命令性代码、声明性配置或默认配置。 但是，配置诊断的首选方法是在应用程序项目中使用 XML 配置文件（SDK 2.5 和更高版本的 diagnostics.wadcfg 或 diagnostics.wadcfgx）。 在此方法中，diagnostics.wadcfg 文件完整地定义配置并可随意进行更新和重新部署。 通过 [DiagnosticMonitor](/previous-versions/azure/reference/ee758597(v=azure.100)) 或 [RoleInstanceDiagnosticManager](/previous-versions/azure/reference/ee773157(v=azure.100)) 类混合使用 diagnostics.wadcfg 配置文件与设置配置所需的编程方法可能会让你感到混乱。 有关详细信息，请参阅[初始化或更改 Azure 诊断配置](/previous-versions/azure/hh411537(v=azure.100))。

从 WAD 1.3（Azure SDK 2.5 已随附）开始，不再能够使用代码来配置诊断。 因此，只能在应用或更新诊断扩展时提供配置。

### <a name="solution"></a>解决方案
使用诊断配置设计器将诊断设置移到诊断配置文件（SDK 2.5 和更高版本的 diagnostics.wadcfg 或 diagnostics.wadcfgx）。 此外，建议安装 [Azure SDK 2.5](https://social.msdn.microsoft.com/Forums/en-US/home) 并使用最新的诊断功能。

1. 在要配置的角色的快捷菜单上，选择“属性”，并选择“配置”选项卡。
2. 在 **“诊断”** 节中，确保 **“启用诊断”** 复选框已选中。
3. 选择 **“配置”** 按钮。

   ![访问“启用诊断”选项](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   有关详细信息，请参阅 [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)（为 Azure 云服务和虚拟机配置诊断）。

## <a name="avoid-declaring-dbcontext-objects-as-static"></a>避免将 DbContext 对象声明为静态
### <a name="id"></a>ID
AP6000

### <a name="description"></a>说明
为了节省内存，请避免将 DBContext 对象声明为静态。

请通过 [Azure 代码分析反馈](https://social.msdn.microsoft.com/Forums/en-US/home)来分享看法和意见。

### <a name="reason"></a>原因
DBContext 对象保存每个调用返回的查询结果。 只有在卸载应用程序域之后，才释放静态 DBContext 对象。 因此，静态 DBContext 对象可能会消耗大量的内存。

### <a name="solution"></a>解决方案
将 DBContext 声明为局部变量或非静态实例字段，将它用于任务，然后让它在使用后释放。

以下 MVC 控制器类示例演示了如何使用 DBContext 对象。

```csharp
public class BlogsController : Controller
    {
        //BloggingContext is a subclass to DbContext
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a>后续步骤
若要详细了解如何对 Azure 应用进行优化和故障排除，请参阅 [使用 Visual Studio 对 Azure 应用服务中的 Web 应用进行故障排除](/azure/app-service/web-sites-dotnet-troubleshoot-visual-studio)。
