---
title: "Библиотеки концентратора событий Azure для Java"
description: "Справочная документация по библиотекам концентратора событий для Java"
keywords: Azure, Java, SDK, API, event hub, IoT, stream processing
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: event-hub
ms.openlocfilehash: 8e5b032624862ffbef18c718abf4fa29359b3e67
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
# <a name="azure-event-hub-libraries-for-java"></a><span data-ttu-id="3b6cf-104">Библиотеки концентратора событий Azure для Java</span><span class="sxs-lookup"><span data-stu-id="3b6cf-104">Azure Event Hub libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="3b6cf-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="3b6cf-105">Overview</span></span>

<span data-ttu-id="3b6cf-106">Собирайте и администрируйте миллионы событий в секунду, поступающих от подключенных устройств и приложений Интернета вещей с помощью [концентраторов событий Azure](/azure/event-hubs/event-hubs-what-is-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="3b6cf-106">Collect and manage millions of events per second from connected IoT devices and applications with [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>

<span data-ttu-id="3b6cf-107">Чтобы приступить к работе с концентраторами событий Azure, см. инструкции по [получению событий из концентраторов событий Azure с помощью Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span><span class="sxs-lookup"><span data-stu-id="3b6cf-107">To get started with Azure Event Hubs, see [Receive events from Azure Event Hubs using Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span></span>


## <a name="client-library"></a><span data-ttu-id="3b6cf-108">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="3b6cf-108">Client library</span></span>

<span data-ttu-id="3b6cf-109">Отправляйте события в концентратор событий Azure, чтобы использовать и обрабатывать события из концентратора событий с помощью клиентской библиотеки концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-109">Send events to an Azure Event Hub and consume and process events from an Event Hub using the Event Hubs client library.</span></span>

<span data-ttu-id="3b6cf-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>0.14.3</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="3b6cf-111">Пример</span><span class="sxs-lookup"><span data-stu-id="3b6cf-111">Example</span></span>

<span data-ttu-id="3b6cf-112">Отправьте событие в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-112">Send an event to an event hub.</span></span>

```java
ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName,sasKeyName, sasKey);

byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
EventData sendEvent = new EventData(payloadBytes);
EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
ehClient.sendSync(sendEvent);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b6cf-113">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="3b6cf-113">Explore the Client APIs</span></span>](/java/api/overview/azure/eventhub/clientlibrary)


## <a name="samples"></a><span data-ttu-id="3b6cf-114">Примеры</span><span class="sxs-lookup"><span data-stu-id="3b6cf-114">Samples</span></span>

<span data-ttu-id="3b6cf-115">[Запись в концентратор событий с помощью JMS и чтение из Apache Storm][1]
[Чтение и запись из концентраторов событий с помощью гибридной топологии .NET и Java Storm][2]</span><span class="sxs-lookup"><span data-stu-id="3b6cf-115">[Write to Event Hub via JMS and read from Apache Storm][1]
[Read and write from EventHubs using a hybrid .NET/Java topology][2]</span></span> 

[1]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[2]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

<span data-ttu-id="3b6cf-116">Ознакомьтесь с [примерами кода Java для концентраторов событий Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=event), которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="3b6cf-116">Explore more [sample Java code for Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) you can use in your apps.</span></span>

