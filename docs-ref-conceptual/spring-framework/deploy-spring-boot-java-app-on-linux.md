---
title: "Развертывание веб-приложения Spring Boot в Linux в Службе контейнеров Azure"
description: "В этом руководстве содержатся пошаговые инструкции по развертыванию приложения Spring Boot в качестве веб-приложения Linux в Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework
ms.assetid: 
ms.service: container-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/01/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 8f7b2cbf66c9ceda6f723a9c9d423d94586fc777
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a><span data-ttu-id="3faea-104">Развертывание приложения Spring Boot в Linux в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="3faea-104">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>

<span data-ttu-id="3faea-105">**[Spring Framework]** — это решение с открытым кодом, которое помогает разработчикам Java создавать приложения корпоративного класса.</span><span class="sxs-lookup"><span data-stu-id="3faea-105">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="3faea-106">Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.</span><span class="sxs-lookup"><span data-stu-id="3faea-106">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="3faea-107">**[Docker]** — это решение с открытым исходным кодом, которое помогает разработчикам автоматизировать развертывание приложений, их масштабирование, а также управление приложениями, которые выполняются в контейнерах.</span><span class="sxs-lookup"><span data-stu-id="3faea-107">**[Docker]** is open-source solutions that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="3faea-108">В этом руководстве рассматривается применение Docker для разработки и развертывания приложения Spring Boot на узле Linux в [Службе контейнеров Azure].</span><span class="sxs-lookup"><span data-stu-id="3faea-108">This tutorial walks you through using Docker to develop and deploy a Spring Boot application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3faea-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3faea-109">Prerequisites</span></span>

<span data-ttu-id="3faea-110">Для работы с этим руководством требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="3faea-110">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="3faea-111">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="3faea-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="3faea-112">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="3faea-112">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="3faea-113">Актуальная версия [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="3faea-113">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="3faea-114">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="3faea-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="3faea-115">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="3faea-115">A [Git] client.</span></span>
* <span data-ttu-id="3faea-116">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="3faea-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="3faea-117">С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="3faea-117">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="3faea-118">Создание веб-приложения Spring Boot в Docker</span><span class="sxs-lookup"><span data-stu-id="3faea-118">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="3faea-119">Ниже приводятся пошаговые инструкции по созданию простого веб-приложения Spring Boot и его локальному тестированию.</span><span class="sxs-lookup"><span data-stu-id="3faea-119">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="3faea-120">Откройте командную строку и создайте локальный каталог для размещения приложения, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="3faea-120">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="3faea-121">-- или --</span><span class="sxs-lookup"><span data-stu-id="3faea-121">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="3faea-122">Клонируйте образец проекта [Spring Boot on Docker Getting Started] (Запуск Spring Boot в Docker) в созданный каталог, например:</span><span class="sxs-lookup"><span data-stu-id="3faea-122">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="3faea-123">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="3faea-123">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="3faea-124">Выполните сборку файла JAR с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="3faea-124">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="3faea-125">После создания веб-приложения перейдите в каталог `target`, где находится JAR-файл, и запустите веб-приложение, например:</span><span class="sxs-lookup"><span data-stu-id="3faea-125">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="3faea-126">Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="3faea-126">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="3faea-127">Например, если у вас установлен CuRL и сервер Tomcat настроен для работы с использованием порта 80:</span><span class="sxs-lookup"><span data-stu-id="3faea-127">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="3faea-128">Должно появиться следующее сообщение: **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="3faea-128">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Локальный просмотр образца приложения][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="3faea-130">Создание реестра контейнеров Azure для использования в качестве частного реестра Docker</span><span class="sxs-lookup"><span data-stu-id="3faea-130">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="3faea-131">Ниже рассмотрена процедура использования портала Azure для создания реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="3faea-131">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="3faea-132">Если вы хотите использовать Azure CLI, а не портал Azure, выполните процедуру, описанную в разделе [Создание частного реестра контейнеров Docker с помощью Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3faea-132">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
>

1. <span data-ttu-id="3faea-133">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="3faea-133">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="3faea-134">После входа в свою учетную запись на портале Azure можно выполнить процедуру, описанную в статье [Создание частного реестра контейнеров Docker с помощью портала Azure], которую здесь полезно представить еще раз.</span><span class="sxs-lookup"><span data-stu-id="3faea-134">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="3faea-135">Щелкните значок меню **+ Создать**, нажмите кнопку **Контейнеры**, а затем нажмите кнопку **Реестр контейнеров Azure**.</span><span class="sxs-lookup"><span data-stu-id="3faea-135">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Создание нового реестра контейнеров Azure][AR01]

1. <span data-ttu-id="3faea-137">При появлении страницы сведений о шаблоне реестра контейнеров Azure нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3faea-137">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Создание нового реестра контейнеров Azure][AR02]

1. <span data-ttu-id="3faea-139">При появлении страницы **Создать реестр контейнеров** введите данные в поля **Имя реестра** и **Группа ресурсов**, выберите **Включить** для параметра **Пользователь-администратор** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3faea-139">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Настройка параметров реестра контейнеров Azure][AR03]

1. <span data-ttu-id="3faea-141">После создания реестра контейнеров перейдите в реестр контейнеров на портале Azure и нажмите кнопку **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="3faea-141">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="3faea-142">Запишите имя пользователя и пароль для последующих шагов.</span><span class="sxs-lookup"><span data-stu-id="3faea-142">Take note of the username and password for the next steps.</span></span>

   ![Ключи доступа к реестру контейнеров Azure][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="3faea-144">Настройка Maven для использования ключей доступа к реестру контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="3faea-144">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="3faea-145">Перейдите в каталог конфигурации для установки Maven и откройте файл *settings.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="3faea-145">Navigate to the configuration directory for your Maven installation and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="3faea-146">Добавьте параметры доступа к реестру контейнеров Azure из предыдущего раздела этого учебника в коллекцию `<servers>` в файле *settings.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="3faea-146">Add your Azure Container Registry access settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="3faea-147">Перейдите в каталог завершенного проекта для приложения Spring Boot (например, *C:\SpringBoot\gs-spring-boot-docker\complete* или */users/robert/SpringBoot/gs-spring-boot-docker/complete*) и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="3faea-147">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="3faea-148">Обновите коллекцию `<properties>` в файле *pom.xml*, добавив значение сервера входа для реестра контейнеров Azure из предыдущего раздела данного учебника, например:</span><span class="sxs-lookup"><span data-stu-id="3faea-148">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="3faea-149">Обновите коллекцию `<plugins>` в файле *pom.xml* таким образом, чтобы в `<plugin>` содержались адрес сервера входа и имя для реестра контейнеров Azure из предыдущего раздела данного учебника.</span><span class="sxs-lookup"><span data-stu-id="3faea-149">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="3faea-150">Например:</span><span class="sxs-lookup"><span data-stu-id="3faea-150">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="3faea-151">Перейдите в каталог завершенного проекта для приложения Spring Boot и выполните команду ниже для перестроения приложения и отправки контейнера в реестр контейнеров Azure:</span><span class="sxs-lookup"><span data-stu-id="3faea-151">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="3faea-152">При отправке контейнера Docker в Azure может появиться сообщение об ошибке, похожее на одно из показанных ниже, даже если контейнер Docker был успешно создан:</span><span class="sxs-lookup"><span data-stu-id="3faea-152">When you are pushing your Docker container to Azure, you may receive an error message that is similar to one of the following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="3faea-153">В этом случае, возможно, потребуется войти в учетную запись Azure из командной строки Docker, например, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="3faea-153">If this happens, you may need to sign in to your Azure account from the Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="3faea-154">Затем контейнер можно передать из командной строки, например:</span><span class="sxs-lookup"><span data-stu-id="3faea-154">You can then push your container from the command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="3faea-155">Создание веб-приложения в Linux в службе приложений Azure с помощью образа контейнера</span><span class="sxs-lookup"><span data-stu-id="3faea-155">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="3faea-156">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="3faea-156">Browse to the [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="3faea-157">Щелкните значок меню **+ Создать**, нажмите кнопку **Интернет + мобильные устройства**, а затем нажмите кнопку **веб-приложения на платформе Linux**.</span><span class="sxs-lookup"><span data-stu-id="3faea-157">Click the menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Создание веб-приложения на портале Azure][LX01]

1. <span data-ttu-id="3faea-159">Когда отобразится страница **Веб-приложение в Linux**, введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="3faea-159">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="3faea-160">а.</span><span class="sxs-lookup"><span data-stu-id="3faea-160">a.</span></span> <span data-ttu-id="3faea-161">Введите уникальное имя в поле **Имя приложения**, например "*wingtiptoyslinux*."</span><span class="sxs-lookup"><span data-stu-id="3faea-161">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="3faea-162">b.</span><span class="sxs-lookup"><span data-stu-id="3faea-162">b.</span></span> <span data-ttu-id="3faea-163">В раскрывающемся списке выберите свою **подписку**.</span><span class="sxs-lookup"><span data-stu-id="3faea-163">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="3faea-164">c.</span><span class="sxs-lookup"><span data-stu-id="3faea-164">c.</span></span> <span data-ttu-id="3faea-165">Выберите существующую **группу ресурсов** или укажите имя, чтобы создать новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3faea-165">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="3faea-166">г)</span><span class="sxs-lookup"><span data-stu-id="3faea-166">d.</span></span> <span data-ttu-id="3faea-167">Нажмите кнопку **Настройка контейнера** и введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="3faea-167">Click **Configure container** and enter the following information:</span></span>

      * <span data-ttu-id="3faea-168">Выберите **Частный реестр**.</span><span class="sxs-lookup"><span data-stu-id="3faea-168">Choose **Private registry**.</span></span>

      * <span data-ttu-id="3faea-169">**Образ и дополнительный тег**: задайте имя контейнера из более ранней версии, например "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span><span class="sxs-lookup"><span data-stu-id="3faea-169">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="3faea-170">**URL-адрес сервера**: укажите URL-адрес реестра из более ранней версии, например "*https://wingtiptoysregistry.azurecr.io*"</span><span class="sxs-lookup"><span data-stu-id="3faea-170">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="3faea-171">**Имя входа пользователя** и **Пароль**: укажите учетные данные для входа из своих **ключей доступа**, которые использовались на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="3faea-171">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="3faea-172">д.</span><span class="sxs-lookup"><span data-stu-id="3faea-172">e.</span></span> <span data-ttu-id="3faea-173">После ввода всех этих данных нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3faea-173">Once you have entered all of the above information, click **OK**.</span></span>

   ![Настройка параметров веб-приложения][LX02]

1. <span data-ttu-id="3faea-175">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3faea-175">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="3faea-176">Azure будет автоматически сопоставлять интернет-запросы со встроенным сервером Tomcat, который использует стандартный порт 80 или 8080.</span><span class="sxs-lookup"><span data-stu-id="3faea-176">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="3faea-177">Однако, если вы настроили свой встроенный сервер Tomcat так, чтобы он работал с пользовательским портом, в веб-приложение необходимо добавить переменную среды, которая определяет порт для вашего встроенного сервера Tomcat.</span><span class="sxs-lookup"><span data-stu-id="3faea-177">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="3faea-178">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3faea-178">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="3faea-179">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="3faea-179">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="3faea-180">Щелкните значок для **служб приложений**.</span><span class="sxs-lookup"><span data-stu-id="3faea-180">Click the icon for **App Services**.</span></span> <span data-ttu-id="3faea-181">(См. элемент ном. 1 на рисунке ниже.)</span><span class="sxs-lookup"><span data-stu-id="3faea-181">(See item #1 in the image below.)</span></span>
>
> 3. <span data-ttu-id="3faea-182">Выберите веб-приложение в списке.</span><span class="sxs-lookup"><span data-stu-id="3faea-182">Select your web app from the list.</span></span> <span data-ttu-id="3faea-183">(Элемент ном. 2 на рисунке ниже.)</span><span class="sxs-lookup"><span data-stu-id="3faea-183">(Item #2 in the image below.)</span></span>
>
> 4. <span data-ttu-id="3faea-184">Щелкните **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="3faea-184">Click **Application Settings**.</span></span> <span data-ttu-id="3faea-185">(Элемент ном. 3 на рисунке ниже.)</span><span class="sxs-lookup"><span data-stu-id="3faea-185">(Item #3 in the image below.)</span></span>
>
> 5. <span data-ttu-id="3faea-186">В разделе **Параметры приложения** добавьте новую переменную среды с именем **PORT** и введите номер пользовательского порта в качестве значения.</span><span class="sxs-lookup"><span data-stu-id="3faea-186">In the **App settings** section, add a new environment variable named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="3faea-187">(Элемент ном. 4 на рисунке ниже.)</span><span class="sxs-lookup"><span data-stu-id="3faea-187">(Item #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="3faea-188">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3faea-188">Click **Save**.</span></span> <span data-ttu-id="3faea-189">(Элемент ном. 5 на рисунке ниже.)</span><span class="sxs-lookup"><span data-stu-id="3faea-189">(Item #5 in the image below.)</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="3faea-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3faea-191">Next steps</span></span>

<span data-ttu-id="3faea-192">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="3faea-192">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="3faea-193">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="3faea-193">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="3faea-194">Развертывание приложения Spring Boot в кластере Kubernetes в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="3faea-194">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="3faea-195">Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [инструментов Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="3faea-195">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="3faea-196">Дополнительные сведения о Spring Boot в образце проекта Docker см. в разделе [Spring Boot on Docker Getting Started] (Начало работы с Spring Boot в Docker).</span><span class="sxs-lookup"><span data-stu-id="3faea-196">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="3faea-197">Справку по началу работы с собственными приложениями Spring Boot см. на странице **Spring Initializr** по адресу https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="3faea-197">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="3faea-198">Дополнительные сведения о начале создания простого приложения Spring Boot см. на странице Spring Initializr по адресу https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="3faea-198">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="3faea-199">Дополнительные примеры использования пользовательских образов Docker в Azure см. в разделе [Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux].</span><span class="sxs-lookup"><span data-stu-id="3faea-199">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Службе контейнеров Azure]: https://azure.microsoft.com/services/container-service/
[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/
[портал Azure]: https://portal.azure.com/
[Создание частного реестра контейнеров Docker с помощью портала Azure]: /azure/container-registry/container-registry-get-started-portal
[Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[инструментов Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

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
