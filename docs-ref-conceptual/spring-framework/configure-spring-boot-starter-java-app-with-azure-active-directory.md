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
ms.openlocfilehash: da44a40b7b52e75bb0a946b46ddfc033bfef54e9
ms.sourcegitcommit: 473c3aec55f3e9b131dc87c62e2eac218ce9564e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/13/2018
ms.locfileid: "51571721"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="faf09-103">Руководство. Защита приложения Java с использованием начального приложения Spring Boot для Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="faf09-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="faf09-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="faf09-104">Overview</span></span>

<span data-ttu-id="faf09-105">В этой статье описано, как создать с помощью **[Spring Initializr]** начальное приложение Spring Boot для Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="faf09-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="faf09-106">Из этого руководства вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="faf09-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="faf09-107">создание приложения Java с помощью Spring Initializr;</span><span class="sxs-lookup"><span data-stu-id="faf09-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="faf09-108">настройка Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="faf09-108">Configure Azure Active Directory</span></span>
> * <span data-ttu-id="faf09-109">защита приложения с помощью классов и аннотаций Spring Boot;</span><span class="sxs-lookup"><span data-stu-id="faf09-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="faf09-110">сборка и тестирование приложения Java.</span><span class="sxs-lookup"><span data-stu-id="faf09-110">Build and test your Java application</span></span>

<span data-ttu-id="faf09-111">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="faf09-111">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="faf09-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="faf09-112">Prerequisites</span></span>

<span data-ttu-id="faf09-113">Чтобы выполнить действия, описанные в этой статье, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="faf09-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="faf09-114">[Пакет разработчиков Java (JDK)](https://aka.ms/azure-jdks) версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="faf09-114">A [Java Development Kit (JDK)](https://aka.ms/azure-jdks), version 1.7 or later.</span></span>
* <span data-ttu-id="faf09-115">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="faf09-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-application-using-the-spring-initializr"></a><span data-ttu-id="faf09-116">Создание приложения с использованием Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="faf09-116">Create an application using the Spring Initializr</span></span>

1. <span data-ttu-id="faf09-117">Перейдите по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="faf09-117">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="faf09-118">Укажите, что необходимо создать проект **Maven** с помощью **Java**, введите имя **группы** и **артефакта** вашего приложения, а затем щелкните ссылку, чтобы **перейти к полной версии** Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="faf09-118">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Указание имен группы и артефакта][security-01]

1. <span data-ttu-id="faf09-120">Прокрутите вниз до раздела **Core** (Основные) и установите флажок рядом с пунктом **Security**, а в разделе **Web** (Веб) — рядом с пунктом **Web**.</span><span class="sxs-lookup"><span data-stu-id="faf09-120">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Выбор начальных приложений Security и Web][security-02]

1. <span data-ttu-id="faf09-122">Прокрутите вниз до раздела **Azure** статьи и установите флажок рядом с пунктом **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="faf09-122">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Выбор начального приложения Azure Active Directory][security-03]

1. <span data-ttu-id="faf09-124">Прокрутите страницу вниз и нажмите соответствующую кнопку, чтобы **создать проект**.</span><span class="sxs-lookup"><span data-stu-id="faf09-124">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Создание проекта Spring Boot][security-04]

1. <span data-ttu-id="faf09-126">При появлении запроса скачайте проект на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="faf09-126">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="faf09-127">Создание и настройка экземпляра Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="faf09-127">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="faf09-128">Создание экземпляра Active Directory</span><span class="sxs-lookup"><span data-stu-id="faf09-128">Create the Active Directory instance</span></span>

1. <span data-ttu-id="faf09-129">Войдите на сайт <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="faf09-129">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="faf09-130">Щелкните **+Создать**, **Безопасность и идентификация**, **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="faf09-130">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Создание экземпляра Azure Active Directory][directory-01]

1. <span data-ttu-id="faf09-132">Укажите **имя организации** и **первоначальное доменное имя**.</span><span class="sxs-lookup"><span data-stu-id="faf09-132">Enter your **Organization name** and your **Initial domain name**.</span></span> <span data-ttu-id="faf09-133">Скопируйте полный URL-адрес вашего каталога. Он вам понадобится, чтобы добавить учетные записи пользователей, как описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="faf09-133">Copy the full URL of your directory; you will use that to add user accounts later in this tutorial.</span></span> <span data-ttu-id="faf09-134">(Например, `wingtiptoysdirectory.onmicrosoft.com`.) По завершении нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="faf09-134">(For example: `wingtiptoysdirectory.onmicrosoft.com`.) When you have finished, click **Create**.</span></span>

   ![Указание имен Azure Active Directory][directory-02]

1. <span data-ttu-id="faf09-136">Выберите новый экземпляр Azure Active Directory в раскрывающемся меню на панели сверху на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="faf09-136">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Выбор экземпляра Azure Active Directory][directory-03]

1. <span data-ttu-id="faf09-138">В меню портала выберите **Azure Active Directory**, щелкните **Свойства** и скопируйте значение параметра **Идентификатор каталога**. Оно вам понадобится при настройке файла *application.properties*, как описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="faf09-138">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID**; you will use that value to configure your *application.properties* file later in this tutorial.</span></span>

   ![Копирование идентификатора каталога Azure Active Directory][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="faf09-140">Регистрация приложения для приложения Spring Boot</span><span class="sxs-lookup"><span data-stu-id="faf09-140">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="faf09-141">На портале в меню выберите **Azure Active Directory**, щелкните **Обзор** и выберите **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="faf09-141">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Регистрация приложения][directory-04]

2. <span data-ttu-id="faf09-143">Щелкните **Регистрация нового приложения**, введите **имя** приложения, укажите http://localhost:8080 в качестве **URL-адреса входа**, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="faf09-143">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Создание регистрации приложения][directory-05]

3. <span data-ttu-id="faf09-145">Щелкните зарегистрированное приложение.</span><span class="sxs-lookup"><span data-stu-id="faf09-145">Click your application registration after it has been created.</span></span>

   ![Выбор зарегистрированного приложения][directory-06]

4. <span data-ttu-id="faf09-147">Когда появится страница для регистрации приложения, скопируйте **идентификатор приложения**. Он вам понадобится при настройке файла *application.properties*, как описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="faf09-147">When the page for your app registration appears, copy your **Application ID**; you will use this value to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="faf09-148">Щелкните **Параметры**, а затем выберите **Ключи**.</span><span class="sxs-lookup"><span data-stu-id="faf09-148">Click **Settings**, and then click **Keys**.</span></span>

   ![Создание ключей зарегистрированного приложения][directory-07]

5. <span data-ttu-id="faf09-150">Добавьте **описание** и укажите **длительность** использования нового ключа, а затем щелкните **Сохранить**. Значение ключа будет указано автоматически, когда вы щелкнете значок **Сохранить**. Скопируйте это значение, чтобы использовать его при настройке файла *application.properties*, как описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="faf09-150">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="faf09-151">(Вы не сможете получить это значение позже.)</span><span class="sxs-lookup"><span data-stu-id="faf09-151">(You will not be able to retrieve this value later.)</span></span>

   ![Указание параметров зарегистрированного приложения][directory-08]

6. <span data-ttu-id="faf09-153">На главной странице зарегистрированного приложения последовательно щелкните **Параметры** и **Требуемые разрешения**.</span><span class="sxs-lookup"><span data-stu-id="faf09-153">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Добавление требуемых разрешений для приложения][directory-09]

7. <span data-ttu-id="faf09-155">Щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="faf09-155">Click **Windows Azure Active Directory**.</span></span>

   ![Выбор Azure Active Directory][directory-10]

8. <span data-ttu-id="faf09-157">Установите флажки рядом с пунктами **Доступ к каталогу как пользователь, выполнивший вход** и **Вход в систему и чтение профиля пользователя**, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="faf09-157">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Включение разрешений на доступ][directory-11]

9. <span data-ttu-id="faf09-159">На странице **Требуемые разрешения** щелкните **Предоставить разрешения** и **Да**.</span><span class="sxs-lookup"><span data-stu-id="faf09-159">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Предоставление разрешений на доступ][directory-12]

10. <span data-ttu-id="faf09-161">На главной странице зарегистрированного приложения последовательно щелкните **Параметры** и **URL-адреса ответа**.</span><span class="sxs-lookup"><span data-stu-id="faf09-161">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

    ![Изменение URL-адресов ответа][directory-14]

11. <span data-ttu-id="faf09-163">Введите <http://localhost:8080/login/oauth2/code/azure> в качестве нового URL-адреса ответа, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="faf09-163">Enter "<http://localhost:8080/login/oauth2/code/azure>" as a new reply URL, and then click **Save**.</span></span>

    ![Добавление нового URL-адреса ответа][directory-15]

12. <span data-ttu-id="faf09-165">На главной странице регистрации приложения щелкните **Манифест**, затем установите для параметра `oauth2AllowImplicitFlow` значение `true` и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="faf09-165">From the main page for your app registration, click **Manifest**, then set the value of the `oauth2AllowImplicitFlow` parameter to `true`, and then click **Save**.</span></span>

    ![Настройка манифеста приложения][directory-16]

    > [!NOTE]
    > 
    > <span data-ttu-id="faf09-167">Дополнительные сведения о параметре `oauth2AllowImplicitFlow` и других параметрах приложения см. в статье [Манифест приложения Azure Active Directory][AAD app manifest].</span><span class="sxs-lookup"><span data-stu-id="faf09-167">For more information about the `oauth2AllowImplicitFlow` parameter and other application settings, see [Azure Active Directory application manifest][AAD app manifest].</span></span> 
    >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a><span data-ttu-id="faf09-168">Добавление учетной записи пользователя в каталог и в группу</span><span class="sxs-lookup"><span data-stu-id="faf09-168">Add a user account to your directory, and add that account to a group</span></span>

1. <span data-ttu-id="faf09-169">На странице **Обзор** в Active Directory щелкните **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="faf09-169">From the **Overview** page of your Active Directory, click **Users**.</span></span>

   ![Открытие панели "Пользователи"][directory-17]

1. <span data-ttu-id="faf09-171">Когда появится панель **Пользователи**, щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="faf09-171">When the **Users** panel is displayed, click **New user**.</span></span>

   ![Добавление новой учетной записи пользователя][directory-18]

1. <span data-ttu-id="faf09-173">Когда появится панель **Пользователь**, введите значения в поля **Имя** и **Имя пользователя**.</span><span class="sxs-lookup"><span data-stu-id="faf09-173">When the **User** panel is displayed, enter the **Name** and **User name**.</span></span>

   ![Ввод сведений об учетной записи пользователя][directory-19]

   > [!NOTE]
   > 
   > <span data-ttu-id="faf09-175">При вводе имени пользователя укажите URL-адрес каталога, ранее скопированный в рамках этого руководства. Например:</span><span class="sxs-lookup"><span data-stu-id="faf09-175">You need to specify your directory URL from earlier in this tutorial when you enter the user name; for example:</span></span>
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. <span data-ttu-id="faf09-176">Щелкните **Группы**, затем выберите группы, которые будут использоваться для авторизации в приложении, и нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="faf09-176">Click **Groups**, then select the groups that you will use for authorization in your application, and then click **Select**.</span></span> <span data-ttu-id="faf09-177">(В рамках этого руководства добавьте учетную запись в группу _Пользователи_.)</span><span class="sxs-lookup"><span data-stu-id="faf09-177">(For the purposes of this tutorial, add the account to the _Users_ group.)</span></span>

   ![Выбор групп пользователей][directory-20]

1. <span data-ttu-id="faf09-179">Установите флажок **Показать пароль** и скопируйте пароль. Он вам понадобится при входе в приложение, как описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="faf09-179">Click **Show password**, and copy the password; you will use this when you log into your application later in this tutorial.</span></span>

   ![Отображение пароля][directory-21]

1. <span data-ttu-id="faf09-181">Нажмите кнопку **Создать**, чтобы добавить в каталог новую учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="faf09-181">Click **Create** to add the new user account to your directory.</span></span>

   ![Создание учетной записи пользователя][directory-22]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="faf09-183">Настройка и компиляция приложения Spring Boot</span><span class="sxs-lookup"><span data-stu-id="faf09-183">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="faf09-184">Распакуйте архив с файлами проекта, который вы создали и скачали в каталог ранее в рамках этого руководства.</span><span class="sxs-lookup"><span data-stu-id="faf09-184">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

1. <span data-ttu-id="faf09-185">Перейдите в родительскую папку проекта и откройте файл проекта Maven `pom.xml` в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="faf09-185">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

1. <span data-ttu-id="faf09-186">Добавьте зависимости для защиты с помощью Spring OAuth2 в `pom.xml`:</span><span class="sxs-lookup"><span data-stu-id="faf09-186">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

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

1. <span data-ttu-id="faf09-187">Сохраните и закройте файл *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="faf09-187">Save and close the *pom.xml* file.</span></span>

1. <span data-ttu-id="faf09-188">В папке *src/main/resources* проекта откройте файл *application.properties* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="faf09-188">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="faf09-189">Задайте параметры для регистрации вашего приложения, используя созданные ранее значения. Например:</span><span class="sxs-lookup"><span data-stu-id="faf09-189">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

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
   <span data-ttu-id="faf09-190">Описание</span><span class="sxs-lookup"><span data-stu-id="faf09-190">Where:</span></span>

   | <span data-ttu-id="faf09-191">Параметр</span><span class="sxs-lookup"><span data-stu-id="faf09-191">Parameter</span></span> | <span data-ttu-id="faf09-192">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="faf09-192">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="faf09-193">Содержит **идентификатор каталога** Active Directory, который вы скопировали ранее.</span><span class="sxs-lookup"><span data-stu-id="faf09-193">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="faf09-194">Содержит **идентификатор приложения**, полученный после регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="faf09-194">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="faf09-195">Содержит **значение** ключа, полученное после регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="faf09-195">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="faf09-196">Содержит список групп Active Directory, используемых для авторизации.</span><span class="sxs-lookup"><span data-stu-id="faf09-196">Contains a list of Active Directory groups to use for authorization.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="faf09-197">Полный список значений, доступных в файле *application.properties*, см. на [сайте GitHub][AAD Spring Boot Sample].</span><span class="sxs-lookup"><span data-stu-id="faf09-197">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

1. <span data-ttu-id="faf09-198">Сохраните и закройте файл *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="faf09-198">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="faf09-199">Создайте папку с именем *controller* в папке с исходным кодом Java для приложения, например: *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="faf09-199">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="faf09-200">Создайте файл Java с именем *HelloController.java* в папке *controller* и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="faf09-200">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="faf09-201">Вставьте следующий код, а затем сохраните и закройте файл:</span><span class="sxs-lookup"><span data-stu-id="faf09-201">Enter the following code, then save and close the file:</span></span>

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
   > <span data-ttu-id="faf09-202">Имя группы, указываемое для метода `@PreAuthorize("hasRole('')")`, должно содержать одну из групп, указанных в поле `azure.activedirectory.active-directory-groups` в файле *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="faf09-202">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   >

   > [!NOTE]
   > 
   > <span data-ttu-id="faf09-203">Для разных сопоставлений запросов можно указывать разные параметры авторизации, например:</span><span class="sxs-lookup"><span data-stu-id="faf09-203">You can specify different authorization settings for different request mappings; for example:</span></span>
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

1. <span data-ttu-id="faf09-204">Создайте папку с именем *security* в папке с исходным кодом Java для приложения, например: *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="faf09-204">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="faf09-205">Создайте файл Java с именем *WebSecurityConfig.java* в папке *security* и откройте его в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="faf09-205">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="faf09-206">Вставьте следующий код, а затем сохраните и закройте файл:</span><span class="sxs-lookup"><span data-stu-id="faf09-206">Enter the following code, then save and close the file:</span></span>

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

## <a name="build-and-test-your-app"></a><span data-ttu-id="faf09-207">Создание и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="faf09-207">Build and test your app</span></span>

1. <span data-ttu-id="faf09-208">Откройте командную строку и перейдите из каталога в папку с файлом *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="faf09-208">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="faf09-209">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="faf09-209">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Сборка приложения][build-application]

1. <span data-ttu-id="faf09-211">Скомпилировав и запустив приложение с помощью Maven, перейдите в веб-браузере по адресу <http://localhost:8080> и введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="faf09-211">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Вход в приложение][application-login]

   > [!NOTE]
   > 
   > <span data-ttu-id="faf09-213">Если это первый вход с новой учетной записью пользователя, возможно, вам будет предложено изменить пароль.</span><span class="sxs-lookup"><span data-stu-id="faf09-213">You may be prompted to change your password if this is the first login for a new user account.</span></span>
   > 
   > ![Изменение пароля][update-password]
   > 

1. <span data-ttu-id="faf09-215">Войдя в приложение, вы увидите сообщение контроллера "Hello World".</span><span class="sxs-lookup"><span data-stu-id="faf09-215">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Успешный вход в приложение][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="faf09-217">Пользователи с неавторизованными учетными записями получат сообщение **HTTP 403 — не авторизовано**.</span><span class="sxs-lookup"><span data-stu-id="faf09-217">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="faf09-218">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="faf09-218">Next steps</span></span>

<span data-ttu-id="faf09-219">В этом руководстве вы создали веб-приложение Java с использованием начального приложения Spring Boot для Azure Active Directory, настроили нового клиента Azure AD, зарегистрировали в нем созданное приложение, а затем настроили это приложение для использования аннотаций и классов Spring с целью защиты веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="faf09-219">In this tutorial, you created a new Java web application using the Azure Active Directory starter, configured a new Azure AD tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span> <span data-ttu-id="faf09-220">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="faf09-220">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="faf09-221">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="faf09-221">Spring on Azure</span></span>](/java/azure/spring-framework)

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
