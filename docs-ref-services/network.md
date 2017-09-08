---
title: "Библиотеки Azure Network для Java"
description: "Справочная документация по библиотекам управления Azure Network для Java"
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
ms.openlocfilehash: 7be23ba896887cc88ccdf0fb049cb5f579d496c3
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
# <a name="azure-network-libraries-for-java"></a>Библиотеки Azure Network для Java

## <a name="overview"></a>Обзор

Подключайте ресурсы Azure, фильтруйте и балансируйте трафик, а также управляйте маршрутизацией с помощью [сетей Azure](/azure/networking/networking-overview).

Чтобы приступить к работе с сетями Azure, см. инструкции по [созданию виртуальной сети](/azure/virtual-network/virtual-network-get-started-vnet-subnet).

## <a name="management-api"></a>API управления

Создавайте и администрируйте [виртуальные сети](/azure/virtual-network/virtual-networks-overview), [каналы ExpressRoute](/azure/expressroute/) и [шлюзы приложений](/azure/application-gateway/) Azure с помощью API управления.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-network</artifactId>
    <version>1.1.2</version>
</dependency>
```   

### <a name="example"></a>Пример

Создайте виртуальную сеть с одной подсетью.

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
> [Обзор API-интерфейсов управления](/java/api/overview/azure/networking/managementapi)

## <a name="samples"></a>Примеры

[Управление виртуальными сетями](https://github.com/Azure-Samples/network-java-manage-virtual-network)   
[Управление сетевыми интерфейсами](https://github.com/Azure-Samples/network-java-manage-network-interface)   
[Управление шлюзами приложения](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways)   
[Управление подсистемами балансировки нагрузки для Интернета](https://github.com/Azure-Samples/network-java-manage-internet-facing-load-balancers)   

Ознакомьтесь с [примерами кода Java для сетей Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=network), которые можно использовать в своих приложениях.
