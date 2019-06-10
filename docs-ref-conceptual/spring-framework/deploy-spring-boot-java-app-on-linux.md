---
title: Развертывание веб-приложения Spring Boot в Службе приложений Azure для контейнеров
description: В этом руководстве содержатся пошаговые инструкции по развертыванию приложения Spring Boot в качестве веб-приложения Linux в Microsoft Azure.
services: azure app service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: azure app service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 407b852e24ef88d2fb075bd064f1acf2b107ddc1
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270867"
---
# <a name="deploy-a-spring-boot-application-on-azure-app-service-for-container"></a><span data-ttu-id="9a503-103">Развертывание приложения Spring Boot в Службе приложений Azure для контейнеров</span><span class="sxs-lookup"><span data-stu-id="9a503-103">Deploy a Spring Boot application on Azure App Service for Container</span></span>

<span data-ttu-id="9a503-104">В этом руководстве описано, как использовать [Docker] для включения приложения [Spring Boot] в контейнер и развертывать образ Docker на узле Linux в [Службе контейнеров Azure](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).</span><span class="sxs-lookup"><span data-stu-id="9a503-104">This tutorial walks you through using [Docker] to containerize your [Spring Boot] application and deploy your own docker image to a Linux host in the [Azure App Service](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a503-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9a503-105">Prerequisites</span></span>

<span data-ttu-id="9a503-106">Для работы с этим руководством требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="9a503-106">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="9a503-107">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="9a503-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="9a503-108">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="9a503-108">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="9a503-109">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="9a503-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="9a503-110">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="9a503-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="9a503-111">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="9a503-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="9a503-112">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="9a503-112">A [Git] client.</span></span>
* <span data-ttu-id="9a503-113">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="9a503-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9a503-114">С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="9a503-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="9a503-115">Создание веб-приложения Spring Boot в Docker</span><span class="sxs-lookup"><span data-stu-id="9a503-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="9a503-116">Ниже приводятся пошаговые инструкции по созданию простого веб-приложения Spring Boot и его локальному тестированию.</span><span class="sxs-lookup"><span data-stu-id="9a503-116">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="9a503-117">Откройте командную строку и создайте локальный каталог для размещения приложения, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="9a503-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="9a503-118">-- или --</span><span class="sxs-lookup"><span data-stu-id="9a503-118">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="9a503-119">Клонируйте образец проекта [Spring Boot on Docker Getting Started] (Запуск Spring Boot в Docker) в созданный каталог, например:</span><span class="sxs-lookup"><span data-stu-id="9a503-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="9a503-120">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="9a503-120">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="9a503-121">Выполните сборку файла JAR с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="9a503-121">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="9a503-122">После создания веб-приложения перейдите в каталог `target`, где находится JAR-файл, и запустите веб-приложение, например:</span><span class="sxs-lookup"><span data-stu-id="9a503-122">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="9a503-123">Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="9a503-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="9a503-124">Например, если у вас установлен CuRL и сервер Tomcat настроен для работы с использованием порта 80:</span><span class="sxs-lookup"><span data-stu-id="9a503-124">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="9a503-125">Должно появиться следующее сообщение: **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="9a503-125">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Локальный просмотр образца приложения][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="9a503-127">Создание реестра контейнеров Azure для использования в качестве частного реестра Docker</span><span class="sxs-lookup"><span data-stu-id="9a503-127">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="9a503-128">Ниже рассмотрена процедура использования портала Azure для создания реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="9a503-128">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9a503-129">Если вы хотите использовать Azure CLI, а не портал Azure, выполните процедуру, описанную в разделе [Создание частного реестра контейнеров Docker с помощью Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9a503-129">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
>

1. <span data-ttu-id="9a503-130">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="9a503-130">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="9a503-131">После входа в свою учетную запись на портале Azure можно выполнить процедуру, описанную в статье [Создание частного реестра контейнеров Docker с помощью портала Azure], которую здесь полезно представить еще раз.</span><span class="sxs-lookup"><span data-stu-id="9a503-131">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="9a503-132">Щелкните значок меню **+ Создать**, нажмите кнопку **Контейнеры**, а затем нажмите кнопку **Реестр контейнеров Azure**.</span><span class="sxs-lookup"><span data-stu-id="9a503-132">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Создание нового реестра контейнеров Azure][AR01]

1. <span data-ttu-id="9a503-134">При появлении страницы сведений о шаблоне реестра контейнеров Azure нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9a503-134">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Создание нового реестра контейнеров Azure][AR02]

1. <span data-ttu-id="9a503-136">При появлении страницы **Создать реестр контейнеров** введите данные в поля **Имя реестра** и **Группа ресурсов**, выберите **Включить** для параметра **Пользователь-администратор** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9a503-136">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Настройка параметров реестра контейнеров Azure][AR03]

1. <span data-ttu-id="9a503-138">После создания реестра контейнеров перейдите в реестр контейнеров на портале Azure и нажмите кнопку **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="9a503-138">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="9a503-139">Запишите имя пользователя и пароль для последующих шагов.</span><span class="sxs-lookup"><span data-stu-id="9a503-139">Take note of the username and password for the next steps.</span></span>

   ![Ключи доступа к реестру контейнеров Azure][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="9a503-141">Настройка Maven для использования ключей доступа к реестру контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="9a503-141">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="9a503-142">Перейдите в каталог завершенного проекта для приложения Spring Boot (например "*C:\SpringBoot\gs-spring-boot-docker\complete*" или " */users/robert/SpringBoot/gs-spring-boot-docker/complete*") и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="9a503-142">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="9a503-143">Обновите коллекцию `<properties>` в файле *pom.xml*, добавив последнюю версию [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin), значение сервера входа и параметры доступа для Реестра контейнеров Azure из предыдущего раздела данного учебника.</span><span class="sxs-lookup"><span data-stu-id="9a503-143">Update the `<properties>` collection in the *pom.xml* file with the latest version of [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) and login server value and access settings for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="9a503-144">Например:</span><span class="sxs-lookup"><span data-stu-id="9a503-144">For example:</span></span>

   ```xml
   <properties>
      <jib-maven-plugin.version>1.2.0</jib-maven-plugin.version>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <username>wingtiptoysregistry</username>
      <password>{put your Azure Container Registry access key here}</password>
   </properties>
   ```

1. <span data-ttu-id="9a503-145">Добавьте [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) в коллекцию `<plugins>` в файле *pom.xml*, укажите базовый образ между тегами `<from>/<image>` и имя окончательного образа `<to>/<image>`, а также укажите имя пользователя и пароль из предыдущего раздела между тегами `<to>/<auth>`.</span><span class="sxs-lookup"><span data-stu-id="9a503-145">Add [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) to the `<plugins>` collection in the *pom.xml* file, specify the base image at `<from>/<image>` and  final image name `<to>/<image>`, specify the username and password from previous section at `<to>/<auth>`.</span></span> <span data-ttu-id="9a503-146">Например:</span><span class="sxs-lookup"><span data-stu-id="9a503-146">For example:</span></span>

   ```xml
   <plugin>
     <artifactId>jib-maven-plugin</artifactId>
     <groupId>com.google.cloud.tools</groupId>
     <version>${jib-maven-plugin.version}</version>
     <configuration>
        <from>
            <image>openjdk:8-jre-alpine</image>
        </from>
        <to>
            <image>${docker.image.prefix}/${project.artifactId}</image>
            <auth>
               <username>${username}</username>
               <password>${password}</password>
            </auth>
        </to>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="9a503-147">Перейдите в каталог завершенного проекта для приложения Spring Boot и выполните команду ниже для перестроения приложения и отправки контейнера в реестр контейнеров Azure:</span><span class="sxs-lookup"><span data-stu-id="9a503-147">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```cmd
   mvn compile jib:build
   ```

> [!NOTE]
>
> <span data-ttu-id="9a503-148">При использовании Jib для отправки образа в Реестр контейнеров Azure образ не будет учитывать *Dockerfile* (дополнительные сведения см. в [этом](https://cloudplatform.googleblog.com/2018/07/introducing-jib-build-java-docker-images-better.html) документе).</span><span class="sxs-lookup"><span data-stu-id="9a503-148">When you are using Jib to push your image to the Azure Container Registry, the image will not honor *Dockerfile*, see [this](https://cloudplatform.googleblog.com/2018/07/introducing-jib-build-java-docker-images-better.html) document for details.</span></span>
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="9a503-149">Создание веб-приложения в Linux в службе приложений Azure с помощью образа контейнера</span><span class="sxs-lookup"><span data-stu-id="9a503-149">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="9a503-150">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="9a503-150">Browse to the [Azure portal] and sign in.</span></span>

2. <span data-ttu-id="9a503-151">Щелкните значок меню **+ Создать ресурс**, а затем последовательно выберите **Веб** и **Веб-приложение для контейнеров**.</span><span class="sxs-lookup"><span data-stu-id="9a503-151">Click the menu icon for **+ Create a resource**, then click **Web**, and then click **Web App for Containers**.</span></span>
   
   ![Создание веб-приложения на портале Azure][LX01]

3. <span data-ttu-id="9a503-153">Когда отобразится страница **Веб-приложение в Linux**, введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="9a503-153">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="9a503-154">a.</span><span class="sxs-lookup"><span data-stu-id="9a503-154">a.</span></span> <span data-ttu-id="9a503-155">Введите уникальное имя в поле **Имя приложения**, например *wingtiptoyslinux*.</span><span class="sxs-lookup"><span data-stu-id="9a503-155">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*"</span></span>

   <span data-ttu-id="9a503-156">b.</span><span class="sxs-lookup"><span data-stu-id="9a503-156">b.</span></span> <span data-ttu-id="9a503-157">В раскрывающемся списке выберите свою **подписку**.</span><span class="sxs-lookup"><span data-stu-id="9a503-157">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="9a503-158">c.</span><span class="sxs-lookup"><span data-stu-id="9a503-158">c.</span></span> <span data-ttu-id="9a503-159">Выберите существующую **группу ресурсов** или укажите имя, чтобы создать новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9a503-159">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="9a503-160">d.</span><span class="sxs-lookup"><span data-stu-id="9a503-160">d.</span></span> <span data-ttu-id="9a503-161">В качестве **ОС** выберите *Linux*.</span><span class="sxs-lookup"><span data-stu-id="9a503-161">Choose *Linux* as the **OS**.</span></span>

   <span data-ttu-id="9a503-162">д.</span><span class="sxs-lookup"><span data-stu-id="9a503-162">e.</span></span> <span data-ttu-id="9a503-163">Щелкните **План службы приложений или расположение** и выберите существующий план службы приложений или щелкните **Создать**, чтобы создать другой план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="9a503-163">Click **App Service plan/Location** and choose an existing app service plan, or click **Create new** to create a new app service plan.</span></span>

   <span data-ttu-id="9a503-164">Е.</span><span class="sxs-lookup"><span data-stu-id="9a503-164">f.</span></span> <span data-ttu-id="9a503-165">Нажмите кнопку **Настройка контейнера** и введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="9a503-165">Click **Configure container** and enter the following information:</span></span>

   * <span data-ttu-id="9a503-166">Выберите **Один контейнер** и **Реестр контейнеров Azure**.</span><span class="sxs-lookup"><span data-stu-id="9a503-166">Choose **Single Container** and  **Azure Container Registry**.</span></span>

   * <span data-ttu-id="9a503-167">**Реестр**: Выберите имя контейнера, созданное ранее, например *wingtiptoysregistry*.</span><span class="sxs-lookup"><span data-stu-id="9a503-167">**Registry**: Choose your container name created earlier; for example: "*wingtiptoysregistry*"</span></span>

   * <span data-ttu-id="9a503-168">**Образ**. Выберите имя образа, например *gs-spring-boot-docker*.</span><span class="sxs-lookup"><span data-stu-id="9a503-168">**Image**: Choose the image name; for example: "*gs-spring-boot-docker*"</span></span>
   
   * <span data-ttu-id="9a503-169">**Тег**. Выберите тег для образа, например *latest*.</span><span class="sxs-lookup"><span data-stu-id="9a503-169">**Tag**: Choose the tag for the image; for example: "*latest*"</span></span>
   
   * <span data-ttu-id="9a503-170">**Загрузочный файл**. Оставьте это поле пустым, так как образ уже включает команду запуска.</span><span class="sxs-lookup"><span data-stu-id="9a503-170">**Startup File**: Keep it blank since the image already has the start up command</span></span>
   
   <span data-ttu-id="9a503-171">д.</span><span class="sxs-lookup"><span data-stu-id="9a503-171">e.</span></span> <span data-ttu-id="9a503-172">После ввода всех этих данных нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="9a503-172">Once you have entered all of the above information, click **Apply**.</span></span>

   ![Настройка параметров веб-приложения][LX02]

4. <span data-ttu-id="9a503-174">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9a503-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9a503-175">Azure будет автоматически сопоставлять интернет-запросы со встроенным сервером Tomcat, который использует стандартный порт 80 или 8080.</span><span class="sxs-lookup"><span data-stu-id="9a503-175">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="9a503-176">Однако, если вы настроили свой встроенный сервер Tomcat так, чтобы он работал с пользовательским портом, в веб-приложение необходимо добавить переменную среды, которая определяет порт для вашего встроенного сервера Tomcat.</span><span class="sxs-lookup"><span data-stu-id="9a503-176">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="9a503-177">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9a503-177">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="9a503-178">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="9a503-178">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="9a503-179">Щелкните значок для **Службы приложений** и выберите веб-приложение из списка.</span><span class="sxs-lookup"><span data-stu-id="9a503-179">Click the icon for **App Services**, and select your web app from the list.</span></span>
>
> 4. <span data-ttu-id="9a503-180">Щелкните **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="9a503-180">Click **Configuration**.</span></span> <span data-ttu-id="9a503-181">(Элемент 1 на приведенном ниже рисунке.)</span><span class="sxs-lookup"><span data-stu-id="9a503-181">(Item #1 in the image below.)</span></span>
>
> 5. <span data-ttu-id="9a503-182">В разделе **Параметры приложения** добавьте новый параметр с именем **PORT** и введите номер пользовательского порта в качестве значения.</span><span class="sxs-lookup"><span data-stu-id="9a503-182">In the **Application settings** section, add a new setting named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="9a503-183">(Элементы 2, 3, 4 на приведенном ниже рисунке.)</span><span class="sxs-lookup"><span data-stu-id="9a503-183">(Item #2, #3, #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="9a503-184">Выберите команду **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9a503-184">Click **Save**.</span></span> <span data-ttu-id="9a503-185">(Элемент ном. 5 на рисунке ниже.)</span><span class="sxs-lookup"><span data-stu-id="9a503-185">(Item #5 in the image below.)</span></span>
>
> ![Сохранение номера пользовательского порта на портале Azure][LX03]
>

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="9a503-187">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="9a503-187">Next steps</span></span>

<span data-ttu-id="9a503-188">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="9a503-188">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a503-189">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="9a503-189">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="9a503-190">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9a503-190">Additional Resources</span></span>

<span data-ttu-id="9a503-191">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="9a503-191">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="9a503-192">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9a503-192">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="9a503-193">Развертывание приложения Spring Boot в кластере Kubernetes в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="9a503-193">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="9a503-194">Дополнительные сведения об использовании Java в Azure см. в статьях [Azure для разработчиков Java] и [Working with Azure DevOps and Java] (Работа с Azure DevOps и Java).</span><span class="sxs-lookup"><span data-stu-id="9a503-194">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="9a503-195">Дополнительные сведения о Spring Boot в образце проекта Docker см. в разделе [Spring Boot on Docker Getting Started] (Начало работы с Spring Boot в Docker).</span><span class="sxs-lookup"><span data-stu-id="9a503-195">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="9a503-196">Справку по началу работы с собственными приложениями Spring Boot см. на странице **Spring Initializr**: https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="9a503-196">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="9a503-197">Дополнительные сведения о создании простого приложения Spring Boot см. на странице Spring Initializr: https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="9a503-197">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="9a503-198">Дополнительные примеры использования пользовательских образов Docker в Azure см. в разделе [Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux].</span><span class="sxs-lookup"><span data-stu-id="9a503-198">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure для разработчиков Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[портал Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Создание частного реестра контейнеров Docker с помощью портала Azure]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/java/ (Работа с Azure DevOps и Java)
[Maven]: http://maven.apache.org/
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-linux/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-linux/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-linux/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-linux/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-linux/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-linux/AR04.png

[LX01]: ./media/deploy-spring-boot-java-app-on-linux/LX01.png
[LX02]: ./media/deploy-spring-boot-java-app-on-linux/LX02.png
[LX03]: ./media/deploy-spring-boot-java-app-on-linux/LX03.png
