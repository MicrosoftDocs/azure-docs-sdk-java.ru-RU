---
title: Как использовать JDBC Spring Data с базой данных Azure MySQL
description: Узнайте, как использовать JDBC Spring Data с базой данных Azure MySQL.
services: mysql
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: mysql
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 5ec89194c72cef81c79d21382e41b33ebe91d3d0
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992508"
---
# <a name="how-to-use-spring-data-jdbc-with-azure-mysql"></a><span data-ttu-id="a802f-103">Как использовать JDBC Spring Data с базой данных Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="a802f-103">How to use Spring Data JDBC with Azure MySQL</span></span>

## <a name="overview"></a><span data-ttu-id="a802f-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a802f-104">Overview</span></span>

<span data-ttu-id="a802f-105">В этой статье показано создание примера приложения, использующего [Spring Data] для хранения и извлечения информации в базу данных Azure [MySQL](https://www.mysql.com/) с помощью [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span><span class="sxs-lookup"><span data-stu-id="a802f-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [MySQL](https://www.mysql.com/) database using [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a802f-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a802f-106">Prerequisites</span></span>

<span data-ttu-id="a802f-107">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="a802f-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="a802f-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="a802f-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="a802f-109">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="a802f-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="a802f-110">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="a802f-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="a802f-111">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="a802f-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="a802f-112">[Curl](https://curl.haxx.se/) или подобная служебная HTTP-программа, с помощью которой можно протестировать функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="a802f-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="a802f-113">Служебная программа командной строки [mysql](https://dev.mysql.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="a802f-113">The [mysql](https://dev.mysql.com/downloads/) command-line utility.</span></span>
* <span data-ttu-id="a802f-114">Клиент [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="a802f-114">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-mysql-database-for-azure"></a><span data-ttu-id="a802f-115">Создание базы данных MySQL в Azure</span><span class="sxs-lookup"><span data-stu-id="a802f-115">Create a MySQL database for Azure</span></span>

### <a name="create-a-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="a802f-116">Создание сервера базы данных MySQL с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="a802f-116">Create a MySQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="a802f-117">Дополнительные сведения см. в статье о [создании базы данных Azure для сервера MySQL с помощью портала Azure](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="a802f-117">You can read more detailed information about creating MySQL databases in [Create an Azure Database for MySQL server by using the Azure portal](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span></span>

1. <span data-ttu-id="a802f-118">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="a802f-118">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="a802f-119">Щелкните элемент **+Create a resource** (+Создать ресурс), **Базы данных**, а затем выберите **База данных Azure для MySQL**.</span><span class="sxs-lookup"><span data-stu-id="a802f-119">Click **+Create a resource**, then **Databases**, and then click **Azure Database for MySQL**.</span></span>

   ![Создание базы данных MySQL][MYSQL01]

1. <span data-ttu-id="a802f-121">Введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="a802f-121">Enter the following information:</span></span>

   - <span data-ttu-id="a802f-122">**Имя сервера**. Для сервера MySQL выберите уникальное имя. Это имя будет использоваться для создания полного доменного имени, например *wingtiptoysmysql.mysql.database.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="a802f-122">**Server name**: Choose a unique name for your MySQL server; this will be used to create a fully-qualified domain name like *wingtiptoysmysql.mysql.database.azure.com*.</span></span>
   - <span data-ttu-id="a802f-123">**Подписка**: Укажите подписку Azure, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="a802f-123">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="a802f-124">**Группа ресурсов.** Укажите, следует ли создать группу ресурсов, или выберите имеющуюся группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a802f-124">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="a802f-125">**Выберите источник**. В рамках данного руководства выберите `Blank`, чтобы создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="a802f-125">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="a802f-126">**Учетные данные администратора сервера для входа**. Укажите имя администратора базы данных.</span><span class="sxs-lookup"><span data-stu-id="a802f-126">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="a802f-127">**Пароль** и **Подтверждение пароля**. Укажите пароль администратора базы данных.</span><span class="sxs-lookup"><span data-stu-id="a802f-127">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="a802f-128">**Расположение.** Укажите ближайший географический регион для базы данных.</span><span class="sxs-lookup"><span data-stu-id="a802f-128">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="a802f-129">**Версия.** Укажите самую последнюю версию базы данных.</span><span class="sxs-lookup"><span data-stu-id="a802f-129">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="a802f-130">**Ценовая категория**. В рамках этого руководства укажите самую низкую ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="a802f-130">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![Создание свойств базы данных MySQL][MYSQL02]

1. <span data-ttu-id="a802f-132">После ввода всех этих данных нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a802f-132">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="a802f-133">Настройка правила брандмауэра для сервера базы данных MySQL с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="a802f-133">Configure a firewall rule for your MySQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="a802f-134">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="a802f-134">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="a802f-135">Нажмите кнопку **Все ресурсы**, а затем щелкните только что созданную базу данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="a802f-135">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![Выбор базы данных MySQL][MYSQL03]

1. <span data-ttu-id="a802f-137">Щелкните **Безопасность подключения**, после этого создайте правило на вкладке **Правила брандмауэра**, указав для него уникальное имя, а затем введите диапазон IP-адресов, которым потребуется доступ к базе данных, и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a802f-137">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Настройка безопасности подключения][MYSQL04]

### <a name="retrieve-the-connection-string-for-your-mysql-server-using-the-azure-portal"></a><span data-ttu-id="a802f-139">Получение строки подключения для сервера MySQL на портале Azure</span><span class="sxs-lookup"><span data-stu-id="a802f-139">Retrieve the connection string for your MySQL server using the Azure Portal</span></span>

1. <span data-ttu-id="a802f-140">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="a802f-140">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="a802f-141">Нажмите кнопку **Все ресурсы**, а затем щелкните только что созданную базу данных MySQL.</span><span class="sxs-lookup"><span data-stu-id="a802f-141">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![Выбор базы данных MySQL][MYSQL03]

1. <span data-ttu-id="a802f-143">Нажмите кнопку **Строки подключения** и скопируйте значение в текстовое поле **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="a802f-143">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![Получение строки подключения JDBC][MYSQL05]

### <a name="create-mysql-database-using-the-mysql-command-line-utility"></a><span data-ttu-id="a802f-145">Создание базы данных MySQL с помощью служебной программы командной строки `mysql`</span><span class="sxs-lookup"><span data-stu-id="a802f-145">Create MySQL database using the `mysql` command-line utility</span></span>

1. <span data-ttu-id="a802f-146">Откройте командную оболочку и подключитесь к серверу MySQL, введя команду `mysql`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="a802f-146">Open a command shell and connect to your MySQL server by entering a `mysql` command like the following example:</span></span>

   ```shell
   mysql --host wingtiptoysmysql.mysql.database.azure.com --user wingtiptoysuser@wingtiptoysmysql -p
   ```
   <span data-ttu-id="a802f-147">Описание</span><span class="sxs-lookup"><span data-stu-id="a802f-147">Where:</span></span>

   | <span data-ttu-id="a802f-148">Параметр</span><span class="sxs-lookup"><span data-stu-id="a802f-148">Parameter</span></span> | <span data-ttu-id="a802f-149">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="a802f-149">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="a802f-150">Указывается полное доменное имя сервера MySQL, описанное ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a802f-150">Specifies your fully qualified MySQL server name from earlier in this article.</span></span> |
   | `user` | <span data-ttu-id="a802f-151">Указываются администратор MySQL и сокращенное имя сервера, описанные ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a802f-151">Specifies your MySQL administrator and shortened server name from earlier in this article.</span></span> |
   | `p` | <span data-ttu-id="a802f-152">Указывается, что следует ожидать запрос пароля.</span><span class="sxs-lookup"><span data-stu-id="a802f-152">Specifies to wait until prompted for a password.</span></span> |

   <span data-ttu-id="a802f-153">Сервер MySQL должен отобразить экран, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="a802f-153">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   Welcome to the MySQL monitor.  Commands end with ; or \g.
   Your MySQL connection id is 64552
   Server version: 5.6.39.0 MySQL Community Server (GPL)
   
   Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.
   
   Oracle is a registered trademark of Oracle Corporation and/or its
   affiliates. Other names may be trademarks of their respective
   owners.
   
   Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
   
   mysql>
   ```

1. <span data-ttu-id="a802f-154">Создайте базу данных с именем *mysqldb*, введя команду `mysql`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="a802f-154">Create a database named *mysqldb* by entering a `mysql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mysqldb;
   ```

   <span data-ttu-id="a802f-155">Сервер MySQL должен отобразить экран, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="a802f-155">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   Query OK, 1 row affected (0.30 sec)
   ```

1. <span data-ttu-id="a802f-156">НЕОБЯЗАТЕЛЬНО. Убедитесь, что база данных создана, введя команду `mysql`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="a802f-156">OPTIONAL: You can verify that your database was created by entering a `mysql` command like the following example:</span></span>

   ```SQL
   SHOW DATABASES;
   ```

   <span data-ttu-id="a802f-157">Сервер MySQL должен отобразить экран, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="a802f-157">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   +--------------------+
   | Database           |
   +--------------------+
   | information_schema |
   | mysql              |
   | mysqldb            |
   | performance_schema |
   | sys                |
   +--------------------+
   ```

1. <span data-ttu-id="a802f-158">Введите `\q` для выхода из служебной программы `mysql`.</span><span class="sxs-lookup"><span data-stu-id="a802f-158">Enter `\q` to exit the `mysql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="a802f-159">Настройка примера приложения</span><span class="sxs-lookup"><span data-stu-id="a802f-159">Configure the sample application</span></span>

1. <span data-ttu-id="a802f-160">Откройте командную строку и клонируйте пример проекта с помощью команды Git, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="a802f-160">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="a802f-161">Найдите файл *application.properties* в каталоге *resources* примера приложения или создайте его, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="a802f-161">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="a802f-162">Откройте файл *application.properties* в текстовом редакторе, добавьте или настройте указанные ниже строки в файл и замените примеры значений на соответствующие полученные ранее значения:</span><span class="sxs-lookup"><span data-stu-id="a802f-162">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:mysql://wingtiptoysmysql.mysql.database.azure.com:3306/mysqldb?useSSL=true&requireSSL=false&serverTimezone=UTC
   spring.datasource.username=wingtiptoysuser@wingtiptoysmysql
   spring.datasource.password=********
    ```
   <span data-ttu-id="a802f-163">Описание</span><span class="sxs-lookup"><span data-stu-id="a802f-163">Where:</span></span>

   | <span data-ttu-id="a802f-164">Параметр</span><span class="sxs-lookup"><span data-stu-id="a802f-164">Parameter</span></span> | <span data-ttu-id="a802f-165">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="a802f-165">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="a802f-166">Указываются строки MySQL JDBC, описанные ранее в этой статье, с добавлением часового пояса.</span><span class="sxs-lookup"><span data-stu-id="a802f-166">Specifies your MySQL JDBC string from earlier in this article, with the time zone added.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="a802f-167">Указывается администратор MySQL, описанный ранее в этой статье, вместе с сокращенным именем сервера.</span><span class="sxs-lookup"><span data-stu-id="a802f-167">Specifies your MySQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="a802f-168">Указывается пароль администратора MySQL, описанный ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="a802f-168">Specifies your MySQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="a802f-169">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="a802f-169">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="a802f-170">Упаковывание и тестирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="a802f-170">Package and test the sample application</span></span> 

1. <span data-ttu-id="a802f-171">Создайте пример приложения с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="a802f-171">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P mysql
   ```

1. <span data-ttu-id="a802f-172">Запустите пример приложения, например:</span><span class="sxs-lookup"><span data-stu-id="a802f-172">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="a802f-173">Из командной строки создайте записи с помощью `curl`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="a802f-173">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="a802f-174">Приложение должно возвращать значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a802f-174">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="a802f-175">Получите все имеющиеся записи из командной строки с помощью `curl`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="a802f-175">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="a802f-176">Приложение должно возвращать значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a802f-176">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="a802f-177">Сводка</span><span class="sxs-lookup"><span data-stu-id="a802f-177">Summary</span></span>

<span data-ttu-id="a802f-178">С помощью этого руководства вы создали пример приложения Java, использующий Spring Data для хранения и извлечения информации в базу данных Azure MySQL с помощью JDBC.</span><span class="sxs-lookup"><span data-stu-id="a802f-178">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure MySQL database using JDBC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a802f-179">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="a802f-179">Next steps</span></span>

<span data-ttu-id="a802f-180">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="a802f-180">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a802f-181">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="a802f-181">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="a802f-182">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a802f-182">Additional Resources</span></span>

<span data-ttu-id="a802f-183">Дополнительные сведения об использовании Java в Azure см. в статьях [Azure для разработчиков Java] и [Working with Azure DevOps and Java] (Работа с Azure DevOps и Java).</span><span class="sxs-lookup"><span data-stu-id="a802f-183">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<!-- URL List -->

[Azure для разработчиков Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Working with Azure DevOps and Java]: /azure/devops/ (Работа с Azure DevOps и Java)
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Data]: https://spring.io/projects/spring-data
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[MYSQL01]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-01.png
[MYSQL02]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-02.png
[MYSQL03]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-03.png
[MYSQL04]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-04.png
[MYSQL05]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-05.png
