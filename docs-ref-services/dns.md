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
ms.openlocfilehash: c29403713b1271091b7c37b796a0e8d65a337a7d
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/09/2017
---
# <a name="azure-traffic-manager-libraries-for-java"></a><span data-ttu-id="abfbf-104">Библиотеки диспетчера трафика Azure для Java</span><span class="sxs-lookup"><span data-stu-id="abfbf-104">Azure Traffic Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="abfbf-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="abfbf-105">Overview</span></span>

<span data-ttu-id="abfbf-106">Предоставляйте разрешения доменных имен и управляйте записями DNS с помощью одних и тех же учетных данных, API-интерфейсов, средств и расценок, как и для других служб Azure с использованием [Azure DNS](/azure/dns/dns-overview).</span><span class="sxs-lookup"><span data-stu-id="abfbf-106">Provide domain name resolution and manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services with [Azure DNS](/azure/dns/dns-overview).</span></span>

<span data-ttu-id="abfbf-107">Чтобы приступить к работе с Azure DNS, см. инструкции по [началу работы с Azure DNS с помощью Azure CLI 2.0](/azure/dns/dns-getstarted-cli).</span><span class="sxs-lookup"><span data-stu-id="abfbf-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure CLI 2.0](/azure/dns/dns-getstarted-cli).</span></span>

## <a name="management-api"></a><span data-ttu-id="abfbf-108">API управления</span><span class="sxs-lookup"><span data-stu-id="abfbf-108">Management API</span></span>

<span data-ttu-id="abfbf-109">Создавайте зоны DNS и добавляйте записи в зоны с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="abfbf-109">Create DNS zones and add records to zones with the management API.</span></span>

<span data-ttu-id="abfbf-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="abfbf-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-dns</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="abfbf-111">Пример</span><span class="sxs-lookup"><span data-stu-id="abfbf-111">Example</span></span>

<span data-ttu-id="abfbf-112">Создайте корневую зону DNS и добавьте запись CNAME `www` в существующую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="abfbf-112">Create a root DNS zone and add a `www` CNAME record in an existing resource group.</span></span>

```java
DnsZone rootDnsZone = azure.dnsZones().define("contoso.com")
        .withExistingResourceGroup("myResourceGroup")
        .create();
rootDnsZone = rootDnsZone.update()
        .withCNameRecordSet("www", "172.30.241.20")
        .apply();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="abfbf-113">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="abfbf-113">Explore the Management APIs</span></span>](/java/api/overview/azure/dns/managementapi)

## <a name="samples"></a><span data-ttu-id="abfbf-114">Примеры</span><span class="sxs-lookup"><span data-stu-id="abfbf-114">Samples</span></span>

[<span data-ttu-id="abfbf-115">Размещение и администрирование доменов с помощью Azure DNS</span><span class="sxs-lookup"><span data-stu-id="abfbf-115">Host and manage your domains with Azure DNS</span></span>](https://github.com/Azure-Samples/dns-java-host-and-manage-your-domains)

<span data-ttu-id="abfbf-116">Ознакомьтесь с [примерами кода Java для Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns), которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="abfbf-116">Explore more [sample Java code for Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) you can use in your apps.</span></span>