---
title: Библиотеки Azure Resource Manager для Java
description: Справочная документация по библиотекам Azure Resource Manager для Java
keywords: Azure, Java, SDK, API, resource groups, arm, resource manager
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 7316c05e39bc88c50670dcb0f6331ce8440fd711
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799810"
---
# <a name="azure-resource-manager-libraries-for-java"></a><span data-ttu-id="75801-104">Библиотеки Azure Resource Manager для Java</span><span class="sxs-lookup"><span data-stu-id="75801-104">Azure Resource Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="75801-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="75801-105">Overview</span></span>

<span data-ttu-id="75801-106">Развертывайте, отслеживайте и администрируйте ресурсы в группах с помощью [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="75801-106">Deploy, monitor, and manage resources in groups with [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-api"></a><span data-ttu-id="75801-107">API управления</span><span class="sxs-lookup"><span data-stu-id="75801-107">Management API</span></span>

<span data-ttu-id="75801-108">Используйте API управления для создания групп ресурсов и развертывания ресурсов на основе шаблонов.</span><span class="sxs-lookup"><span data-stu-id="75801-108">Use the management API to create resource groups and deploy resources from templates.</span></span>

<span data-ttu-id="75801-109">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="75801-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-resources</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="75801-110">Пример</span><span class="sxs-lookup"><span data-stu-id="75801-110">Example</span></span>

<span data-ttu-id="75801-111">Создайте группу ресурсов в следующем регионе Azure: восточная часть США.</span><span class="sxs-lookup"><span data-stu-id="75801-111">Create a new resource group in the Azure Eastern US region.</span></span>

```java
ResourceGroup resourceGroup = azure.resourceGroups().define("myResourceGroup")
            .withRegion(Region.US_EAST)
            .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="75801-112">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="75801-112">Explore the Management APIs</span></span>](/java/api/overview/azure/resources/management)

## <a name="samples"></a><span data-ttu-id="75801-113">Примеры</span><span class="sxs-lookup"><span data-stu-id="75801-113">Samples</span></span>

<span data-ttu-id="75801-114">[Управление группами ресурсов Azure с помощью Java][1] 
[Развертывание ресурсов с помощью шаблона ARM][2]</span><span class="sxs-lookup"><span data-stu-id="75801-114">[Manage Azure Resource Groups with Java][1] 
[Deploy resources using an ARM template][2]</span></span>

[1]: https://github.com/Azure-Samples/resources-java-manage-resource-group
[2]: https://github.com/Azure-Samples/resources-java-deploy-using-arm-template

<span data-ttu-id="75801-115">См. [полный список](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) примеров для Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="75801-115">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) of Azure Resource Manager samples.</span></span>
