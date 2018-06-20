---
title: Библиотеки служебной шины для Java
description: Справочная документация для клиентской библиотеки Java и библиотек управления служебной шины
keywords: Azure, Java, SDK, API, messaging, amqp, qpid, JMS, pubsub, pub-sub, message broker
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: service-bus
ms.openlocfilehash: ed830b4f7ffa104174205f75ea2923235029ea80
ms.sourcegitcommit: 798f4d4199d3be9fc5c9f8bf7a754d7393de31ae
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/08/2018
ms.locfileid: "33887764"
---
# <a name="service-bus-libraries-for-java"></a>Библиотеки служебной шины для Java

## <a name="overview"></a>Обзор

Служебная шина — это корпоративная платформа транзакционного обмена сообщениями, которая предоставляет высокодоступные очереди и разделы публикации и подписки с расширенными функциональными возможностями, такими как упорядоченная доставка, сеансы, секционирование, планирование, комплексные подписки, рабочий процесс и обработка транзакций.

Функциональные возможности служебной шины сравнимы с возможностями локальных брокеров сообщений прежних версий высшего класса и часто превосходят эти возможности. Компоненты служебной шины можно загрузить с помощью стандартизированных протоколов, таких как AMQP 1.0 и HTTPS. Все действия протокола задокументированы, что обеспечивает полное взаимодействие. 

Служебная шина уровня "Премиум" в первую очередь предназначена для надежного обмена сообщениями с высоким уровнем доступности. Кроме того, она обеспечивает конкурентную пропускную способность даже при масштабных развертываниях в локальном центре обработки данных, но не предоставляет выбор оборудования и процессы приобретения, планирование и выполнение развертывания, а также бесконечные сеансы оптимизации производительности. 

Служебная шина уровня "Премиум" — это полностью управляемое предложение с выделенной емкостью, зарезервированной для каждого клиента, которое обеспечивает прогнозируемую производительность. Кроме того, оно отличается простой моделью ценообразования в зависимости от емкости и очень низкой общей стоимостью по сравнению с коммерческими локальными брокерами. Для многих пользователей служебная шина уровня "Премиум" может заменить выделенные локальные кластеры обмена сообщениями, даже если вложенные рабочие нагрузки не выполняются в облаке. 

Дополнительные сведения об основных понятиях, касающихся служебной шины, см. [в документации по обмену сообщениями](https://docs.microsoft.com/azure/service-bus-messaging/). 

Для разработчиков Java служебная шина предоставляет собственный API с поддержкой корпорации Майкрософт. Служебную шину можно также использовать с библиотеками, совместимыми с AMQP 1.0, например с поставщиком JMS Apache Qpid Proton.

## <a name="client-library"></a>Клиентская библиотека

Официальный клиент служебной шины в [формате исходного кода доступен на сайте GitHub](https://github.com/azure/azure-service-bus-java), а двоичные файлы и упакованные файлы с исходным кодом — [в центральном репозитории Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).

**[Репозиторий с примерами кода](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) содержит следующие примеры:**
* Как использовать [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java)
* Как использовать [TopicClient и SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java)
* Как использовать сообщения [MessageSender и MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) из служебной шины

Добавьте зависимость в файл `pom.xml` проекта Maven, чтобы использовать библиотеку в своем проекте. Укажите версию в случае необходимости.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-servicebus</artifactId>
    <version>1.0.0</version>
</dependency>
```

```java
public class BasicSendReceiveWithQueueClient {
    // Connection String for the namespace can be obtained from the Azure portal under the
    // 'Shared Access policies' section.
    private static final String connectionString = "{connection string}";
    private static final String queueName = "{queue name}";
    private static IQueueClient queueClient;
    private static int totalSend = 100;
    private static int totalReceived = 0;

    public static void main(String[] args) throws Exception {

        Log.log("Starting BasicSendReceiveWithQueueClient sample");

        // create client
        Log.log("Create queue client.");
        queueClient = new QueueClient(new ConnectionStringBuilder(connectionString, queueName), ReceiveMode.PeekLock);

        // send and receive
        queueClient.registerMessageHandler(new MessageHandler(queueClient), new MessageHandlerOptions(1, false, Duration.ofMinutes(1)));
        for (int i = 0; i < totalSend; i++) {
            int j = i;
            Log.log("Sending message #%d.", j);
            queueClient.sendAsync(new Message("" + i)).thenRunAsync(() -> { Log.log("Sent message #%d.", j);});
        }

        while(totalReceived != totalSend) {
            Thread.sleep(1000);
        }

        Log.log("Received all messages, exiting the sample.");
        Log.log("Closing queue client.");
        queueClient.close();
    }

    static class MessageHandler implements IMessageHandler {
        private IQueueClient client;

        public MessageHandler(IQueueClient client) {
            this.client = client;
        }

        @Override
        public CompletableFuture<Void> onMessageAsync(IMessage iMessage) {
            Log.log("Received message with sq#: %d and lock token: %s.", iMessage.getSequenceNumber(), iMessage.getLockToken());
            return this.client.completeAsync(iMessage.getLockToken()).thenRunAsync(() -> {
                Log.log("Completed message sq#: %d and locktoken: %s", iMessage.getSequenceNumber(), iMessage.getLockToken());
                totalReceived++;
            });
        }

        @Override
        public void notifyException(Throwable throwable, ExceptionPhase exceptionPhase) {
            Log.log(exceptionPhase + "-" + throwable.getMessage());
        }
    }
}
```

> [!div class="nextstepaction"]
> [Просмотр клиентских API](/java/api/overview/azure/servicebus/client)
> [См. дополнительные примеры здесь (дополнительные сведения см. также по ссылкам выше)](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/)

## <a name="management-api"></a>API управления

Создание пространств имен, разделов, очередей и подписок и управление ими с помощью API управления.

**Несколько примеров см. здесь:**
* [Управление очередями служебной шины](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
* [Создание разделов и подписок служебной шины](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)

**Использование API управления в проекте:**
\
[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-servicebus</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/java/api/overview/azure/servicebus/management)

Ознакомьтесь с другими [примерами кода Java для служебной шины Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=bus), которые можно использовать в приложениях.
