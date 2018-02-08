---
title: "Использование начального приложения Spring Boot с API DocumentDB в Azure Cosmos DB"
description: "Подробные сведения о настройке приложения, созданного с помощью Spring Boot Initializerс API DocumentDB в Azure Cosmos DB."
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm;yungez;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 8190a7c45443ead9855d5a62194e02d7e9a919ee
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2018
---
# <a name="how-to-use-the-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a>Использование начального приложения Spring Boot с API DocumentDB в Azure Cosmos DB

## <a name="overview"></a>Обзор

Azure Cosmos DB — это глобально распределенная служба база данных, предоставляющая разработчикам возможность работать с данными с помощью различных стандартных API, например DocumentDB, MongoDB, Graph и табличных API. Начальное приложение Spring Boot Майкрософт позволяет разработчикам использовать приложения Spring Boot, которые легко интегрируются с Azure Cosmos DB с помощью интерфейсов API DocumentDB.

В этой статье описано, как создать Azure Cosmos DB на портале Azure, создать пользовательское приложение Java с помощью **[Spring Initializr]**, а затем добавить начальное приложение Spring Boot в пользовательское приложение для хранения и получения данных в Azure Cosmos DB с помощью API DocumentDB.

## <a name="prerequisites"></a>предварительным требованиям

Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:

* Подписка Azure. Если у вас ее еще нет, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
* [Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.
* [Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a>Создание Azure Cosmos DB с помощью портала Azure

1. Перейдите на портал Azure по адресу <https://portal.azure.com/> и щелкните **+Создать**.

   ![Портал Azure][AZ01]

1. Щелкните **Базы данных** и **Azure Cosmos DB**.

   ![Портал Azure][AZ02]

1. На странице **Azure Cosmos DB** введите следующие сведения.

   * Введите уникальный **идентификатор**, который будет использоваться в качестве URI для базы данных, например *wingtiptoysdata.documents.azure.com*.
   * Выберите **SQL (Document DB)** для API.
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

1. Укажите, что требуется создать проект **Maven** на **Java**, введите имя **группы** и **артефакта** для приложения, а затем нажмите соответствующую кнопку, чтобы **создать проект**.

   ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > Spring Initializr использует имена **группы** и **артефакта** для создания имени пакета, например *com.example.wintiptoys*.
   >

1. При появлении запроса скачайте проект на локальный компьютер.

   ![Скачивание пользовательского проекта Spring Boot][SI02]

1. После извлечения файлов в локальной системе простое приложение Spring Boot можно будет редактировать.

   ![Пользовательские файлы проекта Spring Boot][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a>Настройка приложения Spring Boot для использования начального приложения Azure Spring Boot

1. Найдите файл *pom.xml* в каталоге приложения, например:

   `C:\SpringBoot\wingtiptoys\pom.xml`

   -или-

   `/users/example/home/wingtiptoys/pom.xml`

   ![Поиск файла pom.xml][PM01]

1. Откройте файл *pom.xml* в текстовом редакторе и добавьте следующие строки в список `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Изменение файла pom.xml][PM02]

1. Сохраните и закройте файл *pom.xml*.

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a>Настройка приложения Spring Boot для использования Azure Cosmos DB

1. Найдите файл *application.properties* в каталоге *resources*, например:

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   -или-

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

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

1. Сохраните и закройте файл *User.java*.

### <a name="define-a-data-repository-interface"></a>Определение интерфейса хранилища данных

1. Создайте файл с именем *UserRepository.java* в том же каталоге, что и основной файл приложения Java.

1. Откройте файл *UserRepository.java* в текстовом редакторе и добавьте в него следующие строки, чтобы определить интерфейс пользовательского репозитория, дополняющего интерфейс репозитория DocumentDB по умолчанию:

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. Сохраните и закройте файл *UserRepository.java*.

### <a name="modify-the-main-application-class"></a>Изменение класса основного приложения

1. Найдите файл основного приложения Java в каталоге пакета приложения, например:

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   -или-

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Поиск файла приложения Java][JV01]

1. Откройте файл основного приложения Java в текстовом редакторе и добавьте в него следующие строки:

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

1. Сохраните и закройте файл основного приложения Java.

## <a name="build-and-test-your-app"></a>Создание и тестирование приложения

1. Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*, например:

   `cd C:\SpringBoot\wingtiptoys`

   -или-

   `cd /users/example/home/wingtiptoys`

1. Создайте приложение Spring Boot с помощью Maven и запустите его, например:

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. В приложении появится несколько сообщений среды выполнения, среди которых будет сообщение `User: testFirstName testLastName`, указывающее, что значения успешно сохранены и извлечены в базе данных.

   ![Успешные результаты приложения][JV02]

1. НЕОБЯЗАТЕЛЬНО. На портале Azure можно просмотреть содержимое Azure Cosmos DB на странице свойств для базы данных. Для этого нужно щелкнуть **обозреватель документов** и выбрать элемент из списка для просмотра содержимого.

   ![Просмотр данных с помощью обозревателя документов][JV03]

## <a name="next-steps"></a>Дополнительная информация

Дополнительные сведения об использовании Azure PowerShell и Java см. в следующих статьях:

* [Документация по Azure Cosmos DB]

* [Azure Cosmos DB. Создание приложения API DocumentDB с помощью Java и портала Azure][Build a DocumentDB API app with Java]

Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:

* [Spring Boot DocumenDB Starter for Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample) (Начальное приложение Spring Boot DocumenDB для Azure)

* [Развертывание приложения Spring Boot Application в службе приложений Azure](deploy-spring-boot-java-web-app-on-azure.md)

* [Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure](deploy-spring-boot-java-app-on-kubernetes.md)

Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].

**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса. Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java. Чтобы помочь разработчикам приступить к работе со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения. Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.

<!-- URL List -->

[Документация по Azure Cosmos DB]: /azure/cosmos-db/
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
