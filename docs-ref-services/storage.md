---
title: Библиотеки службы хранилища Azure для Java
description: ''
keywords: Azure, Java, SDK, API, Storage
author: douge
ms.author: douge
manager: douge
ms.date: 10/19/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: fba48dfa04f223dce72a0ee54da967565ebd3687
ms.sourcegitcommit: 67b3542b174e8448f9ca3e7c9506f1216ea6a8fe
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/08/2018
ms.locfileid: "51285674"
---
# <a name="azure-storage-libraries-for-java"></a>Библиотеки службы хранилища Azure для Java

## <a name="overview"></a>Обзор

Чтение и запись данных BLOB-объектов, файлов и сообщений в приложениях Java с помощью [службы хранилища Azure](/azure/storage/storage-introduction).

Чтобы приступить к работе со службой хранилища Azure, ознакомьтесь со статьей [Использование хранилища BLOB-объектов из Java](/azure/storage/blobs/storage-quickstart-blobs-java-v10).

## <a name="client-library"></a>Клиентская библиотека

Для авторизации в службе хранилища Azure используйте общий ключ, маркер SAS или токен OAuth, получаемый от службы Azure Active Directory. После чего можно использовать классы и методы из клиентских библиотек для работы с хранилищем BLOB-объектов, файлов и очередей. 

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.   

**Зависимость для службы BLOB-объектов**:
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-blob</artifactId>
    <version>10.1.0</version>
</dependency>
```

**Зависимость для службы очередей**:
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-queue</artifactId>
    <version>10.0.0-Preview</version>
</dependency>
```


### <a name="example"></a>Пример

Запишите файл изображения из локальной файловой системы в новый BLOB-объект в существующем контейнере BLOB-объектов службы хранилища Azure.


```java
// Retrieve the credentials and initialize SharedKeyCredentials
String accountName = System.getenv("AZURE_STORAGE_ACCOUNT");
String accountKey = System.getenv("AZURE_STORAGE_ACCESS_KEY");

// Create a BlockBlobURL to run operations on Block Blobs. Alternatively create a ServiceURL, or ContainerURL for operations on Blob service, and Blob containers
SharedKeyCredentials creds = new SharedKeyCredentials(accountName, accountKey);

// We are using a default pipeline here, you can learn more about it at https://github.com/Azure/azure-storage-java/wiki/Azure-Storage-Java-V10-Overview
final BlockBlobURL blobURL = new BlockBlobURL(
    new URL("https://" + accountName + ".blob.core.windows.net/mycontainer/myimage.jpg"), 
        StorageURL.createPipeline(creds, new PipelineOptions())
);

AsynchronousFileChannel fileChannel = AsynchronousFileChannel.open(Paths.get("myimage.jpg"));
TransferManager.uploadFileToBlockBlob(fileChannel, blobURL,0, null).blockingGet();
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
