---
title: Библиотеки базы данных SQL Azure для Java
description: Подключайтесь к базе данных SQL Azure с помощью драйвера JDBC или управляйте экземплярами базы данных Azure SQL помощью API управления.
keywords: Azure, Java, SDK, API, SQL, database, JDBC
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/05/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: sql-database
ms.openlocfilehash: 37f7d3caf10e6b709cee2452c63a543d49e0ead8
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823717"
---
# <a name="azure-sql-database-libraries-for-java"></a><span data-ttu-id="bc7de-104">Библиотеки базы данных SQL Azure для Java</span><span class="sxs-lookup"><span data-stu-id="bc7de-104">Azure SQL Database libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="bc7de-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="bc7de-105">Overview</span></span>

<span data-ttu-id="bc7de-106">[База данных SQL Azure](/azure/sql-database/sql-database-technical-overview) — это служба реляционной базы данных на базе ядра Microsoft SQL Server, которая поддерживает табличные, пространственные, JSON- и XML-данные.</span><span class="sxs-lookup"><span data-stu-id="bc7de-106">[Azure SQL Database](/azure/sql-database/sql-database-technical-overview) is a relational database service using the Microsoft SQL Server engine that supports table, JSON, spatial, and XML data.</span></span> 

<span data-ttu-id="bc7de-107">Чтобы приступить к работе с базой данных SQL Azure, ознакомьтесь со статьей [Использование Java для создания запросов к базе данных SQL Azure](/azure/sql-database/sql-database-connect-query-java).</span><span class="sxs-lookup"><span data-stu-id="bc7de-107">To get started with Azure SQL Database, see [Azure SQL Database: Use Java to connect and query data](/azure/sql-database/sql-database-connect-query-java).</span></span>

## <a name="client-jdbc-driver"></a><span data-ttu-id="bc7de-108">Клиентский драйвер JDBC</span><span class="sxs-lookup"><span data-stu-id="bc7de-108">Client JDBC driver</span></span>

<span data-ttu-id="bc7de-109">Подключайтесь к базе данных SQL Azure из своих приложений с помощью [драйвера JDBC для базы данных SQL](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server).</span><span class="sxs-lookup"><span data-stu-id="bc7de-109">Connect to Azure SQL Database from your applications using the [SQL Database JDBC driver](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server).</span></span> <span data-ttu-id="bc7de-110">Вы можете использовать [API-интерфейс JDBC для Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/), чтобы подключаться непосредственно к базе данных, или платформы доступа к данным, которые взаимодействуют с базой данных через JDBC, например [Hibernate](http://hibernate.org/).</span><span class="sxs-lookup"><span data-stu-id="bc7de-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect with the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="bc7de-111">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентский драйвер JDBC в проекте.</span><span class="sxs-lookup"><span data-stu-id="bc7de-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="bc7de-112">Пример</span><span class="sxs-lookup"><span data-stu-id="bc7de-112">Example</span></span>

<span data-ttu-id="bc7de-113">Подключитесь к базе данных SQL и выберите все записи в таблице с помощью JDBC.</span><span class="sxs-lookup"><span data-stu-id="bc7de-113">Connect to SQL database and select all records in a table using JDBC.</span></span>

```java
String connectionString = "jdbc:sqlserver://fabrikam.database.windows.net:1433;database=fiber;user=raisa;password=testpass;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
try {
    Connection conn = DriverManager.getConnection(connectionString);
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery("SELECT * FROM SALES");
}  
```

## <a name="management-api"></a><span data-ttu-id="bc7de-114">API управления</span><span class="sxs-lookup"><span data-stu-id="bc7de-114">Management API</span></span>

<span data-ttu-id="bc7de-115">Создавайте ресурсы базы данных SQL Azure и управляйте ими в своей подписке с помощью API управления.</span><span class="sxs-lookup"><span data-stu-id="bc7de-115">Create and manage Azure SQL Database resources in your subscription with the management API.</span></span>   

<span data-ttu-id="bc7de-116">[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.</span><span class="sxs-lookup"><span data-stu-id="bc7de-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-sql</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="bc7de-117">Обзор API-интерфейсов управления</span><span class="sxs-lookup"><span data-stu-id="bc7de-117">Explore the Management APIs</span></span>](/java/api/overview/azure/sql/management)

### <a name="example"></a><span data-ttu-id="bc7de-118">Пример</span><span class="sxs-lookup"><span data-stu-id="bc7de-118">Example</span></span>

<span data-ttu-id="bc7de-119">Создайте ресурс базы данных SQL и ограничьте доступ к диапазону IP-адресов с помощью правила брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="bc7de-119">Create a SQL Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlDbName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(resourceGroupName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    .withNewFirewallRule("172.16.0.0", "172.31.255.255")
                    .create();
```

## <a name="samples"></a><span data-ttu-id="bc7de-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="bc7de-120">Samples</span></span>

[!INCLUDE [java-sql-samples](../docs-ref-conceptual/includes/sql.md)]

<span data-ttu-id="bc7de-121">Ознакомьтесь с другими [примерами кода Java для базы данных SQL Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL), которые можно использовать в приложениях.</span><span class="sxs-lookup"><span data-stu-id="bc7de-121">Explore more [sample Java code for Azure SQL Database](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) you can use in your apps.</span></span>