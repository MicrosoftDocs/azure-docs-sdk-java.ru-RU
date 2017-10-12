---
title: "Библиотеки службы хранилища Azure для Java"
description: 
keywords: Azure, Java, SDK, API, Storage
author: douge
ms.author: douge
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: 7ac746105d9add6c96f84389ba0016f4864247f3
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2017
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="06a1b-103">Библиотеки службы хранилища Azure для Java</span><span class="sxs-lookup"><span data-stu-id="06a1b-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="06a1b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="06a1b-104">Overview</span></span>

<span data-ttu-id="06a1b-105">Выполняйте чтение и запись файлов, данных BLOB-объектов, пар "ключ — значение" и сообщений в приложениях Java с помощью [службы хранилища Azure](/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="06a1b-105">Read and write files, blob (object) data, key-value pairs, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="06a1b-106">Чтобы приступить к работе со службой хранилища Azure, ознакомьтесь со статьей [Использование хранилища BLOB-объектов из Java](/azure/storage/storage-java-how-to-use-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="06a1b-106">To get started with Azure Storage, see [How to use Blob storage from Java](/azure/storage/storage-java-how-to-use-blob-storage).</span></span>

## <a name="client-library"></a><span data-ttu-id="06a1b-107">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="06a1b-107">Client library</span></span>

<span data-ttu-id="06a1b-108">Подключитесь к учетной записи хранения Azure с помощью [строк подключения](/azure/storage/storage-create-storage-account#manage-your-storage-account), а затем используйте классы и методы клиентских библиотек для работы с хранилищем BLOB-объектов, таблиц, файлов или очередей.</span><span class="sxs-lookup"><span data-stu-id="06a1b-108">Use [connection strings](/azure/storage/storage-create-storage-account#manage-your-storage-account) to connect to an Azure Storage account, then use the client libraries' classes and methods to work with blob, table, file, or queue storage.</span></span> 

<span data-ttu-id="06a1b-109">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="06a1b-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.3.1</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="06a1b-110">Пример</span><span class="sxs-lookup"><span data-stu-id="06a1b-110">Example</span></span>

<span data-ttu-id="06a1b-111">Запишите файл изображения из локальной файловой системы в новый большой двоичный объект в существующем контейнере больших двоичных объектов службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="06a1b-111">Write a image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


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
> [<span data-ttu-id="06a1b-112">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="06a1b-112">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/clientlibrary)

## <a name="management-api"></a><span data-ttu-id="06a1b-113">API управления</span><span class="sxs-lookup"><span data-stu-id="06a1b-113">Management API</span></span>

<span data-ttu-id="06a1b-114">Создавайте учетные записи хранения Azure и ключи подключения и управляйте ими с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="06a1b-114">Crete and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="06a1b-115">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="06a1b-115">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="06a1b-116">Пример</span><span class="sxs-lookup"><span data-stu-id="06a1b-116">Example</span></span>

<span data-ttu-id="06a1b-117">Создайте учетную запись хранилища Azure в своей подписке и получите ключи доступа для нее.</span><span class="sxs-lookup"><span data-stu-id="06a1b-117">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

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
> [<span data-ttu-id="06a1b-118">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="06a1b-118">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/managementapi)


## <a name="samples"></a><span data-ttu-id="06a1b-119">Примеры</span><span class="sxs-lookup"><span data-stu-id="06a1b-119">Samples</span></span>

<span data-ttu-id="06a1b-120">[Manage Azure storage accounts from your Java applications](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)   (Управление учетными записями хранения Azure из приложений Java)</span><span class="sxs-lookup"><span data-stu-id="06a1b-120">[Manage Azure Storage accounts](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)  </span></span>  
<span data-ttu-id="06a1b-121">[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blob-java-getting-started)  (Чтение и запись объектов в хранилище BLOB-объектов)</span><span class="sxs-lookup"><span data-stu-id="06a1b-121">[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blob-java-getting-started) </span></span>  
<span data-ttu-id="06a1b-122">[Read and write messages with queues](https://github.com/Azure-Samples/storage-queue-java-getting-started)  (Чтение и запись сообщений с помощью очередей)</span><span class="sxs-lookup"><span data-stu-id="06a1b-122">[Read and write messages with queues](https://github.com/Azure-Samples/storage-queue-java-getting-started) </span></span>  
<span data-ttu-id="06a1b-123">[Read files from blob storage in a web app](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux) (Чтение файлов из хранилища BLOB-объектов в веб-приложении)</span><span class="sxs-lookup"><span data-stu-id="06a1b-123">[Read files from blob storage in a web app](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux)</span></span>

<span data-ttu-id="06a1b-124">Ознакомьтесь с другими [примерами кода Java для службы хранилища Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=storage), которые можно использовать в приложениях.</span><span class="sxs-lookup"><span data-stu-id="06a1b-124">Explore more [sample Java code for Azure Storage](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) you can use in your apps.</span></span>