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
ms.openlocfilehash: ee54e92ee0084cd2fc5e827764cfe094434ea784
ms.sourcegitcommit: 1c1412ad5d8960975c3fc7fd3d1948152ef651ef
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2019
ms.locfileid: "57335377"
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="36a40-103">Библиотеки службы хранилища Azure для Java</span><span class="sxs-lookup"><span data-stu-id="36a40-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="36a40-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="36a40-104">Overview</span></span>

<span data-ttu-id="36a40-105">Чтение и запись данных BLOB-объектов, файлов и сообщений в приложениях Java с помощью [службы хранилища Azure](/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="36a40-105">Read and write blob (object) data, files, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="36a40-106">Чтобы приступить к работе со службой хранилища Azure, ознакомьтесь со статьей [Использование хранилища BLOB-объектов из Java](/azure/storage/blobs/storage-quickstart-blobs-java-v10).</span><span class="sxs-lookup"><span data-stu-id="36a40-106">To get started with Azure Storage, see [How to use Blob storage from Java](/azure/storage/blobs/storage-quickstart-blobs-java-v10).</span></span>

## <a name="client-library"></a><span data-ttu-id="36a40-107">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="36a40-107">Client library</span></span>

<span data-ttu-id="36a40-108">Для авторизации в службе хранилища Azure используйте общий ключ, маркер SAS или токен OAuth, получаемый от службы Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="36a40-108">Use a Shared Key, SAS token or an OAuth token from the Azure Active Directory to authorize with Azure Storage services.</span></span> <span data-ttu-id="36a40-109">После чего можно использовать классы и методы из клиентских библиотек для работы с хранилищем BLOB-объектов, файлов и очередей.</span><span class="sxs-lookup"><span data-stu-id="36a40-109">Then use the client libraries' classes and methods to work with blob, file, or queue storage.</span></span> 

<span data-ttu-id="36a40-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="36a40-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

<span data-ttu-id="36a40-111">**Зависимость для службы BLOB-объектов**:</span><span class="sxs-lookup"><span data-stu-id="36a40-111">**Dependency for Blob service**:</span></span>
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-blob</artifactId>
    <version>10.1.0</version>
</dependency>
```

<span data-ttu-id="36a40-112">**Зависимость для службы очередей**:</span><span class="sxs-lookup"><span data-stu-id="36a40-112">**Dependency for Queue service**:</span></span>
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-queue</artifactId>
    <version>10.0.0-Preview</version>
</dependency>
```


### <a name="example"></a><span data-ttu-id="36a40-113">Пример</span><span class="sxs-lookup"><span data-stu-id="36a40-113">Example</span></span>

<span data-ttu-id="36a40-114">Запишите файл изображения из локальной файловой системы в новый BLOB-объект в существующем контейнере BLOB-объектов службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="36a40-114">Write an image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


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
> [<span data-ttu-id="36a40-115">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="36a40-115">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="36a40-116">API управления</span><span class="sxs-lookup"><span data-stu-id="36a40-116">Management API</span></span>

<span data-ttu-id="36a40-117">Создавайте учетные записи хранения Azure и ключи подключения и управляйте ими с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="36a40-117">Create and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="36a40-118">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="36a40-118">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="36a40-119">Пример</span><span class="sxs-lookup"><span data-stu-id="36a40-119">Example</span></span>

<span data-ttu-id="36a40-120">Создайте учетную запись хранилища Azure в своей подписке и получите ключи доступа для нее.</span><span class="sxs-lookup"><span data-stu-id="36a40-120">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

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
> [<span data-ttu-id="36a40-121">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="36a40-121">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="36a40-122">Примеры</span><span class="sxs-lookup"><span data-stu-id="36a40-122">Samples</span></span>

<span data-ttu-id="36a40-123">[Пакет SDK Java для службы хранилища Azure](https://github.com/azure/azure-storage-java)
[Чтение и запись объектов в хранилище BLOB-объектов](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span><span class="sxs-lookup"><span data-stu-id="36a40-123">[Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span></span>  
[<span data-ttu-id="36a40-124">Чтение и запись сообщений с помощью очередей</span><span class="sxs-lookup"><span data-stu-id="36a40-124">Read and write messages with queues</span></span>](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
