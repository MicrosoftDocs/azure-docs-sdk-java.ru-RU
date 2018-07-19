---
title: Библиотеки Java для базы данных Azure для MySQL
description: Справочная документация по клиентским библиотекам Java для базы данных Azure для MySQL
keywords: Azure, Java, SDK, API, SQL, database, PostGres, MySQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: mysql
ms.openlocfilehash: 72c94ef4bdad7adeae63da2efda93b52a9afef53
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931020"
---
# <a name="azure-database-for-mysql-libraries-for-java"></a>Библиотеки Java для базы данных Azure для MySQL

## <a name="overview"></a>Обзор

[База данных Azure для MySQL](/azure/sql-database/sql-database-technical-overview) — это служба реляционной базы данных на основе ядра СУБД [MySQL](https://www.mysql.com/) с открытым кодом. 

Чтобы приступить к работе с базой данных Azure для MySQL, ознакомьтесь со статьей [База данных Azure для MySQL: подключение и запрос данных с помощью Java](/azure/mysql/connect-java).

## <a name="client-jbdc-driver"></a>Клиентский драйвер JBDC

Подключайтесь к базе данных Azure для MySQL из приложений с помощью [драйвера JDBC с открытым кодом для MySQL](https://dev.mysql.com/downloads/connector/j/). Вы можете использовать [API-интерфейс JDBC для Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/), чтобы подключаться непосредственно к базе данных, или платформы доступа к данным, которые взаимодействуют с базой данных через JDBC, например [Hibernate](http://hibernate.org/).

[Добавьте зависимость](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) в файл Maven `pom.xml`, чтобы использовать клиентский драйвер JDBC в проекте.  

```XML
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.42</version>
</dependency>
```   

## <a name="example"></a>Пример

Подключитесь к базе данных Azure для MySQL с помощью JDBC и выберите все записи в таблице продаж. Строку подключения JDBC для базы данных можно получить на портале Azure.

```java
String url = String.format("jdbc:mysql://fabrikamysql.mysql.database.azure.com:3306/fabrikamdb?verifyServerCertificate=true&useSSL=true&requireSSL=false");
try {
    Connection conn = DriverManager.getConnection(url, "frank@fabrikamysql", "aBcDeFgHiJkL");
    String selectSql = "SELECT * FROM SALES";
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a>Примеры

[Создание веб-приложения Java в Azure с подключением к базе данных MySQL](/azure/app-service-web/app-service-web-tutorial-java-mysql)   
[Проектирование первой базы данных Azure для MySQL](/azure/mysql/tutorial-design-database-using-cli)   

Ознакомьтесь с другими [примерами кода Java для базы данных Azure для MySQL](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql), которые можно использовать в приложениях.
