---
title: Библиотеки Azure Cosmos DB для Java
description: Справочная документация по клиентским библиотекам Azure Cosmos DB для Java
keywords: Azure, Java, SDK, API, SQL, database, MongoDB, Cosmos DB, NoSQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/10/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cosmosdb
ms.openlocfilehash: 6fc9f90cb3c8130aa82b20554a94a8b5ab78c083
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823847"
---
# <a name="azure-cosmos-db-libraries-for-java"></a>Библиотеки Azure Cosmos DB для Java

## <a name="overview"></a>Обзор

Храните пары "ключ-значение", документы JSON, диаграммы и данные, расположенные в один столбец, а также отправляйте запросы к этим ресурсам в глобально распределенной базе данных с помощью [Azure Cosmos DB](/azure/cosmos-db/introduction).

Чтобы приступить к работе с Azure Cosmos DB, см. инструкции по [созданию приложения API с помощью Java и портала Azure](/azure/cosmos-db/create-sql-api-java).

## <a name="client-library"></a>Клиентская библиотека

Подключайтесь к Azure Cosmos DB с помощью клиентской библиотеки [API SQL](/azure/cosmos-db/sql-api-introduction) для работы с данными JSON с использованием [синтаксиса SQL-запросов](/azure/cosmos-db/sql-api-sql-query).

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) к файлу Maven `pom.xml`, чтобы использовать клиентскую библиотеку Cosmos DB в своем проекте.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

### <a name="example"></a>Пример

Выберите соответствующие документы JSON в Cosmos DB, используя синтаксис SQL-запросов.

```java
DocumentClient client = new DocumentClient("https://contoso.documents.azure.com:443",
                "contosoCosmosDBKey", 
                new ConnectionPolicy(),
                ConsistencyLevel.Session);

List<Document> results = client.queryDocuments("dbs/" + DATABASE_ID + "/colls/" + COLLECTION_ID,
        "SELECT * FROM myCollection WHERE myCollection.email = 'allen [at] contoso.com'",
        null)
    .getQueryIterable()
    .toList();

```

> [!div class="nextstepaction"]
> [Обзор клиентских API-интерфейсов](/java/api/overview/azure/cosmosdb/client)


## <a name="samples"></a>Примеры

[Разработка приложений Java с помощью API MongoDB Azure Cosmos DB][2]   
[Разработка приложений Java с помощью API Graph Azure Cosmos DB][3]   
[Разработка приложений Java с помощью API SQL Azure Cosmos DB][4]        

Ознакомьтесь с [примерами кода Java для Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos), которые можно использовать в своих приложениях.

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started
