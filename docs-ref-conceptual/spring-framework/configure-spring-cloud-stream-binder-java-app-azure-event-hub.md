---
title: Создание приложения Spring Cloud Stream Binder с помощью Центров событий Azure
description: Настройка приложения Spring Cloud Stream Binder на основе Java, созданного с помощью Spring Boot Initializr и Центров событий Azure.
services: event-hubs
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 09/10/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: dfc3b6121bddcb637735047e2e7bc7485da9a4fe
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799950"
---
# <a name="how-to-create-a-spring-cloud-stream-binder-application-with-azure-event-hubs"></a>Создание приложения Spring Cloud Stream Binder с помощью Центров событий Azure

## <a name="overview"></a>Обзор

В статье показано, как настроить приложение Spring Cloud Stream Binder на основе Java, созданное с помощью Spring Boot Initializr и Центров событий Azure.

## <a name="prerequisites"></a>Предварительные требования

Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:

* Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
* [Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.
* [Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.

> [!IMPORTANT]
>
> Для выполнения операций, описанных в этой статье, требуется Spring Boot 2.0 или более поздней версии.
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a>Создание концентратора событий на портале Azure

### <a name="create-an-azure-event-hub-namespace"></a>Создание пространства имен концентратора событий Azure

1. Перейдите на портал Azure по адресу <https://portal.azure.com/> и выполните вход.

1. Выберите **+Создать ресурс**, **Интернет вещей** и **Центры событий**.

   ![Создание пространства имен концентратора событий Azure][IMG01]

1. На странице **Создание пространства имен** введите такую информацию:

   * Уникальное **имя**, которое станет частью URI для пространства имен концентратора событий. Например, если вы зададите **wingtiptoys** в качестве **имени**, URI примет вид *wingtiptoys.servicebus.windows.net*.
   * Выберите **ценовую категорию** для пространства имен концентратора событий.
   * Выберите **подписку** для пространства имен.
   * Укажите, следует ли создать новую **группу ресурсов** для пространства имен или использовать существующую.
   * Укажите **расположение** для пространства имен Центров событий.

   ![Создание пространства имен для концентратора событий Azure][IMG02]

1. Указав эти параметры, щелкните **Создать**, чтобы создать пространство имен.

### <a name="create-an-azure-event-hub-in-your-namespace"></a>Создание концентратора событий Azure в пространстве имен

1. Перейдите на портал Azure по адресу <https://portal.azure.com/>.

1. Щелкните **Все ресурсы** и выберите созданное пространство имен.

   ![Выбор пространства имен концентратора событий Azure][IMG03]

1. Щелкните **Центры событий**, а затем **+Концентратор событий**.

   ![Добавление нового концентратора событий][IMG04]

1. В области **Создание концентратора событий** введите уникальное **имя** для концентратора событий и щелкните **Создать**.

   ![Создание концентратора событий Azure][IMG05]

1. Созданный концентратор событий появится в списке на странице **Центры событий**.

   ![Создание концентратора событий Azure][IMG06]

### <a name="create-an-azure-storage-account-for-your-event-hub-checkpoints"></a>Создание учетной записи хранения для контрольных точек концентратора событий

1. Перейдите на портал Azure по адресу <https://portal.azure.com/>.

1. Щелкните **+Создать ресурс**, **Служба хранилища**, **Учетная запись хранения**.

   ![Создание учетной записи хранения Azure][IMG07]

1. На странице **Создание пространства имен** введите такую информацию:

   * Уникальное **имя**, которое станет частью URI для учетной записи хранения. Например, если вы зададите **wingtiptoys** в качестве **имени**, URI примет вид *wingtiptoys.core.windows.net*.
   * Выберите **Хранилище BLOB-объектов** в поле **Тип учетной записи**.
   * Укажите **расположение** для учетной записи хранения.
   * Выберите **подписку**, которую нужно использовать для учетной записи хранения.
   * Укажите, следует ли создать новую **группу ресурсов** для учетной записи хранения или использовать существующую.

   ![Создание учетной записи хранения Azure][IMG08]

1. Указав эти параметры, щелкните **Создать**, чтобы создать учетную запись хранения.

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Создание простого приложения Spring Boot с помощью Spring Initializr

1. Перейдите по адресу <https://start.spring.io/>.

1. Задайте такие параметры:

   * Выберите в соответствующих полях **Maven Project** (Проект Maven) и **Java**.
   * Выберите версию **Spring Boot** не ниже версии 2.0.
   * Заполните поля **Group** (Группа) и **Artifact** (Артефакт) для приложения.
   * Добавьте зависимость **Web** (Веб).

      ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > Spring Initializr использует имена в полях **Group** (Группа) и **Artifact** (Артефакт) для создания имени пакета, например *com.example.wintiptoys*.
   >

1. Указав эти параметры, щелкните **Generate Project** (Создать проект).

1. При появлении запроса скачайте проект на локальный компьютер.

   ![Скачивание проекта Spring][SI02]

1. После извлечения файлов в локальной системе простое приложение Spring Boot можно будет редактировать.

## <a name="configure-your-spring-boot-app-to-use-the-azure-event-hub-starter"></a>Настройка приложения Spring Boot для использования начального приложения концентратора событий Azure

1. Найдите файл *pom.xml* в корневой папке приложения, например так:

   `C:\SpringBoot\eventhub\pom.xml`

   -или-

   `/users/example/home/eventhub/pom.xml`

1. Откройте файл *pom.xml* в текстовом редакторе и добавьте начальное приложение Spring Cloud Stream Binder для концентратора событий Azure в список `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-eventhub-stream-binder</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Редактирование файла pom.xml][SI03]

1. Сохраните и закройте файл *pom.xml*.

## <a name="create-an-azure-credential-file"></a>Создание файла учетных данных Azure

1. Откройте окно командной строки.

1. Перейдите к каталогу *resources* приложения Spring Boot, например так:

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   -или-

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. Вход в учетную запись Azure:

   ```azurecli
   az login
   ```

1. Отобразите список подписок:

   ```azurecli
   az account list
   ```
   Azure отобразит список подписок, и вам нужно будет скопировать идентификатор GUID для подписки, которая будет использоваться, например:

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "11111111-1111-1111-1111-111111111111",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "22222222-2222-2222-2222-222222222222",
       "user": {
         "name": "gena.soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]

1. Specify the GUID for the subscription you want to use with Azure; for example:

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. Создайте файл учетных данных Azure:

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   Эта команда создаст файл *my.azureauth* в каталоге *resources* приблизительно с таким содержимым:

   ```json
   {
     "clientId": "33333333-3333-3333-3333-333333333333",
     "clientSecret": "44444444-4444-4444-4444-444444444444",
     "subscriptionId": "11111111-1111-1111-1111-111111111111",
     "tenantId": "22222222-2222-2222-2222-222222222222",
     "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
     "resourceManagerEndpointUrl": "https://management.azure.com/",
     "activeDirectoryGraphResourceId": "https://graph.windows.net/",
     "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
     "galleryEndpointUrl": "https://gallery.azure.com/",
     "managementEndpointUrl": "https://management.core.windows.net/"
   }
   ```

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a>Настройка приложения Spring Boot для использования концентратора событий Azure

1. Найдите файл *application.properties* в каталоге *resources* приложения, например так:

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   -или-

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. Откройте файл *application.properties* в текстовом редакторе, добавьте следующие строки и замените примеры значений соответствующими параметрами концентратора событий:

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace
   spring.cloud.azure.eventhub.checkpoint-storage-account=wingtiptoysstorage
   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   spring.cloud.stream.eventhub.bindings.input.consumer.checkpoint-mode=MANUAL
   ```
   Описание

   |                          Поле                           |                                                                                   ОПИСАНИЕ                                                                                    |
   |----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |        `spring.cloud.azure.credential-file-path`         |                                                    Определяет файл учетных данных Azure, который был создан ранее в этом примере.                                                    |
   |           `spring.cloud.azure.resource-group`            |                                                      Определяет группу ресурсов Azure, которая содержит концентратор событий Azure.                                                      |
   |               `spring.cloud.azure.region`                |                                           Определяет географический регион, указанный при создании концентратора событий Azure.                                            |
   |         `spring.cloud.azure.eventhub.namespace`          |                                          Определяет уникальное имя, заданное при создании пространства имен концентратора событий Azure.                                           |
   | `spring.cloud.azure.eventhub.checkpoint-storage-account` |                                                    Определяет учетную запись хранения Azure, которая была создана ранее в этом примере.                                                    |
   |     `spring.cloud.stream.bindings.input.destination`     |                            Определяет назначение входящих данных концентратора событий Azure, которым в этом примере является сам концентратор, созданный ранее.                            |
   |       `spring.cloud.stream.bindings.input.group `        | Определяет группу потребителей концентратора событий Azure, для которой можно установить значение $Default, чтобы использовать базовую группу потребителей, созданную вместе с концентратором событий Azure. |
   |    `spring.cloud.stream.bindings.output.destination`     |                               Определяет назначение исходящих данных для концентратора событий Azure, которое в этом примере совпадает с назначением входящих данных.                               |


3. Сохраните и закройте файл *application.properties*.

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a>Добавление примера кода для реализации базовых функций концентратора событий

В этом разделе вы создадите классы Java, требуемые для отправки событий в концентратор событий.

### <a name="modify-the-main-application-class"></a>Изменение класса основного приложения

1. Найдите файл основного приложения Java в каталоге пакета приложения, например:

   `C:\SpringBoot\eventhub\src\main\java\com\wingtiptoys\eventhub\EventhubApplication.java`

   -или-

   `/users/example/home/eventhub/src/main/java/com/wingtiptoys/eventhub/EventhubApplication.java`

1. Откройте файл основного приложения Java в текстовом редакторе и добавьте в него следующие строки:

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class EventhubApplication {
      public static void main(String[] args) {
         SpringApplication.run(EventhubApplication.class, args);
      }
   }
   ```

1. Сохраните и закройте файл основного приложения Java.

### <a name="create-a-new-class-for-the-source-connector"></a>Создание класса для соединителя источника

1. В каталоге пакета приложения создайте файл Java с именем *EventhubSource.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class EventhubSource {

      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String postMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```
1. Сохраните и закройте файл *EventhubSource.java*.

### <a name="create-a-new-class-for-the-sink-connector"></a>Создание класса для соединителя приемника

1. В каталоге пакета приложения создайте файл Java с именем *EventhubSink.java*, а затем откройте этот файл в текстовом редакторе и добавьте следующие строки:

   ```java
   package com.wingtiptoys.eventhub;

   import com.microsoft.azure.spring.integration.core.AzureHeaders;
   import com.microsoft.azure.spring.integration.core.api.Checkpointer;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;
   import org.springframework.messaging.handler.annotation.Header;

   @EnableBinding(Sink.class)
   public class EventhubSink {

      private static final Logger LOGGER = LoggerFactory.getLogger(EventhubSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message, @Header(AzureHeaders.CHECKPOINTER) Checkpointer checkpointer) {
         LOGGER.info("New message received: '{}'", message);
         checkpointer.success().handle((r, ex) -> {
            if (ex == null) {
               LOGGER.info("Message '{}' successfully checkpointed", message);
            }
            return null;
         });
      }
   }
   ```

1. Сохраните и закройте файл *EventhubSink.java*.

## <a name="build-and-test-your-application"></a>Сборка и тестирование приложения

1. Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*, например:

   `cd C:\SpringBoot\eventhub`

   -или-

   `cd /users/example/home/eventhub`

1. Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. После запуска приложения можно использовать средство *curl*, чтобы протестировать приложение, например:

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   В журнале приложения должна появиться запись "hello". Например: 

   ```shell
   [Thread-13] INFO com.wingtiptoys.eventhub.EventhubSink - New message received: 'hello'
   [pool-10-thread-7] INFO com.wingtiptoys.eventhub.EventhubSink - Message 'hello' successfully checkpointed
   ```

## <a name="next-steps"></a>Дополнительная информация

Дополнительные сведения о поддержке в Azure приложения Event Hub Stream Binder для концентратора событий см. в следующих статьях:

* [Что такое Центры событий Azure?](/azure/event-hubs/event-hubs-about)

* [Создание пространства имен службы "Центры событий" и концентратора событий с помощью портала Azure](/azure/event-hubs/event-hubs-create)

* [How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs](configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub.md) (Использование начального приложения Spring Boot для Apache Kafka в Центрах событий)

См. дополнительные сведения об использовании Java в Azure и [инструментах Java для Visual Studio Team Services].

**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса. Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java. В помощь разработчикам, начинающим работать со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения. Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.

<!-- URL List -->

[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-03.png
