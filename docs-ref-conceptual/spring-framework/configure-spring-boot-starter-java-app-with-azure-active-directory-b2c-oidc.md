---
title: Как использовать начальное приложение Spring Boot с Azure Active Directory B2C
description: Сведения о настройке приложения Spring Boot Initializer с помощью начального приложения Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: java
author: panli
manager: kevinzha
editor: panli
ms.assetid: ''
ms.author: panli
ms.date: 02/28/2019
ms.devlang: java
ms.service: active-directory-b2c
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 21aa6c812a519d686356851a57f00688d9a24fa4
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65625713"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory-b2c"></a><span data-ttu-id="a7515-103">Руководство по защите приложения Java с использованием начального приложения Spring Boot для Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="a7515-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory B2C.</span></span>

## <a name="overview"></a><span data-ttu-id="a7515-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="a7515-104">Overview</span></span>

<span data-ttu-id="a7515-105">В этой статье описывается, как с помощью [Spring Initializr](https://start.spring.io/) создать начальное приложение Java Spring Boot для Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7515-105">This article demonstrates creating a Java app with the [Spring Initializr](https://start.spring.io/) that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7515-106">Из этого руководства вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="a7515-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a7515-107">создание приложения Java с помощью Spring Initializr;</span><span class="sxs-lookup"><span data-stu-id="a7515-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="a7515-108">настройка Azure Active Directory B2C;</span><span class="sxs-lookup"><span data-stu-id="a7515-108">Configure Azure Active Directory B2C</span></span>
> * <span data-ttu-id="a7515-109">защита приложения с помощью классов и аннотаций Spring Boot;</span><span class="sxs-lookup"><span data-stu-id="a7515-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="a7515-110">сборка и тестирование приложения Java.</span><span class="sxs-lookup"><span data-stu-id="a7515-110">Build and test your Java application</span></span>

<span data-ttu-id="a7515-111">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="a7515-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7515-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a7515-112">Prerequisites</span></span>

<span data-ttu-id="a7515-113">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="a7515-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="a7515-114">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="a7515-114">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="a7515-115">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="a7515-115">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="a7515-116">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="a7515-116">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="a7515-117">Создание приложения с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="a7515-117">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="a7515-118">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="a7515-118">Browse to <https://start.spring.io/>.</span></span>

2. <span data-ttu-id="a7515-119">Укажите, что необходимо создать проект **Maven** с помощью **Java**, введите имя **группы** и **артефакта** вашего приложения, а затем выберите модуль **Интернет** и **Безопасность** Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="a7515-119">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then select the **Web** and **Security** module of the Spring Initializr.</span></span>

   ![Указание имен группы и артефакта](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/SI.png)


3. <span data-ttu-id="a7515-121">При появлении запроса щелкните `Generate Project` и скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="a7515-121">Click `Generate Project`, download the project to a path on your local computer when prompted.</span></span>

## <a name="create-azure-active-directory-instance"></a><span data-ttu-id="a7515-122">Создание экземпляра Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7515-122">Create Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="a7515-123">Создание экземпляра Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7515-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="a7515-124">Войдите на сайт <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="a7515-124">Log into <https://portal.azure.com>.</span></span>

2. <span data-ttu-id="a7515-125">Щелкните **Создать ресурс**, а затем выберите **Удостоверение** и **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="a7515-125">Click **+Create a resource**, then **Identity**, and then **Azure Active Directory B2C**.</span></span>

   ![Создание экземпляра Azure Active Directory B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ1.png)

3. <span data-ttu-id="a7515-127">Укажите **имя организации** и **первоначальное доменное имя**, а затем запишите **имя домена** как `${your-tenant-name}` и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a7515-127">Enter your **Organization name** and your **Initial domain name**, record the **domain name** as your `${your-tenant-name}` and click **Create**.</span></span>

   ![Получение имени клиента B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ5.png)

4. <span data-ttu-id="a7515-129">Выберите имя учетной записи в правом верхнем углу панели инструментов на портале Azure и щелкните **Переключение каталога**.</span><span class="sxs-lookup"><span data-stu-id="a7515-129">Select your account name on the top-right of the Azure portal toolbar, then click **Switch directory**.</span></span>

   ![Выбор экземпляра Azure Active Directory](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ2.png)

5. <span data-ttu-id="a7515-131">Выберите новый экземпляр Azure Active Directory в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="a7515-131">Select your new Azure Active Directory from the drop-down menu.</span></span>

   ![Выбор экземпляра Azure Active Directory](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ3.png)

6. <span data-ttu-id="a7515-133">Найдите `b2c` и щелкните службу `Azure AD B2C`.</span><span class="sxs-lookup"><span data-stu-id="a7515-133">Search `b2c` and click `Azure AD B2C` service.</span></span>

   ![Поиск экземпляра Azure Active Directory B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ4.png)

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="a7515-135">Регистрация приложения для приложения Spring Boot</span><span class="sxs-lookup"><span data-stu-id="a7515-135">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="a7515-136">В меню портала выберите **Azure AD B2C**, щелкните **Приложения**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a7515-136">Select **Azure AD B2C** from the portal menu, click **Applications**, and then click **Add**.</span></span>

   ![Регистрация приложения](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C1.png)

2. <span data-ttu-id="a7515-138">Укажите **имя** приложения, введите `http://localhost:8080/home` в поле **URL-адрес ответа**, запишите значение параметра **Идентификатор приложения** как `${your-client-id}`, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a7515-138">Specify your application **Name**, add `http://localhost:8080/home` for the **Reply URL**, record the **Application ID** as your `${your-client-id}` and then click **Save**.</span></span>

   ![Добавление URL-адреса ответа приложения](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C2.png)

3. <span data-ttu-id="a7515-140">В приложении выберите **Ключи**, щелкните **Создать ключ**, чтобы создать `${your-client-secret}`, а затем выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a7515-140">Select **Keys** from your application, click **Generate key** to generate `${your-client-secret}` and then **Save**.</span></span>

4. <span data-ttu-id="a7515-141">Слева выберите **Потоки пользователей**, а затем щелкните **Создать поток пользователя**.</span><span class="sxs-lookup"><span data-stu-id="a7515-141">Select **User flows** on your left, and then **Click** \*\*New user flow \*\*.</span></span>

   ![Создание потока пользователя](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C3.png)

5. <span data-ttu-id="a7515-143">Выберите **Sign up or in** (Регистрация или вход), **Profile editing** (Изменение профиля) и **Сброс пароля**, чтобы создать соответствующие потоки пользователей.</span><span class="sxs-lookup"><span data-stu-id="a7515-143">Choose **Sign up or in**, **Profile editing** and **Password reset** to create user flows respectively.</span></span> <span data-ttu-id="a7515-144">Укажите **имя** потока пользователя, а также **атрибуты пользователя и утверждения** и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a7515-144">Specify your user flow **Name** and **User attributes and claims**, click **Create**.</span></span>

   ![Настройка потока пользователей](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C4.png)

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="a7515-146">Настройка и компиляция приложения</span><span class="sxs-lookup"><span data-stu-id="a7515-146">Configure and compile your app</span></span>

1. <span data-ttu-id="a7515-147">Распакуйте архив с файлами проекта, который вы создали и скачали в каталог ранее в рамках этого руководства.</span><span class="sxs-lookup"><span data-stu-id="a7515-147">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

2. <span data-ttu-id="a7515-148">Перейдите в родительскую папку проекта и откройте файл проекта Maven `pom.xml` в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="a7515-148">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

3. <span data-ttu-id="a7515-149">Добавьте зависимости для защиты с помощью Spring OAuth2 в `pom.xml`:</span><span class="sxs-lookup"><span data-stu-id="a7515-149">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.azure</groupId>
       <artifactId>azure-active-directory-b2c-spring-boot-starter</artifactId>
       <version>2.1.6.M2</version>
   </dependency>
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-thymeleaf</artifactId>
   </dependency>
   <dependency>
       <groupId>org.thymeleaf.extras</groupId>
       <artifactId>thymeleaf-extras-springsecurity5</artifactId>
   </dependency>
   ```

4. <span data-ttu-id="a7515-150">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="a7515-150">Save and close the *pom.xml* file.</span></span>

5. <span data-ttu-id="a7515-151">В папке *src/main/resources* проекта откройте файл *application.yml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="a7515-151">Navigate to the *src/main/resources* folder in your project and open the *application.yml* file in a text editor.</span></span>

6. <span data-ttu-id="a7515-152">Задайте параметры для регистрации вашего приложения, используя созданные ранее значения. Например:</span><span class="sxs-lookup"><span data-stu-id="a7515-152">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

   ```yaml
   azure:
     activedirectory:
       b2c:
         tenant: ${your-tenant-name}
         client-id: ${your-client-id}
         client-secret: ${your-client-secret}
         reply-url: ${your-reply-url-from-aad} # should be absolute url.
         logout-success-url: ${you-logout-success-url}
         user-flows:
           sign-up-or-sign-in: ${your-sign-up-or-in-user-flow}
           profile-edit: ${your-profile-edit-user-flow}     # optional
           password-reset: ${your-password-reset-user-flow} # optional
   ```
   <span data-ttu-id="a7515-153">Описание</span><span class="sxs-lookup"><span data-stu-id="a7515-153">Where:</span></span>

   | <span data-ttu-id="a7515-154">Параметр</span><span class="sxs-lookup"><span data-stu-id="a7515-154">Parameter</span></span> | <span data-ttu-id="a7515-155">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="a7515-155">Description</span></span> |
   |---|---|
   | `azure.activedirectory.b2c.tenant` | <span data-ttu-id="a7515-156">Содержит имя `${your-tenant-name` AD B2C, указанное ранее.</span><span class="sxs-lookup"><span data-stu-id="a7515-156">Contains your AD B2C's `${your-tenant-name` from earlier.</span></span> |
   | `azure.activedirectory.b2c.client-id` | <span data-ttu-id="a7515-157">Содержит `${your-client-id}` из приложения, указанный ранее.</span><span class="sxs-lookup"><span data-stu-id="a7515-157">Contains the `${your-client-id}` from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.client-secret` | <span data-ttu-id="a7515-158">Содержит `${your-client-secret}` из приложения, указанный ранее.</span><span class="sxs-lookup"><span data-stu-id="a7515-158">Contains the `${your-client-secret}` from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.reply-url` | <span data-ttu-id="a7515-159">Содержит один из **URL-адресов ответа** из приложения, указанных ранее.</span><span class="sxs-lookup"><span data-stu-id="a7515-159">Contains one of the **Reply URL** from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.logout-success-url` | <span data-ttu-id="a7515-160">Указывает URL-адрес после успешного выхода из приложения.</span><span class="sxs-lookup"><span data-stu-id="a7515-160">Specify the URL when your application logout successfully.</span></span> |
   | `azure.activedirectory.b2c.user-flows` | <span data-ttu-id="a7515-161">Содержит имена потоков пользователей, созданных ранее.</span><span class="sxs-lookup"><span data-stu-id="a7515-161">Contains the name of the user flows that you completed earlier.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="a7515-162">Полный список значений, доступных в файле *application.yml*, см. в [примере приложения Spring Boot для Azure Active Directory B2C][примере приложения Spring Boot для AAD B2C] на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="a7515-162">For a full list of values that are available in your *application.yml* file, see the [Azure Active Directory B2C Spring Boot Sample][AAD B2C Spring Boot Sample] on GitHub.</span></span>
   >

7. <span data-ttu-id="a7515-163">Сохраните и закройте файл *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="a7515-163">Save and close the *application.yml* file.</span></span>

8. <span data-ttu-id="a7515-164">Создайте папку с именем *controller* в исходной папке Java для приложения.</span><span class="sxs-lookup"><span data-stu-id="a7515-164">Create a folder named *controller* in the Java source folder for your application.</span></span>

9. <span data-ttu-id="a7515-165">Создайте файл Java с именем *HelloController.java* в папке *controller* и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="a7515-165">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

10. <span data-ttu-id="a7515-166">Вставьте следующий код, а затем сохраните и закройте файл:</span><span class="sxs-lookup"><span data-stu-id="a7515-166">Enter the following code, then save and close the file:</span></span>

    ```java
    package sample.aad.controller;
    
    import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
    import org.springframework.security.oauth2.core.user.OAuth2User;
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.Model;
    import org.springframework.web.bind.annotation.GetMapping;
    
    @Controller
    public class WebController {
    
        private void initializeModel(Model model, OAuth2AuthenticationToken token) {
            if (token != null) {
                final OAuth2User user = token.getPrincipal();
    
                model.addAttribute("grant_type", user.getAuthorities());
                model.addAllAttributes(user.getAttributes());
            }
        }
    
        @GetMapping(value = "/")
        public String index(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "home";
        }
    
        @GetMapping(value = "/greeting")
        public String greeting(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "greeting";
        }
    
        @GetMapping(value = "/home")
        public String home(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "home";
        }
    }
    ```

11. <span data-ttu-id="a7515-167">Создайте папку с именем *security* в исходной папке Java для приложения.</span><span class="sxs-lookup"><span data-stu-id="a7515-167">Create a folder named *security* in the Java source folder for your application.</span></span>

12. <span data-ttu-id="a7515-168">Создайте файл Java с именем *WebSecurityConfig.java* в папке *security* и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="a7515-168">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

13. <span data-ttu-id="a7515-169">Вставьте следующий код, а затем сохраните и закройте файл:</span><span class="sxs-lookup"><span data-stu-id="a7515-169">Enter the following code, then save and close the file:</span></span>

    ```java
    package sample.aad.security;
    
    import com.microsoft.azure.spring.autoconfigure.b2c.AADB2COidcLoginConfigurer;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
    import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
    
    @EnableWebSecurity
    public class WebSecurityConfiguration extends WebSecurityConfigurerAdapter {
    
        private final AADB2COidcLoginConfigurer configurer;
    
        public WebSecurityConfiguration(AADB2COidcLoginConfigurer configurer) {
            this.configurer = configurer;
        }
    
        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                    .authorizeRequests()
                    .anyRequest()
                    .authenticated()
                    .and()
                    .apply(configurer)
            ;
        }
    }
    ```
14. <span data-ttu-id="a7515-170">Скопируйте `greeting.html` и `home.html` из [примера приложения Spring Boot для Azure AD B2C](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates), а затем замените `${your-profile-edit-user-flow}` и `${your-password-reset-user-flow}` именем потока пользователя, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="a7515-170">Copy the `greeting.html` and `home.html` from [Azure AD B2C Spring Boot Sample](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates), and replace the `${your-profile-edit-user-flow}` and `${your-password-reset-user-flow}` with your user flow name respectively that completed earlier.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="a7515-171">Создание и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="a7515-171">Build and test your app</span></span>

1. <span data-ttu-id="a7515-172">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="a7515-172">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

2. <span data-ttu-id="a7515-173">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a7515-173">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

3. <span data-ttu-id="a7515-174">Скомпилировав и запустив приложение с помощью Maven, перейдите в веб-браузере по адресу <http://localhost:8080/>, после чего вы будете перенаправлены на страницу входа.</span><span class="sxs-lookup"><span data-stu-id="a7515-174">After your application is built and started by Maven, open <http://localhost:8080/> in a web browser; you should be redirected to login page.</span></span>

   ![Страница входа](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO1.png)

4. <span data-ttu-id="a7515-176">Щелкните ссылку с именем потока пользователя `${your-sign-up-or-in}`, после чего вы будете перенаправлены в Azure AD B2C, чтобы начать процесс проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="a7515-176">Click linke with name of `${your-sign-up-or-in}` user flow, you should be rediected Azure AD B2C to start the authentication process.</span></span>

   ![Вход в Azure Active Directory B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO2.png)

4. <span data-ttu-id="a7515-178">Войдя в приложение, вы увидите пример `home page` в браузере.</span><span class="sxs-lookup"><span data-stu-id="a7515-178">After you have logged in successfully, you should see the sample `home page` from the browser,</span></span>

   ![Успешный вход в приложение](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO3.png)

## <a name="summary"></a><span data-ttu-id="a7515-180">Сводка</span><span class="sxs-lookup"><span data-stu-id="a7515-180">Summary</span></span>

<span data-ttu-id="a7515-181">В этом учебнике вы создали веб-приложение Java с использованием начального приложения Spring Boot для Azure Active Directory B2C, настроили клиент Azure AD B2C, зарегистрировали в нем созданное приложение, а затем настроили это приложение для использования аннотаций и классов Spring с целью защиты веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="a7515-181">In this tutorial, you created a new Java web application using the Azure Active Directory B2C starter, configured a new Azure AD B2C tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7515-182">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="a7515-182">Next steps</span></span>

<span data-ttu-id="a7515-183">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="a7515-183">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a7515-184">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="a7515-184">Spring on Azure</span></span>](/java/azure/spring-framework)
