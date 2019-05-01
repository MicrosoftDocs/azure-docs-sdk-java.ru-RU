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
ms.openlocfilehash: 9e2ae18f98083cb35bb076a5f84726b669cbf81e
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593365"
---
# <a name="azure-event-hub-libraries-for-java"></a>Библиотеки концентратора событий Azure для Java

## <a name="overview"></a>Обзор

Собирайте и администрируйте миллионы событий в секунду, поступающих от подключенных устройств и приложений Интернета вещей с помощью [Центров событий Azure](/azure/event-hubs/event-hubs-what-is-event-hubs).

Чтобы приступить к работе с Центрами событий Azure, см. инструкции по [получению событий из Центров событий Azure с помощью Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).


## <a name="client-library"></a>Клиентская библиотека

Отправляйте события в Центры событий Azure, чтобы использовать и обрабатывать события из концентратора событий с помощью клиентской библиотеки Центров событий.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать [клиентскую библиотеку](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs) в проекте.
 

## <a name="example"></a>Пример

Отправьте событие в концентратор событий.

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
> [Обзор клиентских API-интерфейсов](/java/api/overview/azure/eventhubs/client)



## <a name="samples"></a>Примеры

[Изучение возможностей API плоскости данных концентратора событий на примерах][1]

[Запись в концентратор событий с помощью JMS и чтение из Apache Storm][2]

[Чтение и запись в концентраторах событий с помощью гибридной топологии .NET и Java][3] 

[1]: https://github.com/Azure/azure-event-hubs/tree/master/samples/Java
[2]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[3]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

Ознакомьтесь с [примерами кода Java для Центров событий Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=event), которые можно использовать в своих приложениях.

