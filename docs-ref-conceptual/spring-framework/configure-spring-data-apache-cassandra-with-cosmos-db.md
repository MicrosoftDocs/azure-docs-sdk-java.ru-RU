---
title: Как использовать API Apache Cassandra Spring Data с Azure Cosmos DB
description: Узнайте, как использовать API Apache Cassandra Spring Data с Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 1f3f7a55b49d64077df9e7d4d6acc3af4495b424
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992505"
---
# <a name="how-to-use-spring-data-apache-cassandra-api-with-azure-cosmos-db"></a><span data-ttu-id="90044-103">Как использовать API Apache Cassandra Spring Data с Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="90044-103">How to use Spring Data Apache Cassandra API with Azure Cosmos DB</span></span>

## <a name="overview"></a><span data-ttu-id="90044-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="90044-104">Overview</span></span>

<span data-ttu-id="90044-105">В этой статье показано создание примера приложения, использующего [Spring Data] для хранения и извлечения информации с помощью [API Cassandra для Azure Cosmos DB](/azure/cosmos-db/cassandra-introduction).</span><span class="sxs-lookup"><span data-stu-id="90044-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information using the [Azure Cosmos DB Cassandra API](/azure/cosmos-db/cassandra-introduction).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90044-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="90044-106">Prerequisites</span></span>

<span data-ttu-id="90044-107">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="90044-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="90044-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="90044-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="90044-109">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="90044-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="90044-110">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="90044-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="90044-111">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="90044-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="90044-112">[Curl](https://curl.haxx.se/) или подобная служебная HTTP-программа, с помощью которой можно протестировать функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="90044-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="90044-113">Клиент [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="90044-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="90044-114">создание учетной записи Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="90044-114">Create an Azure Cosmos DB account</span></span>

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a><span data-ttu-id="90044-115">Создание учетной записи Cosmos DB с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="90044-115">Create a Cosmos DB account using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="90044-116">Более подробные сведения о создании учетных записей Azure Cosmos DB см. в статье [о документации по Azure Cosmos DB](/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="90044-116">You can read more detailed information about creating Azure Cosmos DB accounts in [Azure Cosmos DB Documentation](/azure/cosmos-db/).</span></span>

1. <span data-ttu-id="90044-117">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="90044-117">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="90044-118">Щелкните элемент **+Create a resource** (+Создать ресурс), **Базы данных**, а затем выберите **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="90044-118">Click **+Create a resource**, then **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![создание учетной записи Azure Cosmos DB;][COSMOSDB01]

1. <span data-ttu-id="90044-120">Укажите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="90044-120">Specify the following information:</span></span>

   - <span data-ttu-id="90044-121">**Подписка**: Укажите подписку Azure, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="90044-121">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="90044-122">**Группа ресурсов.** Укажите, следует ли создать группу ресурсов, или выберите имеющуюся группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="90044-122">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="90044-123">**Имя учетной записи**. Для учетной записи Cosmos DB выберите уникальное имя. Это имя будет использоваться для создания полного доменного имени, например *wingtiptoyscassandra.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="90044-123">**Account name**: Choose a unique name for your Cosmos DB account; this will be used to create a fully-qualified domain name like *wingtiptoyscassandra.documents.azure.com*.</span></span>
   - <span data-ttu-id="90044-124">**API**. В данном руководстве укажите `Cassandra`.</span><span class="sxs-lookup"><span data-stu-id="90044-124">**API**: Specify `Cassandra` for this tutorial.</span></span>
   - <span data-ttu-id="90044-125">**Расположение.** Укажите ближайший географический регион для базы данных.</span><span class="sxs-lookup"><span data-stu-id="90044-125">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Указание параметров учетной записи Cosmos DB][COSMOSDB02]
   
1. <span data-ttu-id="90044-127">После ввода всех этих данных нажмите кнопку **Отзыв и создание**.</span><span class="sxs-lookup"><span data-stu-id="90044-127">When you have entered all of the above information, click **Review + create**.</span></span>

1. <span data-ttu-id="90044-128">Если при просмотре страницы все выглядит правильно, щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="90044-128">If everything looks correct on the review page, click **Create**.</span></span>

   ![Проверка параметров учетной записи Cosmos DB][COSMOSDB03]

### <a name="add-a-keyspace-to-your-azure-cosmos-db-account"></a><span data-ttu-id="90044-130">Добавление пространства ключей к учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="90044-130">Add a keyspace to your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="90044-131">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="90044-131">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="90044-132">Нажмите кнопку **Все ресурсы**, а затем щелкните только что созданную учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="90044-132">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Выбор учетной записи Azure Cosmos DB][COSMOSDB04]

1. <span data-ttu-id="90044-134">Щелкните **Обозреватель данных**, а затем выберите **New Keyspace** (Новое пространство ключей).</span><span class="sxs-lookup"><span data-stu-id="90044-134">Click **Data Explorer**, then click **New Keyspace**.</span></span> <span data-ttu-id="90044-135">Введите уникальный идентификатор в поле **Keyspace id** (Идентификатор пространства ключей), а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="90044-135">Enter a unique identifier for your **Keyspace id**, then click **OK**.</span></span>

   ![Создание пространства ключей Cosmos DB][COSMOSDB05]

### <a name="retrieve-the-connection-settings-for-your-azure-cosmos-db-account"></a><span data-ttu-id="90044-137">Получение параметров подключения к учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="90044-137">Retrieve the connection settings for your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="90044-138">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="90044-138">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="90044-139">Нажмите кнопку **Все ресурсы**, а затем щелкните только что созданную учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="90044-139">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Выбор учетной записи Azure Cosmos DB][COSMOSDB04]

1. <span data-ttu-id="90044-141">Нажмите кнопку **Строки подключения** и скопируйте соответствующие значения для полей **Точка контакта**, **Порт**, **Имя пользователя** и **Основной пароль**. Позже эти значения будут использоваться для настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="90044-141">Click **Connection strings**, and copy the values for the **Contact Point**, **Port**, **Username**, and **Primary Password** fields; you will use those values to configure your application later.</span></span>

   ![Получение параметров подключения к Cosmos DB][COSMOSDB05]

## <a name="configure-the-sample-application"></a><span data-ttu-id="90044-143">Настройка примера приложения</span><span class="sxs-lookup"><span data-stu-id="90044-143">Configure the sample application</span></span>

1. <span data-ttu-id="90044-144">Откройте командную строку и клонируйте пример проекта с помощью команды Git, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="90044-144">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-cassandra-on-azure.git
   ```

1. <span data-ttu-id="90044-145">Найдите файл *application.properties* в каталоге *resources* примера приложения или создайте его, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="90044-145">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="90044-146">Откройте файл *application.properties* в текстовом редакторе, добавьте или настройте указанные ниже строки в файл и замените примеры значений на соответствующие полученные ранее значения:</span><span class="sxs-lookup"><span data-stu-id="90044-146">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.data.cassandra.contact-points=wingtiptoyscassandra.cassandra.cosmosdb.azure.com
   spring.data.cassandra.port=10350
   spring.data.cassandra.username=wingtiptoyscassandra
   spring.data.cassandra.password=********
   ```
   <span data-ttu-id="90044-147">Описание</span><span class="sxs-lookup"><span data-stu-id="90044-147">Where:</span></span>

   | <span data-ttu-id="90044-148">Параметр</span><span class="sxs-lookup"><span data-stu-id="90044-148">Parameter</span></span> | <span data-ttu-id="90044-149">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="90044-149">Description</span></span> |
   |---|---|
   | `spring.data.cassandra.contact-points` | <span data-ttu-id="90044-150">Указывается **точка контакта**, описанная ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="90044-150">Specifies the **Contact Point** from earlier in this article.</span></span> |
   | `spring.data.cassandra.port` | <span data-ttu-id="90044-151">Указывается **порт**, описанный ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="90044-151">Specifies the **Port** from earlier in this article.</span></span> |
   | `spring.data.cassandra.username` | <span data-ttu-id="90044-152">Указывается **имя пользователя**, описанное ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="90044-152">Specifies your **Username** from earlier in this article.</span></span> |
   | `spring.data.cassandra.password` | <span data-ttu-id="90044-153">Указывается **основной пароль**, описанный ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="90044-153">Specifies your **Primary Password** from earlier in this article.</span></span> |

1. <span data-ttu-id="90044-154">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="90044-154">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="90044-155">Упаковывание и тестирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="90044-155">Package and test the sample application</span></span> 

1. <span data-ttu-id="90044-156">Создайте пример приложения с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="90044-156">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="90044-157">Запустите пример приложения, например:</span><span class="sxs-lookup"><span data-stu-id="90044-157">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-cassandra-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="90044-158">Из командной строки создайте записи с помощью `curl`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="90044-158">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="90044-159">Приложение должно возвращать значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="90044-159">Your application should return values like the following:</span></span>

   ```shell
   Added Pet{id=60fa8cb0-0423-11e9-9a70-39311962166b, name='dog', species='canine'}.

   Added Pet{id=72c1c9e0-0423-11e9-9a70-39311962166b, name='cat', species='feline'}.
   ```

1. <span data-ttu-id="90044-160">Получите все имеющиеся записи из командной строки с помощью `curl`, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="90044-160">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="90044-161">Приложение должно возвращать значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="90044-161">Your application should return values like the following:</span></span>

   ```json
   [{"id":"60fa8cb0-0423-11e9-9a70-39311962166b","name":"dog","species":"canine"},{"id":"72c1c9e0-0423-11e9-9a70-39311962166b","name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="90044-162">Сводка</span><span class="sxs-lookup"><span data-stu-id="90044-162">Summary</span></span>

<span data-ttu-id="90044-163">С помощью этого руководства вы создали пример приложения Java, использующий Spring Data для хранения и извлечения информации с помощью API Cassandra для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="90044-163">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information using the Azure Cosmos DB Cassandra API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90044-164">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="90044-164">Next steps</span></span>

<span data-ttu-id="90044-165">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="90044-165">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="90044-166">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="90044-166">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="90044-167">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="90044-167">Additional Resources</span></span>

<span data-ttu-id="90044-168">Дополнительные сведения об использовании Java в Azure см. в статьях [Azure для разработчиков Java] и [Working with Azure DevOps and Java] (Работа с Azure DevOps и Java).</span><span class="sxs-lookup"><span data-stu-id="90044-168">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[COSMOSDB01]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB05]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-05.png
