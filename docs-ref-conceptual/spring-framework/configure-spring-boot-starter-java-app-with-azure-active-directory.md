---
title: "Как использовать приложение Spring Boot Starter с Azure Active Directory"
description: "Сведения о настройке приложения Spring Initializr с помощью начального приложения Azure Active Directory."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: cf1cad0b87626058f7204a6565d09fb8901b7ce4
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2018
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="a317b-103">Как использовать приложение Spring Boot Starter с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a317b-103">How to use the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="a317b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a317b-104">Overview</span></span>

<span data-ttu-id="a317b-105">В этой статье описано, как создать с помощью **[Spring Initializr]** начальное приложение Spring Boot для Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a317b-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a317b-106">предварительным требованиям</span><span class="sxs-lookup"><span data-stu-id="a317b-106">Prerequisites</span></span>

<span data-ttu-id="a317b-107">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="a317b-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="a317b-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="a317b-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="a317b-109">[Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="a317b-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="a317b-110">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="a317b-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="a317b-111">Создание пользовательского приложения с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="a317b-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="a317b-112">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="a317b-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="a317b-113">Укажите, что необходимо создать проект **Maven** с помощью **Java**, введите имя **группы** и **артефакта** вашего приложения, а затем щелкните ссылку, чтобы **перейти к полной версии** Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="a317b-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Указание имен группы и артефакта][security-01]

1. <span data-ttu-id="a317b-115">Прокрутите вниз до раздела **Core** (Основные) и установите флажок рядом с пунктом **Security**, а в разделе **Web** (Веб) — рядом с пунктом **Web**.</span><span class="sxs-lookup"><span data-stu-id="a317b-115">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Выбор начальных приложений Security и Web][security-02]

1. <span data-ttu-id="a317b-117">Прокрутите вниз до раздела **Azure** статьи и установите флажок рядом с пунктом **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a317b-117">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Выбор начального приложения Azure Active Directory][security-03]

1. <span data-ttu-id="a317b-119">Прокрутите страницу вниз и нажмите соответствующую кнопку, чтобы **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="a317b-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Создание проекта Spring Boot][security-04]

1. <span data-ttu-id="a317b-121">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="a317b-121">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="a317b-122">Создание и настройка экземпляра Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a317b-122">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="a317b-123">Создание экземпляра Active Directory</span><span class="sxs-lookup"><span data-stu-id="a317b-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="a317b-124">Перейдите по адресу <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="a317b-124">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="a317b-125">Щелкните **+Создать**, **Безопасность и идентификация**, **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a317b-125">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Создание экземпляра Azure Active Directory][directory-01]

1. <span data-ttu-id="a317b-127">Укажите **имя организации** и **первоначальное доменное имя**, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a317b-127">Enter your **Organization name** and your **Initial domain name**, and then click **Create**.</span></span>

   ![Указание имен Azure Active Directory][directory-02]

1. <span data-ttu-id="a317b-129">Выберите новый экземпляр Azure Active Directory в раскрывающемся меню на панели сверху на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a317b-129">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Выбор экземпляра Azure Active Directory][directory-03]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="a317b-131">Регистрация приложения для приложения Spring Boot</span><span class="sxs-lookup"><span data-stu-id="a317b-131">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="a317b-132">На портале в меню выберите **Azure Active Directory**, щелкните **Обзор** и выберите **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="a317b-132">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Регистрация приложения][directory-04]

1. <span data-ttu-id="a317b-134">Щелкните **Регистрация нового приложения**, введите **имя** приложения, укажите http://localhost:8080 в качестве **URL-адреса входа**, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a317b-134">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Создание регистрации приложения][directory-05]

1. <span data-ttu-id="a317b-136">Щелкните зарегистрированное приложение.</span><span class="sxs-lookup"><span data-stu-id="a317b-136">Click your application registration after it has been created.</span></span>

   ![Выбор зарегистрированного приложения][directory-06]

1. <span data-ttu-id="a317b-138">Когда откроется страница приложения, скопируйте **идентификатор приложения** для дальнейшего использования, а затем щелкните **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="a317b-138">When the page for your app registration, copy your **Application ID** for later, then click **Keys**.</span></span>

   ![Создание ключей зарегистрированного приложения][directory-07]

1. <span data-ttu-id="a317b-140">Добавьте **описание** и укажите **длительность** использования нового ключа, а затем щелкните **Сохранить**. Значение ключа будет указано автоматически, когда вы щелкнете значок **Сохранить**. Вам нужно скопировать это значение для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="a317b-140">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key for later.</span></span> <span data-ttu-id="a317b-141">(Вы не сможете получить это значение позже.)</span><span class="sxs-lookup"><span data-stu-id="a317b-141">(You will not be able to retrieve this value later.)</span></span>

   ![Указание параметров зарегистрированного приложения][directory-08]

1. <span data-ttu-id="a317b-143">На главной странице приложения щелкните **Требуемые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="a317b-143">From the main page for your app registration, click **Required permissions**.</span></span>

   ![Добавление требуемых разрешений для приложения][directory-09]

1. <span data-ttu-id="a317b-145">Щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a317b-145">Click **Windows Azure Active Directory**.</span></span>

   ![Выбор Azure Active Directory][directory-10]

1. <span data-ttu-id="a317b-147">Установите флажки рядом с пунктами **Доступ к каталогу как пользователь, выполнивший вход** и **Вход в систему и чтение профиля пользователя**, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a317b-147">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Включение разрешений на доступ][directory-11]

1. <span data-ttu-id="a317b-149">На странице **Требуемые разрешения** щелкните **Предоставить разрешения** и **Да**.</span><span class="sxs-lookup"><span data-stu-id="a317b-149">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Предоставление разрешений на доступ][directory-12]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="a317b-151">Настройка и компиляция приложения Spring Boot</span><span class="sxs-lookup"><span data-stu-id="a317b-151">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="a317b-152">Распакуйте скачанный архив с файлами проекта в каталог.</span><span class="sxs-lookup"><span data-stu-id="a317b-152">Extract the files from the downloaded project archive into a directory.</span></span>

1. <span data-ttu-id="a317b-153">Перейдите в родительскую папку проекта и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="a317b-153">Navigate to the parent folder in your project and open the *pom.xml* file in a text editor.</span></span>

1. <span data-ttu-id="a317b-154">Добавьте зависимости для компонента Spring Security OAuth2, например:</span><span class="sxs-lookup"><span data-stu-id="a317b-154">Add the dependency for Spring OAuth2 security; for example:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.security.oauth</groupId>
      <artifactId>spring-security-oauth2</artifactId>
   </dependency>
   ```

1. <span data-ttu-id="a317b-155">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="a317b-155">Save and close the  the *pom.xml* file.</span></span>

1. <span data-ttu-id="a317b-156">В папке *src/main/resources* проекта откройте файл *application.properties* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="a317b-156">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="a317b-157">Добавьте ключ для учетной записи, используя полученные ранее значения, например:</span><span class="sxs-lookup"><span data-stu-id="a317b-157">Add the key for your storage account using the values from earlier; for example:</span></span>

   ```yaml
   # Specifies your Active Directory Application ID:
   azure.activedirectory.clientId=11111111-1111-1111-1111-1111111111111111

   # Specifies your secret key:
   azure.activedirectory.clientSecret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authentication:
   azure.activedirectory.activeDirectoryGroups=Users
   ```
   <span data-ttu-id="a317b-158">Описание</span><span class="sxs-lookup"><span data-stu-id="a317b-158">Where:</span></span>
   | <span data-ttu-id="a317b-159">Параметр</span><span class="sxs-lookup"><span data-stu-id="a317b-159">Parameter</span></span> | <span data-ttu-id="a317b-160">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="a317b-160">Description</span></span> |
   |---|---|
   | `azure.activedirectory.clientId` | <span data-ttu-id="a317b-161">Содержит **идентификатор приложения** (см. выше).</span><span class="sxs-lookup"><span data-stu-id="a317b-161">Contains your **Application ID** from earlier.</span></span> |
   | `azure.activedirectory.clientSecret` | <span data-ttu-id="a317b-162">Содержит значение ключа, полученное при выполненной ранее регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="a317b-162">Contains the key value from your app registration which you completed earlier.</span></span> |
   | `azure.activedirectory.activeDirectoryGroups` | <span data-ttu-id="a317b-163">Содержит список групп Active Directory, используемых для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="a317b-163">Contains a list of Active Directory groups to use for authentication.</span></span> |


1. <span data-ttu-id="a317b-164">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="a317b-164">Save and close the  the *application.properties* file.</span></span>

1. <span data-ttu-id="a317b-165">Создайте папку с именем *controller* в папке с исходным кодом Java для приложения, например: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="a317b-165">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="a317b-166">Создайте файл Java с именем *HelloController.java* в папке *controller* и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="a317b-166">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="a317b-167">Вставьте следующий код, а затем сохраните и закройте файл:</span><span class="sxs-lookup"><span data-stu-id="a317b-167">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;
   
   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   
   import org.springframework.security.access.prepost.PreAuthorize;
   import org.springframework.security.web.authentication.preauth.PreAuthenticatedAuthenticationToken;
   
   @RestController
   public class HelloController {
      @PreAuthorize("hasRole('Users')")
      @RequestMapping("/")
      public String hello() {
         return "Hello World!";
      }
   }
   ```

1. <span data-ttu-id="a317b-168">Создайте папку с именем *security* в папке с исходным кодом Java для приложения, например: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="a317b-168">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="a317b-169">Создайте файл Java с именем *WebSecurityConfig.java* в папке *security* и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="a317b-169">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="a317b-170">Вставьте следующий код, а затем сохраните и закройте файл:</span><span class="sxs-lookup"><span data-stu-id="a317b-170">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;

   import com.microsoft.azure.spring.autoconfigure.aad.AADAuthenticationFilter;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.autoconfigure.security.oauth2.client.EnableOAuth2Sso;
   import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
   import org.springframework.security.config.annotation.web.builders.HttpSecurity;
   import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
   import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;
   import org.springframework.security.web.csrf.CookieCsrfTokenRepository;
   
   @EnableOAuth2Sso
   @EnableGlobalMethodSecurity(securedEnabled = true, prePostEnabled = true)
   
   public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
      @Autowired
      private AADAuthenticationFilter aadAuthFilter;
      @Override
      protected void configure(HttpSecurity http) throws Exception {
         http.authorizeRequests().anyRequest().permitAll();
         http.addFilterBefore(aadAuthFilter, UsernamePasswordAuthenticationFilter.class);
      }
   }
   ```

## <a name="build-and-test-your-app"></a><span data-ttu-id="a317b-171">Создание и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="a317b-171">Build and test your app</span></span>

1. <span data-ttu-id="a317b-172">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="a317b-172">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="a317b-173">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a317b-173">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   ```

   ![Сборка приложения][build-application]

1. <span data-ttu-id="a317b-175">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a317b-175">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="a317b-176">Когда созданное приложение будет запущено в Maven, перейдите по адресу <http://localhost:8080> в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="a317b-176">After your application is built and started by Maven, open <http://localhost:8080> in a web browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a317b-177">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="a317b-177">Next steps</span></span>

<span data-ttu-id="a317b-178">См. дополнительные сведения об использовании Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="a317b-178">For more information about using Azure Active Directory, see the following articles:</span></span>

* <span data-ttu-id="a317b-179">[Документация Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="a317b-179">[Azure Active Directory Documentation].</span></span>

<span data-ttu-id="a317b-180">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="a317b-180">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="a317b-181">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="a317b-181">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="a317b-182">Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="a317b-182">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="a317b-183">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="a317b-183">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="a317b-184">**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="a317b-184">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="a317b-185">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="a317b-185">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="a317b-186">Чтобы помочь разработчикам приступить к работе со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения.</span><span class="sxs-lookup"><span data-stu-id="a317b-186">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="a317b-187">Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="a317b-187">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Документация Azure Active Directory]: /azure/active-directory/
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[security-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-01.png
[security-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-02.png
[security-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-03.png
[security-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-04.png

[directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-01.png
[directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-02.png
[directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-03.png
[directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-04.png
[directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-05.png
[directory-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-06.png
[directory-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-07.png
[directory-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-08.png
[directory-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-09.png
[directory-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-10.png
[directory-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-11.png
[directory-12]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-12.png

[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
