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
# <a name="how-to-configure-a-spring-boot-initializer-app-to-use-redis-cache"></a><span data-ttu-id="e0921-104">Как настроить приложение Spring Boot Initializer для использования кэша Redis</span><span class="sxs-lookup"><span data-stu-id="e0921-104">How to configure a Spring Boot Initializer app to use Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="e0921-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="e0921-105">Overview</span></span>

<span data-ttu-id="e0921-106">**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="e0921-106">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="e0921-107">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="e0921-107">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="e0921-108">Чтобы помочь разработчикам приступить к работе со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения.</span><span class="sxs-lookup"><span data-stu-id="e0921-108">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="e0921-109">Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="e0921-109">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="e0921-110">В этой статье описывается создание кэша Redis с помощью портала Azure, использование **Spring Initializr** для создания пользовательского приложения, а также создание веб-приложения Java, которое сохраняет и извлекает данные с помощью кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="e0921-110">This article walks you through creating a Redis cache using the Azure portal, then using the **Spring Initializr** to create a custom application, and then creating a Java web application that stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0921-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e0921-111">Prerequisites</span></span>

<span data-ttu-id="e0921-112">Чтобы выполнить действия, описанные в этой статье, необходимо иметь следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="e0921-112">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="e0921-113">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="e0921-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="e0921-114">[Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="e0921-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="e0921-115">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="e0921-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="e0921-116">Создание кэша Redis в Azure</span><span class="sxs-lookup"><span data-stu-id="e0921-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="e0921-117">Перейдите на портал Azure по адресу <https://portal.azure.com/> и щелкните элемент **+Создать**.</span><span class="sxs-lookup"><span data-stu-id="e0921-117">Browse to the Azure portal at <https://portal.azure.com/> and click the item for **+New**.</span></span>

   ![Портал Azure][AZ01]

1. <span data-ttu-id="e0921-119">Выберите **База данных**, а затем — **Кэш Redis**.</span><span class="sxs-lookup"><span data-stu-id="e0921-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Портал Azure][AZ02]

1. <span data-ttu-id="e0921-121">На странице **Новый кэш Redis** укажите следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="e0921-121">On the **New Redis Cache** page, specify the following information:</span></span>

   * <span data-ttu-id="e0921-122">Введите **DNS-имя** для кэша.</span><span class="sxs-lookup"><span data-stu-id="e0921-122">Enter the **DNS name** for your cache.</span></span>
   * <span data-ttu-id="e0921-123">Укажите **подписку**, **группу ресурсов**, **расположение** и **ценовую категорию**.</span><span class="sxs-lookup"><span data-stu-id="e0921-123">Specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span>
   * <span data-ttu-id="e0921-124">Для работы с этим руководством установите флажок **Разблокировать порт 6379 (без шифрования SSL)**.</span><span class="sxs-lookup"><span data-stu-id="e0921-124">For this tutorial, choose **Unblock port 6379**.</span></span>

   > [!NOTE]
   >
   > <span data-ttu-id="e0921-125">С кэшами Redis можно использовать протокол SSL, но при этом вам потребуется другой клиент Redis, например Jedis.</span><span class="sxs-lookup"><span data-stu-id="e0921-125">You can use SSL with Redis caches, but you would need to use a different Redis client like Jedis.</span></span> <span data-ttu-id="e0921-126">Дополнительные сведения см. в статье [Использование кэша Redis для Azure с Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="e0921-126">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>
   >

   <span data-ttu-id="e0921-127">Указав эти параметры, щелкните **Создать**, чтобы создать кэш.</span><span class="sxs-lookup"><span data-stu-id="e0921-127">When you have specified these options, click **Create** to create your cache.</span></span>

   ![Портал Azure][AZ03]

1. <span data-ttu-id="e0921-129">После создания кэша он появится в списке на **информационной панели** Azure, а также на страницах **Все ресурсы** и **Кэш Redis**.</span><span class="sxs-lookup"><span data-stu-id="e0921-129">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="e0921-130">Вы можете выбрать свой кэш в любом из этих расположений, чтобы открыть страницу свойств кэша.</span><span class="sxs-lookup"><span data-stu-id="e0921-130">You can click on your cache on any of those locations to open the properties page for your cache.</span></span>

   ![Портал Azure][AZ04]

1. <span data-ttu-id="e0921-132">Когда отобразится страница, содержащая список свойств кэша, щелкните **Ключи доступа** и скопируйте ключи доступа для кэша.</span><span class="sxs-lookup"><span data-stu-id="e0921-132">When the page that contains the list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Портал Azure][AZ05]

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="e0921-134">Создание пользовательского приложения с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="e0921-134">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="e0921-135">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="e0921-135">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="e0921-136">Укажите, что необходимо создать проект **Maven** с помощью **Java**, введите имя **группы** и **артефакта** вашего приложения, а затем щелкните ссылку, чтобы **перейти к полной версии** Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="e0921-136">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="e0921-138">Spring Initializr будет использовать имена **группы** и **артефакта** для создания имени пакета, например *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="e0921-138">The Spring Initializr will use the **Group** and **Aritifact** names to create the package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="e0921-139">Прокрутите вниз к разделу **Web** (Веб) и установите флажок для параметра **Web** (Веб). Затем прокрутите вниз к разделу **NoSQL** и установите флажок для параметра **Redis**, затем перейдите к нижней части страницы и нажмите кнопку **Generate Project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="e0921-139">Scroll down to the **Web** section and check the box for **Web**, then scroll down to the **NoSQL** section and check the box for **Redis**, then scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Все параметры Spring Initializr][SI02]

1. <span data-ttu-id="e0921-141">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="e0921-141">When prompted, download the project to a path on your local computer.</span></span>

   ![Скачивание пользовательского проекта Spring Boot][SI03]

1. <span data-ttu-id="e0921-143">После извлечения файлов в локальной системе пользовательское приложение Spring Boot можно будет редактировать.</span><span class="sxs-lookup"><span data-stu-id="e0921-143">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Пользовательские файлы проекта Spring Boot][SI04]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a><span data-ttu-id="e0921-145">Настройка пользовательского приложения Spring Boot для использования кэша Redis</span><span class="sxs-lookup"><span data-stu-id="e0921-145">Configure your custom Spring Boot to use your Redis Cache</span></span>

1. <span data-ttu-id="e0921-146">Найдите файл *application.properties* в каталоге *resources* приложения или создайте файл, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="e0921-146">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![Поиск файла application.properties][RE01]

1. <span data-ttu-id="e0921-148">Откройте файл *application.properties* в текстовом редакторе, добавьте указанные ниже строки в файл и замените примеры значений на соответствующие свойства из вашего кэша:</span><span class="sxs-lookup"><span data-stu-id="e0921-148">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties from your cache:</span></span>

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
   > <span data-ttu-id="e0921-150">Если вы используете другой клиент Redis, позволяющий использовать SSL, например Jedis, следует указать порт 6380 в файле *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="e0921-150">If you were using a different Redis client like Jedis that enables SSL, you would specify port 6380 in your *application.properties* file.</span></span> <span data-ttu-id="e0921-151">Дополнительные сведения см. в статье [Использование кэша Redis для Azure с Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="e0921-151">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>
   >

1. <span data-ttu-id="e0921-152">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="e0921-152">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="e0921-153">Создайте папку с именем *controller* в исходной папке пакета, например:</span><span class="sxs-lookup"><span data-stu-id="e0921-153">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="e0921-154">-или-</span><span class="sxs-lookup"><span data-stu-id="e0921-154">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="e0921-155">Создайте файл с именем *HelloController.java* в папке *controller*.</span><span class="sxs-lookup"><span data-stu-id="e0921-155">Create a new file named *HelloController.java* in the *controller* folder.</span></span> <span data-ttu-id="e0921-156">Откройте файл в текстовом редакторе и добавьте в него следующий код:</span><span class="sxs-lookup"><span data-stu-id="e0921-156">Open the file in a text editor and add the following code to it:</span></span>

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
   
   <span data-ttu-id="e0921-157">В этом примере кода необходимо заменить `com.contoso.myazuredemo` именем пакета проекта.</span><span class="sxs-lookup"><span data-stu-id="e0921-157">Where you will need to replace `com.contoso.myazuredemo` with the package name for your project.</span></span>

1. <span data-ttu-id="e0921-158">Сохраните и закройте файл *HelloController.java*.</span><span class="sxs-lookup"><span data-stu-id="e0921-158">Save and close the *HelloController.java* file.</span></span>

1. <span data-ttu-id="e0921-159">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e0921-159">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="e0921-160">Протестируйте веб-приложение, перейдя по адресу http://localhost:8080 в веб-браузере, или, если имеется программа curl, используйте синтаксис, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="e0921-160">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="e0921-161">В примере контроллера должно отобразиться сообщение "Hello World!",</span><span class="sxs-lookup"><span data-stu-id="e0921-161">You should see the "Hello World!"</span></span> <span data-ttu-id="e0921-162">которое динамически извлекается из кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="e0921-162">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0921-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e0921-163">Next steps</span></span>

<span data-ttu-id="e0921-164">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="e0921-164">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="e0921-165">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="e0921-165">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="e0921-166">Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="e0921-166">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="e0921-167">Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [инструментов Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e0921-167">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="e0921-168">Дополнительные сведения о начале работы с кэшем Redis с помощью Java в Azure см. в [этой статье][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="e0921-168">For more information about getting started using Redis Cache with Java on Azure, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>

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
