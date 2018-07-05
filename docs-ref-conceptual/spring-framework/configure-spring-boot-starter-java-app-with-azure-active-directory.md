---
title: Как использовать приложение Spring Boot Starter с Azure Active Directory
description: Сведения о настройке приложения Spring Initializr с помощью начального приложения Azure Active Directory.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 06/20/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: adcbc78cc129daf589bf070741308e4024432e5d
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090837"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="d5c53-103">Как использовать приложение Spring Boot Starter с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5c53-103">How to use the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="d5c53-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="d5c53-104">Overview</span></span>

<span data-ttu-id="d5c53-105">В этой статье описано, как создать с помощью **[Spring Initializr]** начальное приложение Spring Boot для Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d5c53-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5c53-106">предварительным требованиям</span><span class="sxs-lookup"><span data-stu-id="d5c53-106">Prerequisites</span></span>

<span data-ttu-id="d5c53-107">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="d5c53-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="d5c53-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="d5c53-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="d5c53-109">[Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="d5c53-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="d5c53-110">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="d5c53-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="d5c53-111">Создание пользовательского приложения с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="d5c53-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="d5c53-112">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="d5c53-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="d5c53-113">Укажите, что необходимо создать проект **Maven** с помощью **Java**, введите имя **группы** и **артефакта** вашего приложения, а затем щелкните ссылку, чтобы **перейти к полной версии** Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="d5c53-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Указание имен группы и артефакта][security-01]

1. <span data-ttu-id="d5c53-115">Прокрутите вниз до раздела **Core** (Основные) и установите флажок рядом с пунктом **Security**, а в разделе **Web** (Веб) — рядом с пунктом **Web**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-115">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Выбор начальных приложений Security и Web][security-02]

1. <span data-ttu-id="d5c53-117">Прокрутите вниз до раздела **Azure** статьи и установите флажок рядом с пунктом **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-117">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Выбор начального приложения Azure Active Directory][security-03]

1. <span data-ttu-id="d5c53-119">Прокрутите страницу вниз и нажмите соответствующую кнопку, чтобы **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Создание проекта Spring Boot][security-04]

1. <span data-ttu-id="d5c53-121">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="d5c53-121">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="d5c53-122">Создание и настройка экземпляра Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5c53-122">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="d5c53-123">Создание экземпляра Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5c53-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="d5c53-124">Войдите на сайт <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="d5c53-124">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="d5c53-125">Щелкните **+Создать**, **Безопасность и идентификация**, **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-125">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Создание экземпляра Azure Active Directory][directory-01]

1. <span data-ttu-id="d5c53-127">Укажите **имя организации** и **первоначальное доменное имя**, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-127">Enter your **Organization name** and your **Initial domain name**, and then click **Create**.</span></span>

   ![Указание имен Azure Active Directory][directory-02]

1. <span data-ttu-id="d5c53-129">Выберите новый экземпляр Azure Active Directory в раскрывающемся меню на панели сверху на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d5c53-129">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Выбор экземпляра Azure Active Directory][directory-03]

1. <span data-ttu-id="d5c53-131">В меню портала выберите **Azure Active Directory**, щелкните **Свойства** и скопируйте значение **Идентификатор каталога**. Оно вам понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="d5c53-131">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID** - you will use that later in this article.</span></span>

   ![Копирование идентификатора каталога Azure Active Directory][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="d5c53-133">Регистрация приложения для приложения Spring Boot</span><span class="sxs-lookup"><span data-stu-id="d5c53-133">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="d5c53-134">На портале в меню выберите **Azure Active Directory**, щелкните **Обзор** и выберите **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-134">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Регистрация приложения][directory-04]

1. <span data-ttu-id="d5c53-136">Щелкните **Регистрация нового приложения**, введите **имя** приложения, укажите http://localhost:8080 в качестве **URL-адреса входа**, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-136">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Создание регистрации приложения][directory-05]

1. <span data-ttu-id="d5c53-138">Щелкните зарегистрированное приложение.</span><span class="sxs-lookup"><span data-stu-id="d5c53-138">Click your application registration after it has been created.</span></span>

   ![Выбор зарегистрированного приложения][directory-06]

1. <span data-ttu-id="d5c53-140">Когда откроется страница зарегистрированного приложения, скопируйте значение **Идентификатор приложения** (оно вам понадобится позже), после чего последовательно щелкните **Настройки** и **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-140">When the page for your app registration, copy your **Application ID** for later use, then click **Settings**, and then click **Keys**.</span></span>

   ![Создание ключей зарегистрированного приложения][directory-07]

1. <span data-ttu-id="d5c53-142">Добавьте **описание** и укажите **длительность** использования нового ключа, а затем щелкните **Сохранить**. Значение ключа будет указано автоматически, когда вы щелкнете значок **Сохранить**. Вам нужно скопировать это значение для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="d5c53-142">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key for later.</span></span> <span data-ttu-id="d5c53-143">(Вы не сможете получить это значение позже.)</span><span class="sxs-lookup"><span data-stu-id="d5c53-143">(You will not be able to retrieve this value later.)</span></span>

   ![Указание параметров зарегистрированного приложения][directory-08]

1. <span data-ttu-id="d5c53-145">На главной странице зарегистрированного приложения последовательно щелкните **Параметры** и **Требуемые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-145">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Добавление требуемых разрешений для приложения][directory-09]

1. <span data-ttu-id="d5c53-147">Щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-147">Click **Windows Azure Active Directory**.</span></span>

   ![Выбор Azure Active Directory][directory-10]

1. <span data-ttu-id="d5c53-149">Установите флажки рядом с пунктами **Доступ к каталогу как пользователь, выполнивший вход** и **Вход в систему и чтение профиля пользователя**, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-149">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Включение разрешений на доступ][directory-11]

1. <span data-ttu-id="d5c53-151">На странице **Требуемые разрешения** щелкните **Предоставить разрешения** и **Да**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-151">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Предоставление разрешений на доступ][directory-12]

1. <span data-ttu-id="d5c53-153">На главной странице зарегистрированного приложения последовательно щелкните **Параметры** и **URL-адреса ответа**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-153">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

   ![Изменение URL-адресов ответа][directory-14]

1. <span data-ttu-id="d5c53-155">Введите http://localhost:8080/login/oauth2/code/azure в качестве нового URL-адреса ответа, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-155">Enter "http://localhost:8080/login/oauth2/code/azure" as a new reply URL, and then click **Save**.</span></span>

   ![Добавление нового URL-адреса ответа][directory-15]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="d5c53-157">Настройка и компиляция приложения Spring Boot</span><span class="sxs-lookup"><span data-stu-id="d5c53-157">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="d5c53-158">Распакуйте скачанный архив с файлами проекта в каталог.</span><span class="sxs-lookup"><span data-stu-id="d5c53-158">Extract the files from the downloaded project archive into a directory.</span></span>

2. <span data-ttu-id="d5c53-159">Перейдите в родительскую папку проекта и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="d5c53-159">Navigate to the parent folder in your project and open the *pom.xml* file in a text editor.</span></span>

3. <span data-ttu-id="d5c53-160">Добавьте зависимости для защиты Spring OAuth2, например:</span><span class="sxs-lookup"><span data-stu-id="d5c53-160">Add the dependencies for Spring OAuth2 security; for example:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-client</artifactId>
   </dependency>
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-jose</artifactId>
   </dependency>
   ```

4. <span data-ttu-id="d5c53-161">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="d5c53-161">Save and close the *pom.xml* file.</span></span>

5. <span data-ttu-id="d5c53-162">В папке *src/main/resources* проекта откройте файл *application.properties* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="d5c53-162">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

6. <span data-ttu-id="d5c53-163">Добавьте ключ для учетной записи, используя полученные ранее значения, например:</span><span class="sxs-lookup"><span data-stu-id="d5c53-163">Add the key for your storage account using the values from earlier; for example:</span></span>

   ```yaml
   # Specifies your Active Directory ID:
   azure.activedirectory.tenant-id=22222222-2222-2222-2222-222222222222

   # Specifies your App Registration's Application ID:
   spring.security.oauth2.client.registration.azure.client-id=11111111-1111-1111-1111-1111111111111111

   # Specifies your App Registration's secret key:
   spring.security.oauth2.client.registration.azure.client-secret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authentication:
   azure.activedirectory.active-directory-groups=Users
   ```
   <span data-ttu-id="d5c53-164">Описание</span><span class="sxs-lookup"><span data-stu-id="d5c53-164">Where:</span></span>

   | <span data-ttu-id="d5c53-165">Параметр</span><span class="sxs-lookup"><span data-stu-id="d5c53-165">Parameter</span></span> | <span data-ttu-id="d5c53-166">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="d5c53-166">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="d5c53-167">Содержит **идентификатор каталога** Active Directory, который вы скопировали ранее.</span><span class="sxs-lookup"><span data-stu-id="d5c53-167">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="d5c53-168">Содержит **идентификатор приложения**, полученный после регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="d5c53-168">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="d5c53-169">Содержит **значение** ключа, полученное после регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="d5c53-169">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="d5c53-170">Содержит список групп Active Directory, используемых для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="d5c53-170">Contains a list of Active Directory groups to use for authentication.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="d5c53-171">Полный список значений, доступных в файле *application.properties*, см. на [сайте GitHub][AAD Spring Boot Sample].</span><span class="sxs-lookup"><span data-stu-id="d5c53-171">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

7. <span data-ttu-id="d5c53-172">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="d5c53-172">Save and close the *application.properties* file.</span></span>

8. <span data-ttu-id="d5c53-173">Создайте папку с именем *controller* в папке с исходным кодом Java для приложения, например: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="d5c53-173">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

9. <span data-ttu-id="d5c53-174">Создайте файл Java с именем *HelloController.java* в папке *controller* и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="d5c53-174">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

10. <span data-ttu-id="d5c53-175">Вставьте следующий код, а затем сохраните и закройте файл:</span><span class="sxs-lookup"><span data-stu-id="d5c53-175">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.security.access.prepost.PreAuthorize;
   import org.springframework.security.oauth2.client.OAuth2AuthorizedClient;
   import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
   import org.springframework.ui.Model;

   @RestController
   public class HelloController {
      @Autowired
      @PreAuthorize("hasRole('Users')")
      @RequestMapping("/")
      public String helloWorld() {
         return "Hello World!";
      }
   }
   ```
   > [!NOTE]
   > 
   > <span data-ttu-id="d5c53-176">Имя группы, указываемое для метода `@PreAuthorize("hasRole('')")`, должно содержать одну из групп, указанных в поле `azure.activedirectory.active-directory-groups` в файле *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="d5c53-176">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   >

   > [!NOTE]
   > 
   > <span data-ttu-id="d5c53-177">Для разных сопоставлений запросов можно указывать разные параметры авторизации, например:</span><span class="sxs-lookup"><span data-stu-id="d5c53-177">You can specify different authorization settings for different request mappings; for example:</span></span>
   >
   > ``` java
   > public class HelloController {
   >    @Autowired
   >    @PreAuthorize("hasRole('Users')")
   >    @RequestMapping("/")
   >    public String helloWorld() {
   >       return "Hello Users!";
   >    }
   >    @PreAuthorize("hasRole('Group1')")
   >    @RequestMapping("/Group1")
   >    public String groupOne() {
   >       return "Hello Group 1 Users!";
   >    }
   >    @PreAuthorize("hasRole('Group2')")
   >    @RequestMapping("/Group2")
   >    public String groupTwo() {
   >       return "Hello Group 2 Users!";
   >    }
   > }
   > ```
   >    

11. <span data-ttu-id="d5c53-178">Создайте папку с именем *security* в папке с исходным кодом Java для приложения, например: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="d5c53-178">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

12. <span data-ttu-id="d5c53-179">Создайте файл Java с именем *WebSecurityConfig.java* в папке *security* и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="d5c53-179">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

13. <span data-ttu-id="d5c53-180">Вставьте следующий код, а затем сохраните и закройте файл:</span><span class="sxs-lookup"><span data-stu-id="d5c53-180">Enter the following code, then save and close the file:</span></span>

    ```java
    package com.wingtiptoys.security;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
    import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
    import org.springframework.security.oauth2.client.oidc.userinfo.OidcUserRequest;
    import org.springframework.security.oauth2.client.userinfo.OAuth2UserService;
    import org.springframework.security.oauth2.core.oidc.user.OidcUser;

    @EnableWebSecurity
    @EnableGlobalMethodSecurity(prePostEnabled = true)
    public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
        @Autowired
        private OAuth2UserService<OidcUserRequest, OidcUser> oidcUserService;

        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                .authorizeRequests()
                .anyRequest().authenticated()
                .and()
                .oauth2Login()
                .userInfoEndpoint()
                .oidcUserService(oidcUserService);
        }
    }
    ```

## <a name="build-and-test-your-app"></a><span data-ttu-id="d5c53-181">Создание и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="d5c53-181">Build and test your app</span></span>

1. <span data-ttu-id="d5c53-182">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="d5c53-182">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="d5c53-183">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d5c53-183">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Сборка приложения][build-application]

1. <span data-ttu-id="d5c53-185">Скомпилировав и запустив приложение с помощью Maven, перейдите в веб-браузере по адресу <http://localhost:8080> и введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="d5c53-185">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Вход в приложение][application-login]

1. <span data-ttu-id="d5c53-187">Войдя в приложение, вы увидите сообщение контроллера "Hello World".</span><span class="sxs-lookup"><span data-stu-id="d5c53-187">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Успешный вход в приложение][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="d5c53-189">Пользователи с неавторизованными учетными записями получат сообщение **HTTP 403 — не авторизовано**.</span><span class="sxs-lookup"><span data-stu-id="d5c53-189">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="d5c53-190">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="d5c53-190">Next steps</span></span>

<span data-ttu-id="d5c53-191">См. дополнительные сведения об использовании Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="d5c53-191">For more information about using Azure Active Directory, see the following articles:</span></span>

* <span data-ttu-id="d5c53-192">[Документация по Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="d5c53-192">[Azure Active Directory Documentation].</span></span>

<span data-ttu-id="d5c53-193">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="d5c53-193">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="d5c53-194">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="d5c53-194">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="d5c53-195">Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="d5c53-195">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="d5c53-196">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="d5c53-196">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="d5c53-197">**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="d5c53-197">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="d5c53-198">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="d5c53-198">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="d5c53-199">В помощь разработчикам, начинающим работать со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения.</span><span class="sxs-lookup"><span data-stu-id="d5c53-199">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="d5c53-200">Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="d5c53-200">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="d5c53-201">Более подробный пример см. [на сайте GitHub][AAD Spring Boot Sample].</span><span class="sxs-lookup"><span data-stu-id="d5c53-201">For a more-detailed sample, see the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>

<!-- URL List -->

[Документация по Azure Active Directory]: /azure/active-directory/
[Azure Active Directory Documentation]: /azure/active-directory/
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

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
[directory-13]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-13.png
[directory-14]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-14.png
[directory-15]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-15.png

[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
