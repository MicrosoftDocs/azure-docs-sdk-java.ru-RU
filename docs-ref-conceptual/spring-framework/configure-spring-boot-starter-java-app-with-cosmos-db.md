---
title: Использование начального приложения Spring Boot с API SQL Azure Cosmos DB
description: Сведения о настройке приложения, созданного с помощью Spring Boot Initializer в API Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 08/10/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: dcb5ef5f12cc1682175da147268eb4a6a89f820b
ms.sourcegitcommit: 0f38ef9ad64cffdb7b2e9e966224dfd0af251b0f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703527"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a>Использование начального приложения Spring Boot с API SQL Azure Cosmos DB

## <a name="overview"></a>Обзор

Azure Cosmos DB — это глобально распределенная служба баз данных, предоставляющая разработчикам возможность работать с данными с помощью разных стандартных API, например SQL, MongoDB, Graph и табличных API. Начальное приложение Spring Boot от Майкрософт позволяет разработчикам использовать приложения Spring Boot, которые легко интегрируются с Azure Cosmos DB с помощью API SQL.

В этой статье описано, как создать Azure Cosmos DB на портале Azure, создать пользовательское приложение Java с помощью **[Spring Initializr]**, а затем добавить начальное приложение Spring Boot в пользовательское приложение для хранения и получения данных в Azure Cosmos DB с помощью API SQL.

## <a name="prerequisites"></a>Предварительные требования

Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:

* Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
* [Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.
* [Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a>Создание Azure Cosmos DB с помощью портала Azure

1. Перейдите на портал Azure по адресу <https://portal.azure.com/> и щелкните **+Создать ресурс**.

   ![Портал Azure][AZ01]

1. Щелкните **Базы данных** и **Azure Cosmos DB**.

   ![Портал Azure][AZ02]

1. На странице **Azure Cosmos DB** введите следующие сведения.

   * Введите уникальный **идентификатор**, который будет использоваться в качестве URI для базы данных, например *wingtiptoysdata.documents.azure.com*.
   * Выберите **SQL** в качестве API.
   * Выберите **подписку**, которую нужно использовать для базы данных.
   * Укажите, следует ли создать **группу ресурсов** для базы данных, или выберите имеющуюся группу ресурсов.
   * Укажите **расположение** для базы данных.
   
   Указав эти параметры, щелкните **Создать**, чтобы создать базу данных.

   ![Портал Azure][AZ03]

1. При создании база данных указывается на **панели мониторинга** Azure, а также на страницах **Все ресурсы** и **Azure Cosmos DB**. Вы можете выбрать свою базу данных в любом из этих расположений, чтобы открыть страницу свойств кэша.

   ![Портал Azure][AZ04]

1. Когда откроется страница свойств базы данных, щелкните **Ключи доступа** и скопируйте URI и ключи доступа для базы данных. Эти значения будут использоваться в приложении Spring Boot.

   ![Портал Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Создание простого приложения Spring Boot с помощью Spring Initializr

1. Перейдите по адресу <https://start.spring.io/>.

1. Укажите, что требуется создать проект **Maven** на **Java**, введите имя **группы** и **артефакта** для приложения, укажите версию **Spring Boot**, а затем нажмите соответствующую кнопку, чтобы **создать проект**.

   > [!IMPORTANT]
   >
   > Внесены критические изменения в API Spring Boot версии 2.0.n, которые будут использоваться при выполнении действий, описанных в этой статье. Для выполнения этих действий вы также можете использовать одну из версий Spring Boot 1.5.n. Различия будут выделены, где это необходимо.
   >

   ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > Spring Initializr использует имена **группы** и **артефакта** для создания имени пакета, например *com.example.wintiptoysdata*.
   >

1. При появлении запроса скачайте проект на локальный компьютер.

   ![Скачивание пользовательского проекта Spring Boot][SI02]

1. После извлечения файлов в локальной системе простое приложение Spring Boot можно будет редактировать.

   ![Пользовательские файлы проекта Spring Boot][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a>Настройка приложения Spring Boot для использования начального приложения Azure Spring Boot

1. Найдите файл *pom.xml* в каталоге приложения, например:

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   -или-

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Поиск файла pom.xml][PM01]

1. Откройте файл *pom.xml* в текстовом редакторе и добавьте следующие строки в список `<dependencies>`:

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
   > Если для работы с этим руководством вы используете одну из версий Spring Boot 1.5.n, укажите более раннюю версию начального приложения Azure Cosmos DB, например:
   >
   > ```xml
   > <dependency>
   >   <groupId>com.microsoft.azure</groupId>
   >   <artifactId>azure-documentdb-spring-boot-starter</artifactId>
   >   <version>0.1.4</version>
   > </dependency>
   > ```

1. Убедитесь, что версия Spring Boot совпадает с той, которую вы выбрали при создании приложения с помощью Spring Initializr, например:

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
   > Если для работы с этим руководством вы используете одну из версий Spring Boot 1.5.n, проверьте, выбрана ли правильная версия, например `<version>1.5.14.RELEASE</version>`.
   >

1. Сохраните и закройте файл *pom.xml*.

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a>Настройка приложения Spring Boot для использования Azure Cosmos DB

1. Найдите файл *application.properties* в каталоге *resources*, например:

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   -или-

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![Поиск файла application.properties][RE01]

1. Откройте файл *application.properties* в текстовом редакторе, добавьте указанные ниже строки в файл и замените примеры значений на соответствующие свойства для базы данных:

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Редактирование файла application.properties][RE02]

1. Сохраните и закройте файл *application.properties*.

## <a name="add-sample-code-to-implement-basic-database-functionality"></a>Добавление примера кода для реализации базовых возможностей базы данных

В этом разделе мы создадим два класса Java для хранения пользовательских данных, а затем изменим класс основного приложения для создания экземпляра класса пользователя и сохраним его в базу данных.

### <a name="define-a-basic-class-for-storing-user-data"></a>Определение базового класса для хранения пользовательских данных

1. Создайте файл с именем *User.java* в том же каталоге, что и файл основного приложения Java.

1. Откройте файл *User.java* в текстовом редакторе и добавьте в него следующие строки, чтобы определить универсальный класс пользователя, позволяющего сохранять и извлекать значения в базе данных:

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

1. Сохраните и закройте файл *User.java*.

### <a name="define-a-data-repository-interface"></a>Определение интерфейса хранилища данных

1. Создайте файл с именем *UserRepository.java* в том же каталоге, что и основной файл приложения Java.

1. Откройте файл *UserRepository.java* в текстовом редакторе и добавьте в него следующие строки, чтобы определить интерфейс пользовательского репозитория, дополняющего интерфейс репозитория DocumentDB по умолчанию:

   ```java
   package com.example.wingtiptoysdata;
   
   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { } 
   ```

1. Сохраните и закройте файл *UserRepository.java*.

### <a name="modify-the-main-application-class"></a>Изменение класса основного приложения

1. Найдите файл основного приложения Java в каталоге пакета приложения, например:

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   -или-

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Поиск файла приложения Java][JV01]

1. Откройте файл основного приложения Java в текстовом редакторе и добавьте в него следующие строки:

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
   > Если для работы с этим руководством вы используете одну из версий Spring Boot 1.5.n, измените синтаксис `final User result = repository.findById(testUser.getId()).get();` на `final User result = repository.findOne(testUser.getId());`.
   >

1. Сохраните и закройте файл основного приложения Java.

## <a name="build-and-test-your-app"></a>Создание и тестирование приложения

1. Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*, например:

   `cd C:\SpringBoot\wingtiptoysdata`

   -или-

   `cd /users/example/home/wingtiptoysdata`

1. Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. В приложении появится несколько сообщений среды выполнения, включая следующее, указывающее, что значения успешно сохранены и извлечены из базы данных.

   ```
   User: 20170724025215132 Gena Soto
   ```

   ![Успешные результаты приложения][JV02]

1. НЕОБЯЗАТЕЛЬНО. На портале Azure на странице свойств базы данных можно просмотреть содержимое Azure Cosmos DB. Для этого нужно щелкнуть **Обозреватель данных** и выбрать элемент из списка для просмотра содержимого.

   ![Просмотр данных с помощью обозревателя документов][JV03]

## <a name="next-steps"></a>Дополнительная информация

Дополнительные сведения об использовании Azure PowerShell и Java см. в следующих статьях:

* [Документация по Azure Cosmos DB]

* [Azure Cosmos DB. Создание базы данных документов с помощью Java и портала Azure][Build a SQL API app with Java]

* [Spring Data для API SQL для Azure Cosmos DB]

Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:

* [Spring Boot DocumentDB Starter for Azure] (Начальное приложение Spring Boot DocumentDB для Azure)

* [Развертывание приложения Spring Boot Application в службе приложений Azure](deploy-spring-boot-java-web-app-on-azure.md)

* [Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure](deploy-spring-boot-java-app-on-kubernetes.md)

Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].

**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса. Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java. В помощь разработчикам, начинающим работать со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения. Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.

<!-- URL List -->

[Документация по Azure Cosmos DB]: /azure/cosmos-db/
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring Data для API SQL для Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Boot DocumentDB Starter for Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample (Начальное приложение Spring Boot DocumentDB для Azure)
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
