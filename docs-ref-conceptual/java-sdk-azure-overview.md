---
title: "Библиотеки Azure для Java"
description: "Обзор библиотек служб и библиотек управления Azure для Java"
keywords: Azure, Java, SDK, API
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 9aaf22a2-382a-4b13-a8e3-0e467d607207
ms.openlocfilehash: 22a337e928085475e905a271f991147729d97671
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
# <a name="azure-libraries-for-java"></a><span data-ttu-id="eb8bf-104">Библиотеки Azure для Java</span><span class="sxs-lookup"><span data-stu-id="eb8bf-104">Azure libraries for Java</span></span>

<span data-ttu-id="eb8bf-105">Библиотеки Azure для Java позволяют подключаться к службам и управлять ресурсами Azure, используя код приложения.</span><span class="sxs-lookup"><span data-stu-id="eb8bf-105">The Azure libraries for Java help you manage Azure resources and connect to services from your application code.</span></span> <span data-ttu-id="eb8bf-106">Эти библиотеки доступны в качестве [импортируемых файлов Maven](java-sdk-azure-install.md), которые можно использовать в проектах Java.</span><span class="sxs-lookup"><span data-stu-id="eb8bf-106">The libraries are available as [Maven imports](java-sdk-azure-install.md) for use in your Java projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="eb8bf-107">Управление ресурсами Azure</span><span class="sxs-lookup"><span data-stu-id="eb8bf-107">Manage Azure resources</span></span>

<span data-ttu-id="eb8bf-108">Создавайте ресурсы Azure и управляйте ими из приложений Java, используя [библиотеки управления Azure для Java](java-sdk-azure-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eb8bf-108">Create and manage Azure resources from your Java applications using the [Azure management libraries for Java](java-sdk-azure-get-started.md).</span></span> <span data-ttu-id="eb8bf-109">Используйте эти библиотеки для создания собственных служб и средств автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="eb8bf-109">Use these libraries to build your own Azure automation tools and services.</span></span> 

<span data-ttu-id="eb8bf-110">Например, для создания виртуальной машины Linux следует написать следующий код:</span><span class="sxs-lookup"><span data-stu-id="eb8bf-110">For example, to create a Linux VM you would write the following code:</span></span>

```java
VirtualMachine linuxVM = azure.virtualMachines().define("myAzureVM")
           .withRegion(region)
           .withExistingResourceGroup("sampleResourceGroup")
           .withNewPrimaryNetwork("10.0.0.0/28")
           .withPrimaryPrivateIpAddressDynamic()
           .withoutPrimaryPublicIpAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withSsh(key)
           .withUnmanagedStorage()
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
 ```

<span data-ttu-id="eb8bf-111">Полный список библиотек и рекомендации по их импорту в проекты см. в [инструкциях по установке](java-sdk-azure-install.md). А сведения по настройке проверки подлинности и выполнению примера кода в подписке Azure см. в [статье по началу работы](java-sdk-azure-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eb8bf-111">Review the [install instructions](java-sdk-azure-install.md) for a full list of the libraries and how to import them into your projects and then read the [get started article](java-sdk-azure-get-started.md) to set up your authentication and run sample code against your own Azure subscription.</span></span> 

## <a name="connect-to-azure-services"></a><span data-ttu-id="eb8bf-112">Подключение к службам Azure</span><span class="sxs-lookup"><span data-stu-id="eb8bf-112">Connect to Azure services</span></span>

<span data-ttu-id="eb8bf-113">Библиотеки Java можно использовать не только для создания ресурсов и управления ими в Azure, но и для подключения и использования этих ресурсов в приложениях.</span><span class="sxs-lookup"><span data-stu-id="eb8bf-113">In addition to using Java libraries to create and manage resources within Azure, you can also use Java libraries to connect  and use those resources in your apps.</span></span> <span data-ttu-id="eb8bf-114">Например, для обновления табличной базы данных SQL или хранения файлов в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="eb8bf-114">For example, you might update a table SQL Database or store files in Azure Storage.</span></span> <span data-ttu-id="eb8bf-115">Выберите библиотеку, необходимую для конкретной службы, в [полном списке библиотек](java-sdk-azure-install.md) и ознакомьтесь с руководствами и примерами кода, которые помогут вам использовать библиотеки в приложениях, в [центре разработчиков Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="eb8bf-115">Select the library you need for a particular service from the [complete list of libraries](java-sdk-azure-install.md) and visit the [Java developer center](https://azure.microsoft.com/develop/java/) for tutorials and sample code for help using them in your apps.</span></span>

<span data-ttu-id="eb8bf-116">Например, чтобы вывести содержимое каждого большого двоичного объекта в контейнере хранилища Azure, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="eb8bf-116">For example, to print out the contents of every blob in an Azure storage container:</span></span>

```java
// get the container from the blob client
CloudBlobContainer container = blobClient.getContainerReference("blobcontainer");

// For each item in the container
for (ListBlobItem blobItem : container.listBlobs()) {
    // If the item is a blob, not a virtual directory
    if (blobItem instanceof CloudBlockBlob) {
        // Download the text
        CloudBlockBlob retrievedBlob = (CloudBlockBlob) blobItem;
        System.out.println(retrievedBlob.downloadText());
    }
}
```

## <a name="sample-code-and-reference"></a><span data-ttu-id="eb8bf-117">Примеры кода и справочные материалы</span><span class="sxs-lookup"><span data-stu-id="eb8bf-117">Sample code and reference</span></span>

<span data-ttu-id="eb8bf-118">В примерах кода ниже представлены общие задачи автоматизации, выполняемые с помощью библиотек управления Azure для Java. Это готовый код, который вы можете использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="eb8bf-118">The following samples cover common automation tasks with the Azure management libraries for Java and have code ready to use in your own apps:</span></span>

- [<span data-ttu-id="eb8bf-119">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="eb8bf-119">Virtual machines</span></span>](java-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="eb8bf-120">Веб-приложения</span><span class="sxs-lookup"><span data-stu-id="eb8bf-120">Web apps</span></span>](java-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="eb8bf-121">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="eb8bf-121">SQL Database</span></span>](java-sdk-azure-sql-database-samples.md)
   
<span data-ttu-id="eb8bf-122">[Справочник](https://docs.microsoft.com/java/api) доступен для всех пакетов в библиотеках служб и библиотеках управления.</span><span class="sxs-lookup"><span data-stu-id="eb8bf-122">A [reference](https://docs.microsoft.com/java/api) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="eb8bf-123">Сведения о новых функциях и критически важных изменениях, а также инструкции по переходу с предыдущих версий см. в [заметках о выпуске](java-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="eb8bf-123">New features, breaking changes, and migration instructions from previous versions are available in the [release notes](java-sdk-azure-release-notes.md).</span></span>