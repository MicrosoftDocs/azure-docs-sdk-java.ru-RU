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
# <a name="partner-center-libraries-for-java"></a>Библиотеки Центра партнеров для Java

## <a name="overview"></a>Обзор

Библиотеки Центра партнеров для Java — это пакет SDK, который обеспечивает взаимодействие со службой Центра партнеров Майкрософт. С его помощью партнеры могут выполнять операции с Центром партнеров программными средствами. Это последнее дополнение к существующему набору REST API и пакету SDK для .NET.

## <a name="client-library"></a>Клиентская библиотека

Управляйте ресурсами в Центре партнеров с использованием клиентской библиотеки.

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентскую библиотеку в проекте.

```xml
<dependency>
    <groupId>com.microsoft.store</groupId>
    <artifactId>partnercenter</artifactId>
    <version>1.8.0</version>
</dependency>
```   

### <a name="example"></a>Пример

Код в примере ниже извлекает полный список клиентов, связанных с прошедшим аутентификацию торговым посредником.

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

## <a name="samples"></a>Примеры

[Поддерживаемые сценарии](https://docs.microsoft.com/partner-center/develop/scenarios)
[Пример консольного приложения](https://github.com/Microsoft/Partner-Center-Java-Samples)  