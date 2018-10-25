---
title: Развертывание приложения Spring Boot в кластере Kubernetes в Службе Azure Kubernetes
description: В этом руководстве содержатся пошаговые инструкции по развертыванию приложения Spring Boot в кластере Kubernetes в Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: asirveda;robmcm
ms.date: 07/05/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 8e8f9088146af504ba2d9d45e2e82118c4081359
ms.sourcegitcommit: dae7511a9d93ca7f388d5b0e05dc098e22c2f2f6
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2018
ms.locfileid: "49962508"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-kubernetes-service"></a><span data-ttu-id="a1ae3-103">Развертывание приложения Spring Boot в кластере Kubernetes в Службе Azure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a1ae3-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Kubernetes Service</span></span>

<span data-ttu-id="a1ae3-104">**[Kubernetes]** и **[Docker]** — это решения с открытым кодом, которые помогают разработчикам автоматизировать развертывание и масштабирование выполняемых в контейнерах приложений, а также управление ими.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-104">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications running in containers.</span></span>

<span data-ttu-id="a1ae3-105">В этом руководстве представлены пошаговые инструкции по объединению этих двух популярных технологий с открытым кодом для разработки и развертывания приложения Spring Boot в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-105">This tutorial walks you through combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="a1ae3-106">В частности, *[Spring Boot]* используется для разработки приложений, *[Kubernetes]* — для развертывания контейнеров, а [Служба Azure Kubernetes (AKS)] — для размещения приложений.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-106">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Kubernetes Service (AKS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a1ae3-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a1ae3-107">Prerequisites</span></span>

* <span data-ttu-id="a1ae3-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="a1ae3-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="a1ae3-109">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="a1ae3-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="a1ae3-110">Актуальная версия [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="a1ae3-110">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="a1ae3-111">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="a1ae3-112">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="a1ae3-112">A [Git] client.</span></span>
* <span data-ttu-id="a1ae3-113">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="a1ae3-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="a1ae3-114">С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="a1ae3-115">Создание веб-приложения Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="a1ae3-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="a1ae3-116">Ниже представлены инструкции по созданию веб-приложения Spring Boot и его локальному тестированию.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-116">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="a1ae3-117">Откройте командную строку и создайте локальный каталог для размещения приложения, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="a1ae3-118">-- или --</span><span class="sxs-lookup"><span data-stu-id="a1ae3-118">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="a1ae3-119">Клонируйте пример проекта [Spring Boot on Docker Getting Started] в каталог.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="a1ae3-120">Перейдите в каталог готового проекта.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-120">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="a1ae3-121">Используйте Maven для создания и запуска примера приложения.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-121">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="a1ae3-122">Чтобы протестировать веб-приложение, перейдите по адресу `http://localhost:8080` или введите такую команду `curl`:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-122">Test the web app by browsing to `http://localhost:8080`, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="a1ae3-123">Должно появиться следующее сообщение: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-123">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Просмотр примера приложения в локальной среде][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="a1ae3-125">Создание реестра контейнеров Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a1ae3-125">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="a1ae3-126">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-126">Open a command prompt.</span></span>

1. <span data-ttu-id="a1ae3-127">Войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-127">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="a1ae3-128">Выберите подписку Azure:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-128">Choose your Azure Subscription:</span></span>
   ```azurecli
   az account set -s <YourSubscriptionID>
   ```

1. <span data-ttu-id="a1ae3-129">Создайте группу ресурсов Azure, используемых в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-129">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="a1ae3-130">Создайте частный реестр контейнеров Azure в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-130">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="a1ae3-131">Позднее в руководстве пример принудительно отправляется в этот реестр как образ Docker.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-131">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="a1ae3-132">Замените `wingtiptoysregistry` уникальным именем для реестра.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-132">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="a1ae3-133">Принудительная отправка приложения в реестр контейнеров</span><span class="sxs-lookup"><span data-stu-id="a1ae3-133">Push your app to the container registry</span></span>

1. <span data-ttu-id="a1ae3-134">Перейдите в каталог конфигурации для установки Maven (по умолчанию ~/.m2/ или C:\Users\username\.m2) и откройте файл *settings.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-134">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="a1ae3-135">Получите пароль для реестра контейнеров из Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-135">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="a1ae3-136">Добавьте идентификатор и пароль реестра контейнеров Azure для новой коллекции `<server>` в файле *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-136">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="a1ae3-137">`id` и `username` — это имена реестра.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-137">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="a1ae3-138">Используйте значение `password` из предыдущей команды (без кавычек).</span><span class="sxs-lookup"><span data-stu-id="a1ae3-138">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="a1ae3-139">Перейдите в каталог завершенного проекта для приложения Spring Boot (например, *C:\SpringBoot\gs-spring-boot-docker\complete* или */users/robert/SpringBoot/gs-spring-boot-docker/complete*) и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-139">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="a1ae3-140">Обновите коллекцию `<properties>` в файле *pom.xml*, добавив значение сервера входа для реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-140">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="a1ae3-141">Обновите коллекцию `<plugins>` в файле *pom.xml* таким образом, чтобы в `<plugin>` содержались адрес сервера входа и имя реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-141">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <buildArgs>
            <JAR_FILE>target/${project.build.finalName}.jar</JAR_FILE>
         </buildArgs>
         <baseImage>java</baseImage>
         <entryPoint>["java", "-jar", "/${project.build.finalName}.jar"]</entryPoint>
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

1. <span data-ttu-id="a1ae3-142">Перейдите в каталог завершенного проекта для приложения Spring Boot и выполните указанную ниже команду для создания контейнера Docker и отправки образа в реестр:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-142">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="a1ae3-143">При отправке образа из Maven в Azure может появиться сообщение об ошибке такого типа:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-143">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="a1ae3-144">При возникновении этой ошибки войдите в Azure из командной строки Docker.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-144">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="a1ae3-145">Затем принудительно отправьте контейнер:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-145">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a><span data-ttu-id="a1ae3-146">Создание в Службе контейнеров Azure кластера Kubernetes с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a1ae3-146">Create a Kubernetes Cluster on AKS using the Azure CLI</span></span>

1. <span data-ttu-id="a1ae3-147">Создайте кластер Kubernetes в Службе Azure Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-147">Create a Kubernetes cluster in Azure Kubernetes Service.</span></span> <span data-ttu-id="a1ae3-148">Следующая команда отвечает за создание кластера *kubernetes* в группе ресурсов *wingtiptoys-kubernetes* с именем кластера *wingtiptoys-akscluster* и префиксом DNS *wingtiptoys-kubernetes*:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-148">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-akscluster* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az aks create --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster \ 
    --dns-name-prefix=wingtiptoys-kubernetes --generate-ssh-keys
   ```
   <span data-ttu-id="a1ae3-149">Выполнение этой команды может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-149">This command may take a while to complete.</span></span>

1. <span data-ttu-id="a1ae3-150">При использовании реестра контейнеров Azure (ACR) со Службой Azure Kubernetes (AKS) необходимо установить механизм аутентификации.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-150">When you're using Azure Container Registry (ACR) with Azure Kubernetes Service (AKS), an authentication mechanism needs to be established.</span></span> <span data-ttu-id="a1ae3-151">Чтобы предоставить AKS доступ к ACR, выполните инструкции из статьи [Аутентификация с помощью реестра контейнеров Azure из Службы Azure Kubernetes].</span><span class="sxs-lookup"><span data-stu-id="a1ae3-151">Follow the steps in [Authenticate with Azure Container Registry from Azure Kubernetes Service] to grant AKS access to ACR.</span></span>


1. <span data-ttu-id="a1ae3-152">Установите `kubectl` с использованием Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-152">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="a1ae3-153">Пользователи Linux могут добавить к этой команде префикс `sudo`, так как она развертывает интерфейс командной строки Kubernetes в `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-153">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az aks install-cli
   ```

1. <span data-ttu-id="a1ae3-154">Скачайте сведения о конфигурации кластера, чтобы управлять им из веб-интерфейса Kubernetes и `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-154">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az aks get-credentials --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="a1ae3-155">Развертывание образа в кластере Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a1ae3-155">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="a1ae3-156">В этом руководстве с помощью `kubectl` развертывается приложение, а затем предоставляется возможность изучить развертывание с помощью веб-интерфейса Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-156">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="a1ae3-157">Развертывание с помощью веб-интерфейса Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a1ae3-157">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="a1ae3-158">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-158">Open a command prompt.</span></span>

1. <span data-ttu-id="a1ae3-159">Откройте веб-сайт конфигурации кластера Kubernetes в браузере по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-159">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az aks browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

1. <span data-ttu-id="a1ae3-160">Когда в браузере откроется веб-сайт конфигурации Kubernetes, щелкните ссылку, чтобы **развернуть контейнерное приложение**:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-160">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Веб-сайт конфигурации Kubernetes][KB01]

1. <span data-ttu-id="a1ae3-162">Когда отобразится страница **Resource Creation** (Создание ресурса), укажите следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-162">When the **Resource Creation** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="a1ae3-163">a.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-163">a.</span></span> <span data-ttu-id="a1ae3-164">Выберите **Create an App** (Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="a1ae3-164">Select **CREATE AN APP**.</span></span>

   <span data-ttu-id="a1ae3-165">b.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-165">b.</span></span> <span data-ttu-id="a1ae3-166">Укажите имя приложения Spring Boot в поле **Имя приложения** (например, *gs-spring-boot-docker*).</span><span class="sxs-lookup"><span data-stu-id="a1ae3-166">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="a1ae3-167">c.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-167">c.</span></span> <span data-ttu-id="a1ae3-168">Укажите сервер входа и образ контейнера, заданные ранее, в поле **Образ контейнера** (например, *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*).</span><span class="sxs-lookup"><span data-stu-id="a1ae3-168">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="a1ae3-169">d.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-169">d.</span></span> <span data-ttu-id="a1ae3-170">Для параметра **Служба** выберите значение **Внешняя**.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-170">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="a1ae3-171">д.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-171">e.</span></span> <span data-ttu-id="a1ae3-172">Укажите внешний и внутренний порты в текстовых полях **Порт** и **Целевой порт**.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-172">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Веб-сайт конфигурации Kubernetes][KB02]


1. <span data-ttu-id="a1ae3-174">Нажмите кнопку **Развернуть**, чтобы развернуть контейнер.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-174">Click **Deploy** to deploy the container.</span></span>

   ![Развертывание Kubernetes][KB05]

1. <span data-ttu-id="a1ae3-176">После развертывания приложение Spring Boot отобразится в списке **Службы**.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-176">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Службы Kubernetes][KB06]

1. <span data-ttu-id="a1ae3-178">Щелкнув ссылку для **внешних конечных точек**, можно просмотреть сведения о выполнении приложения Spring Boot в Azure.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-178">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Службы Kubernetes][KB07]

   ![Просмотр примера приложения в Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="a1ae3-181">Развертывание с помощью kubectl</span><span class="sxs-lookup"><span data-stu-id="a1ae3-181">Deploy with kubectl</span></span>

1. <span data-ttu-id="a1ae3-182">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-182">Open a command prompt.</span></span>

1. <span data-ttu-id="a1ae3-183">Запустите контейнер в кластере Kubernetes с помощью команды `kubectl run`.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-183">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="a1ae3-184">Присвойте приложению имя службы в Kubernetes и полное имя образа.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-184">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="a1ae3-185">Например: </span><span class="sxs-lookup"><span data-stu-id="a1ae3-185">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="a1ae3-186">В этой команде:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-186">In this command:</span></span>

   * <span data-ttu-id="a1ae3-187">Имя контейнера `gs-spring-boot-docker` указано сразу после команды `run`.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-187">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="a1ae3-188">Параметр `--image` указывает объединенное имя сервера входа и образа как `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-188">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="a1ae3-189">Предоставьте кластер Kubernetes извне с помощью команды `kubectl expose`.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-189">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="a1ae3-190">Укажите имя службы, общедоступный TCP-порт, используемый для доступа к приложению, и внутренний целевой порт, прослушиваемый приложением.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-190">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="a1ae3-191">Например: </span><span class="sxs-lookup"><span data-stu-id="a1ae3-191">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="a1ae3-192">В этой команде:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-192">In this command:</span></span>

   * <span data-ttu-id="a1ae3-193">Имя контейнера `gs-spring-boot-docker` указано сразу после команды `expose deployment`.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-193">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="a1ae3-194">Параметр `--type` указывает, что кластер использует подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-194">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="a1ae3-195">Параметр `--port` указывает общедоступный TCP-порт 80.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-195">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="a1ae3-196">Через этот порт вы осуществляете доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-196">You access the app on this port.</span></span>

   * <span data-ttu-id="a1ae3-197">Параметр `--target-port` указывает общедоступный TCP-порт 8080.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-197">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="a1ae3-198">Через этот порт подсистема балансировки нагрузки переадресовывает запросы к приложению.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-198">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="a1ae3-199">После развертывания приложения в кластере подайте запрос на внешний IP-адрес и откройте его в своем веб-браузере:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-199">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Просмотр примера приложения в Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="a1ae3-201">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="a1ae3-201">Next steps</span></span>

<span data-ttu-id="a1ae3-202">Дополнительные сведения об использовании Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-202">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="a1ae3-203">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="a1ae3-203">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="a1ae3-204">Развертывание приложения Spring Boot в Linux в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="a1ae3-204">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)

<span data-ttu-id="a1ae3-205">Дополнительные сведения об использовании Azure с Java см. в руководствах по [Azure для разработчиков Java] и [инструментах Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="a1ae3-205">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="a1ae3-206"><!-- Newly added --> Дополнительные сведения о развертывании приложения Java в кластере Kubernetes с помощью Visual Studio Code см. в [Руководства по Java для Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="a1ae3-206"><!-- Newly added --> For more information about deploying a Java application to Kubernetes with Visual Studio Code, see [Visual Studio Code Java Tutorials].</span></span>

<span data-ttu-id="a1ae3-207">Дополнительные сведения о примере проекта Spring Boot в Docker см. в разделе [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="a1ae3-207">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="a1ae3-208">По следующим ссылкам представлены дополнительные сведения о создании приложений Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-208">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="a1ae3-209">Дополнительные сведения о создании простого приложения Spring Boot см. на странице Spring Initializr по адресу https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-209">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="a1ae3-210">По следующим ссылкам представлены дополнительные сведения об использовании Kubernetes с Azure:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-210">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="a1ae3-211">Начало работы с кластером Kubernetes в Службе Azure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a1ae3-211">Get started with a Kubernetes cluster in Azure Kubernetes Service</span></span>](https://docs.microsoft.com/azure/aks/intro-kubernetes)

<span data-ttu-id="a1ae3-212">Дополнительные сведения об использовании интерфейса командной строки Kubernetes доступны в руководстве пользователя **kubectl** по адресу <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="a1ae3-212">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="a1ae3-213">На сайте Kubernetes содержится несколько статей, посвященных использованию образов в частных реестрах:</span><span class="sxs-lookup"><span data-stu-id="a1ae3-213">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="a1ae3-214">[Configure Service Accounts for Pods] (Настройка учетных записей службы для модулей Pod)</span><span class="sxs-lookup"><span data-stu-id="a1ae3-214">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="a1ae3-215">[Namespaces] (Пространства имен)</span><span class="sxs-lookup"><span data-stu-id="a1ae3-215">[Namespaces]</span></span>
* <span data-ttu-id="a1ae3-216">[Pull an Image from a Private Registry] (Извлечение образа из частного реестра)</span><span class="sxs-lookup"><span data-stu-id="a1ae3-216">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="a1ae3-217">Дополнительные примеры использования пользовательских образов Docker в Azure см. в разделе [Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux].</span><span class="sxs-lookup"><span data-stu-id="a1ae3-217">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Служба Azure Kubernetes (AKS)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure Kubernetes Service (AKS)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure для разработчиков Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[инструментах Java для Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configure Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Настройка учетных записей службы для модулей Pod)
[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/ (Пространства имен)
[Pull an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Извлечение образа из частного реестра)
[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- Newly added -->
[Аутентификация с помощью реестра контейнеров Azure из Службы Azure Kubernetes]: https://docs.microsoft.com/azure/container-registry/container-registry-auth-aks/
[Authenticate with Azure Container Registry from Azure Kubernetes Service]: https://docs.microsoft.com/azure/container-registry/container-registry-auth-aks/
[Руководства по Java для Visual Studio Code]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Visual Studio Code Java Tutorials]: https://code.visualstudio.com/docs/java/java-kubernetes/

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
