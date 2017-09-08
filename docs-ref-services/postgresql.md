---
title: "База данных Azure для библиотек PostgreSQL для Java"
description: "Справочная документация по клиентским библиотекам для базы данных Azure для PostgreSQL для Java"
keywords: Azure, Java, SDK, API, SQL, database, PostGres, PostgreSQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: postgresql
ms.openlocfilehash: d6fa2acb9a2f44b157ae52ba6e41f6777a43b574
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
# <a name="azure-database-for-postgresql-libraries-for-java"></a><span data-ttu-id="d0c58-104">База данных Azure для библиотек PostgreSQL для Java</span><span class="sxs-lookup"><span data-stu-id="d0c58-104">Azure Database for PostgreSQL libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="d0c58-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="d0c58-105">Overview</span></span>

<span data-ttu-id="d0c58-106">[База данных Azure для PostgreSQL](/azure/sql-database/sql-database-technical-overview) — это служба реляционной базы данных в Azure, созданная для разработчиков на основе версии сообщества СУБД [PostgreSQL](https://www.postgresql.org/) с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="d0c58-106">[Azure Database for PostgreSQL](/azure/sql-database/sql-database-technical-overview) is a relational database service in Azure built for developers based on the community version of open source [PostgreSQL](https://www.postgresql.org/) database engine.</span></span>

<span data-ttu-id="d0c58-107">Чтобы приступить к работе с базой данных Azure для PostgreSQL, см. инструкции по [подключению и созданию запросов к данным с помощью Java](/azure/postgresql/connect-java).</span><span class="sxs-lookup"><span data-stu-id="d0c58-107">To get started with Azure Database for PostgreSQL, see [Use Java to connect and query data](/azure/postgresql/connect-java).</span></span>

## <a name="client-jdbc-driver"></a><span data-ttu-id="d0c58-108">Клиентский драйвер JDBC</span><span class="sxs-lookup"><span data-stu-id="d0c58-108">Client JDBC driver</span></span>

<span data-ttu-id="d0c58-109">Подключайтесь к базе данных Azure для PostgreSQL из приложений с помощью [драйвера JDBC для PostgreSQL](https://jdbc.postgresql.org/) с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="d0c58-109">Connect to Azure Database for PostgreSQL from your applications using the open-source [PostgreSQL JDBC driver](https://jdbc.postgresql.org/).</span></span> <span data-ttu-id="d0c58-110">Вы можете использовать [API-интерфейс JDBC для Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/), чтобы подключаться непосредственно к базе данных, или платформы доступа к данным, которые взаимодействуют с базой данных через JDBC, например [Hibernate](http://hibernate.org/).</span><span class="sxs-lookup"><span data-stu-id="d0c58-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect to the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="d0c58-111">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентский драйвер JDBC в проекте.</span><span class="sxs-lookup"><span data-stu-id="d0c58-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>  

```XML
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.1.1</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="d0c58-112">Пример</span><span class="sxs-lookup"><span data-stu-id="d0c58-112">Example</span></span>

<span data-ttu-id="d0c58-113">Подключитесь к базе данных Azure для PostgreSQL с помощью JDBC и выберите все записи в таблице продаж.</span><span class="sxs-lookup"><span data-stu-id="d0c58-113">Connect to Azure Database for PostgreSQL using JDBC and select all records in the sales table.</span></span> <span data-ttu-id="d0c58-114">Строку подключения JDBC для базы данных можно получить на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d0c58-114">You can get the JDBC connection string for the database from the Azure Portal.</span></span>

```java
String url = String.format("jdbc:postgresql://mypostgresdb.postgres.database.azure.com:5432/mydb?user=frank@mypostgresdb&password=AbCdEfGhIjK&ssl=true");
Connection connection = null;
try {
    connection = DriverManager.getConnection(url);
    String selectSql = "SELECT * FROM SALES";
    Statement statement = connection.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a><span data-ttu-id="d0c58-115">Примеры</span><span class="sxs-lookup"><span data-stu-id="d0c58-115">Samples</span></span>

[<span data-ttu-id="d0c58-116">Проектирование базы данных PostgreSQL с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d0c58-116">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) 

<span data-ttu-id="d0c58-117">Ознакомьтесь с [примерами кода Java для базы данных Azure для PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres), которые можно использовать в своих приложениях.</span><span class="sxs-lookup"><span data-stu-id="d0c58-117">Explore more [sample Java code for Azure Database for PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) you can use in your apps.</span></span>
