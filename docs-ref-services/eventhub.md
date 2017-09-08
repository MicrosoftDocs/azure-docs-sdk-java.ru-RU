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
# <a name="azure-event-hub-libraries-for-java"></a>Библиотеки концентратора событий Azure для Java

## <a name="overview"></a>Обзор

Собирайте и администрируйте миллионы событий в секунду, поступающих от подключенных устройств и приложений Интернета вещей с помощью [концентраторов событий Azure](/azure/event-hubs/event-hubs-what-is-event-hubs).

Чтобы приступить к работе с концентраторами событий Azure, см. инструкции по [получению событий из концентраторов событий Azure с помощью Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).


## <a name="client-library"></a>Клиентская библиотека

Отправляйте события в концентратор событий Azure, чтобы использовать и обрабатывать события из концентратора событий с помощью клиентской библиотеки концентраторов событий.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>0.14.3</version>
</dependency>
```   

## <a name="example"></a>Пример

Отправьте событие в концентратор событий.

```java
ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName,sasKeyName, sasKey);

byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
EventData sendEvent = new EventData(payloadBytes);
EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
ehClient.sendSync(sendEvent);
```

> [!div class="nextstepaction"]
> [Обзор клиентских API-интерфейсов](/java/api/overview/azure/eventhub/clientlibrary)


## <a name="samples"></a>Примеры

[Запись в концентратор событий с помощью JMS и чтение из Apache Storm][1]
[Чтение и запись из концентраторов событий с помощью гибридной топологии .NET и Java Storm][2] 

[1]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[2]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

Ознакомьтесь с [примерами кода Java для концентраторов событий Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=event), которые можно использовать в своих приложениях.

