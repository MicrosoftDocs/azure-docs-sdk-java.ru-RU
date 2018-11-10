---
title: Библиотеки службы хранилища Azure для Java
description: ''
keywords: Azure, Java, SDK, API, Storage
author: douge
ms.author: seguler
manager: dineshm
ms.date: 10/29/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: 68a5fdbf8e2fbfe83f9ea09112d64488e0c11d08
ms.sourcegitcommit: 66f3dd4bdb09712b73c9194e23028567c0c4ee3f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2018
ms.locfileid: "50235255"
---
# <a name="azure-storage-libraries-for-java"></a>Библиотеки службы хранилища Azure для Java

## <a name="overview"></a>Обзор

Чтение и запись данных BLOB-объектов, файлов и сообщений в приложениях Java с помощью [службы хранилища Azure](/azure/storage/storage-introduction).

Чтобы приступить к работе со службой хранилища Azure, см. руководство по [использованию хранилища BLOB-объектов из пакета SDK для Java версии 7](/azure/storage/blobs/storage-quickstart-blobs-java).

## <a name="client-library"></a>Клиентская библиотека

Для авторизации в службе хранилища Azure используйте общий ключ, маркер SAS или токен OAuth, получаемый от службы Azure Active Directory. После чего можно использовать классы и методы из клиентских библиотек для работы с хранилищем BLOB-объектов, файлов и очередей. 

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.   

**Зависимость для устаревшего пакета SDK службы хранилища Azure версии 7**:
```XML
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/azure-storage -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>8.0.0</version>
</dependency>
```

### <a name="example"></a>Пример

Запишите файл изображения из локальной файловой системы в новый BLOB-объект в существующем контейнере BLOB-объектов службы хранилища Azure.


```java
// Parse the connection string and create a blob client to interact with Blob storage
CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient blobClient = storageAccount.createCloudBlobClient();
CloudBlobContainer container = blobClient.getContainerReference("quickstartcontainer");

// Create the container if it does not exist with public access.
container.createIfNotExists(BlobContainerPublicAccessType.CONTAINER, new BlobRequestOptions(), new OperationContext());         
```

> [!div class="nextstepaction"]
> [Обзор клиентских API-интерфейсов](/java/api/overview/azure/storage/client)

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
> [Обзор API-интерфейсов управления](/java/api/overview/azure/storage/management)


## <a name="samples"></a>Примеры

[Пакет SDK Java для службы хранилища Azure](https://github.com/azure/azure-storage-java)
[Чтение и запись объектов в хранилище BLOB-объектов](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart)   
[Чтение и запись сообщений с помощью очередей](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
