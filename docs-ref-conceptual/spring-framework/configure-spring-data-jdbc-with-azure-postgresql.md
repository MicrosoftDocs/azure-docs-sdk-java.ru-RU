---
title: Как использовать JDBC Spring Data с базой данных Azure PostgreSQL
description: Узнайте, как использовать JDBC Spring Data с базой данных Azure PostgreSQL.
services: postgresql
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: postgresql
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 29f3c957dd0ccd754eedef12e3fc01c3484dddf3
ms.sourcegitcommit: 1c1412ad5d8960975c3fc7fd3d1948152ef651ef
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/05/2019
ms.locfileid: "57335397"
---
# <a name="how-to-use-spring-data-jdbc-with-azure-postgresql"></a><span data-ttu-id="24694-103">Как использовать JDBC Spring Data с базой данных Azure PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="24694-103">How to use Spring Data JDBC with Azure PostgreSQL</span></span>

## <a name="overview"></a><span data-ttu-id="24694-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="24694-104">Overview</span></span>

<span data-ttu-id="24694-105">В этой статье показано, как создать пример приложения, использующего [Spring Data] для хранения и извлечения информации в базу данных Azure [PostgreSQL](https://www.postgresql.org/) с помощью [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span><span class="sxs-lookup"><span data-stu-id="24694-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [PostgreSQL](https://www.postgresql.org/) database using [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24694-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="24694-106">Prerequisites</span></span>

<span data-ttu-id="24694-107">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="24694-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="24694-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="24694-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="24694-109">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="24694-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="24694-110">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="24694-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="24694-111">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="24694-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="24694-112">[Curl](https://curl.haxx.se/) или подобная служебная HTTP-программа, с помощью которой можно протестировать функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="24694-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="24694-113">Служебная программа командной строки [psql](https://www.postgresql.org/docs/current/app-psql.html).</span><span class="sxs-lookup"><span data-stu-id="24694-113">The [psql](https://www.postgresql.org/docs/current/app-psql.html) command-line utility.</span></span>
* <span data-ttu-id="24694-114">Клиент [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="24694-114">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-postgresql-database-for-azure"></a><span data-ttu-id="24694-115">Создание базы данных PostgreSQL в Azure</span><span class="sxs-lookup"><span data-stu-id="24694-115">Create a PostgreSQL database for Azure</span></span>

### <a name="create-a-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="24694-116">Создание сервера базы данных PostgreSQL с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="24694-116">Create a PostgreSQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="24694-117">Дополнительные сведения см. в статье о [создании базы данных Azure для сервера PostgreSQL с помощью портала Azure](/azure/postgresql/quickstart-create-server-database-portal).</span><span class="sxs-lookup"><span data-stu-id="24694-117">You can read more detailed information about creating PostgreSQL databases in [Create an Azure Database for PostgreSQL server by using the Azure portal](/azure/postgresql/quickstart-create-server-database-portal).</span></span>

1. <span data-ttu-id="24694-118">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="24694-118">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="24694-119">Щелкните элемент **+Create a resource** (+Создать ресурс), **Базы данных**, а затем выберите **База данных Azure для PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="24694-119">Click **+Create a resource**, then **Databases**, and then click **Azure Database for PostgreSQL**.</span></span>

   ![Создание базы данных PostgreSQL][POSTGRESQL01]

1. <span data-ttu-id="24694-121">Введите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="24694-121">Enter the following information:</span></span>

   - <span data-ttu-id="24694-122">**Имя сервера**. Для сервера PostgreSQL выберите уникальное имя. Это имя будет использоваться для создания полного доменного имени, например *wingtiptoyspostgresql.postgres.database.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="24694-122">**Server name**: Choose a unique name for your PostgreSQL server; this will be used to create a fully-qualified domain name like *wingtiptoyspostgresql.postgres.database.azure.com*.</span></span>
   - <span data-ttu-id="24694-123">**Подписка**: Укажите подписку Azure, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="24694-123">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="24694-124">**Группа ресурсов.** Укажите, следует ли создать группу ресурсов, или выберите имеющуюся группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="24694-124">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="24694-125">**Выберите источник**. В рамках данного руководства выберите `Blank`, чтобы создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="24694-125">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="24694-126">**Учетные данные администратора сервера для входа**. Укажите имя администратора базы данных.</span><span class="sxs-lookup"><span data-stu-id="24694-126">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="24694-127">**Пароль** и **Подтверждение пароля**. Укажите пароль администратора базы данных.</span><span class="sxs-lookup"><span data-stu-id="24694-127">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="24694-128">**Расположение.** Укажите ближайший географический регион для базы данных.</span><span class="sxs-lookup"><span data-stu-id="24694-128">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="24694-129">**Версия.** Укажите самую последнюю версию базы данных.</span><span class="sxs-lookup"><span data-stu-id="24694-129">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="24694-130">**Ценовая категория**. В рамках этого руководства укажите самую низкую ценовую категорию.</span><span class="sxs-lookup"><span data-stu-id="24694-130">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![Создание свойств базы данных PostgreSQL][POSTGRESQL02]

1. <span data-ttu-id="24694-132">После ввода всех этих данных нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="24694-132">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="24694-133">Настройка правила брандмауэра для сервера базы данных PostgreSQL с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="24694-133">Configure a firewall rule for your PostgreSQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="24694-134">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="24694-134">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="24694-135">Нажмите кнопку **Все ресурсы**, а затем щелкните только что созданную базу данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="24694-135">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Выбор базы данных PostgreSQL][POSTGRESQL03]

1. <span data-ttu-id="24694-137">Щелкните **Безопасность подключения**, после этого создайте правило на вкладке **Правила брандмауэра**, указав для него уникальное имя, а затем введите диапазон IP-адресов, которым потребуется доступ к базе данных, и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="24694-137">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Настройка безопасности подключения][POSTGRESQL04]

### <a name="retrieve-the-connection-string-for-your-postgresql-server-using-the-azure-portal"></a><span data-ttu-id="24694-139">Получение строки подключения для сервера PostgreSQL на портале Azure</span><span class="sxs-lookup"><span data-stu-id="24694-139">Retrieve the connection string for your PostgreSQL server using the Azure Portal</span></span>

1. <span data-ttu-id="24694-140">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="24694-140">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="24694-141">Нажмите кнопку **Все ресурсы**, а затем щелкните только что созданную базу данных PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="24694-141">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Выбор базы данных PostgreSQL][POSTGRESQL03]

1. <span data-ttu-id="24694-143">Нажмите кнопку **Строки подключения** и скопируйте значение в текстовое поле **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="24694-143">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![Получение строки подключения JDBC][POSTGRESQL05]

### <a name="create-postgresql-database-using-the-psql-command-line-utility"></a><span data-ttu-id="24694-145">Создание базы данных PostgreSQL с помощью служебной программы командной строки `psql`</span><span class="sxs-lookup"><span data-stu-id="24694-145">Create PostgreSQL database using the `psql` command-line utility</span></span>

1. <span data-ttu-id="24694-146">Откройте командную оболочку и подключитесь к серверу PostgreSQL, введя команду `psql`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="24694-146">Open a command shell and connect to your PostgreSQL server by entering a `psql` command like the following example:</span></span>

   ```shell
   psql --host=wingtiptoyspostgresql.postgres.database.azure.com --port=5432 --username=wingtiptoysuser@wingtiptoyspostgresql --dbname=postgres
   ```
   <span data-ttu-id="24694-147">Описание</span><span class="sxs-lookup"><span data-stu-id="24694-147">Where:</span></span>

   | <span data-ttu-id="24694-148">Параметр</span><span class="sxs-lookup"><span data-stu-id="24694-148">Parameter</span></span> | <span data-ttu-id="24694-149">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="24694-149">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="24694-150">Указывается полное доменное имя сервера PostgreSQL, описанное ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="24694-150">Specifies your fully qualified PostgreSQL server name from earlier in this article.</span></span> |
   | `host` | <span data-ttu-id="24694-151">Указывается порт сервера PostgreSQL, то есть по умолчанию — `5432`.</span><span class="sxs-lookup"><span data-stu-id="24694-151">Specifies the PostgreSQL server port, which is `5432` by default.</span></span> |
   | `username` | <span data-ttu-id="24694-152">Указывается администратор PostgreSQL и сокращенное имя сервера, описанные ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="24694-152">Specifies your PostgreSQL administrator and shortened server name from earlier in this article.</span></span> |
   | `dbname` | <span data-ttu-id="24694-153">Указывается, хотите ли вы сейчас использовать по умолчанию базу данных `postgres`.</span><span class="sxs-lookup"><span data-stu-id="24694-153">Specifies that you want to use the default `postgres` database for now.</span></span> |

   <span data-ttu-id="24694-154">Сервер PostgreSQL должен отобразить экран, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="24694-154">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   psql (9.3.24, server 10.5)
   SSL connection (cipher: ECDHE-RSA-AES256-SHA384, bits: 256)
   Type "help" for help.
   
   postgres=>
   ```

1. <span data-ttu-id="24694-155">Создайте базу данных с именем *mypgsqldb*, введя команду `psql`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="24694-155">Create a database named *mypgsqldb* by entering a `psql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mypgsqldb;
   ```

   <span data-ttu-id="24694-156">Сервер PostgreSQL должен отобразить экран, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="24694-156">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   CREATE DATABASE
   ```

1. <span data-ttu-id="24694-157">НЕОБЯЗАТЕЛЬНО. Убедитесь, что база данных создана, введя `\l` в `psql`. Сервер PostgreSQL должен вернуть ответ примерно такого содержания, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="24694-157">OPTIONAL: You can verify that your database was created by entering a `\l` at the `psql`; your PostgreSQL server should respond with something like the following example:</span></span>

   ```shell
                   List of databases
          Name        |      Owner      | Encoding
   -------------------+-----------------+----------
    azure_maintenance | azure_superuser | UTF8
    azure_sys         | azure_superuser | UTF8
    mypgsqldb         | wingtiptoysuser | UTF8
    postgres          | azure_superuser | UTF8
    template0         | azure_superuser | UTF8
    template1         | azure_superuser | UTF8
   (6 rows)
   ```

1. <span data-ttu-id="24694-158">Введите `\q` для выхода из служебной программы `psql`.</span><span class="sxs-lookup"><span data-stu-id="24694-158">Enter `\q` to exit the `psql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="24694-159">Настройка примера приложения</span><span class="sxs-lookup"><span data-stu-id="24694-159">Configure the sample application</span></span>

1. <span data-ttu-id="24694-160">Откройте командную строку и клонируйте пример проекта с помощью команды Git, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="24694-160">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="24694-161">Найдите файл *application.properties* в каталоге *resources* примера приложения или создайте его, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="24694-161">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="24694-162">Откройте файл *application.properties* в текстовом редакторе, добавьте или настройте указанные ниже строки в файл и замените примеры значений на соответствующие полученные ранее значения:</span><span class="sxs-lookup"><span data-stu-id="24694-162">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:postgresql://wingtiptoyspostgresql.postgres.database.azure.com:5432/mypgsqldb?ssl=true&sslmode=prefer
   spring.datasource.username=wingtiptoysuser@wingtiptoyspostgresql
   spring.datasource.password=********
    ```
   <span data-ttu-id="24694-163">Описание</span><span class="sxs-lookup"><span data-stu-id="24694-163">Where:</span></span>

   | <span data-ttu-id="24694-164">Параметр</span><span class="sxs-lookup"><span data-stu-id="24694-164">Parameter</span></span> | <span data-ttu-id="24694-165">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="24694-165">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="24694-166">Указываются строки PostgreSQL JDBC, описанные ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="24694-166">Specifies your PostgreSQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="24694-167">Указывается администратор PostgreSQL, описанный ранее в этой статье, вместе с сокращенным именем сервера.</span><span class="sxs-lookup"><span data-stu-id="24694-167">Specifies your PostgreSQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="24694-168">Указывается пароль администратора PostgreSQL, описанный ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="24694-168">Specifies your PostgreSQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="24694-169">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="24694-169">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="24694-170">Упаковывание и тестирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="24694-170">Package and test the sample application</span></span> 

1. <span data-ttu-id="24694-171">Создайте пример приложения с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="24694-171">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P postgresql
   ```

1. <span data-ttu-id="24694-172">Запустите пример приложения, например:</span><span class="sxs-lookup"><span data-stu-id="24694-172">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="24694-173">Из командной строки создайте записи с помощью `curl`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="24694-173">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="24694-174">Приложение должно возвращать значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="24694-174">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="24694-175">Получите все имеющиеся записи из командной строки с помощью `curl`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="24694-175">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="24694-176">Приложение должно возвращать значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="24694-176">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="24694-177">Сводка</span><span class="sxs-lookup"><span data-stu-id="24694-177">Summary</span></span>

<span data-ttu-id="24694-178">С помощью этого руководства вы создали пример приложения Java, использующий Spring Data для хранения и извлечения информации в базу данных Azure PostgreSQL с помощью JDBC.</span><span class="sxs-lookup"><span data-stu-id="24694-178">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure PostgreSQL database using JDBC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24694-179">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="24694-179">Next steps</span></span>

<span data-ttu-id="24694-180">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="24694-180">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="24694-181">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="24694-181">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="24694-182">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="24694-182">Additional Resources</span></span>

<span data-ttu-id="24694-183">Дополнительные сведения об использовании Java в Azure см. в статьях [Azure для разработчиков Java] и [Working with Azure DevOps and Java] (Работа с Azure DevOps и Java).</span><span class="sxs-lookup"><span data-stu-id="24694-183">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[POSTGRESQL01]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-01.png
[POSTGRESQL02]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-02.png
[POSTGRESQL03]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-03.png
[POSTGRESQL04]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-04.png
[POSTGRESQL05]: media/configure-spring-data-jdbc-with-azure-postgresql/create-postgresql-05.png
