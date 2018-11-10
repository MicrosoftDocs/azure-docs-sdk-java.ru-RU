---
title: Библиотеки службы "Сетка событий Azure" для Java
description: Справочная документация по библиотекам службы "Сетка событий Azure" для Java
keywords: Azure, Java, SDK, API, event grid, messaging, event driven
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 07/11/2017
ms.topic: managed-reference
ms.devlang: java
ms.service: event-grid
ms.openlocfilehash: 35acbdeede2fbc541128029ad43f149209a057c4
ms.sourcegitcommit: db36eeb667a0bfe6d113953bb0583240db61b0f4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/26/2018
ms.locfileid: "50134636"
---
# <a name="azure-event-grid-libraries-for-java"></a><span data-ttu-id="8af5a-104">Библиотеки службы "Сетка событий Azure" для Java</span><span class="sxs-lookup"><span data-stu-id="8af5a-104">Azure Event Grid libraries for Java</span></span>

<span data-ttu-id="8af5a-105">Создавайте управляемые событиями приложения, которые прослушивают события от служб Azure и пользовательских источников и реагируют на них, с помощью службы "Сетка событий Azure" и простых средств обработки событий на основе HTTP.</span><span class="sxs-lookup"><span data-stu-id="8af5a-105">Build event-driven applications that listen and react to events from Azure services and custom sources using simple HTTP-based event handling with Azure Event Grid.</span></span>

<span data-ttu-id="8af5a-106">См. дополнительные сведения о [службе "Сетка событий Azure"](/azure/event-grid/overview) и начните работу с помощью [краткого руководства по событиям хранилища BLOB-объектов Azure](/azure/storage/blobs/storage-blob-event-quickstart).</span><span class="sxs-lookup"><span data-stu-id="8af5a-106">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart).</span></span> 

## <a name="client-sdk"></a><span data-ttu-id="8af5a-107">Клиентский пакет SDK</span><span class="sxs-lookup"><span data-stu-id="8af5a-107">Client SDK</span></span>

<span data-ttu-id="8af5a-108">Создавайте события, выполняйте аутентификацию и публикацию в разделы с помощью клиентского пакета SDK для службы "Сетка событий Azure".</span><span class="sxs-lookup"><span data-stu-id="8af5a-108">Create events, authenticate, and post to topics using the Azure Event Grid Client SDK.</span></span>

<span data-ttu-id="8af5a-109">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="8af5a-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventgrid</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="publish-events"></a><span data-ttu-id="8af5a-110">Публикация событий</span><span class="sxs-lookup"><span data-stu-id="8af5a-110">Publish events</span></span>

<span data-ttu-id="8af5a-111">Следующий код выполняет аутентификацию с помощью Azure и публикует `List` из событий `EventGridEvent` пользовательского типа (в этом примере — `Contoso.Items.ItemsReceived`) в раздел.</span><span class="sxs-lookup"><span data-stu-id="8af5a-111">The following code authenticates with Azure and publishes a `List` of  `EventGridEvent` events of a custom type (in this example, `Contoso.Items.ItemsReceived` ) to a topic.</span></span> <span data-ttu-id="8af5a-112">Раздел ключа и адрес конечной точки, используемые в примере, можно получить с помощью Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="8af5a-112">The topic key and endpoint address used in the sample can be retrieved from the Azure CLI:</span></span>

```azurecli-interactive
az eventgrid topic show -g gridResourceGroup -n topicName
az eventgrid topic key list -g gridResourceGroup -n topicName
```

```java
// Create an event grid client.
TopicCredentials topicCredentials = new TopicCredentials(System.getenv("EVENTGRID_TOPIC_KEY"));
EventGridClient client = new EventGridClientImpl(topicCredentials);

// Publish custom events to the EventGrid.
System.out.println("Publish custom events to the EventGrid");
List<EventGridEvent> eventsList = new ArrayList<>();
for (int i = 0; i < 5; i++) {
    eventsList.add(new EventGridEvent(
        UUID.randomUUID().toString(),
        String.format("Door%d", i),
        new ContosoItemReceivedEventData("Contoso Item SKU #1"),
        "Contoso.Items.ItemReceived",
        DateTime.now(),
        "2.0"
    ));
}

String eventGridEndpoint = String.format("https://%s/", new URI(System.getenv("EVENTGRID_TOPIC_ENDPOINT")).getHost());

client.publishEvents(eventGridEndpoint, eventsList);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8af5a-113">Обзор клиентских API службы "Сетка событий Azure"</span><span class="sxs-lookup"><span data-stu-id="8af5a-113">Explore the Event Grid Client APIs</span></span>](/java/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="8af5a-114">Пакет SDK для управления</span><span class="sxs-lookup"><span data-stu-id="8af5a-114">Management SDK</span></span>

<span data-ttu-id="8af5a-115">Создавайте, обновляйте и удаляйте экземпляры, разделы и подписки службы "Сетка событий" с помощью пакета SDK для управления службы "Сетка событий Azure".</span><span class="sxs-lookup"><span data-stu-id="8af5a-115">Create, update, or delete Event Grid instances, topics, and subscriptions with the Event Grid management SDK.</span></span>

<span data-ttu-id="8af5a-116">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="8af5a-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.16.0</version>
</dependency>
```   

<span data-ttu-id="8af5a-117">В следующем примере создается подписка "Сетка событий" (см. [примеры EventGrid Java](https://github.com/Azure-Samples/event-grid-java-publish-consume-events)).</span><span class="sxs-lookup"><span data-stu-id="8af5a-117">The following example creates an Event Grid subscription, taken from the [EventGrid Java samples](https://github.com/Azure-Samples/event-grid-java-publish-consume-events)</span></span>

```java
// Create an event grid subscription.
//
System.out.println("Creating an Azure EventGrid Subscription");

EventSubscription eventSubscription = eventGridManager.eventSubscriptions().define(eventSubscriptionName)
    .withScope(eventGridTopic.id())
    .withDestination(new EventHubEventSubscriptionDestination()
        .withResourceId(eventHub.id()))
    .withFilter(new EventSubscriptionFilter()
        .withIsSubjectCaseSensitive(false)
        .withSubjectBeginsWith("")
        .withSubjectEndsWith(""))
    .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8af5a-118">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="8af5a-118">Explore the management APIs</span></span>](/java/api/overview/azure/eventgrid/management)