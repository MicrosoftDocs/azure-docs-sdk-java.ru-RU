---
title: "Библиотеки Azure DNS для Java"
description: "Справочная документация по библиотекам управления Azure DNS для Java"
keywords: Azure, Java, SDK, API, domains, DNS, name, service, domain name service
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: dns
ms.openlocfilehash: 123f61004c473bc060f0360f0fcb027d1591523e
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/09/2017
---
# <a name="azure-traffic-manager-libraries-for-java"></a>Библиотеки диспетчера трафика Azure для Java

## <a name="overview"></a>Обзор

Предоставляйте разрешения доменных имен и управляйте записями DNS с помощью одних и тех же учетных данных, API-интерфейсов, средств и расценок, как и для других служб Azure с использованием [Azure DNS](/azure/dns/dns-overview).

Чтобы приступить к работе с Azure DNS, см. инструкции по [началу работы с Azure DNS с помощью Azure CLI 2.0](/azure/dns/dns-getstarted-cli).

## <a name="management-api"></a>API управления

Создавайте зоны DNS и добавляйте записи в зоны с помощью API управления.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-dns</artifactId>
    <version>1.2.1</version>
</dependency>
```   

### <a name="example"></a>Пример

Создайте корневую зону DNS и добавьте запись CNAME `www` в существующую группу ресурсов.

```java
DnsZone rootDnsZone = azure.dnsZones().define("contoso.com")
        .withExistingResourceGroup("myResourceGroup")
        .create();
rootDnsZone = rootDnsZone.update()
        .withCNameRecordSet("www", "172.30.241.20")
        .apply();
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/java/api/overview/azure/dns/managementapi)

## <a name="samples"></a>Примеры

[Размещение и администрирование доменов с помощью Azure DNS](https://github.com/Azure-Samples/dns-java-host-and-manage-your-domains)

Ознакомьтесь с [примерами кода Java для Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns), которые можно использовать в своих приложениях.