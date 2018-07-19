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
ms.date: 07/02/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 6d20593620c7fb73f8481be8705bdc42d4e9ce32
ms.sourcegitcommit: 0ed7c5af0152125322ff1d265c179f35028f3c15
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37864054"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a>Как использовать приложение Spring Boot Starter с Azure Active Directory

## <a name="overview"></a>Обзор

В этой статье описано, как создать с помощью **[Spring Initializr]** начальное приложение Spring Boot для Azure Active Directory.

## <a name="prerequisites"></a>предварительным требованиям

Чтобы выполнить действия, описанные в этой статье, необходимо следующее:

* Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
* [Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.
* [Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Создание пользовательского приложения с помощью Spring Initializr

1. Перейдите по адресу <https://start.spring.io/>.

1. Укажите, что необходимо создать проект **Maven** с помощью **Java**, введите имя **группы** и **артефакта** вашего приложения, а затем щелкните ссылку, чтобы **перейти к полной версии** Spring Initializr.

   ![Указание имен группы и артефакта][security-01]

1. Прокрутите вниз до раздела **Core** (Основные) и установите флажок рядом с пунктом **Security**, а в разделе **Web** (Веб) — рядом с пунктом **Web**.

   ![Выбор начальных приложений Security и Web][security-02]

1. Прокрутите вниз до раздела **Azure** статьи и установите флажок рядом с пунктом **Azure Active Directory**.

   ![Выбор начального приложения Azure Active Directory][security-03]

1. Прокрутите страницу вниз и нажмите соответствующую кнопку, чтобы **создать проект**.

   ![Создание проекта Spring Boot][security-04]

1. При появлении запроса скачайте проект на локальный компьютер.

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a>Создание и настройка экземпляра Azure Active Directory

### <a name="create-the-active-directory-instance"></a>Создание экземпляра Active Directory

1. Войдите на сайт <https://portal.azure.com>.

1. Щелкните **+Создать**, **Безопасность и идентификация**, **Azure Active Directory**.

   ![Создание экземпляра Azure Active Directory][directory-01]

1. Укажите **имя организации** и **первоначальное доменное имя**. Скопируйте полный URL-адрес вашего каталога. Он вам понадобится, чтобы добавить учетные записи пользователей, как описывается далее в этом руководстве. (Например, `wingtiptoysdirectory.onmicrosoft.com`.) По завершении нажмите кнопку **Создать**.

   ![Указание имен Azure Active Directory][directory-02]

1. Выберите новый экземпляр Azure Active Directory в раскрывающемся меню на панели сверху на портале Azure.

   ![Выбор экземпляра Azure Active Directory][directory-03]

1. В меню портала выберите **Azure Active Directory**, щелкните **Свойства** и скопируйте значение параметра **Идентификатор каталога**. Оно вам понадобится при настройке файла *application.properties*, как описывается далее в этом руководстве.

   ![Копирование идентификатора каталога Azure Active Directory][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Регистрация приложения для приложения Spring Boot

1. На портале в меню выберите **Azure Active Directory**, щелкните **Обзор** и выберите **Регистрация приложений**.

   ![Регистрация приложения][directory-04]

1. Щелкните **Регистрация нового приложения**, введите **имя** приложения, укажите http://localhost:8080 в качестве **URL-адреса входа**, а затем щелкните **Создать**.

   ![Создание регистрации приложения][directory-05]

1. Щелкните зарегистрированное приложение.

   ![Выбор зарегистрированного приложения][directory-06]

1. Когда появится страница для регистрации приложения, скопируйте **идентификатор приложения**. Он вам понадобится при настройке файла *application.properties*, как описывается далее в этом руководстве. Щелкните **Параметры**, а затем выберите **Ключи**.

   ![Создание ключей зарегистрированного приложения][directory-07]

1. Добавьте **описание** и укажите **длительность** использования нового ключа, а затем щелкните **Сохранить**. Значение ключа будет указано автоматически, когда вы щелкнете значок **Сохранить**. Скопируйте это значение, чтобы использовать его при настройке файла *application.properties*, как описывается далее в этом руководстве. (Вы не сможете получить это значение позже.)

   ![Указание параметров зарегистрированного приложения][directory-08]

1. На главной странице зарегистрированного приложения последовательно щелкните **Параметры** и **Требуемые разрешения**.

   ![Добавление требуемых разрешений для приложения][directory-09]

1. Щелкните **Azure Active Directory**.

   ![Выбор Azure Active Directory][directory-10]

1. Установите флажки рядом с пунктами **Доступ к каталогу как пользователь, выполнивший вход** и **Вход в систему и чтение профиля пользователя**, а затем щелкните **Сохранить**.

   ![Включение разрешений на доступ][directory-11]

1. На странице **Требуемые разрешения** щелкните **Предоставить разрешения** и **Да**.

   ![Предоставление разрешений на доступ][directory-12]

1. На главной странице зарегистрированного приложения последовательно щелкните **Параметры** и **URL-адреса ответа**.

   ![Изменение URL-адресов ответа][directory-14]

1. Введите http://localhost:8080/login/oauth2/code/azure в качестве нового URL-адреса ответа, а затем нажмите кнопку **Сохранить**.

   ![Добавление нового URL-адреса ответа][directory-15]

1. На главной странице регистрации приложения щелкните **Манифест**, затем установите для параметра `oauth2AllowImplicitFlow` значение `true` и нажмите кнопку **Сохранить**.

   ![Настройка манифеста приложения][directory-16]

   > [!NOTE]
   > 
   > Дополнительные сведения о параметре `oauth2AllowImplicitFlow` и других параметрах приложения см. в статье [Манифест приложения Azure Active Directory][AAD app manifest]. 
   >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a>Добавление учетной записи пользователя в каталог и в группу

1. На странице **Обзор** в Active Directory щелкните **Пользователи**.

   ![Открытие панели "Пользователи"][directory-17]

1. Когда появится панель **Пользователи**, щелкните **Новый пользователь**.

   ![Добавление новой учетной записи пользователя][directory-18]

1. Когда появится панель **Пользователь**, введите значения в поля **Имя** и **Имя пользователя**.

   ![Ввод сведений об учетной записи пользователя][directory-19]

   > [!NOTE]
   > 
   > При вводе имени пользователя укажите URL-адрес каталога, ранее скопированный в рамках этого руководства. Например:
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. Щелкните **Группы**, затем выберите группы, которые будут использоваться для авторизации в приложении, и нажмите кнопку **Выбрать**. (В рамках этого руководства добавьте учетную запись в группу _Пользователи_.)

   ![Выбор групп пользователей][directory-20]

1. Установите флажок **Показать пароль** и скопируйте пароль. Он вам понадобится при входе в приложение, как описывается далее в этом руководстве.

   ![Отображение пароля][directory-21]

1. Нажмите кнопку **Создать**, чтобы добавить в каталог новую учетную запись пользователя.

   ![Создание учетной записи пользователя][directory-22]

## <a name="configure-and-compile-your-spring-boot-application"></a>Настройка и компиляция приложения Spring Boot

1. Распакуйте архив с файлами проекта, который вы создали и скачали в каталог ранее в рамках этого руководства.

1. Перейдите в родительскую папку проекта и откройте файл *pom.xml* в текстовом редакторе.

1. Добавьте зависимости для защиты Spring OAuth2, например:

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

1. Сохраните и закройте файл *pom.xml*.

1. В папке *src/main/resources* проекта откройте файл *application.properties* в текстовом редакторе.

1. Задайте параметры для регистрации вашего приложения, используя созданные ранее значения. Например:

   ```yaml
   # Specifies your Active Directory ID:
   azure.activedirectory.tenant-id=22222222-2222-2222-2222-222222222222

   # Specifies your App Registration's Application ID:
   spring.security.oauth2.client.registration.azure.client-id=11111111-1111-1111-1111-1111111111111111

   # Specifies your App Registration's secret key:
   spring.security.oauth2.client.registration.azure.client-secret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authorization:
   azure.activedirectory.active-directory-groups=Users
   ```
   Описание

   | Параметр | ОПИСАНИЕ |
   |---|---|
   | `azure.activedirectory.tenant-id` | Содержит **идентификатор каталога** Active Directory, который вы скопировали ранее. |
   | `spring.security.oauth2.client.registration.azure.client-id` | Содержит **идентификатор приложения**, полученный после регистрации приложения. |
   | `spring.security.oauth2.client.registration.azure.client-secret` | Содержит **значение** ключа, полученное после регистрации приложения. |
   | `azure.activedirectory.active-directory-groups` | Содержит список групп Active Directory, используемых для авторизации. |

   > [!NOTE]
   > 
   > Полный список значений, доступных в файле *application.properties*, см. на [сайте GitHub][AAD Spring Boot Sample].
   >

1. Сохраните и закройте файл *application.properties*.

1. Создайте папку с именем *controller* в папке с исходным кодом Java для приложения, например: *src/main/java/com/wingtiptoys/security/controller*.

1. Создайте файл Java с именем *HelloController.java* в папке *controller* и откройте его в текстовом редакторе.

1. Вставьте следующий код, а затем сохраните и закройте файл:

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
   > Имя группы, указываемое для метода `@PreAuthorize("hasRole('')")`, должно содержать одну из групп, указанных в поле `azure.activedirectory.active-directory-groups` в файле *application.properties*.
   >

   > [!NOTE]
   > 
   > Для разных сопоставлений запросов можно указывать разные параметры авторизации, например:
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

1. Создайте папку с именем *security* в папке с исходным кодом Java для приложения, например: *src/main/java/com/wingtiptoys/security/security*.

1. Создайте файл Java с именем *WebSecurityConfig.java* в папке *security* и откройте его в текстовом редакторе.

1. Вставьте следующий код, а затем сохраните и закройте файл:

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

## <a name="build-and-test-your-app"></a>Создание и тестирование приложения

1. Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*.

1. Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Сборка приложения][build-application]

1. Скомпилировав и запустив приложение с помощью Maven, перейдите в веб-браузере по адресу <http://localhost:8080> и введите имя пользователя и пароль.

   ![Вход в приложение][application-login]

   > [!NOTE]
   > 
   > Если это первый вход с новой учетной записью пользователя, возможно, вам будет предложено изменить пароль.
   > 
   > ![Изменение пароля][update-password]
   > 

1. Войдя в приложение, вы увидите сообщение контроллера "Hello World".

   ![Успешный вход в приложение][hello-world]

   > [!NOTE]
   > 
   > Пользователи с неавторизованными учетными записями получат сообщение **HTTP 403 — не авторизовано**.
   >

## <a name="next-steps"></a>Дополнительная информация

См. дополнительные сведения об использовании Azure Active Directory:

* [Документация по Azure Active Directory].

Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:

* [Развертывание приложения Spring Boot Application в службе приложений Azure](deploy-spring-boot-java-web-app-on-azure.md)

* [Запуск приложения Spring Boot в кластере Kubernetes в Службе контейнеров Azure](deploy-spring-boot-java-app-on-kubernetes.md)

Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [Java Tools for Visual Studio Team Services].

**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса. Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java. В помощь разработчикам, начинающим работать со Spring Boot, по адресу <https://github.com/spring-guides/> доступно несколько примеров пакетов этого приложения. Помимо выбора из списка основных проектов Spring Boot, **[Spring Initializr]** помогает разработчикам создавать пользовательские приложения Spring Boot.

Более подробный пример см. [на сайте GitHub][AAD Spring Boot Sample].

<!-- URL List -->

[Документация по Azure Active Directory]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure для разработчиков Java]: /java/azure/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
[directory-16]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-16.png
[directory-17]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-17.png
[directory-18]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-18.png
[directory-19]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-19.png
[directory-20]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-20.png
[directory-21]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-21.png
[directory-22]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-22.png

[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
[update-password]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/update-password.png
