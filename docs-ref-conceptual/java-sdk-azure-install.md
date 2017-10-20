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
ms.openlocfilehash: 570f820e1349e1dfd01a6c7f323b5312c14c40c6
ms.sourcegitcommit: 4b63ecd2c92a9115dfae018618e4e4046b061b3e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/14/2017
---
# <a name="azure-libraries-for-java"></a>Библиотеки Azure для Java

Благодаря библиотекам Azure службы Azure можно использовать в приложениях Java с помощью собственных интерфейсов. Каждая библиотека является независимой и может использоваться отдельно от остальных.

| | | | |
|:-------------:|:----------:|:----:|:---:|
| [Хранилище Azure](#azure-storage) | [База данных SQL](#sql-database)  | [Кэш Redis](#redis-cache)   | [DocumentDB](#documentdb) |
| [Служебная шина](#servicebus)  | [Azure Active Directory](#azuread) | [хранилище ключей;](#keyvault)  | [Концентратор событий](#eventhub)
| [Служба Интернета вещей](#iotservice) | [Устройство IoT](#iotdevice) | [Data Lake](#datalake)  | [AppInsights](#appinsights) | 
| [Пакетная служба](#batch) | [Getting Started with Resources - Manage Resource - in Java (Приступая к работе с ресурсами: управление ресурсами в Java)](#management) |

## <a name="install-with-maven"></a>Установка с помощью Maven

Добавьте запись зависимости в файл `pom.xml`, чтобы импортировать библиотеку в проект [Maven](https://maven.apache.org).

Например, чтобы включить последнюю версию [библиотек управления Azure для Java](#management), используйте следующий код:

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

Поддерживаются и другие средства сборки Java, например Gradle, но инструкции по установке с их помощью не приводятся в этой статье. Сведения об использовании импортируемых файлов Maven в средстве сборки см. в документации по этому средству.

## <a name="azure-service-libraries"></a>Библиотеки служб Azure

Расширьте функциональные возможности своих приложений, интегрировав их со службами Azure с помощью этих библиотек. Дополнительные сведения о создании приложений с помощью служб Azure см. в [центре разработчиков Java](https://azure.microsoft.com/develop/java).

<a name="azure-storage"></a>

### <a name="azure-storageazurestoragestorage-introduction"></a>[Хранилище Azure](/azure/storage/storage-introduction)  

Хранение данных и обмен сообщениями в приложениях.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.4.0</version>
</dependency>
```   

[Примеры кода](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Справочник](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Заметки о выпуске](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)

<a name="sql-database"></a>

### <a name="sql-databaseazuresql-databasesql-database-technical-overview"></a>[База данных SQL](/azure/sql-database/sql-database-technical-overview)

Драйвер JDBC для базы данных SQL Azure.

```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

[Примеры кода](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Справочник](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Заметки о выпуске](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)

<a name="redis-cache"></a>

### <a name="redis-cachehttpsazuremicrosoftcomservicescache"></a>[Кэш Redis](https://azure.microsoft.com/services/cache/)

Хранилище данных типа "ключ — значение" с низкими показателями задержки и высокой производительностью.

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```   

[Примеры кода](/azure/redis-cache/cache-java-get-started) | [Справочник](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Заметки о выпуске](https://github.com/xetorthio/jedis/releases)  

<a name="documentdb"></a>

### <a name="cosmos-dbazuredocumentdbdocumentdb-introduction"></a>[База данных Cosmos](/azure/documentdb/documentdb-introduction)

Масштабируемая база данных NoSQL с документами JSON и синтаксисом запросов SQL или JavaScript.   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

[Примеры кода](/azure/documentdb/documentdb-java-application) | [Справочник](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Заметки о выпуске](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)

<a name="servicebus"></a>
 
 ### <a name="servicebusazureservice-bus-messagingservice-bus-messaging-overview"></a>[Служебная шина](/azure/service-bus-messaging/service-bus-messaging-overview) 
    
 Служебная шина — это корпоративная платформа для транзакционного обмена сообщениями.
 
 ```XML
 <dependency> 
     <groupId>com.microsoft.azure</groupId> 
     <artifactId>azure-servicebus</artifactId> 
     <version>1.0.0</version> 
 </dependency>   
 ```
 
 [Примеры кода](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Справочник](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Заметки о выпуске](https://github.com/Azure/azure-service-bus-java)   
  
<a name="azuread"></a>

### <a name="azure-active-directoryazureactive-directoryactive-directory-whatis"></a>[Azure Active Directory](/azure/active-directory/active-directory-whatis)   

Управление удостоверениями и безопасный вход для приложений.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```
   
[Примеры кода](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Справочник](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Заметки о выпуске](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)
 
<a name="keyvault"></a>

### <a name="key-vaultazurekey-vault"></a>[хранилище ключей;](/azure/key-vault) 

Ключи и секреты для безопасного доступа из приложений. 

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

[Примеры кода](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Справочник](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Заметки о выпуске](https://github.com/Azure/azure-keyvault-java) 

<a name="eventhub"></a>

### <a name="event-hubazureevent-hubsevent-hubs-what-is-event-hubs"></a>[Концентратор событий](/azure/event-hubs/event-hubs-what-is-event-hubs) 
   
Обработка событий и данных телеметрии с высокой пропускной способностью для сценариев инструментирования или сценариев Интернета вещей.

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-eventhubs</artifactId> 
    <version>0.14.4</version> 
</dependency>   
```

[Примеры кода](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Справочник](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Заметки о выпуске](https://github.com/Azure/azure-event-hubs-java)

<a name="iotservice"></a> 

### <a name="iot-serviceazureiot-hub"></a>[Служба Интернета вещей](/azure/iot-hub/)

Управление удостоверениями, отправка сообщений и получение отчетов об ошибках с устройств, зарегистрированных в Центре Интернета вещей.

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.7.23</version>
</dependency>
```   
   
[Примеры кода](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Справочник](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Заметки о выпуске](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="iotdevice"></a> 

### <a name="iot-deviceazureiot-hubiot-hub-devguide"></a>[Устройство IoT](/azure/iot-hub/iot-hub-devguide)

Отправка сообщений с устройства в Центр Интернета вещей.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.32</version>
</dependency>
```  

[Примеры кода](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Справочник](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Заметки о выпуске](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="datalake"></a> 

### <a name="data-lake-storeazuredata-lake-storedata-lake-store-overview"></a>[Data Lake Store](/azure/data-lake-store/data-lake-store-overview)   
   
Централизованный сбор данных любого размера и формы для выполнения анализа.    

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

[Примеры кода](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Справочник](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Заметки о выпуске](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)

<a name="appinsights"></a> 

### <a name="appinsightsazureapplication-insightsapp-insights-overview"></a>[AppInsights](/azure/application-insights/app-insights-overview)

Отслеживание использования, добавление телеметрии и мониторинг веб-приложений.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>
    <version>1.0.8</version>
</dependency>
```

[Примеры кода](/azure/application-insights/app-insights-java-get-started) | [Справочник](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Заметки о выпуске](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)

<a name="batch"></a>

### <a name="batchazurebatch"></a>[Пакетная служба](/azure/batch)

Обеспечение эффективной работы приложений для крупномасштабных параллельных и высокопроизводительных вычислений в облаке.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```

[Примеры кода](https://github.com/azure/azure-batch-samples) | [Справочник](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Заметки о выпуске](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)

<a name="management"></a> 

## <a name="manage-azure-resources"></a>Управление ресурсами Azure

Создание, обновление и удаление ресурсов Azure в коде приложения.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

[Примеры кода](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Справочник](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Заметки о выпуске](java-sdk-azure-release-notes.md)

<a name="servicebus"></a>

### <a name="servicebushttpsdocsmicrosoftcomazureservice-bus-messagingservice-bus-messaging-overview"></a>[Служебная шина](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) 
   
Служебная шина — это корпоративная платформа для транзакционного обмена сообщениями.

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-servicebus</artifactId> 
    <version>1.0.0</version> 
</dependency>   
```

[Примеры кода](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Справочник](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Заметки о выпуске](https://github.com/Azure/azure-service-bus-java)

