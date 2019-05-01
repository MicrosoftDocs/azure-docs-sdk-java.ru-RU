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
ms.openlocfilehash: 2099695784a59bf539aeae745df1fe38ec84f511
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593279"
---
# <a name="service-bus-libraries-for-java"></a><span data-ttu-id="af663-104">Библиотеки служебной шины для Java</span><span class="sxs-lookup"><span data-stu-id="af663-104">Service Bus libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="af663-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="af663-105">Overview</span></span>

<span data-ttu-id="af663-106">Служебная шина — это корпоративная платформа транзакционного обмена сообщениями, которая предоставляет высокодоступные очереди и разделы публикации и подписки с расширенными функциональными возможностями, такими как упорядоченная доставка, сеансы, секционирование, планирование, комплексные подписки, рабочий процесс и обработка транзакций.</span><span class="sxs-lookup"><span data-stu-id="af663-106">Service Bus is an enterprise-class, transactional messaging platform service that provides highly reliable queues and publish/subscribe topics with deep feature capabilities such as ordered delivery, sessions, partitioning, scheduling, complex subscriptions, as well as workflow and transaction handling.</span></span>

<span data-ttu-id="af663-107">Функциональные возможности служебной шины сравнимы с возможностями локальных брокеров сообщений прежних версий высшего класса и часто превосходят эти возможности.</span><span class="sxs-lookup"><span data-stu-id="af663-107">The Service Bus feature capabilities are comparable and often exceed those of high-end, on-premises legacy message brokers.</span></span> <span data-ttu-id="af663-108">Компоненты служебной шины можно загрузить с помощью стандартизированных протоколов, таких как AMQP 1.0 и HTTPS. Все действия протокола задокументированы, что обеспечивает полное взаимодействие.</span><span class="sxs-lookup"><span data-stu-id="af663-108">The Service Bus features are available via standards-based protocols like AMQP 1.0 and HTTPS and all protocol gestures are fully documented, allowing for broad interoperability.</span></span> 

<span data-ttu-id="af663-109">Служебная шина уровня "Премиум" в первую очередь предназначена для надежного обмена сообщениями с высоким уровнем доступности. Кроме того, она обеспечивает конкурентную пропускную способность даже при масштабных развертываниях в локальном центре обработки данных, но не предоставляет выбор оборудования и процессы приобретения, планирование и выполнение развертывания, а также бесконечные сеансы оптимизации производительности.</span><span class="sxs-lookup"><span data-stu-id="af663-109">Focusing on highly available and reliable durable messaging, the Service Bus Premium provides competitive throughput performance even with substantial local datacenter deployments, but without hardware selection and acquisition processes, deployment planning and execution, and endless performance optimization sessions.</span></span> 

<span data-ttu-id="af663-110">Служебная шина уровня "Премиум" — это полностью управляемое предложение с выделенной емкостью, зарезервированной для каждого клиента, которое обеспечивает прогнозируемую производительность. Кроме того, оно отличается простой моделью ценообразования в зависимости от емкости и очень низкой общей стоимостью по сравнению с коммерческими локальными брокерами.</span><span class="sxs-lookup"><span data-stu-id="af663-110">Service Bus Premium is a fully managed offering with dedicated capacity reserved for each tenant that yields predictable performance with a simple, capacity-oriented pricing model and at extremely lower overall cost than commercial on-premises brokers.</span></span> <span data-ttu-id="af663-111">Для многих пользователей служебная шина уровня "Премиум" может заменить выделенные локальные кластеры обмена сообщениями, даже если вложенные рабочие нагрузки не выполняются в облаке.</span><span class="sxs-lookup"><span data-stu-id="af663-111">For many customers, Service Bus Premium can replace dedicated on-premises messaging clusters today, even if the attached workloads do not run in the cloud.</span></span> 

<span data-ttu-id="af663-112">Дополнительные сведения об основных понятиях, касающихся служебной шины, см. [в документации по обмену сообщениями](https://docs.microsoft.com/azure/service-bus-messaging/).</span><span class="sxs-lookup"><span data-stu-id="af663-112">Learn more about Service Bus concepts [in the messaging documentation section](https://docs.microsoft.com/azure/service-bus-messaging/)</span></span> 

<span data-ttu-id="af663-113">Для разработчиков Java служебная шина предоставляет собственный API с поддержкой корпорации Майкрософт. Служебную шину можно также использовать с библиотеками, совместимыми с AMQP 1.0, например с поставщиком JMS Apache Qpid Proton.</span><span class="sxs-lookup"><span data-stu-id="af663-113">For Java developers, Service Bus provides a Microsoft supported native API and Service Bus can also be used with AMQP 1.0 compliant libraries such as Apache Qpid Proton's JMS provider.</span></span>

## <a name="client-library"></a><span data-ttu-id="af663-114">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="af663-114">Client library</span></span>

<span data-ttu-id="af663-115">Официальный клиент служебной шины в [формате исходного кода доступен на сайте GitHub](https://github.com/azure/azure-service-bus-java), а двоичные файлы и упакованные файлы с исходным кодом — [в центральном репозитории Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).</span><span class="sxs-lookup"><span data-stu-id="af663-115">The official Service Bus client is available in [source code form on GitHub](https://github.com/azure/azure-service-bus-java) and binaries and packaged sources [are available on Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).</span></span>

<span data-ttu-id="af663-116">**[Репозиторий с примерами кода](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) содержит следующие примеры:**</span><span class="sxs-lookup"><span data-stu-id="af663-116">**The [sample code repository](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) contains samples for:**</span></span>
* <span data-ttu-id="af663-117">Как использовать [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java)</span><span class="sxs-lookup"><span data-stu-id="af663-117">How to use the [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java)</span></span>
* <span data-ttu-id="af663-118">Как использовать [TopicClient и SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java)</span><span class="sxs-lookup"><span data-stu-id="af663-118">How to use the [TopicClient and SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java)</span></span>
* <span data-ttu-id="af663-119">Как использовать сообщения [MessageSender и MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) из служебной шины</span><span class="sxs-lookup"><span data-stu-id="af663-119">How to use [MessageSender and MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) messages from Service Bus.</span></span>

<span data-ttu-id="af663-120">Добавьте зависимость в файл `pom.xml` проекта Maven, чтобы использовать библиотеку в своем проекте.</span><span class="sxs-lookup"><span data-stu-id="af663-120">Add a dependency to your Maven project's `pom.xml` file to use the library in your own project.</span></span> <span data-ttu-id="af663-121">Укажите версию в случае необходимости.</span><span class="sxs-lookup"><span data-stu-id="af663-121">Specify the version as desired.</span></span>

<span data-ttu-id="af663-122">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="af663-122">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

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
> <span data-ttu-id="af663-123">[Просмотр клиентских API](/java/api/overview/azure/servicebus/client)
> [См. дополнительные примеры здесь (дополнительные сведения см. также по ссылкам выше)](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/)</span><span class="sxs-lookup"><span data-stu-id="af663-123">[Explore the Client APIs](/java/api/overview/azure/servicebus/client)
[Find more examples here (See also above for more details)](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/)</span></span>

## <a name="management-api"></a><span data-ttu-id="af663-124">API управления</span><span class="sxs-lookup"><span data-stu-id="af663-124">Management API</span></span>

<span data-ttu-id="af663-125">Создание пространств имен, разделов, очередей и подписок и управление ими с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="af663-125">Create and manage namespaces, topics, queues, and subscriptions with the management API.</span></span>

<span data-ttu-id="af663-126">**Несколько примеров см. здесь:**</span><span class="sxs-lookup"><span data-stu-id="af663-126">**Please find some examples here:**</span></span>
* [<span data-ttu-id="af663-127">Управление очередями служебной шины</span><span class="sxs-lookup"><span data-stu-id="af663-127">Manage Service Bus queues</span></span>](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
* [<span data-ttu-id="af663-128">Создание разделов и подписок служебной шины</span><span class="sxs-lookup"><span data-stu-id="af663-128">Create and subscribe to Service Bus topics</span></span>](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)

<span data-ttu-id="af663-129">**Использование API управления в проекте:**
\\</span><span class="sxs-lookup"><span data-stu-id="af663-129">**Use the Management API in your project:**
\\</span></span>
<span data-ttu-id="af663-130">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="af663-130">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-servicebus</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="af663-131">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="af663-131">Explore the Management APIs</span></span>](/java/api/overview/azure/servicebus/management)

<span data-ttu-id="af663-132">Ознакомьтесь с другими [примерами кода Java для служебной шины Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=bus), которые можно использовать в приложениях.</span><span class="sxs-lookup"><span data-stu-id="af663-132">Explore more [sample Java code for Azure Service Bus](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) you can use in your apps.</span></span>
