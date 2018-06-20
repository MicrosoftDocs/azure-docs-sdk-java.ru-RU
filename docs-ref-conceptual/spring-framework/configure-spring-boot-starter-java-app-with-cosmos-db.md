---
title: Использование начального приложения Spring Boot с API SQL Azure Cosmos DB
description: Сведения о настройке приложения, созданного с помощью Spring Boot Initializer в API Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;yungez;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 6cf999f3db397760709476dae1f5c0fd83503725
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823807"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="976b2-103">Использование начального приложения Spring Boot с API SQL Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="976b2-103">How to use the Spring Boot Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="976b2-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="976b2-104">Overview</span></span>

<span data-ttu-id="976b2-105">Azure Cosmos DB — это глобально распределенная служба баз данных, предоставляющая разработчикам возможность работать с данными с помощью разных стандартных API, например SQL, MongoDB, Graph и табличных API.</span><span class="sxs-lookup"><span data-stu-id="976b2-105">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as SQL, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="976b2-106">Начальное приложение Spring Boot от Майкрософт позволяет разработчикам использовать приложения Spring Boot, которые легко интегрируются с Azure Cosmos DB с помощью API SQL.</span><span class="sxs-lookup"><span data-stu-id="976b2-106">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using the SQL API.</span></span>

<span data-ttu-id="976b2-107">В этой статье описано, как создать Azure Cosmos DB на портале Azure, создать пользовательское приложение Java с помощью **[Spring Initializr]**, а затем добавить начальное приложение Spring Boot в пользовательское приложение для хранения и получения данных в Azure Cosmos DB с помощью API SQL.</span><span class="sxs-lookup"><span data-stu-id="976b2-107">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Boot Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using the SQL API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="976b2-108">предварительным требованиям</span><span class="sxs-lookup"><span data-stu-id="976b2-108">Prerequisites</span></span>

<span data-ttu-id="976b2-109">Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="976b2-109">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="976b2-110">Подписка Azure. Если у вас ее еще нет, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="976b2-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="976b2-111">[Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="976b2-111">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="976b2-112">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="976b2-112">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="976b2-113">Создание Azure Cosmos DB с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="976b2-113">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="976b2-114">Перейдите на портал Azure по адресу <https://portal.azure.com/> и щелкните **+Создать**.</span><span class="sxs-lookup"><span data-stu-id="976b2-114">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Портал Azure][AZ01]

1. <span data-ttu-id="976b2-116">Щелкните **Базы данных** и **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="976b2-116">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Портал Azure][AZ02]

1. <span data-ttu-id="976b2-118">На странице **Azure Cosmos DB** введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="976b2-118">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="976b2-119">Введите уникальный **идентификатор**, который будет использоваться в качестве URI для базы данных,</span><span class="sxs-lookup"><span data-stu-id="976b2-119">Enter a unique **ID**, which you will use as the URI for your database.</span></span> <span data-ttu-id="976b2-120">например *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="976b2-120">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="976b2-121">Выберите **SQL (Document DB)** для API.</span><span class="sxs-lookup"><span data-stu-id="976b2-121">Choose **SQL (Document DB)** for the API.</span></span>
   * <span data-ttu-id="976b2-122">Выберите **подписку**, которую нужно использовать для базы данных.</span><span class="sxs-lookup"><span data-stu-id="976b2-122">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="976b2-123">Укажите, следует ли создать **группу ресурсов** для базы данных, или выберите имеющуюся группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="976b2-123">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="976b2-124">Укажите **расположение** для базы данных.</span><span class="sxs-lookup"><span data-stu-id="976b2-124">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="976b2-125">Указав эти параметры, щелкните **Создать**, чтобы создать базу данных.</span><span class="sxs-lookup"><span data-stu-id="976b2-125">When you have specified these options, click **Create** to create your database.</span></span>

   ![Портал Azure][AZ03]

1. <span data-ttu-id="976b2-127">При создании база данных указывается на **панели мониторинга** Azure, а также на страницах **Все ресурсы** и **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="976b2-127">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="976b2-128">Вы можете выбрать свою базу данных в любом из этих расположений, чтобы открыть страницу свойств кэша.</span><span class="sxs-lookup"><span data-stu-id="976b2-128">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Портал Azure][AZ04]

1. <span data-ttu-id="976b2-130">Когда откроется страница свойств базы данных, щелкните **Ключи доступа** и скопируйте URI и ключи доступа для базы данных. Эти значения будут использоваться в приложении Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="976b2-130">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Портал Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="976b2-132">Создание простого приложения Spring Boot с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="976b2-132">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="976b2-133">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="976b2-133">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="976b2-134">Укажите, что требуется создать проект **Maven** на **Java**, введите имя **группы** и **артефакта** для приложения, а затем нажмите соответствующую кнопку, чтобы **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="976b2-134">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the button to **Generate Project**.</span></span>

   ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="976b2-136">Spring Initializr использует имена **группы** и **артефакта** для создания имени пакета, например *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="976b2-136">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="976b2-137">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="976b2-137">When prompted, download the project to a path on your local computer.</span></span>

   ![Скачивание пользовательского проекта Spring Boot][SI02]

1. <span data-ttu-id="976b2-139">После извлечения файлов в локальной системе простое приложение Spring Boot можно будет редактировать.</span><span class="sxs-lookup"><span data-stu-id="976b2-139">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Пользовательские файлы проекта Spring Boot][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="976b2-141">Настройка приложения Spring Boot для использования начального приложения Azure Spring Boot</span><span class="sxs-lookup"><span data-stu-id="976b2-141">Configure your Spring Boot app to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="976b2-142">Найдите файл *pom.xml* в каталоге приложения, например:</span><span class="sxs-lookup"><span data-stu-id="976b2-142">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="976b2-143">-или-</span><span class="sxs-lookup"><span data-stu-id="976b2-143">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Поиск файла pom.xml][PM01]

1. <span data-ttu-id="976b2-145">Откройте файл *pom.xml* в текстовом редакторе и добавьте следующие строки в список `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="976b2-145">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Изменение файла pom.xml][PM02]

1. <span data-ttu-id="976b2-147">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="976b2-147">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="976b2-148">Настройка приложения Spring Boot для использования Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="976b2-148">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="976b2-149">Найдите файл *application.properties* в каталоге *resources*, например:</span><span class="sxs-lookup"><span data-stu-id="976b2-149">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="976b2-150">-или-</span><span class="sxs-lookup"><span data-stu-id="976b2-150">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Поиск файла application.properties][RE01]

1. <span data-ttu-id="976b2-152">Откройте файл *application.properties* в текстовом редакторе, добавьте указанные ниже строки в файл и замените примеры значений на соответствующие свойства для базы данных:</span><span class="sxs-lookup"><span data-stu-id="976b2-152">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Редактирование файла application.properties][RE02]

1. <span data-ttu-id="976b2-154">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="976b2-154">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="976b2-155">Добавление примера кода для реализации базовых возможностей базы данных</span><span class="sxs-lookup"><span data-stu-id="976b2-155">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="976b2-156">В этом разделе мы создадим два класса Java для хранения пользовательских данных, а затем изменим класс основного приложения для создания экземпляра класса пользователя и сохраним его в базу данных.</span><span class="sxs-lookup"><span data-stu-id="976b2-156">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the user class and save it to your database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="976b2-157">Определение базового класса для хранения пользовательских данных</span><span class="sxs-lookup"><span data-stu-id="976b2-157">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="976b2-158">Создайте файл с именем *User.java* в том же каталоге, что и файл основного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="976b2-158">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="976b2-159">Откройте файл *User.java* в текстовом редакторе и добавьте в него следующие строки, чтобы определить универсальный класс пользователя, позволяющего сохранять и извлекать значения в базе данных:</span><span class="sxs-lookup"><span data-stu-id="976b2-159">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
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
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="976b2-160">Сохраните и закройте файл *User.java*.</span><span class="sxs-lookup"><span data-stu-id="976b2-160">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="976b2-161">Определение интерфейса хранилища данных</span><span class="sxs-lookup"><span data-stu-id="976b2-161">Define a data repository interface</span></span>

1. <span data-ttu-id="976b2-162">Создайте файл с именем *UserRepository.java* в том же каталоге, что и основной файл приложения Java.</span><span class="sxs-lookup"><span data-stu-id="976b2-162">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="976b2-163">Откройте файл *UserRepository.java* в текстовом редакторе и добавьте в него следующие строки, чтобы определить интерфейс пользовательского репозитория, дополняющего интерфейс репозитория DocumentDB по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="976b2-163">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="976b2-164">Сохраните и закройте файл *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="976b2-164">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="976b2-165">Изменение класса основного приложения</span><span class="sxs-lookup"><span data-stu-id="976b2-165">Modify the main application class</span></span>

1. <span data-ttu-id="976b2-166">Найдите файл основного приложения Java в каталоге пакета приложения, например:</span><span class="sxs-lookup"><span data-stu-id="976b2-166">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="976b2-167">-или-</span><span class="sxs-lookup"><span data-stu-id="976b2-167">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Поиск файла приложения Java][JV01]

1. <span data-ttu-id="976b2-169">Откройте файл основного приложения Java в текстовом редакторе и добавьте в него следующие строки:</span><span class="sxs-lookup"><span data-stu-id="976b2-169">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. <span data-ttu-id="976b2-170">Сохраните и закройте файл основного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="976b2-170">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="976b2-171">Создание и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="976b2-171">Build and test your app</span></span>

1. <span data-ttu-id="976b2-172">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="976b2-172">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="976b2-173">-или-</span><span class="sxs-lookup"><span data-stu-id="976b2-173">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="976b2-174">Создайте приложение Spring Boot с помощью Maven и запустите его, например:</span><span class="sxs-lookup"><span data-stu-id="976b2-174">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="976b2-175">В приложении появится несколько сообщений среды выполнения, среди которых будет сообщение `User: testFirstName testLastName`, указывающее, что значения успешно сохранены и извлечены в базе данных.</span><span class="sxs-lookup"><span data-stu-id="976b2-175">Your application will display several runtime messages, and you should see the message `User: testFirstName testLastName` displayed to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Успешные результаты приложения][JV02]

1. <span data-ttu-id="976b2-177">НЕОБЯЗАТЕЛЬНО. На портале Azure можно просмотреть содержимое Azure Cosmos DB на странице свойств для базы данных. Для этого нужно щелкнуть **обозреватель документов** и выбрать элемент из списка для просмотра содержимого.</span><span class="sxs-lookup"><span data-stu-id="976b2-177">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Document Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Просмотр данных с помощью обозревателя документов][JV03]

## <a name="next-steps"></a><span data-ttu-id="976b2-179">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="976b2-179">Next steps</span></span>

<span data-ttu-id="976b2-180">Дополнительные сведения об использовании Azure PowerShell и Java см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="976b2-180">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="976b2-181">[Документация по Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="976b2-181">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="976b2-182">[Azure Cosmos DB. Создание базы данных документов с помощью Java и портала Azure][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="976b2-182">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="976b2-183">[Spring Data для API SQL для Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="976b2-183">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="976b2-184">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="976b2-184">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* <span data-ttu-id="976b2-185">[Spring Boot DocumenDB Starter for Azure] (Начальное приложение Spring Boot DocumenDB для Azure)</span><span class="sxs-lookup"><span data-stu-id="976b2-185">[Spring Boot DocumenDB Starter for Azure]</span></span>

* [<span data-ttu-id="976b2-186">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="976b2-186">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="976b2-187">Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="976b2-187">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="976b2-188">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="976b2-188">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="976b2-189">**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="976b2-189">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="976b2-190">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="976b2-190">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="976b2-191">В помощь разработчикам, начинающим работать со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения.</span><span class="sxs-lookup"><span data-stu-id="976b2-191">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="976b2-192">Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="976b2-192">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Документация по Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring Data для API SQL для Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Boot DocumenDB Starter for Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample (Начальное приложение Spring Boot DocumenDB для Azure)
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
