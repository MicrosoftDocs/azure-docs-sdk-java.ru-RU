---
title: Библиотеки диспетчера трафика Azure для Java
description: Справочная документация по библиотекам управления диспетчера трафика для Java
keywords: Azure, Java, SDK, API, load balancing, load distribution, network, Traffic Manager
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: traffic-manager
ms.openlocfilehash: fd78402f50df16ad7d57c0ca67815bfad5b18d51
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
---
# <a name="azure-traffic-manager-libraries-for-java"></a><span data-ttu-id="eca71-104">Библиотеки диспетчера трафика Azure для Java</span><span class="sxs-lookup"><span data-stu-id="eca71-104">Azure Traffic Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="eca71-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="eca71-105">Overview</span></span>

<span data-ttu-id="eca71-106">Управляйте распределением пользовательского трафика для конечных точек службы в разных центрах обработки данных с помощью [диспетчера трафика Azure](/azure/traffic-manager/traffic-manager-overview).</span><span class="sxs-lookup"><span data-stu-id="eca71-106">Control the distribution of user traffic for service endpoints in different datacenters with [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>

<span data-ttu-id="eca71-107">Чтобы приступить к работе с диспетчером трафика Azure, см. инструкции по [созданию профиля диспетчера трафика](/azure/traffic-manager/traffic-manager-create-profile).</span><span class="sxs-lookup"><span data-stu-id="eca71-107">To get started with Azure Traffic Manager, see [Create a Traffic Manager profile](/azure/traffic-manager/traffic-manager-create-profile).</span></span>

## <a name="management-api"></a><span data-ttu-id="eca71-108">API управления</span><span class="sxs-lookup"><span data-stu-id="eca71-108">Management API</span></span>

<span data-ttu-id="eca71-109">Создавайте профили диспетчера трафика, определяйте конечные точки и изменяйте способ маршрутизации с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="eca71-109">Create Traffic Manager profiles, define endpoints, and change the routing method with the management API.</span></span> 

<span data-ttu-id="eca71-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="eca71-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-trafficmanager</artifactId>
    <version>1.3.0</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="eca71-111">Пример</span><span class="sxs-lookup"><span data-stu-id="eca71-111">Example</span></span>

<span data-ttu-id="eca71-112">Создайте профиль диспетчера трафика и назначьте одну конечную точку.</span><span class="sxs-lookup"><span data-stu-id="eca71-112">Create a Traffic Manager profile and assign a single endpoint.</span></span>

```java
TrafficManagerProfile tmProfile = azure.trafficManagerProfiles().define("testTMProfile")
        .withNewResourceGroup(Region.US_EAST)
        .withLeafDomainLabel("testTMProfile")
        .withPriorityBasedRouting()
        .defineAzureTargetEndpoint("endpoint")
        .toResourceId(webAppId)
        .withRoutingPriority(1)
        .attach()
        .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="eca71-113">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="eca71-113">Explore the Management APIs</span></span>](/java/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="eca71-114">Примеры</span><span class="sxs-lookup"><span data-stu-id="eca71-114">Samples</span></span>

[<span data-ttu-id="eca71-115">Балансировка трафика веб-приложений между несколькими регионами</span><span class="sxs-lookup"><span data-stu-id="eca71-115">Balance web app traffic across multiple regions</span></span>](https://github.com/Azure-Samples/traffic-manager-java-manage-profiles)

<span data-ttu-id="eca71-116">Ознакомьтесь с [примерами кода Java для диспетчера трафика Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic), которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="eca71-116">Explore more [sample Java code for Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) you can use in your apps.</span></span>
