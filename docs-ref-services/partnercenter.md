---
title: Пакет SDK для Java для Центра партнеров
description: Справочная документация по пакету SDK (Java) для Центра партнеров
keywords: API, CSP, Cloud Soltuion Provider, Java, Partner Center, SDK
author: iswillia
ms.author: iswillia
manager: lesliep
ms.date: 10/09/2018
ms.topic: reference
ms.prod: partnercenter
ms.technology: partnercenter
ms.devlang: java
ms.openlocfilehash: 2adfbdbd37d6eb91e48ee37091f951b3f7d59eb9
ms.sourcegitcommit: 4da7d2f470331feb7d76a1658f5825f365cdba9a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/12/2018
ms.locfileid: "49121651"
---
# <a name="partner-center-libraries-for-java"></a><span data-ttu-id="7f327-104">Библиотеки Центра партнеров для Java</span><span class="sxs-lookup"><span data-stu-id="7f327-104">Partner Center libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="7f327-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="7f327-105">Overview</span></span>

<span data-ttu-id="7f327-106">Библиотеки Центра партнеров для Java — это пакет SDK, который обеспечивает взаимодействие со службой Центра партнеров Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="7f327-106">The Partner Center libraries for Java is a SDK that provides the ability to interact with Microsoft's Partner Center service.</span></span> <span data-ttu-id="7f327-107">С его помощью партнеры могут выполнять операции с Центром партнеров программными средствами.</span><span class="sxs-lookup"><span data-stu-id="7f327-107">This enables partners to perform the Partner Center operations programmatically.</span></span> <span data-ttu-id="7f327-108">Это последнее дополнение к существующему набору REST API и пакету SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="7f327-108">This is the latest addition to existing portfolio of REST APIs and the .NET SDK.</span></span>

## <a name="client-library"></a><span data-ttu-id="7f327-109">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="7f327-109">Client library</span></span>

<span data-ttu-id="7f327-110">Управляйте ресурсами в Центре партнеров с использованием клиентской библиотеки.</span><span class="sxs-lookup"><span data-stu-id="7f327-110">Manage resources in Partner Center using the client library.</span></span>

<span data-ttu-id="7f327-111">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.</span><span class="sxs-lookup"><span data-stu-id="7f327-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```xml
<dependency>
    <groupId>com.microsoft.store</groupId>
    <artifactId>partnercenter</artifactId>
    <version>1.8.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="7f327-112">Пример</span><span class="sxs-lookup"><span data-stu-id="7f327-112">Example</span></span>

<span data-ttu-id="7f327-113">Код в примере ниже извлекает полный список клиентов, связанных с прошедшим аутентификацию торговым посредником.</span><span class="sxs-lookup"><span data-stu-id="7f327-113">Retrieves a complete list of customer associated with the authenticated reseller.</span></span>

```java
IPartnerCredentials appCredentials = PartnerCredentials.getInstance().generateByApplicationCredentials('YOUR_APP_ID', 'YOUR_APP_SECRET', 'YOUR_TENANT_ID');
IAggregatePartner partnerOperations = PartnerService.getInstance().createPartnerOperations(appCredentials);

// Query the customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(100));
this.getContext().getConsoleHelper().stopProgress();

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while ( customersEnumerator.hasValue() )
{
    /*
     * Perform some operation with the current page of customers using 
     * customersEnumerator.getCurrent()  
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="samples"></a><span data-ttu-id="7f327-114">Примеры</span><span class="sxs-lookup"><span data-stu-id="7f327-114">Samples</span></span>

<span data-ttu-id="7f327-115">[Поддерживаемые сценарии](https://docs.microsoft.com/partner-center/develop/scenarios)
[Пример консольного приложения](https://github.com/Microsoft/Partner-Center-Java-Samples)</span><span class="sxs-lookup"><span data-stu-id="7f327-115">[Supported scenarios](https://docs.microsoft.com/partner-center/develop/scenarios)
[Sample console application](https://github.com/Microsoft/Partner-Center-Java-Samples)</span></span>  