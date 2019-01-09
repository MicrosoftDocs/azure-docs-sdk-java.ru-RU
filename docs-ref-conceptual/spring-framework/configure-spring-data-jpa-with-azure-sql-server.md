---
title: Как использовать JPA Spring Data с Базой данных SQL Azure
description: Узнайте, как использовать JPA Spring Data с Базой данных SQL Azure.
services: sql-database
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: sql-database
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 7119283bec250a4ab0854ba2c29b0906624448e9
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992509"
---
# <a name="how-to-use-spring-data-jpa-with-azure-sql-database"></a><span data-ttu-id="fe79c-103">Как использовать JPA Spring Data с Базой данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="fe79c-103">How to use Spring Data JPA with Azure SQL Database</span></span>

## <a name="overview"></a><span data-ttu-id="fe79c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="fe79c-104">Overview</span></span>

<span data-ttu-id="fe79c-105">В этой статье показано создание примера приложения, использующего [Spring Data] для хранения и извлечения информации в [Базу данных SQL Azure](https://azure.microsoft.com/services/sql-database/) с помощью [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span><span class="sxs-lookup"><span data-stu-id="fe79c-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) using [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe79c-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fe79c-106">Prerequisites</span></span>

<span data-ttu-id="fe79c-107">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="fe79c-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="fe79c-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="fe79c-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="fe79c-109">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="fe79c-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="fe79c-110">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="fe79c-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="fe79c-111">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="fe79c-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="fe79c-112">[Curl](https://curl.haxx.se/) или подобная служебная HTTP-программа, с помощью которой можно протестировать функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="fe79c-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="fe79c-113">Клиент [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="fe79c-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-sql-satabase"></a><span data-ttu-id="fe79c-114">Создание Базы данных Azure SQL</span><span class="sxs-lookup"><span data-stu-id="fe79c-114">Create an Azure SQL Satabase</span></span>

### <a name="create-a-sql-database-server-using-the-azure-portal"></a><span data-ttu-id="fe79c-115">Создание сервера Базы данных SQL с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="fe79c-115">Create a SQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="fe79c-116">Дополнительные сведения см. в статье о [создании Базы данных Azure SQL с помощью портала Azure](/azure/sql-database/sql-database-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="fe79c-116">You can read more detailed information about creating Azure SQL databases in [Create an Azure SQL database in the Azure portal](/azure/sql-database/sql-database-get-started-portal).</span></span>

1. <span data-ttu-id="fe79c-117">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="fe79c-117">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="fe79c-118">Щелкните элемент **+Create a resource** (+Создать ресурс), **Базы данных**, а затем выберите **База данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="fe79c-118">Click **+Create a resource**, then **Databases**, and then click **SQL Database**.</span></span>

   ![Создание базы данных SQL][SQL01]

1. <span data-ttu-id="fe79c-120">Укажите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="fe79c-120">Specify the following information:</span></span>

   - <span data-ttu-id="fe79c-121">**Имя базы данных**. Выберите уникальное имя Базы данных SQL. Позже оно будет использоваться при создании сервера SQL.</span><span class="sxs-lookup"><span data-stu-id="fe79c-121">**Database name**: Choose a unique name for your SQL database; this will be created in the SQL server that you will specify later.</span></span>
   - <span data-ttu-id="fe79c-122">**Подписка**: Укажите подписку Azure, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="fe79c-122">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="fe79c-123">**Группа ресурсов.** Укажите, следует ли создать группу ресурсов, или выберите имеющуюся группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fe79c-123">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="fe79c-124">**Выберите источник**. В рамках данного руководства выберите `Blank database`, чтобы создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="fe79c-124">**Select source**: For this tutorial, select `Blank database` to create a new database.</span></span>

   ![Укажите свойства Базы данных SQL][SQL02]
   
1. <span data-ttu-id="fe79c-126">Щелкните **Сервер**, после этого выберите **Создать сервер**, а затем укажите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="fe79c-126">Click **Server**, then **Create a new server**, and then specify the following information:</span></span>

   - <span data-ttu-id="fe79c-127">**Имя сервера**. Для сервера SQL выберите уникальное имя. Это имя будет использоваться для создания полного доменного имени, например *wingtiptoyssql.database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="fe79c-127">**Server name**: Choose a unique name for your SQL server; this will be used to create a fully-qualified domain name like *wingtiptoyssql.database.windows.net*.</span></span>
   - <span data-ttu-id="fe79c-128">**Учетные данные администратора сервера для входа**. Укажите имя администратора базы данных.</span><span class="sxs-lookup"><span data-stu-id="fe79c-128">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="fe79c-129">**Пароль** и **Подтверждение пароля**. Укажите пароль администратора базы данных.</span><span class="sxs-lookup"><span data-stu-id="fe79c-129">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="fe79c-130">**Расположение.** Укажите ближайший географический регион для базы данных.</span><span class="sxs-lookup"><span data-stu-id="fe79c-130">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Укажите SQL сервер][SQL03]

1. <span data-ttu-id="fe79c-132">После ввода всех этих данных нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="fe79c-132">When you have entered all of the above information, click **Select**.</span></span>

1. <span data-ttu-id="fe79c-133">В рамках этого руководства укажите самую низкую **ценовую категорию**, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fe79c-133">For this tutorial, specify the least-expensive **Pricing tier**, and then click **Create**.</span></span>

   ![Создание Базы данных SQL][SQL04]

### <a name="configure-a-firewall-rule-for-your-sql-server-using-the-azure-portal"></a><span data-ttu-id="fe79c-135">Настройка правила брандмауэра для SQL сервера с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="fe79c-135">Configure a firewall rule for your SQL server using the Azure Portal</span></span>

1. <span data-ttu-id="fe79c-136">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="fe79c-136">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="fe79c-137">Нажмите кнопку **Все ресурсы**, а затем щелкните только что созданный SQL сервер.</span><span class="sxs-lookup"><span data-stu-id="fe79c-137">Click **All Resources**, then click the SQL server you just created.</span></span>

   ![Выбор SQL сервера][SQL05]

1. <span data-ttu-id="fe79c-139">В разделе **Обзор** щелкните **Показать параметры брандмауэра**</span><span class="sxs-lookup"><span data-stu-id="fe79c-139">In the **Overview** section, click **Show firewall settings**</span></span>

   ![Показать параметры брандмауэра][SQL06]

1. <span data-ttu-id="fe79c-141">В разделе **Брандмауэры и виртуальные сети** создайте правило, указав для него уникальное имя, а затем введите диапазон IP-адресов, которым потребуется доступ к базе данных, и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fe79c-141">In the **Firewalls and virtual networks** section, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Настройка параметров брандмауэра][SQL07]

### <a name="retrieve-the-connection-string-for-your-sql-server-using-the-azure-portal"></a><span data-ttu-id="fe79c-143">Получение строки подключения для SQL сервера на портале Azure</span><span class="sxs-lookup"><span data-stu-id="fe79c-143">Retrieve the connection string for your SQL server using the Azure Portal</span></span>

1. <span data-ttu-id="fe79c-144">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="fe79c-144">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="fe79c-145">Нажмите кнопку **Все ресурсы**, а затем щелкните только что созданную Базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="fe79c-145">Click **All Resources**, then click the SQL database you just created.</span></span>

   ![Выбор Базы данных SQL][SQL08]

1. <span data-ttu-id="fe79c-147">Нажмите кнопку **Строки подключения**, затем щелкните**JDBC** и скопируйте значение в текстовое поле JDBC.</span><span class="sxs-lookup"><span data-stu-id="fe79c-147">Click **Connection strings**, then click **JDBC**, and copy the value in the JDBC text field.</span></span>

   ![Получение строки подключения JDBC][SQL09]

## <a name="configure-the-sample-application"></a><span data-ttu-id="fe79c-149">Настройка примера приложения</span><span class="sxs-lookup"><span data-stu-id="fe79c-149">Configure the sample application</span></span>

1. <span data-ttu-id="fe79c-150">Откройте командную строку и клонируйте пример проекта с помощью команды Git, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="fe79c-150">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="fe79c-151">Найдите файл *application.properties* в каталоге *resources* примера приложения или создайте его, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="fe79c-151">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="fe79c-152">Откройте файл *application.properties* в текстовом редакторе, добавьте или настройте указанные ниже строки в файл и замените примеры значений на соответствующие полученные ранее значения:</span><span class="sxs-lookup"><span data-stu-id="fe79c-152">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:sqlserver://wingtiptoyssql.database.windows.net:1433;database=wingtiptoys;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
   spring.datasource.username=wingtiptoysuser@wingtiptoyssql
   spring.datasource.password=********
    ```
   <span data-ttu-id="fe79c-153">Описание</span><span class="sxs-lookup"><span data-stu-id="fe79c-153">Where:</span></span>

   | <span data-ttu-id="fe79c-154">Параметр</span><span class="sxs-lookup"><span data-stu-id="fe79c-154">Parameter</span></span> | <span data-ttu-id="fe79c-155">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="fe79c-155">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="fe79c-156">Указывается измененная версия строки SQL JDBC, описанная ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="fe79c-156">Specifies an edited version of your SQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="fe79c-157">Указывается администратор SQL, описанный ранее в этой статье вместе с сокращенным именем сервера.</span><span class="sxs-lookup"><span data-stu-id="fe79c-157">Specifies your SQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="fe79c-158">Указывается пароль администратора SQL, описанный ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="fe79c-158">Specifies your SQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="fe79c-159">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="fe79c-159">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="fe79c-160">Упаковывание и тестирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="fe79c-160">Package and test the sample application</span></span> 

1. <span data-ttu-id="fe79c-161">Создайте пример приложения с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="fe79c-161">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P sql
   ```

1. <span data-ttu-id="fe79c-162">Запустите пример приложения, например:</span><span class="sxs-lookup"><span data-stu-id="fe79c-162">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jpa-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="fe79c-163">Из командной строки создайте записи с помощью `curl`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="fe79c-163">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="fe79c-164">Приложение должно возвращать значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fe79c-164">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="fe79c-165">Получите все имеющиеся записи из командной строки с помощью `curl`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="fe79c-165">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="fe79c-166">Приложение должно возвращать значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fe79c-166">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="fe79c-167">Сводка</span><span class="sxs-lookup"><span data-stu-id="fe79c-167">Summary</span></span>

<span data-ttu-id="fe79c-168">С помощью этого руководства вы создали пример приложения Java, использующий Spring Data для хранения и извлечения информации в Базу данных SQL Azure с помощью JPA.</span><span class="sxs-lookup"><span data-stu-id="fe79c-168">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure SQL database using JPA.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe79c-169">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="fe79c-169">Next steps</span></span>

<span data-ttu-id="fe79c-170">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="fe79c-170">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe79c-171">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="fe79c-171">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="fe79c-172">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fe79c-172">Additional Resources</span></span>

<span data-ttu-id="fe79c-173">Дополнительные сведения об использовании Java в Azure см. в статьях [Azure для разработчиков Java] и [Working with Azure DevOps and Java] (Работа с Azure DevOps и Java).</span><span class="sxs-lookup"><span data-stu-id="fe79c-173">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[SQL01]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-01.png
[SQL02]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-02.png
[SQL03]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-03.png
[SQL04]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-04.png
[SQL05]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-05.png
[SQL06]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-06.png
[SQL07]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-07.png
[SQL08]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-08.png
[SQL09]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-09.png
