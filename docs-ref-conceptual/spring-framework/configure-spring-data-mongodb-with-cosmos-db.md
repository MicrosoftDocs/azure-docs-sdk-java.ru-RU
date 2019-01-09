---
title: Как использовать API MongoDB Spring Data с Azure Cosmos DB
description: Узнайте, как использовать API MongoDB Spring Data с Azure Cosmos DB.
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
ms.openlocfilehash: 55fb356820e2cc5eb8d1fe4030053d9e580583af
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992544"
---
# <a name="how-to-use-spring-data-mongodb-api-with-azure-cosmos-db"></a><span data-ttu-id="b14b9-103">Как использовать API MongoDB Spring Data с Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b14b9-103">How to use Spring Data MongoDB API with Azure Cosmos DB</span></span>

## <a name="overview"></a><span data-ttu-id="b14b9-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="b14b9-104">Overview</span></span>

<span data-ttu-id="b14b9-105">В этой статье показано создание примера приложения, использующего [Spring Data] для хранения и извлечения информации с помощью [API MongoDB для Azure Cosmos DB](/azure/cosmos-db/mongodb-introduction).</span><span class="sxs-lookup"><span data-stu-id="b14b9-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information using the [Azure Cosmos DB MongoDB API](/azure/cosmos-db/mongodb-introduction).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b14b9-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b14b9-106">Prerequisites</span></span>

<span data-ttu-id="b14b9-107">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="b14b9-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="b14b9-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="b14b9-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="b14b9-109">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="b14b9-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="b14b9-110">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="b14b9-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="b14b9-111">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="b14b9-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="b14b9-112">Клиент [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="b14b9-112">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="b14b9-113">создание учетной записи Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="b14b9-113">Create an Azure Cosmos DB account</span></span>

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a><span data-ttu-id="b14b9-114">Создание учетной записи Cosmos DB с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="b14b9-114">Create a Cosmos DB account using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="b14b9-115">Более подробные сведения о создании учетных записей Azure Cosmos DB см. в статье [о документации по Azure Cosmos DB](/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="b14b9-115">You can read more detailed information about creating Azure Cosmos DB accounts in [Azure Cosmos DB Documentation](/azure/cosmos-db/).</span></span>

1. <span data-ttu-id="b14b9-116">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="b14b9-116">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="b14b9-117">Щелкните элемент **+Create a resource** (+Создать ресурс), **Базы данных**, а затем выберите **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="b14b9-117">Click **+Create a resource**, then **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![создание учетной записи Azure Cosmos DB;][COSMOSDB01]

1. <span data-ttu-id="b14b9-119">Укажите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="b14b9-119">Specify the following information:</span></span>

   - <span data-ttu-id="b14b9-120">**Подписка**: Укажите подписку Azure, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="b14b9-120">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="b14b9-121">**Группа ресурсов.** Укажите, следует ли создать группу ресурсов, или выберите имеющуюся группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b14b9-121">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="b14b9-122">**Имя учетной записи**. Для учетной записи Cosmos DB выберите уникальное имя. Это имя будет использоваться для создания полного доменного имени, например *wingtiptoysmongodb.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="b14b9-122">**Account name**: Choose a unique name for your Cosmos DB account; this will be used to create a fully-qualified domain name like *wingtiptoysmongodb.documents.azure.com*.</span></span>
   - <span data-ttu-id="b14b9-123">**API**. В данном руководстве укажите `Azure Cosmos DB for MongoDB API`.</span><span class="sxs-lookup"><span data-stu-id="b14b9-123">**API**: Specify `Azure Cosmos DB for MongoDB API` for this tutorial.</span></span>
   - <span data-ttu-id="b14b9-124">**Расположение.** Укажите ближайший географический регион для базы данных.</span><span class="sxs-lookup"><span data-stu-id="b14b9-124">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Указание параметров учетной записи Cosmos DB][COSMOSDB02]
   
1. <span data-ttu-id="b14b9-126">После ввода всех этих данных нажмите кнопку **Отзыв и создание**.</span><span class="sxs-lookup"><span data-stu-id="b14b9-126">When you have entered all of the above information, click **Review + create**.</span></span>

1. <span data-ttu-id="b14b9-127">Если при просмотре страницы все выглядит правильно, щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b14b9-127">If everything looks correct on the review page, click **Create**.</span></span>

   ![Проверка параметров учетной записи Cosmos DB][COSMOSDB03]

### <a name="retrieve-the-connection-string-for-your-azure-cosmos-db-account"></a><span data-ttu-id="b14b9-129">Получение строки подключения к учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b14b9-129">Retrieve the connection string for your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="b14b9-130">Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="b14b9-130">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="b14b9-131">Нажмите кнопку **Все ресурсы**, а затем щелкните только что созданную учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b14b9-131">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Выбор учетной записи Azure Cosmos DB][COSMOSDB04]

1. <span data-ttu-id="b14b9-133">Нажмите кнопку **Строки подключения** и скопируйте значение для поля **Основная строка подключения**. Позже это значение будет использоваться для настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b14b9-133">Click **Connection strings**, and copy the value for the **Primary Connection String** field; you will use that value to configure your application later.</span></span>

   ![Получение строк подключения к Cosmos DB][COSMOSDB06]

## <a name="configure-the-sample-application"></a><span data-ttu-id="b14b9-135">Настройка примера приложения</span><span class="sxs-lookup"><span data-stu-id="b14b9-135">Configure the sample application</span></span>

1. <span data-ttu-id="b14b9-136">Откройте командную строку и клонируйте пример проекта с помощью команды Git, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="b14b9-136">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/spring-guides/gs-accessing-data-mongodb.git
   ```

1. <span data-ttu-id="b14b9-137">Создайте каталог *resources* в каталоге примера проекта *&lt;project root&gt;/complete/src/main*, а затем создайте файл *application.properties* в каталоге *resources*.</span><span class="sxs-lookup"><span data-stu-id="b14b9-137">Create a *resources* directory in the *&lt;project root&gt;/complete/src/main* directory of the sample project, and create an *application.properties* file in the *resources* directory.</span></span>

1. <span data-ttu-id="b14b9-138">Откройте файл *application.properties* в текстовом редакторе и добавьте указанные ниже строки в файл и замените примеры значений на соответствующие полученные ранее значения:</span><span class="sxs-lookup"><span data-stu-id="b14b9-138">Open the *application.properties* file in a text editor, and add the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.data.mongodb.database=wingtiptoysmongodb
   spring.data.mongodb.uri=mongodb://wingtiptoysmongodb:AbCdEfGhIjKlMnOpQrStUvWxYz==@wingtiptoysmongodb.documents.azure.com:10255/?ssl=true&replicaSet=globaldb
   ```
   <span data-ttu-id="b14b9-139">Описание</span><span class="sxs-lookup"><span data-stu-id="b14b9-139">Where:</span></span>

   | <span data-ttu-id="b14b9-140">Параметр</span><span class="sxs-lookup"><span data-stu-id="b14b9-140">Parameter</span></span> | <span data-ttu-id="b14b9-141">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="b14b9-141">Description</span></span> |
   |---|---|
   | `spring.data.mongodb.database` | <span data-ttu-id="b14b9-142">Определяет имя учетной записи Cosmos DB, описанное в этой статье.</span><span class="sxs-lookup"><span data-stu-id="b14b9-142">Specifies the name of your Cosmos DB account from earlier in this article.</span></span> |
   | `spring.data.mongodb.uri` | <span data-ttu-id="b14b9-143">Указывает **основную строку подключения**, описанную в этой статье.</span><span class="sxs-lookup"><span data-stu-id="b14b9-143">Specifies the **Primary Connection String** from earlier in this article.</span></span> |

1. <span data-ttu-id="b14b9-144">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="b14b9-144">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="b14b9-145">Упаковывание и тестирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="b14b9-145">Package and test the sample application</span></span> 

1. <span data-ttu-id="b14b9-146">Создайте пример приложения с помощью Maven, а затем настройте Maven на пропуск тестов, например:</span><span class="sxs-lookup"><span data-stu-id="b14b9-146">Build the sample application with Maven, and configure Maven to skip tests; for example:</span></span>

   ```shell
   mvn clean package -DskipTests
   ```

1. <span data-ttu-id="b14b9-147">Запустите пример приложения, например:</span><span class="sxs-lookup"><span data-stu-id="b14b9-147">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/gs-accessing-data-mongodb-0.1.0.jar
   ```
    
   <span data-ttu-id="b14b9-148">Приложение должно возвращать значения следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b14b9-148">Your application should return values like the following:</span></span>

   ```json
   Customers found with findAll():
   -------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customer[id=5c1b4ae4d0b5080ac105cc14, firstName='Bob', lastName='Smith']
   
   Customer found with findByFirstName('Alice'):
   --------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customers found with findByLastName('Smith'):
   --------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customer[id=5c1b4ae4d0b5080ac105cc14, firstName='Bob', lastName='Smith']
   ```

## <a name="summary"></a><span data-ttu-id="b14b9-149">Сводка</span><span class="sxs-lookup"><span data-stu-id="b14b9-149">Summary</span></span>

<span data-ttu-id="b14b9-150">С помощью этого руководства вы создали пример приложения Java, использующий Spring Data для хранения и извлечения информации с помощью API MongoDB для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b14b9-150">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information using the Azure Cosmos DB MongoDB API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b14b9-151">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="b14b9-151">Next steps</span></span>

<span data-ttu-id="b14b9-152">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="b14b9-152">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b14b9-153">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="b14b9-153">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="b14b9-154">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b14b9-154">Additional Resources</span></span>

<span data-ttu-id="b14b9-155">Дополнительные сведения об использовании Java в Azure см. в статьях [Azure для разработчиков Java] и [Working with Azure DevOps and Java] (Работа с Azure DevOps и Java).</span><span class="sxs-lookup"><span data-stu-id="b14b9-155">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[COSMOSDB01]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB06]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-06.png
