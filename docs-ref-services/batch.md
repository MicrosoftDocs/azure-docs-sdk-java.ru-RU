---
title: "Библиотеки пакетной службы Azure для Java"
description: "Справочная документация по библиотекам пакетной службы для Java"
keywords: Azure, Java, SDK, API, Batch, processing, scheduling, long-running
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: batch
ms.openlocfilehash: dfc14b08ee39a1422cb54a3b9a80fa579e704499
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
# <a name="azure-batch-libraries-for-java"></a><span data-ttu-id="5a175-104">Библиотеки пакетной службы Azure для Java</span><span class="sxs-lookup"><span data-stu-id="5a175-104">Azure Batch libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="5a175-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="5a175-105">Overview</span></span>

<span data-ttu-id="5a175-106">Обеспечьте эффективную работу приложений для крупномасштабных параллельных и высокопроизводительных вычислений в облаке с помощью [пакетной службы Azure](/azure/batch/batch-technical-overview).</span><span class="sxs-lookup"><span data-stu-id="5a175-106">Run large-scale parallel and high-performance computing applications efficiently in the cloud with [Azure Batch](/azure/batch/batch-technical-overview).</span></span>   

<span data-ttu-id="5a175-107">Чтобы приступить к работе с пакетной службой Azure, ознакомьтесь со статьей [Создание учетной записи пакетной службы на портале Azure](/azure/batch/batch-account-create-portal).</span><span class="sxs-lookup"><span data-stu-id="5a175-107">To get started with Azure Batch, see [Create a Batch account with the Azure portal](/azure/batch/batch-account-create-portal).</span></span>

## <a name="client-library"></a><span data-ttu-id="5a175-108">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="5a175-108">Client library</span></span>

<span data-ttu-id="5a175-109">Клиентские библиотеки пакетной службы Azure позволяют настроить вычислительные узлы и пулы, определить и настроить выполняемые задачи в заданиях, а также настроить диспетчер заданий, чтобы отслеживать выполнение заданий и управлять им.</span><span class="sxs-lookup"><span data-stu-id="5a175-109">The Azure Batch client libraries let you configure compute nodes and pools, define tasks and configure them to run in jobs, and set up a job manager to control and monitor job execution.</span></span> <span data-ttu-id="5a175-110">Дополнительные сведения об использовании этих объектов для запуска решений для крупномасштабных параллельных вычислений см. [здесь](/azure/batch/batch-api-basics).</span><span class="sxs-lookup"><span data-stu-id="5a175-110">[Learn more](/azure/batch/batch-api-basics) about using these objects to run large-scale parallel compute solutions.</span></span>

<span data-ttu-id="5a175-111">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="5a175-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="5a175-112">Пример</span><span class="sxs-lookup"><span data-stu-id="5a175-112">Example</span></span>

<span data-ttu-id="5a175-113">Настройте пул вычислительных узлов Linux в учетной записи пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="5a175-113">Set up a pool of Linux compute nodes in a batch account:</span></span>

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="5a175-114">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="5a175-114">Explore the Client APIs</span></span>](/java/api/overview/azure/batch/clientlibrary)


## <a name="management-api"></a><span data-ttu-id="5a175-115">API управления</span><span class="sxs-lookup"><span data-stu-id="5a175-115">Management API</span></span>

<span data-ttu-id="5a175-116">Используйте библиотеки управления пакетной службы Azure, чтобы создавать и удалять учетные записи пакетной службы, считывать и повторно создавать ключи учетной записи пакетной службы и управлять хранилищем учетных записей пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="5a175-116">Use the Azure Batch management libraries to create and delete batch accounts, read and regenerate batch account keys, and manage batch account storage.</span></span>

<span data-ttu-id="5a175-117">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="5a175-117">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.1.2</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="5a175-118">Пример</span><span class="sxs-lookup"><span data-stu-id="5a175-118">Example</span></span>

<span data-ttu-id="5a175-119">Создайте учетную запись пакетной службы Azure и настройте новое приложение и учетную запись хранения Azure для него.</span><span class="sxs-lookup"><span data-stu-id="5a175-119">Create an Azure Batch account and configure a new application and Azure storage account for it.</span></span>

```java
BatchAccount batchAccount = azure.batchAccounts().define("newBatchAcct")
    .withRegion(Region.US_EAST)
    .withNewResourceGroup("myResourceGroup")
    .defineNewApplication("batchAppName")
        .defineNewApplicationPackage(applicationPackageName)
        .withAllowUpdates(true)
        .withDisplayName(applicationDisplayName)
        .attach()
    .withNewStorageAccount("batchStorageAcct")
    .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="5a175-120">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="5a175-120">Explore the Management APIs</span></span>](/java/api/overview/azure/batch/managementapi)


## <a name="samples"></a><span data-ttu-id="5a175-121">Примеры</span><span class="sxs-lookup"><span data-stu-id="5a175-121">Samples</span></span>

<span data-ttu-id="5a175-122">[Управление учетными записями пакетной службы][1]</span><span class="sxs-lookup"><span data-stu-id="5a175-122">[Manage Batch accounts][1]</span></span>   

<span data-ttu-id="5a175-123">Ознакомьтесь с другими [примерами кода Java для пакетной службы Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=batch), которые можно использовать в приложениях.</span><span class="sxs-lookup"><span data-stu-id="5a175-123">Explore more [sample Java code for Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) you can use in your apps.</span></span>

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts