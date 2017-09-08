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
# <a name="azure-database-for-postgresql-libraries-for-java"></a>База данных Azure для библиотек PostgreSQL для Java

## <a name="overview"></a>Обзор

[База данных Azure для PostgreSQL](/azure/sql-database/sql-database-technical-overview) — это служба реляционной базы данных в Azure, созданная для разработчиков на основе версии сообщества СУБД [PostgreSQL](https://www.postgresql.org/) с открытым исходным кодом.

Чтобы приступить к работе с базой данных Azure для PostgreSQL, см. инструкции по [подключению и созданию запросов к данным с помощью Java](/azure/postgresql/connect-java).

## <a name="client-jdbc-driver"></a>Клиентский драйвер JDBC

Подключайтесь к базе данных Azure для PostgreSQL из приложений с помощью [драйвера JDBC для PostgreSQL](https://jdbc.postgresql.org/) с открытым кодом. Вы можете использовать [API-интерфейс JDBC для Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/), чтобы подключаться непосредственно к базе данных, или платформы доступа к данным, которые взаимодействуют с базой данных через JDBC, например [Hibernate](http://hibernate.org/).

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентский драйвер JDBC в проекте.  

```XML
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.1.1</version>
</dependency>
```   

## <a name="example"></a>Пример

Подключитесь к базе данных Azure для PostgreSQL с помощью JDBC и выберите все записи в таблице продаж. Строку подключения JDBC для базы данных можно получить на портале Azure.

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

## <a name="samples"></a>Примеры

[Проектирование базы данных PostgreSQL с помощью Azure CLI](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) 

Ознакомьтесь с [примерами кода Java для базы данных Azure для PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres), которые можно использовать в своих приложениях.
