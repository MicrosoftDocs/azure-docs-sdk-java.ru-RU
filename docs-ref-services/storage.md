---
title: "Библиотеки службы хранилища Azure для Java"
description: 
keywords: Azure, Java, SDK, API, Storage
author: douge
ms.author: douge
manager: douge
ms.date: 02/07/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: 3c7a3a1fcf2e97202e7f38f8df5acb6637fb4b47
ms.sourcegitcommit: 2ae0d99c02f4ad7efa9e3d3fbd1db7e9de20c6e7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/14/2018
---
# <a name="azure-storage-libraries-for-java"></a>Библиотеки службы хранилища Azure для Java

## <a name="overview"></a>Обзор

Выполняйте чтение и запись файлов, данных BLOB-объектов, пар "ключ — значение" и сообщений в приложениях Java с помощью [службы хранилища Azure](/azure/storage/storage-introduction).

Чтобы приступить к работе со службой хранилища Azure, ознакомьтесь со статьей [Использование хранилища BLOB-объектов из Java](/azure/storage/storage-java-how-to-use-blob-storage).

## <a name="client-library"></a>Клиентская библиотека

Подключитесь к учетной записи хранения Azure с помощью [строк подключения](/azure/storage/storage-create-storage-account#manage-your-storage-account), а затем используйте классы и методы клиентских библиотек для работы с хранилищем BLOB-объектов, таблиц, файлов или очередей. 

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>7.0.0</version>
</dependency>
```   

### <a name="example"></a>Пример

Запишите файл изображения из локальной файловой системы в новый большой двоичный объект в существующем контейнере больших двоичных объектов службы хранилища Azure.


```java
String storageConnectionString = "DefaultEndpointsProtocol=https;" + 
"AccountName=fabrikamblobstorage;" + 
"AccountKey=keyvalue;EndpointSuffix=core.windows.net";

CloudStorageAccount account = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient serviceClient = account.createCloudBlobClient();
CloudBlobContainer container = serviceClient.getContainerReference(blobContainer);

// write a blob from a local filesystem path to the container as logo.png
CloudBlockBlob blob = container.getBlockBlobReference("logo.png");
blob.uploadFromFile("/Users/raisa/fabrikam.png");
```

> [!div class="nextstepaction"]
> [Обзор клиентских API-интерфейсов](/java/api/overview/azure/storage/clientlibrary)

## <a name="management-api"></a>API управления

Создавайте учетные записи хранения Azure и ключи подключения и управляйте ими с помощью API управления.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a>Пример

Создайте учетную запись хранилища Azure в своей подписке и получите ключи доступа для нее.

```java
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
        .withRegion(Region.US_EAST)
        .withNewResourceGroup(rgName)
        .create();

// get a list of storage account keys related to the account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/java/api/overview/azure/storage/managementapi)


## <a name="samples"></a>Примеры

[Manage Azure storage accounts from your Java applications](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)   (Управление учетными записями хранения Azure из приложений Java)  
[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blob-java-getting-started)  (Чтение и запись объектов в хранилище BLOB-объектов)  
[Read and write messages with queues](https://github.com/Azure-Samples/storage-queue-java-getting-started)  (Чтение и запись сообщений с помощью очередей)  
[Read files from blob storage in a web app](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux) (Чтение файлов из хранилища BLOB-объектов в веб-приложении)

Ознакомьтесь с другими [примерами кода Java для службы хранилища Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=storage), которые можно использовать в приложениях.
