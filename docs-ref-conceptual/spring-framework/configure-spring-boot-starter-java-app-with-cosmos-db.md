---
title: Использование начального приложения Spring Boot с API SQL Azure Cosmos DB
description: Сведения о настройке приложения, созданного с помощью Spring Boot Initializer в API Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 6675b3f76f19ec0bfdb28351681258b8c4792104
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339108"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="f7508-103">Использование начального приложения Spring Boot с API SQL Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f7508-103">How to use the Spring Boot Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="f7508-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f7508-104">Overview</span></span>

<span data-ttu-id="f7508-105">Azure Cosmos DB — это глобально распределенная служба баз данных, предоставляющая разработчикам возможность работать с данными с помощью разных стандартных API, например SQL, MongoDB, Graph и табличных API.</span><span class="sxs-lookup"><span data-stu-id="f7508-105">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as SQL, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="f7508-106">Начальное приложение Spring Boot от Майкрософт позволяет разработчикам использовать приложения Spring Boot, которые легко интегрируются с Azure Cosmos DB с помощью API SQL.</span><span class="sxs-lookup"><span data-stu-id="f7508-106">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using the SQL API.</span></span>

<span data-ttu-id="f7508-107">В этой статье описано, как создать Azure Cosmos DB на портале Azure, создать пользовательское приложение Java с помощью **[Spring Initializr]**, а затем добавить начальное приложение Spring Boot в пользовательское приложение для хранения и получения данных в Azure Cosmos DB с помощью API SQL.</span><span class="sxs-lookup"><span data-stu-id="f7508-107">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Boot Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using the SQL API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7508-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f7508-108">Prerequisites</span></span>

<span data-ttu-id="f7508-109">Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="f7508-109">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="f7508-110">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="f7508-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="f7508-111">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="f7508-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="f7508-112">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="f7508-112">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="f7508-113">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="f7508-113">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="f7508-114">Создание Azure Cosmos DB с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="f7508-114">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="f7508-115">Перейдите на портал Azure по адресу <https://portal.azure.com/> и щелкните **+Создать ресурс**.</span><span class="sxs-lookup"><span data-stu-id="f7508-115">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Портал Azure][AZ01]

1. <span data-ttu-id="f7508-117">Щелкните **Базы данных** и **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="f7508-117">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Портал Azure][AZ02]

1. <span data-ttu-id="f7508-119">На странице **Azure Cosmos DB** введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="f7508-119">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="f7508-120">Введите уникальный **идентификатор**, который будет использоваться в качестве URI для базы данных,</span><span class="sxs-lookup"><span data-stu-id="f7508-120">Enter a unique **ID**, which you will use as the URI for your database.</span></span> <span data-ttu-id="f7508-121">например *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="f7508-121">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="f7508-122">Выберите **SQL** в качестве API.</span><span class="sxs-lookup"><span data-stu-id="f7508-122">Choose **SQL** for the API.</span></span>
   * <span data-ttu-id="f7508-123">Выберите **подписку**, которую нужно использовать для базы данных.</span><span class="sxs-lookup"><span data-stu-id="f7508-123">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="f7508-124">Укажите, следует ли создать **группу ресурсов** для базы данных, или выберите имеющуюся группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f7508-124">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="f7508-125">Укажите **расположение** для базы данных.</span><span class="sxs-lookup"><span data-stu-id="f7508-125">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="f7508-126">Указав эти параметры, щелкните **Создать**, чтобы создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="f7508-126">When you have specified these options, click **Create** to create your database.</span></span>

   ![Портал Azure][AZ03]

1. <span data-ttu-id="f7508-128">При создании база данных указывается на **панели мониторинга** Azure, а также на страницах **Все ресурсы** и **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="f7508-128">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="f7508-129">Вы можете выбрать свою базу данных в любом из этих расположений, чтобы открыть страницу свойств кэша.</span><span class="sxs-lookup"><span data-stu-id="f7508-129">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Портал Azure][AZ04]

1. <span data-ttu-id="f7508-131">Когда откроется страница свойств базы данных, щелкните **Ключи доступа** и скопируйте URI и ключи доступа для базы данных. Эти значения будут использоваться в приложении Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="f7508-131">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Портал Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="f7508-133">Создание простого приложения Spring Boot с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="f7508-133">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="f7508-134">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="f7508-134">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="f7508-135">Укажите, что требуется создать проект **Maven** на **Java**, введите имя **группы** и **артефакта** для приложения, укажите версию **Spring Boot**, а затем нажмите соответствующую кнопку, чтобы **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="f7508-135">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, specify your **Spring Boot** version, and then click the button to **Generate Project**.</span></span>

   > [!IMPORTANT]
   >
   > <span data-ttu-id="f7508-136">Внесены критические изменения в API Spring Boot версии 2.0.n, которые будут использоваться при выполнении действий, описанных в этой статье.</span><span class="sxs-lookup"><span data-stu-id="f7508-136">There were several breaking changes to the APIs in Spring Boot version 2.0.n, which will be used to complete the steps in this article.</span></span> <span data-ttu-id="f7508-137">Для выполнения этих действий вы также можете использовать одну из версий Spring Boot 1.5.n. Различия будут выделены, где это необходимо.</span><span class="sxs-lookup"><span data-stu-id="f7508-137">You can still use one of the Spring Boot 1.5.n versions to complete the steps in this tutorial, and the differences will be highlighted when necessary.</span></span>
   >

   ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="f7508-139">Spring Initializr использует имена **группы** и **артефакта** для создания имени пакета, например *com.example.wintiptoysdata*.</span><span class="sxs-lookup"><span data-stu-id="f7508-139">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoysdata*.</span></span>
   >

1. <span data-ttu-id="f7508-140">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="f7508-140">When prompted, download the project to a path on your local computer.</span></span>

   ![Скачивание пользовательского проекта Spring Boot][SI02]

1. <span data-ttu-id="f7508-142">После извлечения файлов в локальной системе простое приложение Spring Boot можно будет редактировать.</span><span class="sxs-lookup"><span data-stu-id="f7508-142">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Пользовательские файлы проекта Spring Boot][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="f7508-144">Настройка приложения Spring Boot для использования начального приложения Azure Spring Boot</span><span class="sxs-lookup"><span data-stu-id="f7508-144">Configure your Spring Boot app to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="f7508-145">Найдите файл *pom.xml* в каталоге приложения, например:</span><span class="sxs-lookup"><span data-stu-id="f7508-145">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="f7508-146">-или-</span><span class="sxs-lookup"><span data-stu-id="f7508-146">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Поиск файла pom.xml][PM01]

1. <span data-ttu-id="f7508-148">Откройте файл *pom.xml* в текстовом редакторе и добавьте следующие строки в список `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="f7508-148">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>2.0.4</version>
   </dependency>
   ```

   ![Изменение файла pom.xml][PM02]

   > [!IMPORTANT]
   >
   > <span data-ttu-id="f7508-150">Если для работы с этим руководством вы используете одну из версий Spring Boot 1.5.n, укажите более раннюю версию начального приложения Azure Cosmos DB, например:</span><span class="sxs-lookup"><span data-stu-id="f7508-150">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to specify the older version of the Azure Cosmos DB starter; for example:</span></span>
   >
   > ```xml
   > <dependency>
   >   <groupId>com.microsoft.azure</groupId>
   >   <artifactId>azure-documentdb-spring-boot-starter</artifactId>
   >   <version>0.1.4</version>
   > </dependency>
   > ```

1. <span data-ttu-id="f7508-151">Убедитесь, что версия Spring Boot совпадает с той, которую вы выбрали при создании приложения с помощью Spring Initializr, например:</span><span class="sxs-lookup"><span data-stu-id="f7508-151">Verify that the Spring Boot version is the version that you chose when you created your application with the Spring Initializr; for example:</span></span>

   ```xml
   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.0.1.RELEASE</version>
      <relativePath/>
   </parent>
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="f7508-152">Если для работы с этим руководством вы используете одну из версий Spring Boot 1.5.n, проверьте, выбрана ли правильная версия, например `<version>1.5.14.RELEASE</version>`.</span><span class="sxs-lookup"><span data-stu-id="f7508-152">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to verify the correct version; for example: `<version>1.5.14.RELEASE</version>`.</span></span>
   >

1. <span data-ttu-id="f7508-153">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="f7508-153">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="f7508-154">Настройка приложения Spring Boot для использования Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f7508-154">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="f7508-155">Найдите файл *application.properties* в каталоге *resources*, например:</span><span class="sxs-lookup"><span data-stu-id="f7508-155">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   <span data-ttu-id="f7508-156">-или-</span><span class="sxs-lookup"><span data-stu-id="f7508-156">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![Поиск файла application.properties][RE01]

1. <span data-ttu-id="f7508-158">Откройте файл *application.properties* в текстовом редакторе, добавьте указанные ниже строки в файл и замените примеры значений на соответствующие свойства для базы данных:</span><span class="sxs-lookup"><span data-stu-id="f7508-158">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Редактирование файла application.properties][RE02]

1. <span data-ttu-id="f7508-160">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="f7508-160">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="f7508-161">Добавление примера кода для реализации базовых возможностей базы данных</span><span class="sxs-lookup"><span data-stu-id="f7508-161">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="f7508-162">В этом разделе мы создадим два класса Java для хранения пользовательских данных, а затем изменим класс основного приложения для создания экземпляра класса пользователя и сохраним его в базу данных.</span><span class="sxs-lookup"><span data-stu-id="f7508-162">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the user class and save it to your database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="f7508-163">Определение базового класса для хранения пользовательских данных</span><span class="sxs-lookup"><span data-stu-id="f7508-163">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="f7508-164">Создайте файл с именем *User.java* в том же каталоге, что и файл основного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="f7508-164">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="f7508-165">Откройте файл *User.java* в текстовом редакторе и добавьте в него следующие строки, чтобы определить универсальный класс пользователя, позволяющего сохранять и извлекать значения в базе данных:</span><span class="sxs-lookup"><span data-stu-id="f7508-165">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoysdata;

   // Define a generic User class.
   public class User {
      private String id;
      private String firstName;
      private String lastName;
   
      public User() {
      }
   
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }
   
      public void setId(String id) {
         this.id = id;
      }
   
      public String getFirstName() {
         return firstName;
      }
   
      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }
   
      public String getLastName() {
         return lastName;
      }
   
      public void setLastName(String lastName) {
         this.lastName = lastName;
      }
   
      @Override
      public String toString() {
         return String.format("User: %s %s %s", id, firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="f7508-166">Сохраните и закройте файл *User.java*.</span><span class="sxs-lookup"><span data-stu-id="f7508-166">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="f7508-167">Определение интерфейса хранилища данных</span><span class="sxs-lookup"><span data-stu-id="f7508-167">Define a data repository interface</span></span>

1. <span data-ttu-id="f7508-168">Создайте файл с именем *UserRepository.java* в том же каталоге, что и основной файл приложения Java.</span><span class="sxs-lookup"><span data-stu-id="f7508-168">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="f7508-169">Откройте файл *UserRepository.java* в текстовом редакторе и добавьте в него следующие строки, чтобы определить интерфейс пользовательского репозитория, дополняющего интерфейс репозитория DocumentDB по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="f7508-169">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoysdata;
   
   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { } 
   ```

1. <span data-ttu-id="f7508-170">Сохраните и закройте файл *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="f7508-170">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="f7508-171">Изменение класса основного приложения</span><span class="sxs-lookup"><span data-stu-id="f7508-171">Modify the main application class</span></span>

1. <span data-ttu-id="f7508-172">Найдите файл основного приложения Java в каталоге пакета приложения, например:</span><span class="sxs-lookup"><span data-stu-id="f7508-172">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="f7508-173">-или-</span><span class="sxs-lookup"><span data-stu-id="f7508-173">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Поиск файла приложения Java][JV01]

1. <span data-ttu-id="f7508-175">Откройте файл основного приложения Java в текстовом редакторе и добавьте в него следующие строки:</span><span class="sxs-lookup"><span data-stu-id="f7508-175">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoysdata;

   // These imports are required for the application.
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   // These imports are only used to create an ID for this example.
   import java.util.Date;
   import java.text.SimpleDateFormat;

   @SpringBootApplication
   public class wingtiptoysdataApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;

      public static void main(String[] args) {
         // Execute the command line runner.
         SpringApplication.run(wingtiptoysdataApplication.class, args);
         System.exit(0);
      }

      public void run(String... args) throws Exception {
         // Create a simple date/time ID.
         SimpleDateFormat userId = new SimpleDateFormat("yyyyMMddHHmmssSSS");
         Date currentDate = new Date();

         // Create a new User class.
         final User testUser = new User(userId.format(currentDate), "Gena", "Soto");

         // For this example, remove all of the existing records.
         repository.deleteAll();

         // Save the User class to the Azure database.
         repository.save(testUser);
      
         // Retrieve the database record for the User class you just saved by ID.
         // final User result = repository.findOne(testUser.getId());
         final User result = repository.findById(testUser.getId()).get();

         // Display the results of the database record retrieval.
         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

   > [!IMPORTANT]
   >
   > <span data-ttu-id="f7508-176">Если для работы с этим руководством вы используете одну из версий Spring Boot 1.5.n, измените синтаксис `final User result = repository.findById(testUser.getId()).get();` на `final User result = repository.findOne(testUser.getId());`.</span><span class="sxs-lookup"><span data-stu-id="f7508-176">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to replace the `final User result = repository.findById(testUser.getId()).get();` syntax with `final User result = repository.findOne(testUser.getId());`.</span></span>
   >

1. <span data-ttu-id="f7508-177">Сохраните и закройте файл основного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="f7508-177">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="f7508-178">Создание и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="f7508-178">Build and test your app</span></span>

1. <span data-ttu-id="f7508-179">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="f7508-179">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="f7508-180">-или-</span><span class="sxs-lookup"><span data-stu-id="f7508-180">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="f7508-181">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f7508-181">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="f7508-182">В приложении появится несколько сообщений среды выполнения, включая следующее, указывающее, что значения успешно сохранены и извлечены из базы данных.</span><span class="sxs-lookup"><span data-stu-id="f7508-182">Your application will display several runtime messages, and it will display a message like the following examples to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ```
   User: 20170724025215132 Gena Soto
   ```

   ![Успешные результаты приложения][JV02]

1. <span data-ttu-id="f7508-184">НЕОБЯЗАТЕЛЬНО. На портале Azure на странице свойств базы данных можно просмотреть содержимое Azure Cosmos DB. Для этого нужно щелкнуть **Обозреватель данных** и выбрать элемент из списка для просмотра содержимого.</span><span class="sxs-lookup"><span data-stu-id="f7508-184">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Data Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Просмотр данных с помощью обозревателя документов][JV03]

## <a name="next-steps"></a><span data-ttu-id="f7508-186">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="f7508-186">Next steps</span></span>

<span data-ttu-id="f7508-187">Дополнительные сведения об использовании Azure PowerShell и Java см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="f7508-187">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="f7508-188">[Документация по Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="f7508-188">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="f7508-189">[Azure Cosmos DB. Создание базы данных документов с помощью Java и портала Azure][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="f7508-189">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="f7508-190">[Spring Data для API SQL для Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="f7508-190">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="f7508-191">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="f7508-191">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* <span data-ttu-id="f7508-192">[Spring Boot DocumentDB Starter for Azure] (Начальное приложение Spring Boot DocumentDB для Azure)</span><span class="sxs-lookup"><span data-stu-id="f7508-192">[Spring Boot Document DB Starter for Azure]</span></span>

* [<span data-ttu-id="f7508-193">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="f7508-193">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="f7508-194">Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="f7508-194">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="f7508-195">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="f7508-195">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="f7508-196">**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="f7508-196">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="f7508-197">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="f7508-197">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="f7508-198">В помощь разработчикам, начинающим работать со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения.</span><span class="sxs-lookup"><span data-stu-id="f7508-198">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="f7508-199">Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="f7508-199">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Документация по Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring Data для API SQL для Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Boot DocumentDB Starter for Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample (Начальное приложение Spring Boot DocumentDB для Azure)
[Spring Boot Document DB Starter for Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[инструментах Java для Visual Studio Team Services]: https://azure.microsoft.com/services/devops/java/
[Java Tools for Visual Studio Team Services]: https://azure.microsoft.com/services/devops/java/
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV03.png
