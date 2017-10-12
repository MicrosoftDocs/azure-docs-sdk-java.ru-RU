---
title: "Библиотеки служебной шины для Java"
description: "Справочная документация для клиентской библиотеки Java и библиотек управления служебной шины"
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
ms.openlocfilehash: f7c2b1fd35fbb9dbdc782577c3464b7a38977254
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2017
---
# <a name="service-bus-libraries-for-java"></a><span data-ttu-id="df06e-104">Библиотеки служебной шины для Java</span><span class="sxs-lookup"><span data-stu-id="df06e-104">Service Bus libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="df06e-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="df06e-105">Overview</span></span>

<span data-ttu-id="df06e-106">Служебная шина — это корпоративная платформа транзакционного обмена сообщениями, которая предоставляет высокодоступные очереди и разделы публикации и подписки с расширенными функциональными возможностями, такими как упорядоченная доставка, сеансы, секционирование, планирование, комплексные подписки, рабочий процесс и обработка транзакций.</span><span class="sxs-lookup"><span data-stu-id="df06e-106">Service Bus is an enterprise-class, transactional messaging platform service that provides highly reliable queues and publish/subscribe topics with deep feature capabilities such as ordered delivery, sessions, partitioning, scheduling, complex subscriptions, as well as workflow and transaction handling.</span></span>

<span data-ttu-id="df06e-107">Функциональные возможности служебной шины сравнимы с возможностями локальных брокеров сообщений прежних версий высшего класса и часто превосходят эти возможности.</span><span class="sxs-lookup"><span data-stu-id="df06e-107">The Service Bus feature capabilities are comparable and often exceed those of high-end, on-premises legacy message brokers.</span></span> <span data-ttu-id="df06e-108">Компоненты служебной шины можно загрузить с помощью стандартизированных протоколов, таких как AMQP 1.0 и HTTPS. Все действия протокола задокументированы, что обеспечивает полное взаимодействие.</span><span class="sxs-lookup"><span data-stu-id="df06e-108">The Service Bus features are available via standards-based protocols like AMQP 1.0 and HTTPS and all protocol gestures are fully documented, allowing for broad interoperability.</span></span> 

<span data-ttu-id="df06e-109">Служебная шина уровня "Премиум" в первую очередь предназначена для надежного обмена сообщениями с высоким уровнем доступности. Кроме того, она обеспечивает конкурентную пропускную способность даже при масштабных развертываниях в локальном центре обработки данных, но не предоставляет выбор оборудования и процессы приобретения, планирование и выполнение развертывания, а также бесконечные сеансы оптимизации производительности.</span><span class="sxs-lookup"><span data-stu-id="df06e-109">Focusing on highly available and reliable durable messaging, the Service Bus Premium provides competitive throughput performance even with substantial local datacenter deployments, but without hardware selection and acquisition processes, deployment planning and execution, and endless performance optimization sessions.</span></span> 

<span data-ttu-id="df06e-110">Служебная шина уровня "Премиум" — это полностью управляемое предложение с выделенной емкостью, зарезервированной для каждого клиента, которое обеспечивает прогнозируемую производительность. Кроме того, оно отличается простой моделью ценообразования в зависимости от емкости и очень низкой общей стоимостью по сравнению с коммерческими локальными брокерами.</span><span class="sxs-lookup"><span data-stu-id="df06e-110">Service Bus Premium is a fully managed offering with dedicated capacity reserved for each tenant that yields predictable performance with a simple, capacity-oriented pricing model and at extremely lower overall cost than commercial on-premises brokers.</span></span> <span data-ttu-id="df06e-111">Для многих пользователей служебная шина уровня "Премиум" может заменить выделенные локальные кластеры обмена сообщениями, даже если вложенные рабочие нагрузки не выполняются в облаке.</span><span class="sxs-lookup"><span data-stu-id="df06e-111">For many customers, Service Bus Premium can replace dedicated on-premises messaging clusters today, even if the attached workloads do not run in the cloud.</span></span> 

<span data-ttu-id="df06e-112">Дополнительные сведения об основных понятиях, касающихся служебной шины, см. [в документации по обмену сообщениями](https://docs.microsoft.com/en-us/azure/service-bus-messaging/).</span><span class="sxs-lookup"><span data-stu-id="df06e-112">Learn more about Service Bus concepts [in the messaging documentation section](https://docs.microsoft.com/en-us/azure/service-bus-messaging/)</span></span> 

<span data-ttu-id="df06e-113">Для разработчиков Java служебная шина предоставляет собственный API с поддержкой корпорации Майкрософт. Служебную шину можно также использовать с библиотеками, совместимыми с AMQP 1.0, например с поставщиком JMS Apache Qpid Proton.</span><span class="sxs-lookup"><span data-stu-id="df06e-113">For Java developers, Service Bus provides a Microsoft supported native API and Service Bus can also be used with AMQP 1.0 compliant libraries such as Apache Qpid Proton's JMS provider.</span></span>

<span data-ttu-id="df06e-114">Официальный клиент служебной шины в [формате исходного кода доступен на сайте GitHub](https://github.com/azure/azure-service-bus-java), а двоичные файлы и упакованные файлы с исходным кодом — [в центральном репозитории Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).</span><span class="sxs-lookup"><span data-stu-id="df06e-114">The official Service Bus client is available in [source code form on GitHub](https://github.com/azure/azure-service-bus-java) and binaries and packaged sources [are available on Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).</span></span> 


## <a name="client-library"></a><span data-ttu-id="df06e-115">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="df06e-115">Client library</span></span>


<span data-ttu-id="df06e-116">Добавьте зависимость в файл `pom.xml` проекта Maven, чтобы использовать библиотеку в своем проекте.</span><span class="sxs-lookup"><span data-stu-id="df06e-116">Add a dependency to your Maven project's `pom.xml` file to use the library in your own project.</span></span> <span data-ttu-id="df06e-117">Укажите версию в случае необходимости.</span><span class="sxs-lookup"><span data-stu-id="df06e-117">Specify the version as desired.</span></span>

<span data-ttu-id="df06e-118">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="df06e-118">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-servicebus</artifactId>
    <version>1.0.0</version>
</dependency>
```

## <a name="examples"></a><span data-ttu-id="df06e-119">Примеры</span><span class="sxs-lookup"><span data-stu-id="df06e-119">Examples</span></span>

<span data-ttu-id="df06e-120">[Репозиторий примеров кода](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) содержит примеры отправки и получения сообщений из служебной шины с помощью [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java), [TopicClient и SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java), [MessageSender и MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java).</span><span class="sxs-lookup"><span data-stu-id="df06e-120">The [sample code repository](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) contains samples for how to [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java) and [TopicClient and SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java) and [MessageSender and MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) messages from Service Bus.</span></span>


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
> [<span data-ttu-id="df06e-121">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="df06e-121">Explore the Client APIs</span></span>](/java/api/overview/azure/servicebus/clientlibrary)

## <a name="management-api"></a><span data-ttu-id="df06e-122">API управления</span><span class="sxs-lookup"><span data-stu-id="df06e-122">Management API</span></span>

<span data-ttu-id="df06e-123">Создание пространств имен, разделов, очередей и подписок и управление ими с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="df06e-123">Create and manage namespaces, topics, queues, and subscriptions with the management API.</span></span>

<span data-ttu-id="df06e-124">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="df06e-124">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-servicebus</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="df06e-125">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="df06e-125">Explore the Management APIs</span></span>](/java/api/overview/azure/servicebus/managementapi)


## <a name="examples"></a><span data-ttu-id="df06e-126">Примеры</span><span class="sxs-lookup"><span data-stu-id="df06e-126">Examples</span></span>

<span data-ttu-id="df06e-127">[Управление очередями служебной шины](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
[Создание разделов служебной шины и подписка на них](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)</span><span class="sxs-lookup"><span data-stu-id="df06e-127">[Manage Service Bus queues](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
[Create and subscribe to Service Bus topics](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)</span></span>

<span data-ttu-id="df06e-128">Ознакомьтесь с другими [примерами кода Java для служебной шины Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=bus), которые можно использовать в приложениях.</span><span class="sxs-lookup"><span data-stu-id="df06e-128">Explore more [sample Java code for Azure Service Bus](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) you can use in your apps.</span></span>