---
title: "Как настроить приложение Spring Boot Initializer для использования кэша Redis"
description: "Узнайте, как настроить приложение Spring Boot, созданное с помощью Spring Initializer, для использования кэша Redis для Azure."
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Spring Starter, Redis Cache
ms.assetid: 
ms.service: cache
ms.workload: na
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: ce8202b48c6759a80560616492eab018434e9307
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2017
---
# <a name="how-to-configure-a-spring-boot-initializer-app-to-use-redis-cache"></a>Как настроить приложение Spring Boot Initializer для использования кэша Redis

## <a name="overview"></a>Обзор

**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса. Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java. Чтобы помочь разработчикам приступить к работе со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения. Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.

В этой статье описывается создание кэша Redis с помощью портала Azure, использование **Spring Initializr** для создания пользовательского приложения, а также создание веб-приложения Java, которое сохраняет и извлекает данные с помощью кэша Redis.

## <a name="prerequisites"></a>Предварительные требования

Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:

* Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].

* [Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.

* [Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.

## <a name="create-a-redis-cache-on-azure"></a>Создание кэша Redis в Azure

1. Перейдите на портал Azure по адресу <https://portal.azure.com/> и щелкните элемент **+Создать**.

   ![Портал Azure][AZ01]

1. Выберите **База данных**, а затем — **Кэш Redis**.

   ![Портал Azure][AZ02]

1. На странице **Новый кэш Redis** укажите следующие сведения:

   * Введите **DNS-имя** для кэша.
   * Укажите **подписку**, **группу ресурсов**, **расположение** и **ценовую категорию**.
   * Для работы с этим руководством установите флажок **Разблокировать порт 6379 (без шифрования SSL)**.

   > [!NOTE]
   >
   > С кэшами Redis можно использовать протокол SSL, но при этом вам потребуется другой клиент Redis, например Jedis. Дополнительные сведения см. в статье [Использование кэша Redis для Azure с Java][Redis Cache with Java].
   >

   Указав эти параметры, щелкните **Создать**, чтобы создать кэш.

   ![Портал Azure][AZ03]

1. После создания кэша он появится в списке на **информационной панели** Azure, а также на страницах **Все ресурсы** и **Кэш Redis**. Вы можете выбрать свой кэш в любом из этих расположений, чтобы открыть страницу свойств кэша.

   ![Портал Azure][AZ04]

1. Когда отобразится страница, содержащая список свойств кэша, щелкните **Ключи доступа** и скопируйте ключи доступа для кэша.

   ![Портал Azure][AZ05]

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Создание пользовательского приложения с помощью Spring Initializr

1. Перейдите по адресу <https://start.spring.io/>.

1. Укажите, что необходимо создать проект **Maven** с помощью **Java**, введите имя **группы** и **артефакта** вашего приложения, а затем щелкните ссылку, чтобы **перейти к полной версии** Spring Initializr.

   ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > Spring Initializr будет использовать имена **группы** и **артефакта** для создания имени пакета, например *com.contoso.myazuredemo*.
   >

1. Прокрутите вниз к разделу **Web** (Веб) и установите флажок для параметра **Web** (Веб). Затем прокрутите вниз к разделу **NoSQL** и установите флажок для параметра **Redis**, затем перейдите к нижней части страницы и нажмите кнопку **Generate Project** (Создать проект).

   ![Все параметры Spring Initializr][SI02]

1. При появлении запроса скачайте проект на локальный компьютер.

   ![Скачивание пользовательского проекта Spring Boot][SI03]

1. После извлечения файлов в локальной системе пользовательское приложение Spring Boot можно будет редактировать.

   ![Пользовательские файлы проекта Spring Boot][SI04]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a>Настройка пользовательского приложения Spring Boot для использования кэша Redis

1. Найдите файл *application.properties* в каталоге *resources* приложения или создайте файл, если он еще не существует.

   ![Поиск файла application.properties][RE01]

1. Откройте файл *application.properties* в текстовом редакторе, добавьте указанные ниже строки в файл и замените примеры значений на соответствующие свойства из вашего кэша:

   ```yaml
   # Specify the DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify the port for your Redis cache.
   spring.redis.port=6379

   # Specify the access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Редактирование файла application.properties][RE02]

   > [!NOTE]
   >
   > Если вы используете другой клиент Redis, позволяющий использовать SSL, например Jedis, следует указать порт 6380 в файле *application.properties*. Дополнительные сведения см. в статье [Использование кэша Redis для Azure с Java][Redis Cache with Java].
   >

1. Сохраните и закройте файл *application.properties*.

1. Создайте папку с именем *controller* в исходной папке пакета, например:

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   -или-

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. Создайте файл с именем *HelloController.java* в папке *controller*. Откройте файл в текстовом редакторе и добавьте в него следующий код:

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.data.redis.core.StringRedisTemplate;
   import org.springframework.data.redis.core.ValueOperations;

   @RestController
   public class HelloController {
   
      @Autowired
      private StringRedisTemplate template;

      @RequestMapping("/")
      // Define the Hello World controller.
      public String hello() {
      
         ValueOperations<String, String> ops = this.template.opsForValue();

         // Add a Hello World string to your cache.
         String key = "greeting";
         if (!this.template.hasKey(key)) {
             ops.set(key, "Hello World!");
         }

         // Return the string from your cache.
         return ops.get(key);
      }
   }
   ```
   
   В этом примере кода необходимо заменить `com.contoso.myazuredemo` именем пакета проекта.

1. Сохраните и закройте файл *HelloController.java*.

1. Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Протестируйте веб-приложение, перейдя по адресу http://localhost:8080 в веб-браузере, или, если имеется программа curl, используйте синтаксис, как в следующем примере:

   ```shell
   curl http://localhost:8080
   ```

   В примере контроллера должно отобразиться сообщение "Hello World!", которое динамически извлекается из кэша Redis.

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:

* [Развертывание приложения Spring Boot Application в службе приложений Azure](deploy-spring-boot-java-web-app-on-azure.md)

* [Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure](deploy-spring-boot-java-app-on-kubernetes.md)

Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [инструментов Java для Visual Studio Team Services].

Дополнительные сведения о начале работы с кэшем Redis с помощью Java в Azure см. в [этой статье][Redis Cache with Java].

<!-- URL List -->

[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[инструментов Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Redis Cache with Java]: /azure/redis-cache/cache-java-get-started

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ01.png
[AZ02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ02.png
[AZ03]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ03.png
[AZ04]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ04.png
[AZ05]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ05.png

[SI01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI01.png
[SI02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI02.png
[SI03]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI03.png
[SI04]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI04.png

[RE01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/RE01.png
[RE02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/RE02.png
