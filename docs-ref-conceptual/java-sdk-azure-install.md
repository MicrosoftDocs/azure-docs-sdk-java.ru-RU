---
title: "Документация Майкрософт по Azure для разработчиков Java"
description: "Справочник по пакету SDK и API Azure для Java"
keywords: Azure Java, Azure Java API Reference, Azure Java class library, Azure SDK
author: routlaw
manager: douge
ms.assetid: 7b92e776-959b-4632-8b1d-047ce1417616
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 10073a1b2250a37347128dd9c8faf1375b2ab6ae
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
# <a name="azure-libraries-for-java"></a><span data-ttu-id="cb38a-104">Библиотеки Azure для Java</span><span class="sxs-lookup"><span data-stu-id="cb38a-104">Azure libraries for Java</span></span>

<span data-ttu-id="cb38a-105">Благодаря библиотекам Azure службы Azure можно использовать в приложениях Java с помощью собственных интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="cb38a-105">Azure libraries help you consume Azure services in your Java apps using native interfaces.</span></span> <span data-ttu-id="cb38a-106">Каждая библиотека является независимой и может использоваться отдельно от остальных.</span><span class="sxs-lookup"><span data-stu-id="cb38a-106">Each library is independent and can be used separately from the others another.</span></span>

| | | | |
|:-------------:|:----------:|:----:|:---:|
| [<span data-ttu-id="cb38a-107">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="cb38a-107">Azure Storage</span></span>](#azure-storage) | [<span data-ttu-id="cb38a-108">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="cb38a-108">SQL Database</span></span>](#sql-database)  | [<span data-ttu-id="cb38a-109">Кэш Redis</span><span class="sxs-lookup"><span data-stu-id="cb38a-109">Redis Cache</span></span>](#redis-cache)   | [<span data-ttu-id="cb38a-110">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="cb38a-110">DocumentDB</span></span>](#documentdb) |
| [<span data-ttu-id="cb38a-111">Служебная шина</span><span class="sxs-lookup"><span data-stu-id="cb38a-111">Service Bus</span></span>](#servicebus)  | [<span data-ttu-id="cb38a-112">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb38a-112">Azure Active Directory</span></span>](#azuread) | [<span data-ttu-id="cb38a-113">хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="cb38a-113">Key Vault</span></span>](#keyvault)  | [<span data-ttu-id="cb38a-114">Концентратор событий</span><span class="sxs-lookup"><span data-stu-id="cb38a-114">Event Hub</span></span>](#eventhub)
| [<span data-ttu-id="cb38a-115">Служба Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="cb38a-115">IoT Service</span></span>](#iotservice) | [<span data-ttu-id="cb38a-116">Устройство IoT</span><span class="sxs-lookup"><span data-stu-id="cb38a-116">IoT Device</span></span>](#iotdevice) | [<span data-ttu-id="cb38a-117">Data Lake</span><span class="sxs-lookup"><span data-stu-id="cb38a-117">Data Lake</span></span>](#datalake)  | [<span data-ttu-id="cb38a-118">AppInsights</span><span class="sxs-lookup"><span data-stu-id="cb38a-118">AppInsights</span></span>](#appinsights) | 
| [<span data-ttu-id="cb38a-119">Пакетная служба</span><span class="sxs-lookup"><span data-stu-id="cb38a-119">Batch</span></span>](#batch) | [<span data-ttu-id="cb38a-120">Getting Started with Resources - Manage Resource - in Java (Приступая к работе с ресурсами: управление ресурсами в Java)</span><span class="sxs-lookup"><span data-stu-id="cb38a-120">Manage Azure resources</span></span>](#management) |

## <a name="install-with-maven"></a><span data-ttu-id="cb38a-121">Установка с помощью Maven</span><span class="sxs-lookup"><span data-stu-id="cb38a-121">Install with Maven</span></span>

<span data-ttu-id="cb38a-122">Добавьте запись зависимости в файл `pom.xml`, чтобы импортировать библиотеку в проект [Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="cb38a-122">Add a dependency entry in your `pom.xml` to import a library into your [Maven](https://maven.apache.org) project.</span></span>

<span data-ttu-id="cb38a-123">Например, чтобы включить последнюю версию [библиотек управления Azure для Java](#management), используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="cb38a-123">For example, to include the latest version of the [Azure management libraries for Java](#management):</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.1.2</version>
</dependency>
```

<span data-ttu-id="cb38a-124">Поддерживаются и другие средства сборки Java, например Gradle, но инструкции по установке с их помощью не приводятся в этой статье.</span><span class="sxs-lookup"><span data-stu-id="cb38a-124">Other Java build tools like Gradle are supported but the install steps are not provided in this article.</span></span> <span data-ttu-id="cb38a-125">Сведения об использовании импортируемых файлов Maven в средстве сборки см. в документации по этому средству.</span><span class="sxs-lookup"><span data-stu-id="cb38a-125">Review the documentation for your build tool on how to consume Maven imports.</span></span>

## <a name="azure-service-libraries"></a><span data-ttu-id="cb38a-126">Библиотеки служб Azure</span><span class="sxs-lookup"><span data-stu-id="cb38a-126">Azure service libraries</span></span>

<span data-ttu-id="cb38a-127">Расширьте функциональные возможности своих приложений, интегрировав их со службами Azure с помощью этих библиотек.</span><span class="sxs-lookup"><span data-stu-id="cb38a-127">Integrate Azure services to add functionality to your apps using these libraries.</span></span> <span data-ttu-id="cb38a-128">Дополнительные сведения о создании приложений с помощью служб Azure см. в [центре разработчиков Java](https://azure.microsoft.com/develop/java).</span><span class="sxs-lookup"><span data-stu-id="cb38a-128">Learn more about building apps with Azure services at the [Java developer center](https://azure.microsoft.com/develop/java).</span></span>

<a name="azure-storage"></a>

### <a name="azure-storageazurestoragestorage-introduction"></a>[<span data-ttu-id="cb38a-129">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="cb38a-129">Azure Storage</span></span>](/azure/storage/storage-introduction)  

<span data-ttu-id="cb38a-130">Хранение данных и обмен сообщениями в приложениях.</span><span class="sxs-lookup"><span data-stu-id="cb38a-130">Data storage and messaging for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.4.0</version>
</dependency>
```   

[<span data-ttu-id="cb38a-131">Примеры кода](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Справочник](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-131">Samples](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Reference](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Release Notes</span></span>](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)

<a name="sql-database"></a>

### <a name="sql-databaseazuresql-databasesql-database-technical-overview"></a>[<span data-ttu-id="cb38a-132">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="cb38a-132">SQL Database</span></span>](/azure/sql-database/sql-database-technical-overview)

<span data-ttu-id="cb38a-133">Драйвер JDBC для базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cb38a-133">JDBC driver for Azure SQL Database.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

[<span data-ttu-id="cb38a-134">Примеры кода](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Справочник](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-134">Samples](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Reference](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Release Notes</span></span>](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)

<a name="redis-cache"></a>

### <a name="redis-cachehttpsazuremicrosoftcomservicescache"></a>[<span data-ttu-id="cb38a-135">Кэш Redis</span><span class="sxs-lookup"><span data-stu-id="cb38a-135">Redis Cache</span></span>](https://azure.microsoft.com/services/cache/)

<span data-ttu-id="cb38a-136">Хранилище данных типа "ключ — значение" с низкими показателями задержки и высокой производительностью.</span><span class="sxs-lookup"><span data-stu-id="cb38a-136">Low-latency, high-performance key-value store.</span></span>

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```   

[<span data-ttu-id="cb38a-137">Примеры кода](/azure/redis-cache/cache-java-get-started) | [Справочник](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-137">Samples](/azure/redis-cache/cache-java-get-started) | [Reference](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Release Notes</span></span>](https://github.com/xetorthio/jedis/releases)  

<a name="documentdb"></a>

### <a name="cosmos-dbazuredocumentdbdocumentdb-introduction"></a>[<span data-ttu-id="cb38a-138">База данных Cosmos</span><span class="sxs-lookup"><span data-stu-id="cb38a-138">Cosmos DB</span></span>](/azure/documentdb/documentdb-introduction)

<span data-ttu-id="cb38a-139">Масштабируемая база данных NoSQL с документами JSON и синтаксисом запросов SQL или JavaScript.</span><span class="sxs-lookup"><span data-stu-id="cb38a-139">Scalable NoSQL database with JSON documents and a SQL or JavaScript query syntax.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

[<span data-ttu-id="cb38a-140">Примеры кода](/azure/documentdb/documentdb-java-application) | [Справочник](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-140">Samples](/azure/documentdb/documentdb-java-application) | [Reference](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Release Notes</span></span>](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)

<a name="servicebus"></a>
 
 ### <a name="servicebusazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="cb38a-141">Служебная шина</span><span class="sxs-lookup"><span data-stu-id="cb38a-141">ServiceBus</span></span>](/azure/service-bus-messaging/service-bus-messaging-overview) 
    
 <span data-ttu-id="cb38a-142">Служебная шина — это корпоративная платформа для транзакционного обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="cb38a-142">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>
 
 ```XML
 <dependency> 
     <groupId>com.microsoft.azure</groupId> 
     <artifactId>azure-servicebus</artifactId> 
     <version>1.0.0</version> 
 </dependency>   
 ```
 
 [<span data-ttu-id="cb38a-143">Примеры кода](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Справочник](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-143">Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes</span></span>](https://github.com/Azure/azure-service-bus-java)   
  
<a name="azuread"></a>

### <a name="azure-active-directoryazureactive-directoryactive-directory-whatis"></a>[<span data-ttu-id="cb38a-144">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cb38a-144">Azure Active Directory</span></span>](/azure/active-directory/active-directory-whatis)   

<span data-ttu-id="cb38a-145">Управление удостоверениями и безопасный вход для приложений.</span><span class="sxs-lookup"><span data-stu-id="cb38a-145">Identity management and secure sign-in for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```
   
[<span data-ttu-id="cb38a-146">Примеры кода](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Справочник](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-146">Samples](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Reference](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Release Notes</span></span>](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)
 
<a name="keyvault"></a>

### <a name="key-vaultazurekey-vault"></a>[<span data-ttu-id="cb38a-147">хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="cb38a-147">Key Vault</span></span>](/azure/key-vault) 

<span data-ttu-id="cb38a-148">Ключи и секреты для безопасного доступа из приложений.</span><span class="sxs-lookup"><span data-stu-id="cb38a-148">Safely access keys and secrets from your applications.</span></span> 

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

[<span data-ttu-id="cb38a-149">Примеры кода](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Справочник](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-149">Samples](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Reference](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Release Notes</span></span>](https://github.com/Azure/azure-keyvault-java) 

<a name="eventhub"></a>

### <a name="event-hubazureevent-hubsevent-hubs-what-is-event-hubs"></a>[<span data-ttu-id="cb38a-150">Концентратор событий</span><span class="sxs-lookup"><span data-stu-id="cb38a-150">Event Hub</span></span>](/azure/event-hubs/event-hubs-what-is-event-hubs) 
   
<span data-ttu-id="cb38a-151">Обработка событий и данных телеметрии с высокой пропускной способностью для сценариев инструментирования или сценариев Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cb38a-151">High-throughput event and telemetry handling for your instrumentation or IoT scenarios.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-eventhubs</artifactId> 
    <version>0.14.4</version> 
</dependency>   
```

[<span data-ttu-id="cb38a-152">Примеры кода](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Справочник](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-152">Samples](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Reference](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Release Notes</span></span>](https://github.com/Azure/azure-event-hubs-java)

<a name="iotservice"></a> 

### <a name="iot-serviceazureiot-hub"></a>[<span data-ttu-id="cb38a-153">Служба Интернета вещей</span><span class="sxs-lookup"><span data-stu-id="cb38a-153">IoT Service</span></span>](/azure/iot-hub/)

<span data-ttu-id="cb38a-154">Управление удостоверениями, отправка сообщений и получение отчетов об ошибках с устройств, зарегистрированных в Центре Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cb38a-154">Manage identities, send messages, and get feedback from devices registered with your IoT hub.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.7.23</version>
</dependency>
```   
   
[<span data-ttu-id="cb38a-155">Примеры кода](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Справочник](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-155">Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes</span></span>](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="iotdevice"></a> 

### <a name="iot-deviceazureiot-hubiot-hub-devguide"></a>[<span data-ttu-id="cb38a-156">Устройство IoT</span><span class="sxs-lookup"><span data-stu-id="cb38a-156">IoT Device</span></span>](/azure/iot-hub/iot-hub-devguide)

<span data-ttu-id="cb38a-157">Отправка сообщений с устройства в Центр Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="cb38a-157">Send a message to an IoT hub from your device.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.32</version>
</dependency>
```  

[<span data-ttu-id="cb38a-158">Примеры кода](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Справочник](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-158">Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes</span></span>](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="datalake"></a> 

### <a name="data-lake-storeazuredata-lake-storedata-lake-store-overview"></a>[<span data-ttu-id="cb38a-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cb38a-159">Data Lake Store</span></span>](/azure/data-lake-store/data-lake-store-overview)   
   
<span data-ttu-id="cb38a-160">Централизованный сбор данных любого размера и формы для выполнения анализа.</span><span class="sxs-lookup"><span data-stu-id="cb38a-160">Capture data of any size and shape into a single location for performing analytics.</span></span>    

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

[<span data-ttu-id="cb38a-161">Примеры кода](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Справочник](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-161">Samples](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Reference](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Release Notes</span></span>](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)

<a name="appinsights"></a> 

### <a name="appinsightsazureapplication-insightsapp-insights-overview"></a>[<span data-ttu-id="cb38a-162">AppInsights</span><span class="sxs-lookup"><span data-stu-id="cb38a-162">AppInsights</span></span>](/azure/application-insights/app-insights-overview)

<span data-ttu-id="cb38a-163">Отслеживание использования, добавление телеметрии и мониторинг веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="cb38a-163">Track usage, add telemetry, and monitor your web apps.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>
    <version>1.0.8</version>
</dependency>
```

[<span data-ttu-id="cb38a-164">Примеры кода](/azure/application-insights/app-insights-java-get-started) | [Справочник](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-164">Samples](/azure/application-insights/app-insights-java-get-started) | [Reference](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Release Notes</span></span>](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)

<a name="batch"></a>

### <a name="batchazurebatch"></a>[<span data-ttu-id="cb38a-165">Пакетная служба</span><span class="sxs-lookup"><span data-stu-id="cb38a-165">Batch</span></span>](/azure/batch)

<span data-ttu-id="cb38a-166">Обеспечение эффективной работы приложений для крупномасштабных параллельных и высокопроизводительных вычислений в облаке.</span><span class="sxs-lookup"><span data-stu-id="cb38a-166">Run large-scale parallel and high-performance computing applications efficiently in the cloud.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```

[<span data-ttu-id="cb38a-167">Примеры кода](https://github.com/azure/azure-batch-samples) | [Справочник](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-167">Samples](https://github.com/azure/azure-batch-samples) | [Reference](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Release Notes</span></span>](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)

<a name="management"></a> 

## <a name="manage-azure-resources"></a><span data-ttu-id="cb38a-168">Управление ресурсами Azure</span><span class="sxs-lookup"><span data-stu-id="cb38a-168">Manage Azure resources</span></span>

<span data-ttu-id="cb38a-169">Создание, обновление и удаление ресурсов Azure в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="cb38a-169">Create, update, and delete Azure resources from your application code.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.1.2</version>
</dependency>
```

[<span data-ttu-id="cb38a-170">Примеры кода](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Справочник](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-170">Samples](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Reference](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Release Notes</span></span>](java-sdk-azure-release-notes.md)

<a name="servicebus"></a>

### <a name="servicebushttpsdocsmicrosoftcomen-usazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="cb38a-171">Служебная шина</span><span class="sxs-lookup"><span data-stu-id="cb38a-171">ServiceBus</span></span>](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview) 
   
<span data-ttu-id="cb38a-172">Служебная шина — это корпоративная платформа для транзакционного обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="cb38a-172">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-servicebus</artifactId> 
    <version>1.0.0</version> 
</dependency>   
```

[<span data-ttu-id="cb38a-173">Примеры кода](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Справочник](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="cb38a-173">Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes</span></span>](https://github.com/Azure/azure-service-bus-java)

