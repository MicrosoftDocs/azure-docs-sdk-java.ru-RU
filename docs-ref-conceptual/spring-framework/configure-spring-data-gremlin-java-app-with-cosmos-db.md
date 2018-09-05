---
title: Использование начального приложения Spring Data Gremlin с API SQL Azure Cosmos DB
description: Сведения о настройке приложения, созданного с помощью Spring Boot Initializer в API Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 08/20/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 0976f4b0c13ce5c577458f2974f5dce123bf7e59
ms.sourcegitcommit: 77dc6c03a2e6264df688d91a04fc6b40950779ef
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2018
ms.locfileid: "43241076"
---
# <a name="how-to-use-the-spring-data-gremlin-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="49e33-103">Использование начального приложения Spring Data Gremlin с API SQL Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="49e33-103">How to use the Spring Data Gremlin Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="49e33-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="49e33-104">Overview</span></span>

<span data-ttu-id="49e33-105">Начальное приложение Spring Data Gremlin обеспечивает поддержку Spring Data для языка запросов Gremlin от Apache, который разработчики могут использовать с любым хранилищем данных, совместимым с Gremlin.</span><span class="sxs-lookup"><span data-stu-id="49e33-105">The Spring Data Gremlin Starter provides Spring Data support for the Gremlin query language from Apache, which developers can use with any Gremlin-compatible data store.</span></span>

<span data-ttu-id="49e33-106">В этой статье демонстрируется создание базы данных Azure Cosmos DB на портале Azure для использования с API Gremlin, создание пользовательского приложения Java с помощью **[Spring Initializr]**, а затем добавление в это приложение функций начального приложения Spring Data Gremlin для хранения данных в Azure Cosmos DB и получения этих данных с помощью языка запросов Gremlin.</span><span class="sxs-lookup"><span data-stu-id="49e33-106">This article demonstrates creating an Azure Cosmos DB by using the Azure portal for use with Gremlin API, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Data Gremlin Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using Gremlin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49e33-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="49e33-107">Prerequisites</span></span>

<span data-ttu-id="49e33-108">Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="49e33-108">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="49e33-109">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="49e33-109">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="49e33-110">[Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="49e33-110">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="49e33-111">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="49e33-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="49e33-112">Для выполнения операций, описанных в этой статье, требуется Spring Boot 2.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="49e33-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-cosmos-db-using-the-azure-portal"></a><span data-ttu-id="49e33-113">Создание базы данных Azure Cosmos DB с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="49e33-113">Create an Azure Cosmos DB using the Azure portal</span></span>

### <a name="create-your-azure-cosmos-database-for-use-with-gremlin-api"></a><span data-ttu-id="49e33-114">Создание базы данных Azure Cosmos DB для использования с API Gremlin</span><span class="sxs-lookup"><span data-stu-id="49e33-114">Create your Azure Cosmos Database for use with Gremlin API</span></span>

1. <span data-ttu-id="49e33-115">Перейдите на портал Azure по адресу <https://portal.azure.com/> и щелкните **+Создать ресурс**.</span><span class="sxs-lookup"><span data-stu-id="49e33-115">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Создание ресурса][AZ01]

1. <span data-ttu-id="49e33-117">Щелкните **Базы данных** и **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="49e33-117">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Создание Azure Cosmos DB][AZ02]

1. <span data-ttu-id="49e33-119">На странице **Azure Cosmos DB** введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="49e33-119">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="49e33-120">Введите уникальный **ИД**, который будет использоваться как элемент универсального кода ресурса (URI) Gremlin создаваемой базы данных.</span><span class="sxs-lookup"><span data-stu-id="49e33-120">Enter a unique **ID**, which you will use as part of the Gremlin URI for your database.</span></span> <span data-ttu-id="49e33-121">Например, если указать в качестве **ИД** **wingtiptoysdata**, URI Gremlin будет *wingtiptoysdata.gremlin.cosmosdb.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="49e33-121">For example: if you entered **wingtiptoysdata** for the **ID**, the Gremlin URI would be *wingtiptoysdata.gremlin.cosmosdb.azure.com*.</span></span>
   * <span data-ttu-id="49e33-122">В поле "API" выберите **Gremlin (Graph)**.</span><span class="sxs-lookup"><span data-stu-id="49e33-122">Choose **Gremlin (Graph)** for the API.</span></span>
   * <span data-ttu-id="49e33-123">Выберите **подписку**, которую нужно использовать для базы данных.</span><span class="sxs-lookup"><span data-stu-id="49e33-123">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="49e33-124">Укажите, следует ли создать **группу ресурсов** для базы данных, или выберите имеющуюся группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="49e33-124">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="49e33-125">Укажите **расположение** для базы данных.</span><span class="sxs-lookup"><span data-stu-id="49e33-125">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="49e33-126">Указав эти параметры, щелкните **Создать**, чтобы создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="49e33-126">When you have specified these options, click **Create** to create your database.</span></span>

   ![Указание параметров Azure Cosmos DB][AZ03]

1. <span data-ttu-id="49e33-128">При создании база данных указывается на **панели мониторинга** Azure, а также на страницах **Все ресурсы** и **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="49e33-128">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="49e33-129">Вы можете выбрать свою базу данных в любом из этих расположений, чтобы открыть страницу свойств кэша.</span><span class="sxs-lookup"><span data-stu-id="49e33-129">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Все ресурсы][AZ04]

1. <span data-ttu-id="49e33-131">Когда откроется страница свойств базы данных, щелкните **Ключи доступа** и скопируйте URI и ключи доступа для базы данных. Эти значения будут использоваться в приложении Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="49e33-131">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Ключи доступа][AZ05]

### <a name="add-a-graph-to-your-azure-cosmos-database"></a><span data-ttu-id="49e33-133">Добавление графа в базу данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="49e33-133">Add a graph to your Azure Cosmos Database</span></span>

1. <span data-ttu-id="49e33-134">Щелкните **Обозреватель данных**, а затем выберите **Добавление графа**.</span><span class="sxs-lookup"><span data-stu-id="49e33-134">Click **Data Explorer**, and then click **New Graph**.</span></span>

   ![Добавление графа][AZ06]

1. <span data-ttu-id="49e33-136">В окне **Добавление графа** добавьте следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="49e33-136">When the **Add Graph** is displayed, enter the following information:</span></span>

   * <span data-ttu-id="49e33-137">Укажите уникальное значение в поле **Идентификатор базы данных**.</span><span class="sxs-lookup"><span data-stu-id="49e33-137">Specify a unique **Database id** for your database.</span></span>
   * <span data-ttu-id="49e33-138">Укажите уникальное значение в поле **Идентификатор графа**.</span><span class="sxs-lookup"><span data-stu-id="49e33-138">Specify a unique **Graph id** for your graph.</span></span>
   * <span data-ttu-id="49e33-139">Можно указать свое значение в поле **Емкость хранилища** или оставить значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="49e33-139">You can choose to specify your **Storage capacity**, or you can accept the default.</span></span>
   * <span data-ttu-id="49e33-140">Укажите значение в поле **Пропускная способность**. В этом примере можно выбрать 400 единиц запросов (ЕЗ).</span><span class="sxs-lookup"><span data-stu-id="49e33-140">Specify your **Throughout**, and for this example you can choose 400 Request Units (RUs).</span></span>
   
   <span data-ttu-id="49e33-141">Указав эти параметры, щелкните **ОК**, чтобы создать граф.</span><span class="sxs-lookup"><span data-stu-id="49e33-141">When you have specified these options, click **OK** to create your graph.</span></span>

   ![Добавление графа][AZ07]

1. <span data-ttu-id="49e33-143">После создания графа его можно просмотреть при помощи **обозревателя данных**.</span><span class="sxs-lookup"><span data-stu-id="49e33-143">After your graph has been created, you can use the **Data Explorer** to view it.</span></span>

   ![Окно свойств графа][AZ08]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="49e33-145">Создание простого приложения Spring Boot с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="49e33-145">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="49e33-146">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="49e33-146">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="49e33-147">Укажите, что требуется создать проект **Maven** на **Java**, введите имена **группы** и **артефакта** для приложения, укажите версию **Spring Boot** (необходима версия 2.0 или более поздняя версия), а затем щелкните **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="49e33-147">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, specify your **Spring Boot** version with a version that is equal to or greater than 2.0, and then click **Generate Project**.</span></span>

   ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="49e33-149">Spring Initializr использует имена **группы** и **артефакта**, чтобы создать имя пакета, например \*com.example.wintiptoysdata.</span><span class="sxs-lookup"><span data-stu-id="49e33-149">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: \*com.example.wintiptoysdata.</span></span>
   >

1. <span data-ttu-id="49e33-150">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="49e33-150">When prompted, download the project to a path on your local computer.</span></span>

   ![Скачивание пользовательского проекта Spring Boot][SI02]

1. <span data-ttu-id="49e33-152">После извлечения файлов в локальной системе простое приложение Spring Boot можно будет редактировать.</span><span class="sxs-lookup"><span data-stu-id="49e33-152">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Пользовательские файлы проекта Spring Boot][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-spring-data-gremlin-starter"></a><span data-ttu-id="49e33-154">Настройка приложения Spring Boot для использования начального приложения Spring Data Gremlin</span><span class="sxs-lookup"><span data-stu-id="49e33-154">Configure your Spring Boot app to use the Spring Data Gremlin Starter</span></span>

1. <span data-ttu-id="49e33-155">Найдите файл *pom.xml* в каталоге приложения, например:</span><span class="sxs-lookup"><span data-stu-id="49e33-155">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="49e33-156">-или-</span><span class="sxs-lookup"><span data-stu-id="49e33-156">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Поиск файла pom.xml][PM01]

1. <span data-ttu-id="49e33-158">Откройте файл *pom.xml* в текстовом редакторе и добавьте начальное приложение Spring Data Gremlin в список `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="49e33-158">Open the *pom.xml* file in a text editor, and add the Spring Data Gremlin Starter to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.spring.data.gremlin</groupId>
      <artifactId>spring-data-gremlin</artifactId>
      <version>2.0.0</version>
   </dependency>
   ```

   ![Изменение файла pom.xml][PM02]

1. <span data-ttu-id="49e33-160">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="49e33-160">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="49e33-161">Настройка приложения Spring Boot для использования Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="49e33-161">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="49e33-162">Найдите каталог *resources* своего приложения и создайте файл с именем *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="49e33-162">Locate the *resources* directory of your app, and create a new file named *application.yml*.</span></span> <span data-ttu-id="49e33-163">Например: </span><span class="sxs-lookup"><span data-stu-id="49e33-163">For example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.yml`

   <span data-ttu-id="49e33-164">-или-</span><span class="sxs-lookup"><span data-stu-id="49e33-164">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.yml`

   ![Создание файла application.yml][RE01]

1.  <span data-ttu-id="49e33-166">Откройте файл *application.yml* в текстовом редакторе, добавьте указанные ниже строки в файл и замените примеры значений соответствующими свойствами своей базы данных:</span><span class="sxs-lookup"><span data-stu-id="49e33-166">Open the *application.yml* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   gremlin:
      endpoint: wingtiptoys.gremlin.cosmosdb.azure.com
      port: 443
      username: /dbs/wingtiptoysdb/colls/wingtiptoysgraph
      password: 57686f6120447564652c20426f6220526f636b73==
      telemetryAllowed: false
   ```
   <span data-ttu-id="49e33-167">Описание</span><span class="sxs-lookup"><span data-stu-id="49e33-167">Where:</span></span>
   | <span data-ttu-id="49e33-168">Поле</span><span class="sxs-lookup"><span data-stu-id="49e33-168">Field</span></span> | <span data-ttu-id="49e33-169">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="49e33-169">Description</span></span> |
   | ---|---|
   | `endpoint` | <span data-ttu-id="49e33-170">Указывает URI Gremlin, который создается на основе уникального **ИД**, введенного при создании базы данных Azure Cosmos DB ранее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="49e33-170">Specifies the Gremlin URI for your database, which is derived from the unique **ID** that you specified when you created your Azure Cosmos DB earlier in this tutorial.</span></span> |
   | `port` | <span data-ttu-id="49e33-171">Указывает порт TCP/IP, который для протокола HTTPS должен иметь значение **443**.</span><span class="sxs-lookup"><span data-stu-id="49e33-171">Specifies the TCP/IP port, which should be **443** for HTTPS.</span></span> |
   | `username` | <span data-ttu-id="49e33-172">Указывает уникальные значения параметров **Идентификатор базы данных** и **Идентификатор графа**, которые использовались при добавлении графа ранее в этом руководстве. Это значение нужно вводить, используя следующий синтаксис: "/dbs/**{Идентификатор базы данных}**/colls/**{Идентификатор графа}**".</span><span class="sxs-lookup"><span data-stu-id="49e33-172">Specifies the unique **Database id** and **Graph id** that you used when you added your graph earlier in this tutorial; this must be entered using the following syntax: "/dbs/**{Database id}**/colls/**{Graph id}**".</span></span> |
   | `password` | <span data-ttu-id="49e33-173">Указывает основной или дополнительный **ключ доступа**, который вы скопировали ранее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="49e33-173">Specifies either the primary or secondary **Access key** that you copied earlier in this tutorial.</span></span> |
   | `telemetryAllowed` | <span data-ttu-id="49e33-174">Укажите **true**, если нужно включить телеметрию. В противном случае укажите **false**.</span><span class="sxs-lookup"><span data-stu-id="49e33-174">Specify **true** if you want to enable telemetry; otherwise, **false**.</span></span>

1. <span data-ttu-id="49e33-175">Сохраните и закройте файл *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="49e33-175">Save and close the *application.yml* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="49e33-176">Добавление примера кода для реализации базовых возможностей базы данных</span><span class="sxs-lookup"><span data-stu-id="49e33-176">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="49e33-177">В этом разделе вы создадите классы Java, необходимые для хранения данных в созданной базе данных.</span><span class="sxs-lookup"><span data-stu-id="49e33-177">In this section, you create the necessary Java classes for storing data in your database.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="49e33-178">Изменение класса основного приложения</span><span class="sxs-lookup"><span data-stu-id="49e33-178">Modify the main application class</span></span>

1. <span data-ttu-id="49e33-179">Найдите файл основного приложения Java в каталоге пакета приложения, например:</span><span class="sxs-lookup"><span data-stu-id="49e33-179">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="49e33-180">-или-</span><span class="sxs-lookup"><span data-stu-id="49e33-180">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Поиск файла приложения Java][JV01]

1. <span data-ttu-id="49e33-182">Откройте файл основного приложения Java в текстовом редакторе и добавьте в него следующие строки:</span><span class="sxs-lookup"><span data-stu-id="49e33-182">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoysdata;
   
   // These imports are required for the application.
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.example.wingtiptoysdata.domain.Network;
   import com.example.wingtiptoysdata.domain.Person;
   import com.example.wingtiptoysdata.domain.Relation;
   import com.example.wingtiptoysdata.repository.NetworkRepository;
   import com.example.wingtiptoysdata.repository.PersonRepository;
   import com.example.wingtiptoysdata.repository.RelationRepository;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import javax.annotation.PostConstruct;
   import javax.annotation.PreDestroy;
   
   @SpringBootApplication
   public class WingtiptoysdataApplication {
   
       // Define several person classes to store personal data.
       private final Person person1 = new Person("01", "Nellie Hughes", "23");
       private final Person person2 = new Person("02", "Delmar Alfred", "34");
       private final Person person3 = new Person("03", "Kelley Hunter", "45");
       private final Person person4 = new Person("04", "Roscoe Guerin", "56");
       private final Person person5 = new Person("05", "Gracie Chavez", "67");
   
       // Define relationship classes to define the relationships between some of the persons.
       private final Relation relation1 = new Relation("0102", "siblings", person1, person2);
       private final Relation relation2 = new Relation("0203", "coworkers", person2, person3);
       private final Relation relation3 = new Relation("0301", "parent", person3, person1);
       private final Relation relation4 = new Relation("0302", "parent", person3, person2);
       private final Relation relation5 = new Relation("0501", "grandparent", person5, person1);
       private final Relation relation6 = new Relation("0502", "grandparent", person5, person2);
   
       // Define the network.
       private final Network network = new Network();
   
       // Autowire the repositories and factory.
       @Autowired
       private PersonRepository personRepo;
       @Autowired
       private RelationRepository relationRepo;
       @Autowired
       private NetworkRepository networkRepo;
       @Autowired
       private GremlinFactory factory;
   
       // Run the Spring application and exit.
    public static void main(String[] args) {
           SpringApplication.run(WingtiptoysdataApplication.class, args);
           System.exit(0);
    }
   
       // Perform post-construct operations.    
       @PostConstruct
       public void setup() {
           // Delete any existing data from the database.
           this.networkRepo.deleteAll();
   
           // Add the relationship classes as edges.
           this.network.getEdges().add(this.relation1);
           this.network.getEdges().add(this.relation2);
           this.network.getEdges().add(this.relation3);
           this.network.getEdges().add(this.relation4);
           this.network.getEdges().add(this.relation5);
           this.network.getEdges().add(this.relation6);
   
           // Add the person classes as vertices.
           this.network.getVertexes().add(this.person1);
           this.network.getVertexes().add(this.person2);
           this.network.getVertexes().add(this.person3);
           this.network.getVertexes().add(this.person4);
           this.network.getVertexes().add(this.person5);
   
           // Save the network.
           this.networkRepo.save(this.network);
       }
   }
   ```

1. <span data-ttu-id="49e33-183">Сохраните и закройте файл основного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="49e33-183">Save and close the main application Java file.</span></span>

### <a name="define-a-basic-class-for-storing-configuration-information"></a><span data-ttu-id="49e33-184">Создание простого класса для хранения сведений о конфигурации</span><span class="sxs-lookup"><span data-stu-id="49e33-184">Define a basic class for storing configuration information</span></span>

1. <span data-ttu-id="49e33-185">В каталоге пакета своего приложения создайте папку с именем *config*, например:</span><span class="sxs-lookup"><span data-stu-id="49e33-185">Create a folder named *config* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\config`

   <span data-ttu-id="49e33-186">-или-</span><span class="sxs-lookup"><span data-stu-id="49e33-186">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/config`

1. <span data-ttu-id="49e33-187">В каталоге *config* создайте файл Java с именем *UserRepositoryConfiguration.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="49e33-187">Create a new Java file named *UserRepositoryConfiguration.java* in the *config* directory, then open the file in a text editor, and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.config;

   import com.microsoft.spring.data.gremlin.common.GremlinConfiguration;
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.microsoft.spring.data.gremlin.config.AbstractGremlinConfiguration;
   import com.microsoft.spring.data.gremlin.repository.config.EnableGremlinRepositories;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.context.properties.EnableConfigurationProperties;
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   import org.springframework.context.annotation.PropertySource;
   
   @Configuration
   @EnableGremlinRepositories(basePackages = "com.example.wingtiptoysdata.repository")
   @EnableConfigurationProperties(GremlinConfiguration.class)
   @PropertySource("classpath:application.yml")
   public class UserRepositoryConfiguration extends AbstractGremlinConfiguration {
   
       @Autowired
       private GremlinConfiguration config;
   
       @Override
       public GremlinConfiguration getGremlinConfiguration() {
           return this.config;
       }
   }
   ```

1. <span data-ttu-id="49e33-188">Сохраните и закройте файл *UserRepositoryConfiguration.java*.</span><span class="sxs-lookup"><span data-stu-id="49e33-188">Save and close the *UserRepositoryConfiguration.java* file.</span></span>

### <a name="define-a-set-of-classes-that-define-the-elements-of-your-graph-database"></a><span data-ttu-id="49e33-189">Создание набора классов, которые определяют элементы графовой базы данных</span><span class="sxs-lookup"><span data-stu-id="49e33-189">Define a set of classes that define the elements of your graph database</span></span>

1. <span data-ttu-id="49e33-190">В каталоге пакета своего приложения создайте папку с именем *domain*, например:</span><span class="sxs-lookup"><span data-stu-id="49e33-190">Create a folder named *domain* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\domain`

   <span data-ttu-id="49e33-191">-или-</span><span class="sxs-lookup"><span data-stu-id="49e33-191">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/domain`

1. <span data-ttu-id="49e33-192">В каталоге *domain* создайте файл Java с именем *Person.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="49e33-192">Create a new Java file named *Person.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Vertex;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Vertex
   @AllArgsConstructor
   @NoArgsConstructor
   public class Person {
   
       @Id
       private String id;
   
       private String name;
   
       private String age;
   }
   ```

1. <span data-ttu-id="49e33-193">Сохраните и закройте файл *Person.java*.</span><span class="sxs-lookup"><span data-stu-id="49e33-193">Save and close the *Person.java* file.</span></span>

1. <span data-ttu-id="49e33-194">В каталоге *domain* создайте файл Java с именем *Relation.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="49e33-194">Create a new Java file named *Relation.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Edge;
   import com.microsoft.spring.data.gremlin.annotation.EdgeFrom;
   import com.microsoft.spring.data.gremlin.annotation.EdgeTo;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Edge
   @AllArgsConstructor
   @NoArgsConstructor
   public class Relation {
   
       @Id
       private String id;
   
       private String name;
   
       @EdgeFrom
       private Person personFrom;
   
       @EdgeTo
       private Person personTo;
   }
   ```

1. <span data-ttu-id="49e33-195">Сохраните и закройте файл *Relation.java*.</span><span class="sxs-lookup"><span data-stu-id="49e33-195">Save and close the *Relation.java* file.</span></span>

1. <span data-ttu-id="49e33-196">В каталоге *domain* создайте файл Java с именем *Network.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="49e33-196">Create a new Java file named *Network.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.EdgeSet;
   import com.microsoft.spring.data.gremlin.annotation.Graph;
   import com.microsoft.spring.data.gremlin.annotation.VertexSet;
   import lombok.Getter;
   import org.springframework.data.annotation.Id;
   
   import java.util.ArrayList;
   import java.util.List;
   
   @Graph
   public class Network {
   
       @Id
       private String id;
   
       public Network() {
           this.edges = new ArrayList<Object>();
           this.vertexes = new ArrayList<Object>();
       }
   
       @EdgeSet
       @Getter
       private List<Object> edges;
   
       @VertexSet
       @Getter
       private List<Object> vertexes;
   }
   ```

1. <span data-ttu-id="49e33-197">Сохраните и закройте файл *Network.java*.</span><span class="sxs-lookup"><span data-stu-id="49e33-197">Save and close the *Network.java* file.</span></span>

### <a name="define-a-set-of-classes-that-define-the-repositories-for-your-graph-database"></a><span data-ttu-id="49e33-198">Создание набора классов, которые определяют репозитории графовой базы данных</span><span class="sxs-lookup"><span data-stu-id="49e33-198">Define a set of classes that define the repositories for your graph database</span></span>

1. <span data-ttu-id="49e33-199">В каталоге пакета своего приложения создайте папку с именем *repository*, например:</span><span class="sxs-lookup"><span data-stu-id="49e33-199">Create a folder named *repository* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\repository`

   <span data-ttu-id="49e33-200">-или-</span><span class="sxs-lookup"><span data-stu-id="49e33-200">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/repository`

1. <span data-ttu-id="49e33-201">В каталоге *repository* создайте файл Java с именем *NetworkRepository.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="49e33-201">Create a new Java file named *NetworkRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Network;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface NetworkRepository extends GremlinRepository<Network, String> {
   }
   ```

1. <span data-ttu-id="49e33-202">Сохраните и закройте файл *NetworkRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="49e33-202">Save and close the *NetworkRepository.java* file.</span></span>

1. <span data-ttu-id="49e33-203">В каталоге *repository* создайте файл Java с именем *PersonRepository.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="49e33-203">Create a new Java file named *PersonRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Person;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface PersonRepository extends GremlinRepository<Person, String> {
   }
   ```

1. <span data-ttu-id="49e33-204">Сохраните и закройте файл *PersonRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="49e33-204">Save and close the *PersonRepository.java* file.</span></span>

1. <span data-ttu-id="49e33-205">В каталоге *repository* создайте файл Java с именем *RelationRepository.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="49e33-205">Create a new Java file named *RelationRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Relation;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface RelationRepository extends GremlinRepository<Relation, String> {
   }
   ```

1. <span data-ttu-id="49e33-206">Сохраните и закройте файл *RelationRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="49e33-206">Save and close the *RelationRepository.java* file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="49e33-207">Создание и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="49e33-207">Build and test your app</span></span>

1. <span data-ttu-id="49e33-208">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="49e33-208">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="49e33-209">-или-</span><span class="sxs-lookup"><span data-stu-id="49e33-209">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="49e33-210">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="49e33-210">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="49e33-211">Ваше приложение отобразит несколько сообщений среды выполнения. При отсутствии ошибок вы сможете просмотреть содержимое базы данных Azure Cosmos DB на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="49e33-211">Your application will display several runtime messages, and if there were no errors, you can use the Azure portal to view the contents of your Azure Cosmos DB.</span></span> <span data-ttu-id="49e33-212">Для этого на странице свойств базы данных выберите **Обозреватель данных**, щелкните **Execute Gremlin Query** (Выполнить запрос Gremlin), а затем выберите элемент в списке результатов, чтобы просмотреть данные.</span><span class="sxs-lookup"><span data-stu-id="49e33-212">To do so, click **Data Explorer** on the properties page for your database, then click **Execute Gremlin Query**, and then select an item from the list of results to view the data.</span></span>

   ![Просмотр данных с помощью обозревателя документов][JV03]

## <a name="next-steps"></a><span data-ttu-id="49e33-214">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="49e33-214">Next steps</span></span>

<span data-ttu-id="49e33-215">Дополнительные сведения о поддержке Gremlin и API Graph в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="49e33-215">For more information about Azure support for Gremlin and Graph API, see the following articles:</span></span>

* [<span data-ttu-id="49e33-216">Знакомство с базой данных Azure Cosmos DB. API Graph</span><span class="sxs-lookup"><span data-stu-id="49e33-216">Introduction to Azure Cosmos DB: Graph API</span></span>](https://docs.microsoft.com/azure/cosmos-db/graph-introduction)

* [<span data-ttu-id="49e33-217">Поддержка графа Gremlin в базе данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="49e33-217">Azure Cosmos DB Gremlin graph support</span></span>](https://docs.microsoft.com/azure/cosmos-db/gremlin-support)

* [<span data-ttu-id="49e33-218">Azure Cosmos DB: создание графовой базы данных с помощью Java и портала Azure</span><span class="sxs-lookup"><span data-stu-id="49e33-218">Azure Cosmos DB: Create a graph database using Java and the Azure portal</span></span>](https://docs.microsoft.com/azure/cosmos-db/create-graph-java)

* [<span data-ttu-id="49e33-219">Руководство по выполнению запросов к API Graph в Azure Cosmos DB с использованием Gremlin</span><span class="sxs-lookup"><span data-stu-id="49e33-219">Tutorial: Query Azure Cosmos DB Graph API by using Gremlin</span></span>](https://docs.microsoft.com/azure/cosmos-db/tutorial-query-graph)

* <span data-ttu-id="49e33-220">[Spring Data Gremlin Starter] (Начальное приложение Spring Data Gremlin)</span><span class="sxs-lookup"><span data-stu-id="49e33-220">[Spring Data Gremlin Starter]</span></span>

<span data-ttu-id="49e33-221">Дополнительные сведения об использовании Azure PowerShell и Java см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="49e33-221">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="49e33-222">[Документация по Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="49e33-222">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="49e33-223">[Azure Cosmos DB. Создание базы данных документов с помощью Java и портала Azure][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="49e33-223">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="49e33-224">[Spring Data для API SQL для Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="49e33-224">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="49e33-225">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="49e33-225">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="49e33-226">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="49e33-226">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="49e33-227">Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="49e33-227">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="49e33-228">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="49e33-228">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="49e33-229">**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="49e33-229">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="49e33-230">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="49e33-230">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="49e33-231">В помощь разработчикам, начинающим работать со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения.</span><span class="sxs-lookup"><span data-stu-id="49e33-231">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="49e33-232">Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="49e33-232">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>


<!-- URL List -->

[Документация по Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring Data для API SQL для Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data Gremlin Starter]: https://github.com/Microsoft/spring-data-gremlin (Начальное приложение Spring Data Gremlin)
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ05.png
[AZ06]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ06.png
[AZ07]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ07.png
[AZ08]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ08.png

[SI01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV03.png
