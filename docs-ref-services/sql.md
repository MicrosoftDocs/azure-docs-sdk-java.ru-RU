---
title: "Библиотеки базы данных SQL Azure для Java"
description: "Подключайтесь к базе данных SQL Azure с помощью драйвера JDBC или управляйте экземплярами базы данных Azure SQL помощью API управления."
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
ms.openlocfilehash: 332bfa45b41f7b183e5c35ec9a1f3537f7d849ba
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
# <a name="azure-sql-database-libraries-for-java"></a>Библиотеки базы данных SQL Azure для Java

## <a name="overview"></a>Обзор

[База данных SQL Azure](/azure/sql-database/sql-database-technical-overview) — это служба реляционной базы данных на базе ядра Microsoft SQL Server, которая поддерживает табличные, пространственные, JSON- и XML-данные. 

Чтобы приступить к работе с базой данных SQL Azure, ознакомьтесь со статьей [Использование Java для создания запросов к базе данных SQL Azure](/azure/sql-database/sql-database-connect-query-java).

## <a name="client-jdbc-driver"></a>Клиентский драйвер JDBC

Подключайтесь к базе данных SQL Azure из своих приложений с помощью [драйвера JDBC для базы данных SQL](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server). Вы можете использовать [API-интерфейс JDBC для Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/), чтобы подключаться непосредственно к базе данных, или платформы доступа к данным, которые взаимодействуют с базой данных через JDBC, например [Hibernate](http://hibernate.org/).

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентский драйвер JDBC в проекте.


```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```   

### <a name="example"></a>Пример

Подключитесь к базе данных SQL и выберите все записи в таблице с помощью JDBC.

```java
String connectionString = "jdbc:sqlserver://fabrikam.database.windows.net:1433;database=fiber;user=raisa;password=testpass;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
try {
    Connection conn = DriverManager.getConnection(connectionString);
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery("SELECT * FROM SALES");
}  
```

## <a name="management-api"></a>API управления

Создавайте ресурсы базы данных SQL Azure и управляйте ими в своей подписке с помощью API управления.   

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать API управления в проекте.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-sql</artifactId>
    <version>1.1.2</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Обзор API-интерфейсов управления](/java/api/overview/azure/sql/managementapi)

### <a name="example"></a>Пример

Создайте ресурс базы данных SQL и ограничьте доступ к диапазону IP-адресов с помощью правила брандмауэра.

```java
SqlServer sqlServer = azure.sqlServers().define(sqlDbName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(resourceGroupName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    .withNewFirewallRule("172.16.0.0", "172.31.255.255")
                    .create();
```

## <a name="samples"></a>Примеры

[!INCLUDE [java-sql-samples](../docs-ref-conceptual/includes/sql.md)]

Ознакомьтесь с другими [примерами кода Java для базы данных SQL Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL), которые можно использовать в приложениях.