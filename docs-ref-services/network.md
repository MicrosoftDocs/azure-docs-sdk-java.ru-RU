---
title: Библиотеки Azure Network для Java
description: Справочная документация по библиотекам управления Azure Network для Java
keywords: Azure, Java, SDK, API, networking, load balancing, vnet, subnet
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: networking
ms.openlocfilehash: 4eb4f583da686508db9fb0c4346f2525502f669d
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593329"
---
# <a name="azure-network-libraries-for-java"></a><span data-ttu-id="d96f2-104">Библиотеки Azure Network для Java</span><span class="sxs-lookup"><span data-stu-id="d96f2-104">Azure Network libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="d96f2-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="d96f2-105">Overview</span></span>

<span data-ttu-id="d96f2-106">Подключайте ресурсы Azure, фильтруйте и балансируйте трафик, а также управляйте маршрутизацией с помощью [сетей Azure](/azure/networking/networking-overview).</span><span class="sxs-lookup"><span data-stu-id="d96f2-106">Connect Azure resources, filter and balance traffic, and manage routing with [Azure Networking](/azure/networking/networking-overview).</span></span>

<span data-ttu-id="d96f2-107">Чтобы приступить к работе с сетями Azure, см. инструкции по [созданию виртуальной сети](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span><span class="sxs-lookup"><span data-stu-id="d96f2-107">To get started with Azure Networking, see [Create your first virtual network](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span></span>

## <a name="management-api"></a><span data-ttu-id="d96f2-108">API управления</span><span class="sxs-lookup"><span data-stu-id="d96f2-108">Management API</span></span>

<span data-ttu-id="d96f2-109">Создавайте и администрируйте [виртуальные сети](/azure/virtual-network/virtual-networks-overview), [каналы ExpressRoute](/azure/expressroute/) и [шлюзы приложений](/azure/application-gateway/) Azure с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="d96f2-109">Create and manage Azure [virtual networks](/azure/virtual-network/virtual-networks-overview) , [ExpressRoutes](/azure/expressroute/) , and [Application Gateways](/azure/application-gateway/) with the management API.</span></span>

<span data-ttu-id="d96f2-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="d96f2-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-network</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="d96f2-111">Пример</span><span class="sxs-lookup"><span data-stu-id="d96f2-111">Example</span></span>

<span data-ttu-id="d96f2-112">Создайте виртуальную сеть с одной подсетью.</span><span class="sxs-lookup"><span data-stu-id="d96f2-112">Create a new virtual network with a single subnet.</span></span>

```java
Network virtualNetwork1 = azure.networks().define(vnetName1)
        .withRegion(Region.US_EAST)
        .withExistingResourceGroup("myResourceGroup")
        .withAddressSpace("192.168.0.0/16")
        .defineSubnet("myVirtualNetwork")
            .withAddressPrefix("192.168.2.0/24")
            .attach()
        .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d96f2-113">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="d96f2-113">Explore the Management APIs</span></span>](/java/api/overview/azure/networking/management)

## <a name="samples"></a><span data-ttu-id="d96f2-114">Примеры</span><span class="sxs-lookup"><span data-stu-id="d96f2-114">Samples</span></span>

<span data-ttu-id="d96f2-115">[Управление виртуальными сетями](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span><span class="sxs-lookup"><span data-stu-id="d96f2-115">[Manage virtual networks](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span></span>  
<span data-ttu-id="d96f2-116">[Управление сетевыми интерфейсами](https://github.com/Azure-Samples/network-java-manage-network-interface) </span><span class="sxs-lookup"><span data-stu-id="d96f2-116">[Manage network interfaces](https://github.com/Azure-Samples/network-java-manage-network-interface) </span></span>  
<span data-ttu-id="d96f2-117">[Управление шлюзами приложения](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span><span class="sxs-lookup"><span data-stu-id="d96f2-117">[Manage Application Gateways](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span></span>  
[<span data-ttu-id="d96f2-118">Управление подсистемами балансировки нагрузки для Интернета</span><span class="sxs-lookup"><span data-stu-id="d96f2-118">Manage internet facing load balancers</span></span>](https://github.com/Azure-Samples/network-java-manage-internet-facing-load-balancers)   

<span data-ttu-id="d96f2-119">Ознакомьтесь с [примерами кода Java для сетей Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=network), которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="d96f2-119">Explore more [sample Java code for Azure Networking](https://azure.microsoft.com/resources/samples/?platform=java&term=network) you can use in your apps.</span></span>
