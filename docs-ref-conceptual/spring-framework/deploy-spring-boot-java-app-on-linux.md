---
title: Развертывание веб-приложения Spring Boot в Linux в Службе контейнеров Azure
description: В этом руководстве содержатся пошаговые инструкции по развертыванию приложения Spring Boot в качестве веб-приложения Linux в Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 30be16aebb18e3c9e18f9a023ea9b82e5d614e94
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339148"
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a><span data-ttu-id="79be5-103">Развертывание приложения Spring Boot в Linux в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="79be5-103">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>

<span data-ttu-id="79be5-104">В этом руководстве описано, как использовать [Docker] для разработки и развертывания приложения [Spring Boot] на узле Linux в [Служба контейнеров Azure].</span><span class="sxs-lookup"><span data-stu-id="79be5-104">This tutorial walks you through using [Docker] to develop and deploy a [Spring Boot] application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79be5-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="79be5-105">Prerequisites</span></span>

<span data-ttu-id="79be5-106">Для работы с этим руководством требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="79be5-106">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="79be5-107">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="79be5-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="79be5-108">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="79be5-108">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="79be5-109">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="79be5-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="79be5-110">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="79be5-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="79be5-111">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="79be5-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="79be5-112">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="79be5-112">A [Git] client.</span></span>
* <span data-ttu-id="79be5-113">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="79be5-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="79be5-114">С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="79be5-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="79be5-115">Создание веб-приложения Spring Boot в Docker</span><span class="sxs-lookup"><span data-stu-id="79be5-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="79be5-116">Ниже приводятся пошаговые инструкции по созданию простого веб-приложения Spring Boot и его локальному тестированию.</span><span class="sxs-lookup"><span data-stu-id="79be5-116">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="79be5-117">Откройте командную строку и создайте локальный каталог для размещения приложения, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="79be5-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="79be5-118">-- или --</span><span class="sxs-lookup"><span data-stu-id="79be5-118">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="79be5-119">Клонируйте образец проекта [Spring Boot on Docker Getting Started] (Запуск Spring Boot в Docker) в созданный каталог, например:</span><span class="sxs-lookup"><span data-stu-id="79be5-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="79be5-120">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="79be5-120">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="79be5-121">Выполните сборку файла JAR с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="79be5-121">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="79be5-122">После создания веб-приложения перейдите в каталог `target`, где находится JAR-файл, и запустите веб-приложение, например:</span><span class="sxs-lookup"><span data-stu-id="79be5-122">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="79be5-123">Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="79be5-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="79be5-124">Например, если у вас установлен CuRL и сервер Tomcat настроен для работы с использованием порта 80:</span><span class="sxs-lookup"><span data-stu-id="79be5-124">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="79be5-125">Должно появиться следующее сообщение: **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="79be5-125">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Локальный просмотр образца приложения][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="79be5-127">Создание реестра контейнеров Azure для использования в качестве частного реестра Docker</span><span class="sxs-lookup"><span data-stu-id="79be5-127">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="79be5-128">Ниже рассмотрена процедура использования портала Azure для создания реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="79be5-128">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="79be5-129">Если вы хотите использовать Azure CLI, а не портал Azure, выполните процедуру, описанную в разделе [Создание частного реестра контейнеров Docker с помощью Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="79be5-129">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
>

1. <span data-ttu-id="79be5-130">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="79be5-130">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="79be5-131">После входа в свою учетную запись на портале Azure можно выполнить процедуру, описанную в статье [Создание частного реестра контейнеров Docker с помощью портала Azure], которую здесь полезно представить еще раз.</span><span class="sxs-lookup"><span data-stu-id="79be5-131">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="79be5-132">Щелкните значок меню **+ Создать**, нажмите кнопку **Контейнеры**, а затем нажмите кнопку **Реестр контейнеров Azure**.</span><span class="sxs-lookup"><span data-stu-id="79be5-132">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Создание нового реестра контейнеров Azure][AR01]

1. <span data-ttu-id="79be5-134">При появлении страницы сведений о шаблоне реестра контейнеров Azure нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="79be5-134">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Создание нового реестра контейнеров Azure][AR02]

1. <span data-ttu-id="79be5-136">При появлении страницы **Создать реестр контейнеров** введите данные в поля **Имя реестра** и **Группа ресурсов**, выберите **Включить** для параметра **Пользователь-администратор** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="79be5-136">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Настройка параметров реестра контейнеров Azure][AR03]

1. <span data-ttu-id="79be5-138">После создания реестра контейнеров перейдите в реестр контейнеров на портале Azure и нажмите кнопку **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="79be5-138">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="79be5-139">Запишите имя пользователя и пароль для последующих шагов.</span><span class="sxs-lookup"><span data-stu-id="79be5-139">Take note of the username and password for the next steps.</span></span>

   ![Ключи доступа к реестру контейнеров Azure][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="79be5-141">Настройка Maven для использования ключей доступа к реестру контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="79be5-141">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="79be5-142">Перейдите в каталог конфигурации для установки Maven и откройте файл *settings.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="79be5-142">Navigate to the configuration directory for your Maven installation and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="79be5-143">Добавьте параметры доступа к реестру контейнеров Azure из предыдущего раздела этого учебника в коллекцию `<servers>` в файле *settings.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="79be5-143">Add your Azure Container Registry access settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="79be5-144">Перейдите в каталог завершенного проекта для приложения Spring Boot (например, *C:\SpringBoot\gs-spring-boot-docker\complete* или */users/robert/SpringBoot/gs-spring-boot-docker/complete*) и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="79be5-144">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="79be5-145">Обновите коллекцию `<properties>` в файле *pom.xml*, добавив значение сервера входа для реестра контейнеров Azure из предыдущего раздела данного учебника, например:</span><span class="sxs-lookup"><span data-stu-id="79be5-145">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="79be5-146">Обновите коллекцию `<plugins>` в файле *pom.xml* таким образом, чтобы в `<plugin>` содержались адрес сервера входа и имя для реестра контейнеров Azure из предыдущего раздела данного учебника.</span><span class="sxs-lookup"><span data-stu-id="79be5-146">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="79be5-147">Например: </span><span class="sxs-lookup"><span data-stu-id="79be5-147">For example:</span></span>

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

1. <span data-ttu-id="79be5-148">Перейдите в каталог завершенного проекта для приложения Spring Boot и выполните команду ниже для перестроения приложения и отправки контейнера в реестр контейнеров Azure:</span><span class="sxs-lookup"><span data-stu-id="79be5-148">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="79be5-149">При отправке контейнера Docker в Azure может появиться сообщение об ошибке, похожее на одно из показанных ниже, даже если контейнер Docker был успешно создан:</span><span class="sxs-lookup"><span data-stu-id="79be5-149">When you are pushing your Docker container to Azure, you may receive an error message that is similar to one of the following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="79be5-150">В этом случае, возможно, потребуется войти в учетную запись Azure из командной строки Docker, например, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="79be5-150">If this happens, you may need to sign in to your Azure account from the Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="79be5-151">Затем контейнер можно передать из командной строки, например:</span><span class="sxs-lookup"><span data-stu-id="79be5-151">You can then push your container from the command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="79be5-152">Создание веб-приложения в Linux в службе приложений Azure с помощью образа контейнера</span><span class="sxs-lookup"><span data-stu-id="79be5-152">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="79be5-153">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="79be5-153">Browse to the [Azure portal] and sign in.</span></span>

2. <span data-ttu-id="79be5-154">Щелкните значок меню **+ Создать**, нажмите кнопку **Интернет + мобильные устройства**, а затем нажмите кнопку **веб-приложения на платформе Linux**.</span><span class="sxs-lookup"><span data-stu-id="79be5-154">Click the menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Создание веб-приложения на портале Azure][LX01]

3. <span data-ttu-id="79be5-156">Когда отобразится страница **Веб-приложение в Linux**, введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="79be5-156">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="79be5-157">a.</span><span class="sxs-lookup"><span data-stu-id="79be5-157">a.</span></span> <span data-ttu-id="79be5-158">Введите уникальное имя в поле **Имя приложения**, например "*wingtiptoyslinux*."</span><span class="sxs-lookup"><span data-stu-id="79be5-158">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="79be5-159">b.</span><span class="sxs-lookup"><span data-stu-id="79be5-159">b.</span></span> <span data-ttu-id="79be5-160">В раскрывающемся списке выберите свою **подписку**.</span><span class="sxs-lookup"><span data-stu-id="79be5-160">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="79be5-161">c.</span><span class="sxs-lookup"><span data-stu-id="79be5-161">c.</span></span> <span data-ttu-id="79be5-162">Выберите существующую **группу ресурсов** или укажите имя, чтобы создать новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="79be5-162">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="79be5-163">d.</span><span class="sxs-lookup"><span data-stu-id="79be5-163">d.</span></span> <span data-ttu-id="79be5-164">Нажмите кнопку **Настройка контейнера** и введите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="79be5-164">Click **Configure container** and enter the following information:</span></span>

   * <span data-ttu-id="79be5-165">Выберите **Частный реестр**.</span><span class="sxs-lookup"><span data-stu-id="79be5-165">Choose **Private registry**.</span></span>

   * <span data-ttu-id="79be5-166">**Образ и дополнительный тег**: задайте имя контейнера из более ранней версии, например "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span><span class="sxs-lookup"><span data-stu-id="79be5-166">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

   * <span data-ttu-id="79be5-167">**URL-адрес сервера**: укажите URL-адрес реестра из более ранней версии, например *<https://wingtiptoysregistry.azurecr.io>*.</span><span class="sxs-lookup"><span data-stu-id="79be5-167">**Server URL**: Specify your registry URL from earlier; for example: "*<https://wingtiptoysregistry.azurecr.io>*"</span></span>

   * <span data-ttu-id="79be5-168">**Имя входа пользователя** и **Пароль**: укажите учетные данные для входа из своих **ключей доступа**, которые использовались на предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="79be5-168">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="79be5-169">д.</span><span class="sxs-lookup"><span data-stu-id="79be5-169">e.</span></span> <span data-ttu-id="79be5-170">После ввода всех этих данных нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="79be5-170">Once you have entered all of the above information, click **OK**.</span></span>

   ![Настройка параметров веб-приложения][LX02]

4. <span data-ttu-id="79be5-172">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="79be5-172">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="79be5-173">Azure будет автоматически сопоставлять интернет-запросы со встроенным сервером Tomcat, который использует стандартный порт 80 или 8080.</span><span class="sxs-lookup"><span data-stu-id="79be5-173">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="79be5-174">Однако, если вы настроили свой встроенный сервер Tomcat так, чтобы он работал с пользовательским портом, в веб-приложение необходимо добавить переменную среды, которая определяет порт для вашего встроенного сервера Tomcat.</span><span class="sxs-lookup"><span data-stu-id="79be5-174">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="79be5-175">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="79be5-175">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="79be5-176">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="79be5-176">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="79be5-177">Щелкните значок для **служб приложений**.</span><span class="sxs-lookup"><span data-stu-id="79be5-177">Click the icon for **App Services**.</span></span> <span data-ttu-id="79be5-178">(См. элемент ном. 1 на рисунке ниже.)</span><span class="sxs-lookup"><span data-stu-id="79be5-178">(See item #1 in the image below.)</span></span>
>
> 3. <span data-ttu-id="79be5-179">Выберите веб-приложение в списке.</span><span class="sxs-lookup"><span data-stu-id="79be5-179">Select your web app from the list.</span></span> <span data-ttu-id="79be5-180">(Элемент ном. 2 на рисунке ниже.)</span><span class="sxs-lookup"><span data-stu-id="79be5-180">(Item #2 in the image below.)</span></span>
>
> 4. <span data-ttu-id="79be5-181">Щелкните **Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="79be5-181">Click **Application Settings**.</span></span> <span data-ttu-id="79be5-182">(Элемент ном. 3 на рисунке ниже.)</span><span class="sxs-lookup"><span data-stu-id="79be5-182">(Item #3 in the image below.)</span></span>
>
> 5. <span data-ttu-id="79be5-183">В разделе **Параметры приложения** добавьте новую переменную среды с именем **PORT** и введите номер пользовательского порта в качестве значения.</span><span class="sxs-lookup"><span data-stu-id="79be5-183">In the **App settings** section, add a new environment variable named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="79be5-184">(Элемент ном. 4 на рисунке ниже.)</span><span class="sxs-lookup"><span data-stu-id="79be5-184">(Item #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="79be5-185">Выберите команду **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="79be5-185">Click **Save**.</span></span> <span data-ttu-id="79be5-186">(Элемент ном. 5 на рисунке ниже.)</span><span class="sxs-lookup"><span data-stu-id="79be5-186">(Item #5 in the image below.)</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="79be5-188">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="79be5-188">Next steps</span></span>

<span data-ttu-id="79be5-189">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="79be5-189">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="79be5-190">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="79be5-190">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="79be5-191">Развертывание приложения Spring Boot в кластере Kubernetes в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="79be5-191">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="79be5-192">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="79be5-192">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="79be5-193">Дополнительные сведения о Spring Boot в образце проекта Docker см. в разделе [Spring Boot on Docker Getting Started] (Начало работы с Spring Boot в Docker).</span><span class="sxs-lookup"><span data-stu-id="79be5-193">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="79be5-194">Справку по началу работы с собственными приложениями Spring Boot см. на странице **Spring Initializr**: https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="79be5-194">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="79be5-195">Дополнительные сведения о создании простого приложения Spring Boot см. на странице Spring Initializr: https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="79be5-195">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="79be5-196">Дополнительные примеры использования пользовательских образов Docker в Azure см. в разделе [Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux].</span><span class="sxs-lookup"><span data-stu-id="79be5-196">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Служба контейнеров Azure]: https://azure.microsoft.com/services/container-service/
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
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
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
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
