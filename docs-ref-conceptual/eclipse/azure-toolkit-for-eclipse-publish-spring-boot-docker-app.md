---
title: Публикация приложения Spring Boot в виде контейнера Docker с помощью набора средств Azure для Eclipse
description: Вы можете узнать, как опубликовать веб-приложение в Microsoft Azure в виде контейнера Docker с помощью набора средств Azure для Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: c116e0712afd8e48983f946f43eddfd0c79c0ba8
ms.sourcegitcommit: 0ed7c5af0152125322ff1d265c179f35028f3c15
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2018
ms.locfileid: "38075480"
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="13da2-103">Публикация приложения Spring Boot в виде контейнера Docker с помощью набора средств Azure для Eclipse</span><span class="sxs-lookup"><span data-stu-id="13da2-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="13da2-104">[Spring Framework] — это решение с открытым исходным кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="13da2-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="13da2-105">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="13da2-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="13da2-106">[Docker] — это решение с открытым исходным кодом, которое помогает разработчикам автоматизировать развертывание приложений, их масштабирование, а также управление приложениями, которые выполняются в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="13da2-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="13da2-107">В данном руководстве описывается процесс развертывания приложения Spring Boot в качестве контейнера Docker в Microsoft Azure с помощью набора средств Azure для Eclipse.</span><span class="sxs-lookup"><span data-stu-id="13da2-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a><span data-ttu-id="13da2-108">Клонирование репозитория по умолчанию приложения Docker Spring Boot</span><span class="sxs-lookup"><span data-stu-id="13da2-108">Clone the default Spring Boot Docker repository</span></span>

### <a name="import-the-public-repository"></a><span data-ttu-id="13da2-109">Импорт общедоступного репозитория</span><span class="sxs-lookup"><span data-stu-id="13da2-109">Import the public repository</span></span>

<span data-ttu-id="13da2-110">Ниже рассмотрена процедура клонирования репозитория приложения Docker Spring Boot на локальный компьютер с помощью IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="13da2-110">The following steps walk you through cloning the Spring Boot Docker repository to your local computer by using IntelliJ.</span></span> <span data-ttu-id="13da2-111">Процесс использования командной строки см. в разделе [Развертывание приложения Spring Boot в Linux в службе контейнеров Azure][Deploy Spring Boot on Linux in AKS].</span><span class="sxs-lookup"><span data-stu-id="13da2-111">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in AKS].</span></span>

1. <span data-ttu-id="13da2-112">Откройте Eclipse.</span><span class="sxs-lookup"><span data-stu-id="13da2-112">Open Eclipse.</span></span>

1. <span data-ttu-id="13da2-113">Последовательно выберите **Файл** > **Импортировать**.</span><span class="sxs-lookup"><span data-stu-id="13da2-113">Click **File** > **Import**.</span></span>

   ![Меню "File" (Файл) > "Import" (Импортировать)][CL01]

1. <span data-ttu-id="13da2-115">Когда откроется диалоговое окно **Import** (Импорт), сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="13da2-115">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="13da2-116">a.</span><span class="sxs-lookup"><span data-stu-id="13da2-116">a.</span></span> <span data-ttu-id="13da2-117">Разверните элемент **Git**.</span><span class="sxs-lookup"><span data-stu-id="13da2-117">Expand **Git**.</span></span>

   <span data-ttu-id="13da2-118">Б.</span><span class="sxs-lookup"><span data-stu-id="13da2-118">b.</span></span> <span data-ttu-id="13da2-119">Выберите **Projects from Git** (Проекты из Git).</span><span class="sxs-lookup"><span data-stu-id="13da2-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="13da2-120">c.</span><span class="sxs-lookup"><span data-stu-id="13da2-120">c.</span></span> <span data-ttu-id="13da2-121">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="13da2-121">Click **Next**.</span></span>

   ![Диалоговое окно "Import" (Импорт)][CL02]

1. <span data-ttu-id="13da2-123">На странице **Select Repository Source** (Выбор источника репозитория) сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="13da2-123">On the **Select Repository Source** page:</span></span>

   <span data-ttu-id="13da2-124">a.</span><span class="sxs-lookup"><span data-stu-id="13da2-124">a.</span></span> <span data-ttu-id="13da2-125">Выберите **Клонировать URI**.</span><span class="sxs-lookup"><span data-stu-id="13da2-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="13da2-126">Б.</span><span class="sxs-lookup"><span data-stu-id="13da2-126">b.</span></span> <span data-ttu-id="13da2-127">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="13da2-127">Click **Next**.</span></span>

   ![Страница "Выбор источника репозитория"][CL03]

1. <span data-ttu-id="13da2-129">На странице **Source Git Repository** (Исходный репозиторий Git) сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="13da2-129">On the **Source Git Repository** page:</span></span>

   <span data-ttu-id="13da2-130">a.</span><span class="sxs-lookup"><span data-stu-id="13da2-130">a.</span></span> <span data-ttu-id="13da2-131">В поле **URI** введите `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="13da2-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="13da2-132">Поля **Host** (Узел) и **Repository path** (Путь к репозиторию) должны автоматически заполниться правильными значениями.</span><span class="sxs-lookup"><span data-stu-id="13da2-132">This step should automatically populate the **Host** and **Repository path** fields with the correct values.</span></span>
   
   <span data-ttu-id="13da2-133">Б.</span><span class="sxs-lookup"><span data-stu-id="13da2-133">b.</span></span> <span data-ttu-id="13da2-134">Репозиторий Spring Boot является общедоступным, поэтому нет необходимости вводить имя пользователя и пароль Git.</span><span class="sxs-lookup"><span data-stu-id="13da2-134">The Spring Boot repository is public, so you should not have to enter your Git username and password.</span></span>
   
   <span data-ttu-id="13da2-135">c.</span><span class="sxs-lookup"><span data-stu-id="13da2-135">c.</span></span> <span data-ttu-id="13da2-136">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="13da2-136">Click **Next**.</span></span>

   ![Страница "Исходный репозиторий Git"][CL04]

1. <span data-ttu-id="13da2-138">На странице **Branch Selection** (Выбор ветви) нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="13da2-138">On the **Branch Selection** page, click **Next**.</span></span>

   ![Страница "Выбор ветви"][CL05]

1. <span data-ttu-id="13da2-140">На странице **Local Destination** (Локальное назначение) сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="13da2-140">On the **Local Destination** page:</span></span>

   <span data-ttu-id="13da2-141">a.</span><span class="sxs-lookup"><span data-stu-id="13da2-141">a.</span></span> <span data-ttu-id="13da2-142">Укажите локальную папку, в которой должен находиться локальный репозиторий.</span><span class="sxs-lookup"><span data-stu-id="13da2-142">Specify the local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="13da2-143">Б.</span><span class="sxs-lookup"><span data-stu-id="13da2-143">b.</span></span> <span data-ttu-id="13da2-144">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="13da2-144">Click **Next**.</span></span>

   ![Страница "Локальное назначение"][CL06]

1. <span data-ttu-id="13da2-146">На странице **Select a wizard to use for importing projects** (Выбор мастера для импорта проектов) сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="13da2-146">On the **Select a wizard to use for importing projects** page:</span></span>

   <span data-ttu-id="13da2-147">a.</span><span class="sxs-lookup"><span data-stu-id="13da2-147">a.</span></span> <span data-ttu-id="13da2-148">Выберите **Import as a general project** (Импортировать как универсальный проект).</span><span class="sxs-lookup"><span data-stu-id="13da2-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="13da2-149">Б.</span><span class="sxs-lookup"><span data-stu-id="13da2-149">b.</span></span> <span data-ttu-id="13da2-150">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="13da2-150">Click **Next**.</span></span>

   ![На страница "Выбор мастера для импорта проектов"][CL07]

1. <span data-ttu-id="13da2-152">На странице **Import Projects** (Импорт проектов) сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="13da2-152">On the **Import Projects** page:</span></span>

   <span data-ttu-id="13da2-153">a.</span><span class="sxs-lookup"><span data-stu-id="13da2-153">a.</span></span> <span data-ttu-id="13da2-154">Укажите имя проекта.</span><span class="sxs-lookup"><span data-stu-id="13da2-154">Specify your project name.</span></span>
   
   <span data-ttu-id="13da2-155">Б.</span><span class="sxs-lookup"><span data-stu-id="13da2-155">b.</span></span> <span data-ttu-id="13da2-156">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="13da2-156">Click **Finish**.</span></span>

   ![Страница "Импорт проектов"][CL08]

1. <span data-ttu-id="13da2-158">Если репозиторий успешно клонирован, вы увидите полный список файлов в Eclipse.</span><span class="sxs-lookup"><span data-stu-id="13da2-158">When the repository is cloned successfully, you see all the files listed in Eclipse.</span></span>

   ![Локальный репозиторий][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="13da2-160">Создание проекта Maven из локального репозитория</span><span class="sxs-lookup"><span data-stu-id="13da2-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="13da2-161">Репозиторий Docker Spring Boot содержит завершенный проект Maven, который будет использоваться в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="13da2-161">The Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="13da2-162">Последовательно выберите **Файл** > **Импортировать**.</span><span class="sxs-lookup"><span data-stu-id="13da2-162">Click **File** > **Import**.</span></span>

   ![Команда "Импортировать" в меню "Файл"][CL01]

1. <span data-ttu-id="13da2-164">Когда откроется диалоговое окно **Import** (Импорт), сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="13da2-164">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="13da2-165">a.</span><span class="sxs-lookup"><span data-stu-id="13da2-165">a.</span></span> <span data-ttu-id="13da2-166">Разверните элемент **Maven**.</span><span class="sxs-lookup"><span data-stu-id="13da2-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="13da2-167">Б.</span><span class="sxs-lookup"><span data-stu-id="13da2-167">b.</span></span> <span data-ttu-id="13da2-168">Выберите **Existing Maven Projects** (Существующие проекты Maven).</span><span class="sxs-lookup"><span data-stu-id="13da2-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="13da2-169">c.</span><span class="sxs-lookup"><span data-stu-id="13da2-169">c.</span></span> <span data-ttu-id="13da2-170">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="13da2-170">Click **Next**.</span></span>

   ![Диалоговое окно "Import" (Импорт)][MV01]

1. <span data-ttu-id="13da2-172">На странице **Maven Projects** (Проекты Maven) сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="13da2-172">On the **Maven Projects** page:</span></span>

   <span data-ttu-id="13da2-173">a.</span><span class="sxs-lookup"><span data-stu-id="13da2-173">a.</span></span> <span data-ttu-id="13da2-174">В поле **Root Directory** (Корневой каталог) укажите папку **complete** в локальном каталоге.</span><span class="sxs-lookup"><span data-stu-id="13da2-174">For **Root Directory**, specify the **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="13da2-175">Б.</span><span class="sxs-lookup"><span data-stu-id="13da2-175">b.</span></span> <span data-ttu-id="13da2-176">Разверните раздел **Advanced** (Дополнительно) и введите пользовательское имя в поле **Name template** (Шаблон имени).</span><span class="sxs-lookup"><span data-stu-id="13da2-176">Expand the **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="13da2-177">c.</span><span class="sxs-lookup"><span data-stu-id="13da2-177">c.</span></span> <span data-ttu-id="13da2-178">Установите флажок для файла **pom.xml** в проекте.</span><span class="sxs-lookup"><span data-stu-id="13da2-178">Select the box for the **pom.xml** file in the project.</span></span>
   
   <span data-ttu-id="13da2-179">d.</span><span class="sxs-lookup"><span data-stu-id="13da2-179">d.</span></span> <span data-ttu-id="13da2-180">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="13da2-180">Click **Finish**.</span></span>

   ![Страница "Проекты Maven"][MV02]

1. <span data-ttu-id="13da2-182">После успешного открытия проекта Maven в Eclipse появится второй проект.</span><span class="sxs-lookup"><span data-stu-id="13da2-182">When the Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Локальный проект Maven][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="13da2-184">Построение приложения Spring Boot с помощью Maven</span><span class="sxs-lookup"><span data-stu-id="13da2-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="13da2-185">В обозревателе проектов Eclipse выберите проект Maven.</span><span class="sxs-lookup"><span data-stu-id="13da2-185">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="13da2-186">Последовательно выберите **Запуск** > **Запуск от имени** > **Сборка Maven**.</span><span class="sxs-lookup"><span data-stu-id="13da2-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Команды для выполнения в качестве сборки Maven][BU01]

1. <span data-ttu-id="13da2-188">После успешной сборки приложения в окне консоли отобразится состояние.</span><span class="sxs-lookup"><span data-stu-id="13da2-188">When your application is successfully built, the console window shows the status.</span></span>

   ![Успешное выполнение сборки Maven][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="13da2-190">Публикация веб-приложения в Azure с помощью контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="13da2-190">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="13da2-191">В обозревателе проектов Eclipse выберите проект Maven.</span><span class="sxs-lookup"><span data-stu-id="13da2-191">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="13da2-192">Щелкните меню Azure **Publish** (Публикация) и выберите **Publish as Docker container** (Опубликовать как контейнер Docker).</span><span class="sxs-lookup"><span data-stu-id="13da2-192">Click the Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Команда публикации в виде контейнера Docker][PU01]

1. <span data-ttu-id="13da2-194">Когда откроется диалоговое окно **Deploy Docker Container on Azure** (Развертывание контейнера Docker в Azure), сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="13da2-194">When the **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="13da2-195">a.</span><span class="sxs-lookup"><span data-stu-id="13da2-195">a.</span></span> <span data-ttu-id="13da2-196">Введите пользовательское имя образа Docker.</span><span class="sxs-lookup"><span data-stu-id="13da2-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="13da2-197">Б.</span><span class="sxs-lookup"><span data-stu-id="13da2-197">b.</span></span> <span data-ttu-id="13da2-198">В поле **Artifact to deploy** (Развертываемый артефакт) укажите путь к файлу **gs-spring-boot-docker-0.1.0.jar**, сборку которого вы только что выполнили.</span><span class="sxs-lookup"><span data-stu-id="13da2-198">For **Artifact to deploy**, specify the path to the **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Задание параметров Docker][PU02]

   <span data-ttu-id="13da2-200">Отобразятся все существующие узлы Docker.</span><span class="sxs-lookup"><span data-stu-id="13da2-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="13da2-201">Если требуется выполнить развертывание на существующий узел, можно сразу перейти к шагу 5.</span><span class="sxs-lookup"><span data-stu-id="13da2-201">If you choose to deploy to an existing host, you can skip to step 5.</span></span> <span data-ttu-id="13da2-202">В противном случае, чтобы создать узел, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="13da2-202">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="13da2-203">a.</span><span class="sxs-lookup"><span data-stu-id="13da2-203">a.</span></span> <span data-ttu-id="13da2-204">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="13da2-204">Click **Add**.</span></span>

      ![Добавление нового узла Docker][PU03]

   <span data-ttu-id="13da2-206">Б.</span><span class="sxs-lookup"><span data-stu-id="13da2-206">b.</span></span> <span data-ttu-id="13da2-207">При появлении диалогового окна **Создание узла Docker** можно принять значения по умолчанию или задать пользовательские параметры для нового узла Docker.</span><span class="sxs-lookup"><span data-stu-id="13da2-207">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="13da2-208">(Подробное описание различных параметров см. в статье [Публикация веб-приложения в виде контейнера Docker с помощью набора средств Azure для IntelliJ][Publish Container with Azure Toolkit].) Нажмите кнопку **Next** (Далее) после задания используемых параметров.</span><span class="sxs-lookup"><span data-stu-id="13da2-208">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Задание параметров узла Docker][PU04]

   <span data-ttu-id="13da2-210">c.</span><span class="sxs-lookup"><span data-stu-id="13da2-210">c.</span></span> <span data-ttu-id="13da2-211">Можно использовать для входа в систему существующие учетные данные, хранящиеся в Azure Key Vault, или ввести новые учетные данные для входа в Docker.</span><span class="sxs-lookup"><span data-stu-id="13da2-211">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="13da2-212">После задания параметров нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="13da2-212">Click **Finish** when you have specified your options.</span></span>

      ![Задание учетных данных узла Docker][PU05]

1. <span data-ttu-id="13da2-214">Выберите узел Docker и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="13da2-214">Select your Docker host, and then click **Next**.</span></span>

   ![Выбор используемого узла Docker][PU06]

1. <span data-ttu-id="13da2-216">На последней странице диалогового окна **Deploy Docker Container on Azure** (Развертывание контейнера Docker в Azure) задайте следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="13da2-216">On the last page of the **Deploying Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="13da2-217">a.</span><span class="sxs-lookup"><span data-stu-id="13da2-217">a.</span></span> <span data-ttu-id="13da2-218">Можно указать пользовательское имя для контейнера, в котором будет размещаться контейнер Docker, или принять значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="13da2-218">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="13da2-219">Б.</span><span class="sxs-lookup"><span data-stu-id="13da2-219">b.</span></span> <span data-ttu-id="13da2-220">Для узла Docker укажите TCP-порты с помощью следующего синтаксиса: *[внешний порт]*:*[внутренний порт]*.</span><span class="sxs-lookup"><span data-stu-id="13da2-220">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="13da2-221">Например, **80:8080** означает внешний порт "80" и внутренний порт Spring Boot по умолчанию "8080".</span><span class="sxs-lookup"><span data-stu-id="13da2-221">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="13da2-222">После настройки внутреннего порта (например, с помощью файла application.yml) необходимо указать номер порта для обеспечения корректной маршрутизации в Azure.</span><span class="sxs-lookup"><span data-stu-id="13da2-222">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="13da2-223">c.</span><span class="sxs-lookup"><span data-stu-id="13da2-223">c.</span></span> <span data-ttu-id="13da2-224">После настройки этих параметров щелкните **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="13da2-224">After you configure these options, click **Finish**.</span></span>

   ![Развертывание контейнера Docker в Azure][PU07]

1. <span data-ttu-id="13da2-226">После завершения публикации набора средств Azure в журнале действий Azure будет отображаться состояние **Опубликовано**.</span><span class="sxs-lookup"><span data-stu-id="13da2-226">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Успешно развернутый узел Docker][PU08]

## <a name="next-steps"></a><span data-ttu-id="13da2-228">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="13da2-228">Next steps</span></span>

<span data-ttu-id="13da2-229">Дополнительные материалы по Docker доступны на официальном [веб-сайте Docker](https://www.docker.com/).</span><span class="sxs-lookup"><span data-stu-id="13da2-229">For additional resources for Docker, see the official [Docker website](https://www.docker.com/).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: azure-toolkit-for-eclipse-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
