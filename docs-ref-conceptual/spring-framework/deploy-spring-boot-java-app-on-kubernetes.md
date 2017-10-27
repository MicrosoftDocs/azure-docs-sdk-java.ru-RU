---
title: "Развертывание приложения Spring Boot в Kubernetes в Службе контейнеров Azure"
description: "В этом руководстве содержатся пошаговые инструкции по развертыванию приложения Spring Boot в кластере Kubernetes в Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Kubernetes
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 44c20e9084d53fa366137fc191726aaa4be177f2
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a><span data-ttu-id="b0b35-104">Развертывание приложения Spring Boot в кластере Kubernetes в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="b0b35-104">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>

<span data-ttu-id="b0b35-105">**[Spring Framework]** — это популярная платформа с открытым кодом, которая помогает Java-разработчикам создавать мобильные приложения, веб-приложения и приложения API.</span><span class="sxs-lookup"><span data-stu-id="b0b35-105">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="b0b35-106">В этом руководстве для удобства используется пример приложения, созданный с помощью [Spring Boot] — подхода к использованию Spring на основе соглашений.</span><span class="sxs-lookup"><span data-stu-id="b0b35-106">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="b0b35-107">**[Kubernetes]** и **[Docker]** — это решения с открытым кодом, которые помогают разработчикам автоматизировать развертывание и масштабирование выполняемых в контейнере приложений, а также управление ими.</span><span class="sxs-lookup"><span data-stu-id="b0b35-107">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="b0b35-108">В этом руководстве представлены пошаговые инструкции по объединению этих двух популярных технологий с открытым кодом для разработки и развертывания приложения Spring Boot в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b35-108">This tutorial walks you though combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="b0b35-109">В частности *[Spring Boot]* используется для разработки приложения, *[Kubernetes]* — для развертывания контейнера, а [служба контейнеров Azure (ACS)] — для размещения приложения.</span><span class="sxs-lookup"><span data-stu-id="b0b35-109">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Container Service (ACS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b0b35-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b0b35-110">Prerequisites</span></span>

* <span data-ttu-id="b0b35-111">Подписка Azure. Если у вас ее еще нет, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="b0b35-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="b0b35-112">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="b0b35-112">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="b0b35-113">Актуальная версия [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="b0b35-113">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="b0b35-114">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="b0b35-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="b0b35-115">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="b0b35-115">A [Git] client.</span></span>
* <span data-ttu-id="b0b35-116">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="b0b35-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b0b35-117">С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="b0b35-117">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="b0b35-118">Создание веб-приложения Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="b0b35-118">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="b0b35-119">Ниже представлены инструкции по созданию веб-приложения Spring Boot и его локальному тестированию.</span><span class="sxs-lookup"><span data-stu-id="b0b35-119">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="b0b35-120">Откройте командную строку и создайте локальный каталог для размещения приложения, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="b0b35-120">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="b0b35-121">-- или --</span><span class="sxs-lookup"><span data-stu-id="b0b35-121">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="b0b35-122">Клонируйте пример проекта [Spring Boot on Docker Getting Started] в каталог.</span><span class="sxs-lookup"><span data-stu-id="b0b35-122">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="b0b35-123">Перейдите в каталог готового проекта.</span><span class="sxs-lookup"><span data-stu-id="b0b35-123">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="b0b35-124">Используйте Maven для создания и запуска примера приложения.</span><span class="sxs-lookup"><span data-stu-id="b0b35-124">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="b0b35-125">Чтобы протестировать веб-приложение, перейдите по адресу http://localhost:8080 или введите команду `curl`:</span><span class="sxs-lookup"><span data-stu-id="b0b35-125">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="b0b35-126">Должно появиться следующее сообщение: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="b0b35-126">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Просмотр примера приложения в локальной среде][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="b0b35-128">Создание реестра контейнеров Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b0b35-128">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="b0b35-129">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="b0b35-129">Open a command prompt.</span></span>

1. <span data-ttu-id="b0b35-130">Войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b35-130">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="b0b35-131">Создайте группу ресурсов Azure, используемых в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="b0b35-131">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="b0b35-132">Создайте частный реестр контейнеров Azure в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b0b35-132">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="b0b35-133">Позднее в руководстве пример принудительно отправляется в этот реестр как образ Docker.</span><span class="sxs-lookup"><span data-stu-id="b0b35-133">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="b0b35-134">Замените `wingtiptoysregistry` уникальным именем для реестра.</span><span class="sxs-lookup"><span data-stu-id="b0b35-134">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="b0b35-135">Принудительная отправка приложения в реестр контейнеров</span><span class="sxs-lookup"><span data-stu-id="b0b35-135">Push your app to the container registry</span></span>

1. <span data-ttu-id="b0b35-136">Перейдите в каталог конфигурации для установки Maven (по умолчанию ~/.m2/ или C:\Users\username\.m2) и откройте файл *settings.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="b0b35-136">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="b0b35-137">Получите пароль для реестра контейнеров из Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b0b35-137">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="b0b35-138">Добавьте идентификатор и пароль реестра контейнеров Azure для новой коллекции `<server>` в файле *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="b0b35-138">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="b0b35-139">`id` и `username` — это имена реестра.</span><span class="sxs-lookup"><span data-stu-id="b0b35-139">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="b0b35-140">Используйте значение `password` из предыдущей команды (без кавычек).</span><span class="sxs-lookup"><span data-stu-id="b0b35-140">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="b0b35-141">Перейдите в каталог завершенного проекта для приложения Spring Boot (например, *C:\SpringBoot\gs-spring-boot-docker\complete* или */users/robert/SpringBoot/gs-spring-boot-docker/complete*) и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="b0b35-141">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="b0b35-142">Обновите коллекцию `<properties>` в файле *pom.xml*, добавив значение сервера входа для реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b35-142">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="b0b35-143">Обновите коллекцию `<plugins>` в файле *pom.xml* таким образом, чтобы в `<plugin>` содержались адрес сервера входа и имя реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b35-143">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="b0b35-144">Перейдите в каталог завершенного проекта для приложения Spring Boot и выполните указанную ниже команду для создания контейнера Docker и отправки образа в реестр:</span><span class="sxs-lookup"><span data-stu-id="b0b35-144">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="b0b35-145">При отправке образа из Maven в Azure может появиться сообщение об ошибке такого типа:</span><span class="sxs-lookup"><span data-stu-id="b0b35-145">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="b0b35-146">При возникновении этой ошибки войдите в Azure из командной строки Docker.</span><span class="sxs-lookup"><span data-stu-id="b0b35-146">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="b0b35-147">Затем принудительно отправьте контейнер:</span><span class="sxs-lookup"><span data-stu-id="b0b35-147">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-the-azure-cli"></a><span data-ttu-id="b0b35-148">Создание в ACS кластера Kubernetes с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b0b35-148">Create a Kubernetes Cluster on ACS using the Azure CLI</span></span>

1. <span data-ttu-id="b0b35-149">Создайте кластер Kubernetes в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b35-149">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="b0b35-150">Следующая команда отвечает за создание кластера *kubernetes* в группе ресурсов *wingtiptoys-kubernetes* с именем кластера *wingtiptoys-containerservice* и префиксом DNS *wingtiptoys kubernetes*:</span><span class="sxs-lookup"><span data-stu-id="b0b35-150">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="b0b35-151">Выполнение этой команды может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="b0b35-151">This command may take a while to complete.</span></span>

1. <span data-ttu-id="b0b35-152">Установите `kubectl` с использованием Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b0b35-152">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="b0b35-153">Пользователи Linux могут добавить к этой команде префикс `sudo`, так как она развертывает интерфейс командной строки Kubernetes в `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="b0b35-153">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="b0b35-154">Скачайте сведения о конфигурации кластера, чтобы управлять им из веб-интерфейса Kubernetes и `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="b0b35-154">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="b0b35-155">Развертывание образа в кластере Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b0b35-155">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="b0b35-156">В этом руководстве с помощью `kubectl` развертывается приложение, а затем предоставляется возможность изучить развертывание с помощью веб-интерфейса Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b0b35-156">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="b0b35-157">Развертывание с помощью веб-интерфейса Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b0b35-157">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="b0b35-158">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="b0b35-158">Open a command prompt.</span></span>

1. <span data-ttu-id="b0b35-159">Откройте веб-сайт конфигурации кластера Kubernetes в браузере по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="b0b35-159">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="b0b35-160">Когда в браузере откроется веб-сайт конфигурации Kubernetes, щелкните ссылку, чтобы **развернуть контейнерное приложение**:</span><span class="sxs-lookup"><span data-stu-id="b0b35-160">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Веб-сайт конфигурации Kubernetes][KB01]

1. <span data-ttu-id="b0b35-162">Когда отобразится страница **Deploy a containerized app** (Развернуть контейнерное приложение), укажите следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="b0b35-162">When the **Deploy a containerized app** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="b0b35-163">а.</span><span class="sxs-lookup"><span data-stu-id="b0b35-163">a.</span></span> <span data-ttu-id="b0b35-164">Выберите **Specify app details below** (Указать сведения о приложении ниже).</span><span class="sxs-lookup"><span data-stu-id="b0b35-164">Select **Specify app details below**.</span></span>

   <span data-ttu-id="b0b35-165">b.</span><span class="sxs-lookup"><span data-stu-id="b0b35-165">b.</span></span> <span data-ttu-id="b0b35-166">Укажите имя приложения Spring Boot в поле **Имя приложения** (например, *gs-spring-boot-docker*).</span><span class="sxs-lookup"><span data-stu-id="b0b35-166">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="b0b35-167">c.</span><span class="sxs-lookup"><span data-stu-id="b0b35-167">c.</span></span> <span data-ttu-id="b0b35-168">Укажите сервер входа и образ контейнера, заданные ранее, в поле **Образ контейнера** (например, *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*).</span><span class="sxs-lookup"><span data-stu-id="b0b35-168">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="b0b35-169">г)</span><span class="sxs-lookup"><span data-stu-id="b0b35-169">d.</span></span> <span data-ttu-id="b0b35-170">Для параметра **Служба** выберите значение **Внешняя**.</span><span class="sxs-lookup"><span data-stu-id="b0b35-170">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="b0b35-171">д.</span><span class="sxs-lookup"><span data-stu-id="b0b35-171">e.</span></span> <span data-ttu-id="b0b35-172">Укажите внешний и внутренний порты в текстовых полях **Порт** и **Целевой порт**.</span><span class="sxs-lookup"><span data-stu-id="b0b35-172">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Веб-сайт конфигурации Kubernetes][KB02]


1. <span data-ttu-id="b0b35-174">Нажмите кнопку **Развернуть**, чтобы развернуть контейнер.</span><span class="sxs-lookup"><span data-stu-id="b0b35-174">Click **Deploy** to deploy the container.</span></span>

   ![Развертывание контейнера][KB05]

1. <span data-ttu-id="b0b35-176">После развертывания приложение Spring Boot отобразится в списке **Службы**.</span><span class="sxs-lookup"><span data-stu-id="b0b35-176">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Службы Kubernetes][KB06]

1. <span data-ttu-id="b0b35-178">Щелкнув ссылку для **внешних конечных точек**, можно просмотреть сведения о выполнении приложения Spring Boot в Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b35-178">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Службы Kubernetes][KB07]

   ![Просмотр примера приложения в Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="b0b35-181">Развертывание с помощью kubectl</span><span class="sxs-lookup"><span data-stu-id="b0b35-181">Deploy with kubectl</span></span>

1. <span data-ttu-id="b0b35-182">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="b0b35-182">Open a command prompt.</span></span>

1. <span data-ttu-id="b0b35-183">Запустите контейнер в кластере Kubernetes с помощью команды `kubectl run`.</span><span class="sxs-lookup"><span data-stu-id="b0b35-183">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="b0b35-184">Присвойте приложению имя службы в Kubernetes и полное имя образа.</span><span class="sxs-lookup"><span data-stu-id="b0b35-184">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="b0b35-185">Например:</span><span class="sxs-lookup"><span data-stu-id="b0b35-185">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="b0b35-186">В этой команде:</span><span class="sxs-lookup"><span data-stu-id="b0b35-186">In this command:</span></span>

   * <span data-ttu-id="b0b35-187">Имя контейнера `gs-spring-boot-docker` указано сразу после команды `run`.</span><span class="sxs-lookup"><span data-stu-id="b0b35-187">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="b0b35-188">Параметр `--image` указывает объединенное имя сервера входа и образа как `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`.</span><span class="sxs-lookup"><span data-stu-id="b0b35-188">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="b0b35-189">Предоставьте кластер Kubernetes извне с помощью команды `kubectl expose`.</span><span class="sxs-lookup"><span data-stu-id="b0b35-189">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="b0b35-190">Укажите имя службы, общедоступный TCP-порт, используемый для доступа к приложению, и внутренний целевой порт, прослушиваемый приложением.</span><span class="sxs-lookup"><span data-stu-id="b0b35-190">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="b0b35-191">Например:</span><span class="sxs-lookup"><span data-stu-id="b0b35-191">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="b0b35-192">В этой команде:</span><span class="sxs-lookup"><span data-stu-id="b0b35-192">In this command:</span></span>

   * <span data-ttu-id="b0b35-193">Имя контейнера `gs-spring-boot-docker` указано сразу после команды `expose deployment`.</span><span class="sxs-lookup"><span data-stu-id="b0b35-193">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="b0b35-194">Параметр `--type` указывает, что кластер использует подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="b0b35-194">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="b0b35-195">Параметр `--port` указывает общедоступный TCP-порт 80.</span><span class="sxs-lookup"><span data-stu-id="b0b35-195">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="b0b35-196">Через этот порт вы осуществляете доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="b0b35-196">You access the app on this port.</span></span>

   * <span data-ttu-id="b0b35-197">Параметр `--target-port` указывает общедоступный TCP-порт 8080.</span><span class="sxs-lookup"><span data-stu-id="b0b35-197">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="b0b35-198">Через этот порт подсистема балансировки нагрузки переадресовывает запросы к приложению.</span><span class="sxs-lookup"><span data-stu-id="b0b35-198">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="b0b35-199">После развертывания приложения в кластере подайте запрос на внешний IP-адрес и откройте его в своем веб-браузере:</span><span class="sxs-lookup"><span data-stu-id="b0b35-199">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Просмотр примера приложения в Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="b0b35-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b0b35-201">Next steps</span></span>

<span data-ttu-id="b0b35-202">Дополнительные сведения об использовании Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="b0b35-202">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="b0b35-203">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="b0b35-203">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="b0b35-204">Развертывание приложения Spring Boot в Linux в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="b0b35-204">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)

<span data-ttu-id="b0b35-205">Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [инструментов Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="b0b35-205">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="b0b35-206">Дополнительные сведения о примере проекта Spring Boot в Docker см. в разделе [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="b0b35-206">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="b0b35-207">По следующим ссылкам представлены дополнительные сведения о создании приложений Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="b0b35-207">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="b0b35-208">Дополнительные сведения о создании простого приложения Spring Boot см. на странице Spring Initializr по адресу https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="b0b35-208">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="b0b35-209">По следующим ссылкам представлены дополнительные сведения об использовании Kubernetes с Azure:</span><span class="sxs-lookup"><span data-stu-id="b0b35-209">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="b0b35-210">Развертывание кластера Kubernetes для контейнеров Linux</span><span class="sxs-lookup"><span data-stu-id="b0b35-210">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="b0b35-211">Использование веб-интерфейса Kubernetes со службой контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="b0b35-211">Using the Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="b0b35-212">Дополнительные сведения об использовании интерфейса командной строки Kubernetes доступны в руководстве пользователя **kubectl** по адресу <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="b0b35-212">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="b0b35-213">На сайте Kubernetes содержится несколько статей, посвященных использованию образов в частных реестрах:</span><span class="sxs-lookup"><span data-stu-id="b0b35-213">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="b0b35-214">[Configure Service Accounts for Pods] (Настройка учетных записей службы для модулей Pod)</span><span class="sxs-lookup"><span data-stu-id="b0b35-214">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="b0b35-215">[Namespaces] (Пространства имен)</span><span class="sxs-lookup"><span data-stu-id="b0b35-215">[Namespaces]</span></span>
* <span data-ttu-id="b0b35-216">[Pull an Image from a Private Registry] (Извлечение образа из частного реестра)</span><span class="sxs-lookup"><span data-stu-id="b0b35-216">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="b0b35-217">Дополнительные примеры использования пользовательских образов Docker в Azure см. в разделе [Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux].</span><span class="sxs-lookup"><span data-stu-id="b0b35-217">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[служба контейнеров Azure (ACS)]: https://azure.microsoft.com/services/container-service/
[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[инструментов Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configure Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Настройка учетных записей службы для модулей Pod)
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/ (Пространства имен)
[Pull an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Извлечение образа из частного реестра)

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR04.png

[KB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB01.png
[KB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB02.png
[KB03]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB03.png
[KB04]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB04.png
[KB05]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB05.png
[KB06]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB06.png
[KB07]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB07.png
