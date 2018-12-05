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
ms.date: 11/21/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 89e294fa739b59f87667f901e914fd5f050b5b8c
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338778"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="76082-103">Руководство. Защита приложения Java с использованием начального приложения Spring Boot для Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76082-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="76082-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="76082-104">Overview</span></span>

<span data-ttu-id="76082-105">В этой статье описывается, как с помощью **[Spring Initializr]** создать начальное приложение Java Spring Boot для Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="76082-105">This article demonstrates creating a Java app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="76082-106">Из этого руководства вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="76082-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="76082-107">создание приложения Java с помощью Spring Initializr;</span><span class="sxs-lookup"><span data-stu-id="76082-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="76082-108">настройка Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="76082-108">Configure Azure Active Directory</span></span>
> * <span data-ttu-id="76082-109">защита приложения с помощью классов и аннотаций Spring Boot;</span><span class="sxs-lookup"><span data-stu-id="76082-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="76082-110">сборка и тестирование приложения Java.</span><span class="sxs-lookup"><span data-stu-id="76082-110">Build and test your Java application</span></span>

<span data-ttu-id="76082-111">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="76082-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76082-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="76082-112">Prerequisites</span></span>

<span data-ttu-id="76082-113">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="76082-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="76082-114">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="76082-114">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="76082-115">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="76082-115">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="76082-116">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="76082-116">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="76082-117">Создание приложения с помощью Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="76082-117">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="76082-118">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="76082-118">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="76082-119">Укажите, что необходимо создать проект **Maven** с помощью **Java**, введите имя **группы** и **артефакта** вашего приложения, а затем щелкните ссылку, чтобы **перейти к полной версии** Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="76082-119">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Указание имен группы и артефакта][create-spring-app-01]

1. <span data-ttu-id="76082-121">Прокрутите страницу вниз до раздела **Core** (Основные параметры) и установите флажок **Security** (Безопасность). В разделе **Web** (Веб-приложение) установите флажок **Web** (Веб-приложение). Затем прокрутите страницу вниз до раздела **Azure** и установите флажок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="76082-121">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**, then scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Выбор начальных компонентов Security, Web и Azure Active Directory][create-spring-app-02]

1. <span data-ttu-id="76082-123">Прокрутите страницу вверх или вниз до конца и нажмите кнопку **Generate Project** (Создать проект).</span><span class="sxs-lookup"><span data-stu-id="76082-123">Scroll to the top or bottom of the page and click the button to **Generate Project**.</span></span>

   ![Создание проекта Spring Boot][create-spring-app-03]

1. <span data-ttu-id="76082-125">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="76082-125">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-azure-active-directory-instance"></a><span data-ttu-id="76082-126">Создание экземпляра Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76082-126">Create Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="76082-127">Создание экземпляра Active Directory</span><span class="sxs-lookup"><span data-stu-id="76082-127">Create the Active Directory instance</span></span>

1. <span data-ttu-id="76082-128">Войдите на сайт <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="76082-128">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="76082-129">Щелкните **Создать ресурс**, а затем выберите **Удостоверение** и **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="76082-129">Click **+Create a resource**, then **Identity**, and then **Azure Active Directory**.</span></span>

   ![Создание экземпляра Azure Active Directory][create-directory-01]

1. <span data-ttu-id="76082-131">Укажите **имя организации** и **первоначальное доменное имя**.</span><span class="sxs-lookup"><span data-stu-id="76082-131">Enter your **Organization name** and your **Initial domain name**.</span></span> <span data-ttu-id="76082-132">Скопируйте полный URL-адрес вашего каталога. Он вам понадобится, чтобы добавить учетные записи пользователей, как описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="76082-132">Copy the full URL of your directory; you will use that to add user accounts later in this tutorial.</span></span> <span data-ttu-id="76082-133">(Например, `wingtiptoysdirectory.onmicrosoft.com`.) По завершении нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="76082-133">(For example: `wingtiptoysdirectory.onmicrosoft.com`.) When you have finished, click **Create**.</span></span>

   ![Указание имен Azure Active Directory][create-directory-02]

1. <span data-ttu-id="76082-135">Выберите имя учетной записи в правом верхнем углу панели инструментов на портале Azure и щелкните **Переключение каталога**.</span><span class="sxs-lookup"><span data-stu-id="76082-135">Select your account name on the top-right of the Azure portal toolbar, then click **Switch directory**.</span></span>

   ![Выбор учетной записи Azure][create-directory-03]

1. <span data-ttu-id="76082-137">Выберите новый экземпляр Azure Active Directory в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="76082-137">Select your new Azure Active Directory from the drop-down menu.</span></span>

   ![Выбор экземпляра Azure Active Directory][create-directory-04]

1. <span data-ttu-id="76082-139">В меню портала выберите **Azure Active Directory**, щелкните **Свойства** и скопируйте значение параметра **Идентификатор каталога**. Оно вам понадобится при настройке файла *application.properties*, как описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="76082-139">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID**; you will use that value to configure your *application.properties* file later in this tutorial.</span></span>

   ![Копирование идентификатора каталога Azure Active Directory][create-directory-05]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="76082-141">Регистрация приложения для приложения Spring Boot</span><span class="sxs-lookup"><span data-stu-id="76082-141">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="76082-142">В меню портала выберите **Azure Active Directory**, затем выберите **Регистрация приложений**, после чего щелкните **Регистрация нового приложения**.</span><span class="sxs-lookup"><span data-stu-id="76082-142">Select **Azure Active Directory** from the portal menu, click **App registrations**, and then click **New application registration**, .</span></span>

   ![Регистрация приложения][create-app-registration-01]

2. <span data-ttu-id="76082-144">Укажите **имя** приложения, используйте http://localhost:8080 в качестве **URL-адреса для входа** и щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="76082-144">Specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Создание регистрации приложения][create-app-registration-02]

4. <span data-ttu-id="76082-146">Когда появится страница для регистрации приложения, скопируйте **идентификатор приложения**. Он вам понадобится при настройке файла *application.properties*, как описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="76082-146">When the page for your app registration appears, copy your **Application ID**; you will use this value to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="76082-147">Щелкните **Параметры**, а затем выберите **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="76082-147">Click **Settings**, and then click **Keys**.</span></span>

   ![Создание ключей зарегистрированного приложения][create-app-registration-03]

5. <span data-ttu-id="76082-149">Добавьте **описание** и укажите **длительность** использования нового ключа, а затем щелкните **Сохранить**. Значение ключа будет указано автоматически, когда вы щелкнете значок **Сохранить**. Скопируйте это значение, чтобы использовать его при настройке файла *application.properties*, как описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="76082-149">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="76082-150">(Вы не сможете получить это значение позже.)</span><span class="sxs-lookup"><span data-stu-id="76082-150">(You will not be able to retrieve this value later.)</span></span>

   ![Указание параметров зарегистрированного приложения][create-app-registration-04]

6. <span data-ttu-id="76082-152">На главной странице зарегистрированного приложения последовательно щелкните **Параметры** и **Требуемые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="76082-152">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Добавление требуемых разрешений для приложения][create-app-registration-05]

7. <span data-ttu-id="76082-154">Щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="76082-154">Click **Windows Azure Active Directory**.</span></span>

   ![Выбор Azure Active Directory][create-app-registration-06]

8. <span data-ttu-id="76082-156">Установите флажки рядом с пунктами **Доступ к каталогу как пользователь, выполнивший вход** и **Вход в систему и чтение профиля пользователя**, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="76082-156">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Включение разрешений на доступ][create-app-registration-07]

9. <span data-ttu-id="76082-158">На странице **Требуемые разрешения** щелкните **Предоставить разрешения** и **Да**.</span><span class="sxs-lookup"><span data-stu-id="76082-158">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Предоставление разрешений на доступ][create-app-registration-08]

10. <span data-ttu-id="76082-160">На главной странице зарегистрированного приложения последовательно щелкните **Параметры** и **URL-адреса ответа**.</span><span class="sxs-lookup"><span data-stu-id="76082-160">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

    ![Изменение URL-адресов ответа][create-app-registration-09]

11. <span data-ttu-id="76082-162">Введите <http://localhost:8080/login/oauth2/code/azure> в качестве нового URL-адреса ответа, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="76082-162">Enter "<http://localhost:8080/login/oauth2/code/azure>" as a new reply URL, and then click **Save**.</span></span>

    ![Добавление нового URL-адреса ответа][create-app-registration-10]

12. <span data-ttu-id="76082-164">На главной странице регистрации приложения щелкните **Манифест**, затем установите для параметра `oauth2AllowImplicitFlow` значение `true` и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="76082-164">From the main page for your app registration, click **Manifest**, then set the value of the `oauth2AllowImplicitFlow` parameter to `true`, and then click **Save**.</span></span>

    ![Настройка манифеста приложения][create-app-registration-11]

    > [!NOTE]
    > 
    > <span data-ttu-id="76082-166">Дополнительные сведения о параметре `oauth2AllowImplicitFlow` и других параметрах приложения см. в статье [Манифест приложения Azure Active Directory][AAD app manifest].</span><span class="sxs-lookup"><span data-stu-id="76082-166">For more information about the `oauth2AllowImplicitFlow` parameter and other application settings, see [Azure Active Directory application manifest][AAD app manifest].</span></span> 
    >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a><span data-ttu-id="76082-167">Добавление учетной записи пользователя в каталог и в группу</span><span class="sxs-lookup"><span data-stu-id="76082-167">Add a user account to your directory, and add that account to a group</span></span>

1. <span data-ttu-id="76082-168">На странице **Обзор** своего экземпляра службы Active Directory щелкните **Все пользователи**, а затем — **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="76082-168">From the **Overview** page of your Active Directory, click **All Users**, and then click **New user**.</span></span>

   ![Добавление новой учетной записи пользователя][create-user-01]

1. <span data-ttu-id="76082-170">Когда появится панель **Пользователь**, введите значения в поля **Имя** и **Имя пользователя**.</span><span class="sxs-lookup"><span data-stu-id="76082-170">When the **User** panel is displayed, enter the **Name** and **User name**.</span></span>

   ![Ввод сведений об учетной записи пользователя][create-user-02]

   > [!NOTE]
   > 
   > <span data-ttu-id="76082-172">При вводе имени пользователя укажите URL-адрес каталога, ранее скопированный в рамках этого руководства. Например:</span><span class="sxs-lookup"><span data-stu-id="76082-172">You need to specify your directory URL from earlier in this tutorial when you enter the user name; for example:</span></span>
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. <span data-ttu-id="76082-173">Щелкните **Группы**, затем выберите группы, которые будут использоваться для авторизации в приложении, и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="76082-173">Click **Groups**, then select the groups that you will use for authorization in your application, and then click **Select**.</span></span> <span data-ttu-id="76082-174">(В рамках этого руководства добавьте учетную запись в группу _Пользователи_.)</span><span class="sxs-lookup"><span data-stu-id="76082-174">(For the purposes of this tutorial, add the account to the _Users_ group.)</span></span>

   ![Выбор групп пользователей][create-user-03]

1. <span data-ttu-id="76082-176">Установите флажок **Показать пароль** и скопируйте пароль. Он вам понадобится при входе в приложение, как описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="76082-176">Click **Show password**, and copy the password; you will use this when you log into your application later in this tutorial.</span></span> <span data-ttu-id="76082-177">После того как вы скопировали пароль, щелкните **Создать**, чтобы добавить новую учетную запись пользователя в свой каталог.</span><span class="sxs-lookup"><span data-stu-id="76082-177">When you have copied the password, click **Create** to add the new user account to your directory.</span></span>

   ![Отображение пароля][create-user-04]

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="76082-179">Настройка и компиляция приложения</span><span class="sxs-lookup"><span data-stu-id="76082-179">Configure and compile your app</span></span>

1. <span data-ttu-id="76082-180">Распакуйте архив с файлами проекта, который вы создали и скачали в каталог ранее в рамках этого руководства.</span><span class="sxs-lookup"><span data-stu-id="76082-180">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

1. <span data-ttu-id="76082-181">Перейдите в родительскую папку проекта и откройте файл проекта Maven `pom.xml` в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="76082-181">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

1. <span data-ttu-id="76082-182">Добавьте зависимости для защиты с помощью Spring OAuth2 в `pom.xml`:</span><span class="sxs-lookup"><span data-stu-id="76082-182">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

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

1. <span data-ttu-id="76082-183">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="76082-183">Save and close the *pom.xml* file.</span></span>

1. <span data-ttu-id="76082-184">В папке *src/main/resources* проекта откройте файл *application.properties* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="76082-184">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="76082-185">Задайте параметры для регистрации вашего приложения, используя созданные ранее значения. Например:</span><span class="sxs-lookup"><span data-stu-id="76082-185">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

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
   <span data-ttu-id="76082-186">Описание</span><span class="sxs-lookup"><span data-stu-id="76082-186">Where:</span></span>

   | <span data-ttu-id="76082-187">Параметр</span><span class="sxs-lookup"><span data-stu-id="76082-187">Parameter</span></span> | <span data-ttu-id="76082-188">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="76082-188">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="76082-189">Содержит **идентификатор каталога** Active Directory, который вы скопировали ранее.</span><span class="sxs-lookup"><span data-stu-id="76082-189">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="76082-190">Содержит **идентификатор приложения**, полученный после регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="76082-190">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="76082-191">Содержит **значение** ключа, полученное после регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="76082-191">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="76082-192">Содержит список групп Active Directory, используемых для авторизации.</span><span class="sxs-lookup"><span data-stu-id="76082-192">Contains a list of Active Directory groups to use for authorization.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="76082-193">Полный список значений, доступных в файле *application.properties*, см. на [сайте GitHub][AAD Spring Boot Sample].</span><span class="sxs-lookup"><span data-stu-id="76082-193">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

1. <span data-ttu-id="76082-194">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="76082-194">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="76082-195">Создайте папку с именем *controller* в папке с исходным кодом Java для приложения, например: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="76082-195">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="76082-196">Создайте файл Java с именем *HelloController.java* в папке *controller* и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="76082-196">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="76082-197">Вставьте следующий код, а затем сохраните и закройте файл:</span><span class="sxs-lookup"><span data-stu-id="76082-197">Enter the following code, then save and close the file:</span></span>

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
   > <span data-ttu-id="76082-198">Имя группы, указываемое для метода `@PreAuthorize("hasRole('')")`, должно содержать одну из групп, указанных в поле `azure.activedirectory.active-directory-groups` в файле *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="76082-198">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   > 
   > <span data-ttu-id="76082-199">Для разных сопоставлений запросов можно указывать разные параметры авторизации, например:</span><span class="sxs-lookup"><span data-stu-id="76082-199">You can also specify different authorization settings for different request mappings; for example:</span></span>
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

1. <span data-ttu-id="76082-200">Создайте папку с именем *security* в папке с исходным кодом Java для приложения, например: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="76082-200">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="76082-201">Создайте файл Java с именем *WebSecurityConfig.java* в папке *security* и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="76082-201">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="76082-202">Вставьте следующий код, а затем сохраните и закройте файл:</span><span class="sxs-lookup"><span data-stu-id="76082-202">Enter the following code, then save and close the file:</span></span>

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

## <a name="build-and-test-your-app"></a><span data-ttu-id="76082-203">Создание и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="76082-203">Build and test your app</span></span>

1. <span data-ttu-id="76082-204">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="76082-204">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="76082-205">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="76082-205">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Сборка приложения][build-application]

1. <span data-ttu-id="76082-207">Скомпилировав и запустив приложение с помощью Maven, перейдите в веб-браузере по адресу <http://localhost:8080> и введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="76082-207">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Вход в приложение][application-login]

   > [!NOTE]
   > 
   > <span data-ttu-id="76082-209">Если это первый вход с новой учетной записью пользователя, возможно, вам будет предложено изменить пароль.</span><span class="sxs-lookup"><span data-stu-id="76082-209">You may be prompted to change your password if this is the first login for a new user account.</span></span>
   > 
   > ![Изменение пароля][update-password]
   > 

1. <span data-ttu-id="76082-211">Войдя в приложение, вы увидите сообщение контроллера "Hello World".</span><span class="sxs-lookup"><span data-stu-id="76082-211">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Успешный вход в приложение][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="76082-213">Пользователи с неавторизованными учетными записями получат сообщение **HTTP 403 — не авторизовано**.</span><span class="sxs-lookup"><span data-stu-id="76082-213">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="summary"></a><span data-ttu-id="76082-214">Сводка</span><span class="sxs-lookup"><span data-stu-id="76082-214">Summary</span></span>

<span data-ttu-id="76082-215">В этом руководстве вы создали веб-приложение Java с использованием начального приложения Spring Boot для Azure Active Directory, настроили нового клиента Azure AD, зарегистрировали в нем созданное приложение, а затем настроили это приложение для использования аннотаций и классов Spring с целью защиты веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="76082-215">In this tutorial, you created a new Java web application using the Azure Active Directory starter, configured a new Azure AD tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76082-216">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="76082-216">Next steps</span></span>

<span data-ttu-id="76082-217">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="76082-217">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="76082-218">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="76082-218">Spring on Azure</span></span>](/java/azure/spring-framework)

<!-- URL List -->

[Azure Active Directory Documentation]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure for Java Developers]: /java/azure/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

<!-- IMG List -->

[create-spring-app-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-01.png
[create-spring-app-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-02.png
[create-spring-app-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-03.png

[create-directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-01.png
[create-directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-02.png
[create-directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-03.png
[create-directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-04.png
[create-directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-05.png

[create-app-registration-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-01.png
[create-app-registration-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-02.png
[create-app-registration-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-03.png
[create-app-registration-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-04.png
[create-app-registration-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-05.png
[create-app-registration-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-06.png
[create-app-registration-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-07.png
[create-app-registration-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-08.png
[create-app-registration-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-09.png
[create-app-registration-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-10.png
[create-app-registration-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-11.png

[create-user-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-01.png
[create-user-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-02.png
[create-user-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-03.png
[create-user-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-04.png

[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
[update-password]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/update-password.png
