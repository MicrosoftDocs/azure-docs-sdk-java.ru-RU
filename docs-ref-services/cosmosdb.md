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
ms.openlocfilehash: d8748dc6fcc0c839a8b2d2f817c0477bcac5baa2
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799890"
---
# <a name="azure-cosmos-db-libraries-for-java"></a><span data-ttu-id="8c10c-104">Библиотеки Azure Cosmos DB для Java</span><span class="sxs-lookup"><span data-stu-id="8c10c-104">Azure Cosmos DB libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="8c10c-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="8c10c-105">Overview</span></span>

<span data-ttu-id="8c10c-106">Храните пары "ключ-значение", документы JSON, диаграммы и данные, расположенные в один столбец, а также отправляйте запросы к этим ресурсам в глобально распределенной базе данных с помощью [Azure Cosmos DB](/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="8c10c-106">Store and query key-value, JSON document, graph, and columnar data in a globally distributed database with [Azure Cosmos DB](/azure/cosmos-db/introduction).</span></span>

<span data-ttu-id="8c10c-107">Чтобы приступить к работе с Azure Cosmos DB, см. инструкции по [созданию приложения API с помощью Java и портала Azure](/azure/cosmos-db/create-sql-api-java).</span><span class="sxs-lookup"><span data-stu-id="8c10c-107">To get started with Azure Cosmos DB, see [Azure Cosmos DB: Build an API app with Java and the Azure portal](/azure/cosmos-db/create-sql-api-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="8c10c-108">Клиентская библиотека</span><span class="sxs-lookup"><span data-stu-id="8c10c-108">Client library</span></span>

<span data-ttu-id="8c10c-109">Подключайтесь к Azure Cosmos DB с помощью клиентской библиотеки [API SQL](/azure/cosmos-db/sql-api-introduction) для работы с данными JSON с использованием [синтаксиса SQL-запросов](/azure/cosmos-db/sql-api-sql-query).</span><span class="sxs-lookup"><span data-stu-id="8c10c-109">Connect to Azure Cosmos DB using the [SQL API](/azure/cosmos-db/sql-api-introduction) client library to work with JSON data with [SQL query syntax](/azure/cosmos-db/sql-api-sql-query).</span></span>

<span data-ttu-id="8c10c-110">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) к файлу Maven `pom.xml`, чтобы использовать клиентскую библиотеку Cosmos DB в своем проекте.</span><span class="sxs-lookup"><span data-stu-id="8c10c-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the Cosmos DB client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="8c10c-111">Пример</span><span class="sxs-lookup"><span data-stu-id="8c10c-111">Example</span></span>

<span data-ttu-id="8c10c-112">Выберите соответствующие документы JSON в Cosmos DB, используя синтаксис SQL-запросов.</span><span class="sxs-lookup"><span data-stu-id="8c10c-112">Select matching JSON documents in Cosmos DB using SQL query syntax.</span></span>

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
> [<span data-ttu-id="8c10c-113">Обзор клиентских API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="8c10c-113">Explore the Client APIs</span></span>](/java/api/overview/azure/cosmosdb/client)


## <a name="samples"></a><span data-ttu-id="8c10c-114">Примеры</span><span class="sxs-lookup"><span data-stu-id="8c10c-114">Samples</span></span>

<span data-ttu-id="8c10c-115">[Разработка приложений Java с помощью API MongoDB Azure Cosmos DB][2] </span><span class="sxs-lookup"><span data-stu-id="8c10c-115">[Develop a Java app using Azure Cosmos DB MongoDB API][2] </span></span>  
<span data-ttu-id="8c10c-116">[Разработка приложений Java с помощью API Graph Azure Cosmos DB][3] </span><span class="sxs-lookup"><span data-stu-id="8c10c-116">[Develop a Java app using Azure Cosmos DB Graph API][3] </span></span>  
<span data-ttu-id="8c10c-117">[Разработка приложений Java с помощью API SQL Azure Cosmos DB][4]</span><span class="sxs-lookup"><span data-stu-id="8c10c-117">[Develop a Java app using Azure Cosmos DB SQL API][4]</span></span>        

<span data-ttu-id="8c10c-118">Ознакомьтесь с [примерами кода Java для Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos), которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="8c10c-118">Explore more [sample Java code for Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) you can use in your apps.</span></span>

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started
