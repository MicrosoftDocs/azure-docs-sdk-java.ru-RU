---
title: "Библиотеки диспетчера трафика Azure для Java"
description: "Справочная документация по библиотекам управления диспетчера трафика для Java"
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
ms.openlocfilehash: a38db9a0d92d7dedc5ff49b83ad2658aa61729dd
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/09/2017
---
# <a name="azure-traffic-manager-libraries-for-java"></a>Библиотеки диспетчера трафика Azure для Java

## <a name="overview"></a>Обзор

Управляйте распределением пользовательского трафика для конечных точек службы в разных центрах обработки данных с помощью [диспетчера трафика Azure](/azure/traffic-manager/traffic-manager-overview).

Чтобы приступить к работе с диспетчером трафика Azure, см. инструкции по [созданию профиля диспетчера трафика](/azure/traffic-manager/traffic-manager-create-profile).

## <a name="management-api"></a>API управления

Создавайте профили диспетчера трафика, определяйте конечные точки и изменяйте способ маршрутизации с помощью API управления. 

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-trafficmanager</artifactId>
    <version>1.2.1</version>
</dependency>
```   

## <a name="example"></a>Пример

Создайте профиль диспетчера трафика и назначьте одну конечную точку.

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
> [Обзор API-интерфейсов управления](/java/api/overview/azure/trafficmanager/managementapi)

## <a name="samples"></a>Примеры

[Балансировка трафика веб-приложений между несколькими регионами](https://github.com/Azure-Samples/traffic-manager-java-manage-profiles)

Ознакомьтесь с [примерами кода Java для диспетчера трафика Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic), которые можно использовать в своих приложениях.
