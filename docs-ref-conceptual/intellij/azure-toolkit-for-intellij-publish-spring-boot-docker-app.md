---
title: "Публикация приложения Spring Boot в виде контейнера Docker с помощью набора средств Azure для IntelliJ"
description: "Вы можете узнать, как опубликовать веб-приложение в Microsoft Azure в виде контейнера Docker с помощью набора средств Azure для IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: 65fbdc32824c2b6312929f4888844d1673101ac8
ms.sourcegitcommit: 062e07cbd42cda74f02c82b933ce90da646a50a0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="12ba9-103">Публикация приложения Spring Boot в виде контейнера Docker с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="12ba9-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="12ba9-104">[Spring Framework] — это решение с открытым исходным кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="12ba9-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="12ba9-105">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="12ba9-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="12ba9-106">[Docker] — это решение с открытым исходным кодом, которое помогает разработчикам автоматизировать развертывание приложений, их масштабирование, а также управление приложениями, которые выполняются в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="12ba9-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="12ba9-107">В данном руководстве описывается процесс развертывания приложения Spring Boot в качестве контейнера Docker в Microsoft Azure с помощью набора средств Azure для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="12ba9-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a><span data-ttu-id="12ba9-108">Клонирование репозитория по умолчанию приложения Docker Spring Boot</span><span class="sxs-lookup"><span data-stu-id="12ba9-108">Clone the default Spring Boot Docker repo</span></span>

<span data-ttu-id="12ba9-109">Ниже рассмотрена процедура клонирования репозитория приложения Spring Boot Docker с помощью IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="12ba9-109">The following steps walk you through cloning the Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="12ba9-110">Процесс использования командной строки см. в разделе [Развертывание приложения Spring Boot в Linux в службе контейнеров Azure][Deploy Spring Boot on Linux in AKS].</span><span class="sxs-lookup"><span data-stu-id="12ba9-110">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in AKS].</span></span>

1. <span data-ttu-id="12ba9-111">Откройте IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="12ba9-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="12ba9-112">На экране приветствия выберите пункт **GitHub** из списка **Check out from Version Control (Извлечь из системы управления версиями)**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-112">On the welcome screen, select the **GitHub** option in the **Check out from Version Control** list.</span></span>

   ![Параметр GitHub для управления версиями][CL01]

1. <span data-ttu-id="12ba9-114">При появлении запроса на вход введите свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="12ba9-114">Enter your credentials if you are prompted to log in.</span></span>

   * <span data-ttu-id="12ba9-115">Если для входа в GitHub вы используете имя пользователя и пароль:</span><span class="sxs-lookup"><span data-stu-id="12ba9-115">If you are using a username/password to log in to GitHub:</span></span> 

      ![Диалоговое окно для ввода имени пользователя и пароля для входа в GitHub][CL02a]

   * <span data-ttu-id="12ba9-117">Если для входа в GitHub вы используете токен:</span><span class="sxs-lookup"><span data-stu-id="12ba9-117">If you are using a token to log in to GitHub:</span></span> 

      ![Диалоговое окно для ввода токена GitHub][CL02b]

1. <span data-ttu-id="12ba9-119">В качестве URL-адреса репозитория введите **https://github.com/spring-guides/gs-spring-boot-docker.git**, укажите локальный путь и сведения о папке, а затем нажмите кнопку **Клонировать**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for the repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Диалоговое окно "Clone Repository" (Клонирование репозитория)][CL03]

1. <span data-ttu-id="12ba9-121">При появлении запроса на создание проекта IntelliJ выберите **Нет**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-121">When you're prompted to create an IntelliJ project, select **No**.</span></span>

   ![Отклонение создания проекта IntelliJ][CL04]

1. <span data-ttu-id="12ba9-123">На экране приветствия щелкните пункт **Импорт проекта**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-123">On the welcome page, click **Import Project**.</span></span>

   ![Пункт "Импорт проекта"][CL05]

1. <span data-ttu-id="12ba9-125">Найдите путь, по которому был клонирован репозиторий Spring Boot, выделите папку **complete** в корневом каталоге и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-125">Locate the path where you cloned the Spring Boot repo, select the **complete** folder under the root, and then click **OK**.</span></span>

   ![Выбор папки для импорта][CL06]

1. <span data-ttu-id="12ba9-127">При появлении запроса выберите **Создать проект из существующих источников**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Параметр для создания проекта из существующих источников][CL07]

1. <span data-ttu-id="12ba9-129">Укажите имя проекта или примите имя по умолчанию, проверьте путь к папке **complete**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-129">Specify your project name or accept the default, verify the correct path to the **complete** folder, and then click **Next**.</span></span>

   ![Выбор имени проекта][CL08]

1. <span data-ttu-id="12ba9-131">Настройте все каталоги для импорта и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Выбор каталогов][CL09]

1. <span data-ttu-id="12ba9-133">Просмотрите библиотеки для импорта и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-133">Review the libraries to import, and then click **Next**.</span></span>

   ![Просмотр библиотек проекта][CL10]

1. <span data-ttu-id="12ba9-135">Просмотрите структуру модулей и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-135">Review the module structure, and then click **Next**.</span></span>

   ![Просмотр структуры модулей][CL11]

1. <span data-ttu-id="12ba9-137">Укажите свой JDK и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-137">Specify your JDK, and then click **Next**.</span></span>

   ![Указание JDK][CL12]

1. <span data-ttu-id="12ba9-139">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="12ba9-139">Click **Finish**.</span></span>

   ![Кнопка "Готово"][CL13]

<span data-ttu-id="12ba9-141">IntelliJ импортирует приложение Spring Boot в качестве проекта и по окончании отобразит структуру.</span><span class="sxs-lookup"><span data-stu-id="12ba9-141">IntelliJ imports the Spring Boot app as a project and displays the structure when the import has finished.</span></span>

![Приложение Spring Boot в IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="12ba9-143">Создание приложения Spring Boot</span><span class="sxs-lookup"><span data-stu-id="12ba9-143">Build your Spring Boot app</span></span>

### <a name="build-the-app-by-using-the-maven-pom"></a><span data-ttu-id="12ba9-144">Создание приложения с помощью Maven POM</span><span class="sxs-lookup"><span data-stu-id="12ba9-144">Build the app by using the Maven POM</span></span>

1. <span data-ttu-id="12ba9-145">Откройте окно инструментов Maven, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="12ba9-145">Open the Maven tool window if it is not already opened.</span></span> <span data-ttu-id="12ba9-146">Последовательно выберите **Вид** > **Окна инструментов** > **Проекты Maven**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Окна инструментов и команды проектов Maven][BU01]

1. <span data-ttu-id="12ba9-148">В окне инструментов Maven щелкните правой кнопкой мыши **пакет** и выберите пункт **Выполнить сборку Maven**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-148">In the Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="12ba9-149">(Если проект Maven не отображается автоматически, щелкните значок **Повторный импорт** на панели инструментов Maven.)</span><span class="sxs-lookup"><span data-stu-id="12ba9-149">(If your Maven project does not show up automatically, click the **Reimport** icon on the Maven toolbar.)</span></span>

   ![Команда "Запуск сборки Maven"][BU02]

1. <span data-ttu-id="12ba9-151">После успешного создания приложения Spring Boot IntelliJ отобразит сообщение **Сборка выполнена успешно**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Сообщение "Сборка выполнена успешно"][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="12ba9-153">Создание готового к развертыванию артефакта</span><span class="sxs-lookup"><span data-stu-id="12ba9-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="12ba9-154">Чтобы опубликовать приложение Spring Boot, необходимо создать готовый к развертыванию артефакт.</span><span class="sxs-lookup"><span data-stu-id="12ba9-154">To publish your Spring Boot app, you need to create a deployment-ready artifact.</span></span> <span data-ttu-id="12ba9-155">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="12ba9-155">Use the following steps:</span></span>

1. <span data-ttu-id="12ba9-156">Откройте проект веб-приложения в IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="12ba9-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="12ba9-157">В меню **File** (Файл) выберите **Project Structure** (Структура проекта).</span><span class="sxs-lookup"><span data-stu-id="12ba9-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Команда "Project Structure" (Структура проекта)][ART01]

1. <span data-ttu-id="12ba9-159">Щелкните зеленый знак "плюс" (**+**), чтобы добавить артефакт, затем щелкните **JAR** и **Empty** (пустой).</span><span class="sxs-lookup"><span data-stu-id="12ba9-159">Click the green plus (**+**) symbol to add an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Добавление артефакта][ART02]

1. <span data-ttu-id="12ba9-161">Укажите имя артефакта без расширения JAR, а затем укажите целевую папку назначения для выходных данных Maven.</span><span class="sxs-lookup"><span data-stu-id="12ba9-161">Name your artifact while making sure not to add the ".jar" extension, and then specify the target folder for the Maven output.</span></span>

   ![Указание свойств артефакта][ART03]

1. <span data-ttu-id="12ba9-163">Создайте манифест для артефакта (необязательно).</span><span class="sxs-lookup"><span data-stu-id="12ba9-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="12ba9-164">а.</span><span class="sxs-lookup"><span data-stu-id="12ba9-164">a.</span></span> <span data-ttu-id="12ba9-165">Нажмите кнопку **Create Manifest** (Создать манифест).</span><span class="sxs-lookup"><span data-stu-id="12ba9-165">Click **Create Manifest**.</span></span>

      ![Кнопка "Создать манифест"][ART04a]

   <span data-ttu-id="12ba9-167">b.</span><span class="sxs-lookup"><span data-stu-id="12ba9-167">b.</span></span> <span data-ttu-id="12ba9-168">Выберите путь по умолчанию для артефакта и нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-168">Choose the default path for the artifact, and then click **OK**.</span></span>

      ![Указание пути к артефакту][ART04b]

   <span data-ttu-id="12ba9-170">c.</span><span class="sxs-lookup"><span data-stu-id="12ba9-170">c.</span></span> <span data-ttu-id="12ba9-171">Нажмите кнопку с многоточием (**...**) для указания основного класса (main).</span><span class="sxs-lookup"><span data-stu-id="12ba9-171">Click the ellipsis (**...**) to locate the main class.</span></span>

      ![Поиск основного (main) класса][ART04c]

   <span data-ttu-id="12ba9-173">d.</span><span class="sxs-lookup"><span data-stu-id="12ba9-173">d.</span></span> <span data-ttu-id="12ba9-174">Выберите основной класс и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-174">Choose your main class, and then click **OK**.</span></span>

      ![Указание основного (main) класса][ART04d]

1. <span data-ttu-id="12ba9-176">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-176">Click **OK**.</span></span>

   ![Закрытие диалогового окна "Project Structure" (Структура проекта)][ART05]

> [!NOTE]
> <span data-ttu-id="12ba9-178">Дополнительные сведения о создании артефактов в IntelliJ см. в разделе [Configuring Artifacts] (Настройка артефактов) на веб-сайте JetBrains.</span><span class="sxs-lookup"><span data-stu-id="12ba9-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on the JetBrains website.</span></span>
>

### <a name="build-the-artifact-for-deployment"></a><span data-ttu-id="12ba9-179">Создание артефакта для развертывания</span><span class="sxs-lookup"><span data-stu-id="12ba9-179">Build the artifact for deployment</span></span>

1. <span data-ttu-id="12ba9-180">Нажмите кнопку **Build** (Сборка), а затем кнопку **Artifacts** (Артефакты).</span><span class="sxs-lookup"><span data-stu-id="12ba9-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Команда "Build Artifacts" (Создать артефакты)][BU04]

1. <span data-ttu-id="12ba9-182">При появлении контекстного меню **Build Artifact** (Создание артефактов) нажмите кнопку **Build** (Сборка).</span><span class="sxs-lookup"><span data-stu-id="12ba9-182">When the **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Контекстное меню "Build Artifacts" (Создание артефакта)][BU05]

<span data-ttu-id="12ba9-184">IntelliJ должен отобразить созданный артефакт для приложения Spring Boot в окне инструментов проекта.</span><span class="sxs-lookup"><span data-stu-id="12ba9-184">IntelliJ should display the completed artifact for your Spring Boot app in the project tool window.</span></span>

   ![Созданный артефакт][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="12ba9-186">Публикация веб-приложения в Azure с помощью контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="12ba9-186">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="12ba9-187">Если вы еще не вошли в свою учетную запись Azure, выполните процедуру в статье [Инструкции по входу для набора средств Azure для IntelliJ][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="12ba9-187">If you have not signed in to your Azure account, follow the steps in [Sign-in instructions for the Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="12ba9-188">В окне инструментов обозревателя проектов щелкните правой кнопкой мыши проект и выберите **Azure** > **Publish as Docker Container** (Опубликовать как контейнер Docker).</span><span class="sxs-lookup"><span data-stu-id="12ba9-188">In the Project Explorer tool window, right-click the project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Команда публикации в виде контейнера Docker][PU01]

1. <span data-ttu-id="12ba9-190">Когда появится диалоговое окно **Развертывание контейнера Docker в Azure**, в нем будут отображаться все существующие узлы Docker.</span><span class="sxs-lookup"><span data-stu-id="12ba9-190">When the **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="12ba9-191">Если требуется развернуть на существующий узел, можно пропустить шаг 4.</span><span class="sxs-lookup"><span data-stu-id="12ba9-191">If you choose to deploy to an existing host, you can skip to step 4.</span></span> <span data-ttu-id="12ba9-192">В противном случае, чтобы создать узел, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="12ba9-192">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="12ba9-193">а.</span><span class="sxs-lookup"><span data-stu-id="12ba9-193">a.</span></span> <span data-ttu-id="12ba9-194">Щелкните зеленый знак "плюс" (**+**).</span><span class="sxs-lookup"><span data-stu-id="12ba9-194">Click the green plus (**+**) symbol.</span></span>

      ![Добавление нового узла Docker][PU02]

   <span data-ttu-id="12ba9-196">b.</span><span class="sxs-lookup"><span data-stu-id="12ba9-196">b.</span></span> <span data-ttu-id="12ba9-197">При появлении диалогового окна **Создание узла Docker** можно принять значения по умолчанию или задать пользовательские параметры для нового узла Docker.</span><span class="sxs-lookup"><span data-stu-id="12ba9-197">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="12ba9-198">(Подробное описание различных параметров см. в статье [Публикация веб-приложения в виде контейнера Docker с помощью набора средств Azure для IntelliJ][Publish Container with Azure Toolkit].) Нажмите кнопку **Next** (Далее) после задания используемых параметров.</span><span class="sxs-lookup"><span data-stu-id="12ba9-198">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Задание параметров узла Docker][PU03a]

   <span data-ttu-id="12ba9-200">c.</span><span class="sxs-lookup"><span data-stu-id="12ba9-200">c.</span></span> <span data-ttu-id="12ba9-201">Можно использовать для входа в систему существующие учетные данные, хранящиеся в Azure Key Vault, или ввести новые учетные данные для входа в Docker.</span><span class="sxs-lookup"><span data-stu-id="12ba9-201">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="12ba9-202">После задания параметров нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="12ba9-202">Click **Finish** when you have specified your options.</span></span>

      ![Задание учетных данных узла Docker][PU03b]

1. <span data-ttu-id="12ba9-204">Выберите узел Docker и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="12ba9-204">Select your Docker host, and then click **Next**.</span></span>

   ![Выбор используемого узла Docker][PU04]

1. <span data-ttu-id="12ba9-206">На последней странице диалогового окна **Deploy Docker Container on Azure** (Развертывание контейнера Docker в Azure) задайте следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="12ba9-206">On the last page of the **Deploy Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="12ba9-207">а.</span><span class="sxs-lookup"><span data-stu-id="12ba9-207">a.</span></span> <span data-ttu-id="12ba9-208">Можно указать пользовательское имя для контейнера, в котором будет размещаться контейнер Docker, или принять значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="12ba9-208">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="12ba9-209">b.</span><span class="sxs-lookup"><span data-stu-id="12ba9-209">b.</span></span> <span data-ttu-id="12ba9-210">Для узла Docker укажите TCP-порты с помощью следующего синтаксиса: *[внешний порт]*:*[внутренний порт]*.</span><span class="sxs-lookup"><span data-stu-id="12ba9-210">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="12ba9-211">Например, **80:8080** означает внешний порт "80" и внутренний порт Spring Boot по умолчанию "8080".</span><span class="sxs-lookup"><span data-stu-id="12ba9-211">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="12ba9-212">После настройки внутреннего порта (например, с помощью файла application.yml) необходимо указать номер порта для обеспечения корректной маршрутизации в Azure.</span><span class="sxs-lookup"><span data-stu-id="12ba9-212">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="12ba9-213">c.</span><span class="sxs-lookup"><span data-stu-id="12ba9-213">c.</span></span> <span data-ttu-id="12ba9-214">После настройки этих параметров щелкните **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="12ba9-214">After you have configured these options, click **Finish**.</span></span>

   ![Развертывание контейнера Docker в Azure][PU05]

1. <span data-ttu-id="12ba9-216">После завершения публикации набора средств Azure в журнале действий Azure будет отображаться состояние **Опубликовано**.</span><span class="sxs-lookup"><span data-stu-id="12ba9-216">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Успешно развернутый узел Docker][PU06]

## <a name="next-steps"></a><span data-ttu-id="12ba9-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="12ba9-218">Next steps</span></span>

<span data-ttu-id="12ba9-219">Сведения о дополнительных методах создания приложений Spring Boot с помощью IntelliJ см. в разделе [Создание проектов Spring Boot](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) на веб-сайте JetBrains.</span><span class="sxs-lookup"><span data-stu-id="12ba9-219">To learn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on the JetBrains website.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Configuring Artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
