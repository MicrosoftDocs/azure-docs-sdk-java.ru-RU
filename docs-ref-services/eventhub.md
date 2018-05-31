---
title: Библиотеки концентратора событий Azure для Java
description: Справочная документация по библиотекам концентратора событий для Java
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
ms.openlocfilehash: b6646ef27edace4247090e749c9a52cd6a33a82c
ms.sourcegitcommit: 3d3460289ab6b9165c2cf6a3dd56eafd0692501e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34283028"
---
# <a name="azure-event-hub-libraries-for-java"></a><span data-ttu-id="2ba57-104">Библиотеки концентратора событий Azure для Java</span><span class="sxs-lookup"><span data-stu-id="2ba57-104">Azure Event Hub libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="2ba57-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="2ba57-105">Overview</span></span>

<span data-ttu-id="2ba57-106">Собирайте и администрируйте миллионы событий в секунду, поступающих от подключенных устройств и приложений Интернета вещей с помощью [концентраторов событий Azure](/azure/event-hubs/event-hubs-what-is-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="2ba57-106">Collect and manage millions of events per second from connected IoT devices and applications with [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>

<span data-ttu-id="2ba57-107">Чтобы приступить к работе с концентраторами событий Azure, см. инструкции по [получению событий из концентраторов событий Azure с помощью Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span><span class="sxs-lookup"><span data-stu-id="2ba57-107">To get started with Azure Event Hubs, see [Receive events from Azure Event Hubs using Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span></span>


## <a name="client-library"></a><span data-ttu-id="2ba57-108">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="2ba57-108">Client library</span></span>

<span data-ttu-id="2ba57-109">Отправляйте события в концентратор событий Azure, чтобы использовать и обрабатывать события из концентратора событий с помощью клиентской библиотеки концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="2ba57-109">Send events to an Azure Event Hub and consume and process events from an Event Hub using the Event Hubs client library.</span></span>

<span data-ttu-id="2ba57-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать [клиентскую библиотеку](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs) в проекте.</span><span class="sxs-lookup"><span data-stu-id="2ba57-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the [client library](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs) in your project.</span></span>
 

## <a name="example"></a><span data-ttu-id="2ba57-111">Пример</span><span class="sxs-lookup"><span data-stu-id="2ba57-111">Example</span></span>

<span data-ttu-id="2ba57-112">Отправьте событие в концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="2ba57-112">Send an event to an event hub.</span></span>

```java
final ConnectionStringBuilder connStr = new ConnectionStringBuilder()
                                            .setNamespaceName(namespaceName)
                                            .setEventHubName(eventHubName)
                                            .setSasKeyName(sasKeyName)
                                            .setSasKey(sasKey);
final EventHubClient ehClient = EventHubClient.createSync(connStr.toString());

final byte[] payloadBytes = "Test AMQP message".getBytes("UTF-8");
final EventData sendEvent = new EventData(payloadBytes);

ehClient.sendSync(sendEvent);
```


> [!div class="nextstepaction"]
> [<span data-ttu-id="2ba57-113">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="2ba57-113">Explore the Client APIs</span></span>](/java/api/overview/azure/eventhubs/client)



## <a name="samples"></a><span data-ttu-id="2ba57-114">Примеры</span><span class="sxs-lookup"><span data-stu-id="2ba57-114">Samples</span></span>

<span data-ttu-id="2ba57-115">[Изучение возможностей API плоскости данных концентратора событий на примерах][1]</span><span class="sxs-lookup"><span data-stu-id="2ba57-115">[Explore Event Hub data-plane API using samples][1]</span></span>

<span data-ttu-id="2ba57-116">[Запись в концентратор событий с помощью JMS и чтение из Apache Storm][2]</span><span class="sxs-lookup"><span data-stu-id="2ba57-116">[Write to Event Hub via JMS and read from Apache Storm][2]</span></span>

<span data-ttu-id="2ba57-117">[Чтение и запись в концентраторах событий с помощью гибридной топологии .NET и Java][3]</span><span class="sxs-lookup"><span data-stu-id="2ba57-117">[Read and write from EventHubs using a hybrid .NET/Java topology][3]</span></span> 

[1]: https://github.com/Azure/azure-event-hubs/tree/master/samples/Java
[2]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[3]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

<span data-ttu-id="2ba57-118">Ознакомьтесь с [примерами кода Java для концентраторов событий Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=event), которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="2ba57-118">Explore more [sample Java code for Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) you can use in your apps.</span></span>

