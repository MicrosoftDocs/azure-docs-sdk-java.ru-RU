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
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="1de05-103">Библиотеки службы хранилища Azure для Java</span><span class="sxs-lookup"><span data-stu-id="1de05-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="1de05-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="1de05-104">Overview</span></span>

<span data-ttu-id="1de05-105">Чтение и запись данных BLOB-объектов, файлов и сообщений в приложениях Java с помощью [службы хранилища Azure](/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="1de05-105">Read and write blob (object) data, files, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="1de05-106">Чтобы приступить к работе со службой хранилища Azure, см. руководство по [использованию хранилища BLOB-объектов из пакета SDK для Java версии 7](/azure/storage/blobs/storage-quickstart-blobs-java).</span><span class="sxs-lookup"><span data-stu-id="1de05-106">To get started with Azure Storage, see [How to use Blob storage from Java SDK v7](/azure/storage/blobs/storage-quickstart-blobs-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="1de05-107">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="1de05-107">Client library</span></span>

<span data-ttu-id="1de05-108">Для авторизации в службе хранилища Azure используйте общий ключ, маркер SAS или токен OAuth, получаемый от службы Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1de05-108">Use a Shared Key, SAS token or an OAuth token from the Azure Active Directory to authorize with Azure Storage services.</span></span> <span data-ttu-id="1de05-109">После чего можно использовать классы и методы из клиентских библиотек для работы с хранилищем BLOB-объектов, файлов и очередей.</span><span class="sxs-lookup"><span data-stu-id="1de05-109">Then use the client libraries' classes and methods to work with blob, file, or queue storage.</span></span> 

<span data-ttu-id="1de05-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="1de05-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

<span data-ttu-id="1de05-111">**Зависимость для устаревшего пакета SDK службы хранилища Azure версии 7**:</span><span class="sxs-lookup"><span data-stu-id="1de05-111">**Dependency for the legacy Azure Storage SDK v7**:</span></span>
```XML
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/azure-storage -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>8.0.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="1de05-112">Пример</span><span class="sxs-lookup"><span data-stu-id="1de05-112">Example</span></span>

<span data-ttu-id="1de05-113">Запишите файл изображения из локальной файловой системы в новый BLOB-объект в существующем контейнере BLOB-объектов службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="1de05-113">Write an image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


```java
// Parse the connection string and create a blob client to interact with Blob storage
CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient blobClient = storageAccount.createCloudBlobClient();
CloudBlobContainer container = blobClient.getContainerReference("quickstartcontainer");

// Create the container if it does not exist with public access.
container.createIfNotExists(BlobContainerPublicAccessType.CONTAINER, new BlobRequestOptions(), new OperationContext());         
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="1de05-114">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="1de05-114">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="1de05-115">API управления</span><span class="sxs-lookup"><span data-stu-id="1de05-115">Management API</span></span>

<span data-ttu-id="1de05-116">Создавайте учетные записи хранения Azure и ключи подключения и управляйте ими с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="1de05-116">Crete and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="1de05-117">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="1de05-117">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="1de05-118">Пример</span><span class="sxs-lookup"><span data-stu-id="1de05-118">Example</span></span>

<span data-ttu-id="1de05-119">Создайте учетную запись хранилища Azure в своей подписке и получите ключи доступа для нее.</span><span class="sxs-lookup"><span data-stu-id="1de05-119">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

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
> [<span data-ttu-id="1de05-120">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="1de05-120">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="1de05-121">Примеры</span><span class="sxs-lookup"><span data-stu-id="1de05-121">Samples</span></span>

<span data-ttu-id="1de05-122">[Пакет SDK Java для службы хранилища Azure](https://github.com/azure/azure-storage-java)
[Чтение и запись объектов в хранилище BLOB-объектов](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span><span class="sxs-lookup"><span data-stu-id="1de05-122">[Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span></span>  
[<span data-ttu-id="1de05-123">Чтение и запись сообщений с помощью очередей</span><span class="sxs-lookup"><span data-stu-id="1de05-123">Read and write messages with queues</span></span>](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
