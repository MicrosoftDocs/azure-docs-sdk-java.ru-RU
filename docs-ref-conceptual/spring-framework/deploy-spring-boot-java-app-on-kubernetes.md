---
title: Развертывание приложения Spring Boot в кластере Kubernetes в Службе Azure Kubernetes
description: В этом руководстве содержатся пошаговые инструкции по развертыванию приложения Spring Boot в кластере Kubernetes в Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 42bb030a916cc5aaf1e20242518a0a400b8baa88
ms.sourcegitcommit: 3b10fe30dcc83e4c2e4c94d5b55e37ddbaa23c7a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2019
ms.locfileid: "59071013"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-kubernetes-service"></a><span data-ttu-id="d6999-103">Развертывание приложения Spring Boot в кластере Kubernetes в Службе Azure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d6999-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Kubernetes Service</span></span>

<span data-ttu-id="d6999-104">**[Kubernetes]** и **[Docker]** — это решения с открытым кодом, которые помогают разработчикам автоматизировать развертывание и масштабирование выполняемых в контейнерах приложений, а также управление ими.</span><span class="sxs-lookup"><span data-stu-id="d6999-104">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications running in containers.</span></span>

<span data-ttu-id="d6999-105">В этом руководстве представлены пошаговые инструкции по объединению этих двух популярных технологий с открытым кодом для разработки и развертывания приложения Spring Boot в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d6999-105">This tutorial walks you through combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="d6999-106">В частности, *[Spring Boot]* используется для разработки приложений, *[Kubernetes]* — для развертывания контейнеров, а [Служба Azure Kubernetes (AKS)] — для размещения приложений.</span><span class="sxs-lookup"><span data-stu-id="d6999-106">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Kubernetes Service (AKS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d6999-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d6999-107">Prerequisites</span></span>

* <span data-ttu-id="d6999-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="d6999-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="d6999-109">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="d6999-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="d6999-110">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="d6999-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="d6999-111">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="d6999-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="d6999-112">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="d6999-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="d6999-113">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="d6999-113">A [Git] client.</span></span>
* <span data-ttu-id="d6999-114">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="d6999-114">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d6999-115">С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="d6999-115">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="d6999-116">Создание веб-приложения Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="d6999-116">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="d6999-117">Ниже представлены инструкции по созданию веб-приложения Spring Boot и его локальному тестированию.</span><span class="sxs-lookup"><span data-stu-id="d6999-117">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="d6999-118">Откройте командную строку и создайте локальный каталог для размещения приложения, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="d6999-118">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="d6999-119">-- или --</span><span class="sxs-lookup"><span data-stu-id="d6999-119">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="d6999-120">Клонируйте пример проекта [Spring Boot on Docker Getting Started] в каталог.</span><span class="sxs-lookup"><span data-stu-id="d6999-120">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="d6999-121">Перейдите в каталог готового проекта.</span><span class="sxs-lookup"><span data-stu-id="d6999-121">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="d6999-122">Используйте Maven для создания и запуска примера приложения.</span><span class="sxs-lookup"><span data-stu-id="d6999-122">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="d6999-123">Чтобы протестировать веб-приложение, перейдите по адресу `http://localhost:8080` или введите такую команду `curl`:</span><span class="sxs-lookup"><span data-stu-id="d6999-123">Test the web app by browsing to `http://localhost:8080`, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="d6999-124">Должно появиться следующее сообщение: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="d6999-124">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Локальный просмотр образца приложения][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="d6999-126">Создание реестра контейнеров Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6999-126">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="d6999-127">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="d6999-127">Open a command prompt.</span></span>

1. <span data-ttu-id="d6999-128">Войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="d6999-128">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="d6999-129">Выберите подписку Azure:</span><span class="sxs-lookup"><span data-stu-id="d6999-129">Choose your Azure Subscription:</span></span>
   ```azurecli
   az account set -s <YourSubscriptionID>
   ```

1. <span data-ttu-id="d6999-130">Создайте группу ресурсов Azure, используемых в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="d6999-130">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="d6999-131">Создайте частный реестр контейнеров Azure в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d6999-131">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="d6999-132">Позднее в руководстве пример принудительно отправляется в этот реестр как образ Docker.</span><span class="sxs-lookup"><span data-stu-id="d6999-132">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="d6999-133">Замените `wingtiptoysregistry` уникальным именем для реестра.</span><span class="sxs-lookup"><span data-stu-id="d6999-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --resource-group wingtiptoys-kubernetes --location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry-via-jib"></a><span data-ttu-id="d6999-134">Принудительная отправка приложения в реестр контейнеров с использованием Jib</span><span class="sxs-lookup"><span data-stu-id="d6999-134">Push your app to the container registry via Jib</span></span>

1. <span data-ttu-id="d6999-135">Войдите в Реестр контейнеров с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d6999-135">Log in to your Azure Container Registry from the Azure CLI.</span></span>
   ```azurecli
   # set the default name for Azure Container Registry, otherwise you will need to specify the name in "az acr login"
   az configure --defaults acr=wingtiptoysregistry
   az acr login
   ```

1. <span data-ttu-id="d6999-136">Перейдите в каталог завершенного проекта для приложения Spring Boot (например, *C:\SpringBoot\gs-spring-boot-docker\complete* или */users/robert/SpringBoot/gs-spring-boot-docker/complete*) и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="d6999-136">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="d6999-137">Обновите коллекцию `<properties>` в файле *pom.xml*, добавив имя для своего реестра в Реестре контейнеров Azure и последнюю версию [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).</span><span class="sxs-lookup"><span data-stu-id="d6999-137">Update the `<properties>` collection in the *pom.xml* file with the registry name for your Azure Container Registry and the latest version of [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <jib-maven-plugin.version>1.0.2</jib-maven-plugin.version>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="d6999-138">Обновите коллекцию `<plugins>` в файле *pom.xml* таким образом, чтобы в `<plugin>` содержался подключаемый модуль `jib-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="d6999-138">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the `jib-maven-plugin`.</span></span>

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
        </to>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="d6999-139">Перейдите в каталог завершенного проекта для приложения Spring Boot и выполните указанную ниже команду для создания образа и его отправки в реестр:</span><span class="sxs-lookup"><span data-stu-id="d6999-139">Navigate to the completed project directory for your Spring Boot application and run the following command to build the image and push the image to the registry:</span></span>

   ```
   mvn compile jib:build
   ```

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a><span data-ttu-id="d6999-140">Создание в Службе контейнеров Azure кластера Kubernetes с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6999-140">Create a Kubernetes Cluster on AKS using the Azure CLI</span></span>

1. <span data-ttu-id="d6999-141">Создайте кластер Kubernetes в Службе Azure Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="d6999-141">Create a Kubernetes cluster in Azure Kubernetes Service.</span></span> <span data-ttu-id="d6999-142">Следующая команда отвечает за создание кластера *kubernetes* в группе ресурсов *wingtiptoys-kubernetes* с именем кластера *wingtiptoys-akscluster* и префиксом DNS *wingtiptoys-kubernetes*:</span><span class="sxs-lookup"><span data-stu-id="d6999-142">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-akscluster* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az aks create --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster \ 
    --dns-name-prefix=wingtiptoys-kubernetes --generate-ssh-keys
   ```
   <span data-ttu-id="d6999-143">Выполнение этой команды может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="d6999-143">This command may take a while to complete.</span></span>

1. <span data-ttu-id="d6999-144">При использовании Реестра контейнеров Azure (ACR) со Службой Azure Kubernetes (AKS) необходимо предоставить Службе Azure Kubernetes доступ для извлечения данных из Реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="d6999-144">When you're using Azure Container Registry (ACR) with Azure Kubernetes Service (AKS), you need to grant Azure Kubernetes Service pull access to Azure Container Registry.</span></span> <span data-ttu-id="d6999-145">Когда вы создаете Службу Kubernetes, в Azure создается субъект-служба по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d6999-145">Azure creates a default service principal when you are creating Azure Kubernetes Service.</span></span> <span data-ttu-id="d6999-146">Выполните приведенные ниже скрипты в Bash или PowerShell, чтобы предоставить AKS доступ к ACR. Дополнительные сведения см. в статье об [Аутентификация с помощью реестра контейнеров Azure из Службы Azure Kubernetes].</span><span class="sxs-lookup"><span data-stu-id="d6999-146">Please run the following scripts in bash or Powershell to grant AKS access to ACR, see more details at [Authenticate with Azure Container Registry from Azure Kubernetes Service].</span></span>

```bash
   # Get the id of the service principal configured for AKS
   CLIENT_ID=$(az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv)
   
   # Get the ACR registry resource id
   ACR_ID=$(az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv)
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

  <span data-ttu-id="d6999-147">-- или --</span><span class="sxs-lookup"><span data-stu-id="d6999-147">-- or --</span></span>

```PowerShell
   # Get the id of the service principal configured for AKS
   $CLIENT_ID = az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv
   
   # Get the ACR registry resource id
   $ACR_ID = az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

1. <span data-ttu-id="d6999-148">Установите `kubectl` с использованием Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d6999-148">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="d6999-149">Пользователи Linux могут добавить к этой команде префикс `sudo`, так как она развертывает интерфейс командной строки Kubernetes в `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="d6999-149">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az aks install-cli
   ```

1. <span data-ttu-id="d6999-150">Скачайте сведения о конфигурации кластера, чтобы управлять им из веб-интерфейса Kubernetes и `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="d6999-150">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az aks get-credentials --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="d6999-151">Развертывание образа в кластере Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d6999-151">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="d6999-152">В этом руководстве с помощью `kubectl` развертывается приложение, а затем предоставляется возможность изучить развертывание с помощью веб-интерфейса Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="d6999-152">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-kubectl"></a><span data-ttu-id="d6999-153">Развертывание с помощью kubectl</span><span class="sxs-lookup"><span data-stu-id="d6999-153">Deploy with kubectl</span></span>

1. <span data-ttu-id="d6999-154">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="d6999-154">Open a command prompt.</span></span>

1. <span data-ttu-id="d6999-155">Запустите контейнер в кластере Kubernetes с помощью команды `kubectl run`.</span><span class="sxs-lookup"><span data-stu-id="d6999-155">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="d6999-156">Присвойте приложению имя службы в Kubernetes и полное имя образа.</span><span class="sxs-lookup"><span data-stu-id="d6999-156">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="d6999-157">Например: </span><span class="sxs-lookup"><span data-stu-id="d6999-157">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="d6999-158">В этой команде:</span><span class="sxs-lookup"><span data-stu-id="d6999-158">In this command:</span></span>

   * <span data-ttu-id="d6999-159">Имя контейнера `gs-spring-boot-docker` указано сразу после команды `run`.</span><span class="sxs-lookup"><span data-stu-id="d6999-159">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="d6999-160">Параметр `--image` указывает объединенное имя сервера входа и образа как `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`.</span><span class="sxs-lookup"><span data-stu-id="d6999-160">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="d6999-161">Предоставьте кластер Kubernetes извне с помощью команды `kubectl expose`.</span><span class="sxs-lookup"><span data-stu-id="d6999-161">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="d6999-162">Укажите имя службы, общедоступный TCP-порт, используемый для доступа к приложению, и внутренний целевой порт, прослушиваемый приложением.</span><span class="sxs-lookup"><span data-stu-id="d6999-162">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="d6999-163">Например: </span><span class="sxs-lookup"><span data-stu-id="d6999-163">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="d6999-164">В этой команде:</span><span class="sxs-lookup"><span data-stu-id="d6999-164">In this command:</span></span>

   * <span data-ttu-id="d6999-165">Имя контейнера `gs-spring-boot-docker` указано сразу после команды `expose deployment`.</span><span class="sxs-lookup"><span data-stu-id="d6999-165">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="d6999-166">Параметр `--type` указывает, что кластер использует подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d6999-166">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="d6999-167">Параметр `--port` указывает общедоступный TCP-порт 80.</span><span class="sxs-lookup"><span data-stu-id="d6999-167">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="d6999-168">Через этот порт вы осуществляете доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="d6999-168">You access the app on this port.</span></span>

   * <span data-ttu-id="d6999-169">Параметр `--target-port` указывает общедоступный TCP-порт 8080.</span><span class="sxs-lookup"><span data-stu-id="d6999-169">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="d6999-170">Через этот порт подсистема балансировки нагрузки переадресовывает запросы к приложению.</span><span class="sxs-lookup"><span data-stu-id="d6999-170">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="d6999-171">После развертывания приложения в кластере подайте запрос на внешний IP-адрес и откройте его в своем веб-браузере:</span><span class="sxs-lookup"><span data-stu-id="d6999-171">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=default
   ```

   ![Просмотр примера приложения в Azure][SB02]



### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="d6999-173">Развертывание с помощью веб-интерфейса Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d6999-173">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="d6999-174">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="d6999-174">Open a command prompt.</span></span>

1. <span data-ttu-id="d6999-175">Откройте веб-сайт конфигурации кластера Kubernetes в браузере по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="d6999-175">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az aks browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

1. <span data-ttu-id="d6999-176">Когда в браузере откроется веб-сайт конфигурации Kubernetes, щелкните ссылку, чтобы **развернуть контейнерное приложение**:</span><span class="sxs-lookup"><span data-stu-id="d6999-176">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Веб-сайт конфигурации Kubernetes][KB01]

1. <span data-ttu-id="d6999-178">Когда отобразится страница **Resource Creation** (Создание ресурса), укажите следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="d6999-178">When the **Resource Creation** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="d6999-179">a.</span><span class="sxs-lookup"><span data-stu-id="d6999-179">a.</span></span> <span data-ttu-id="d6999-180">Выберите **Create an App** (Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="d6999-180">Select **CREATE AN APP**.</span></span>

   <span data-ttu-id="d6999-181">b.</span><span class="sxs-lookup"><span data-stu-id="d6999-181">b.</span></span> <span data-ttu-id="d6999-182">Укажите имя приложения Spring Boot в поле **Имя приложения** (например, *gs-spring-boot-docker*).</span><span class="sxs-lookup"><span data-stu-id="d6999-182">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="d6999-183">c.</span><span class="sxs-lookup"><span data-stu-id="d6999-183">c.</span></span> <span data-ttu-id="d6999-184">Укажите сервер входа и образ контейнера, заданные ранее, в поле **Образ контейнера** (например, *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*).</span><span class="sxs-lookup"><span data-stu-id="d6999-184">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="d6999-185">d.</span><span class="sxs-lookup"><span data-stu-id="d6999-185">d.</span></span> <span data-ttu-id="d6999-186">Для параметра **Служба** выберите значение **Внешняя**.</span><span class="sxs-lookup"><span data-stu-id="d6999-186">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="d6999-187">д.</span><span class="sxs-lookup"><span data-stu-id="d6999-187">e.</span></span> <span data-ttu-id="d6999-188">Укажите внешний и внутренний порты в текстовых полях **Порт** и **Целевой порт**.</span><span class="sxs-lookup"><span data-stu-id="d6999-188">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Веб-сайт конфигурации Kubernetes][KB02]


1. <span data-ttu-id="d6999-190">Нажмите кнопку **Развернуть**, чтобы развернуть контейнер.</span><span class="sxs-lookup"><span data-stu-id="d6999-190">Click **Deploy** to deploy the container.</span></span>

   ![Развертывание Kubernetes][KB05]

1. <span data-ttu-id="d6999-192">После развертывания приложение Spring Boot отобразится в списке **Службы**.</span><span class="sxs-lookup"><span data-stu-id="d6999-192">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Службы Kubernetes][KB06]

1. <span data-ttu-id="d6999-194">Щелкнув ссылку для **внешних конечных точек**, можно просмотреть сведения о выполнении приложения Spring Boot в Azure.</span><span class="sxs-lookup"><span data-stu-id="d6999-194">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Службы Kubernetes][KB07]

   ![Просмотр примера приложения в Azure][SB02]

## <a name="next-steps"></a><span data-ttu-id="d6999-197">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="d6999-197">Next steps</span></span>

<span data-ttu-id="d6999-198">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="d6999-198">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6999-199">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="d6999-199">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="d6999-200">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d6999-200">Additional Resources</span></span>

<span data-ttu-id="d6999-201">Дополнительные сведения об использовании Spring Boot в Azure см. в следующей статье:</span><span class="sxs-lookup"><span data-stu-id="d6999-201">For more information about using Spring Boot on Azure, see the following article:</span></span>

* [<span data-ttu-id="d6999-202">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="d6999-202">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

<span data-ttu-id="d6999-203">Дополнительные сведения об использовании Java в Azure см. в статьях [Azure для разработчиков Java] и [Working with Azure DevOps and Java] (Работа с Azure DevOps и Java).</span><span class="sxs-lookup"><span data-stu-id="d6999-203">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="d6999-204">Дополнительные сведения о развертывании приложения Java в кластере Kubernetes с помощью Visual Studio Code см. в [Руководства по Java для Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="d6999-204">For more information about deploying a Java application to Kubernetes with Visual Studio Code, see [Visual Studio Code Java Tutorials].</span></span>

<span data-ttu-id="d6999-205">Дополнительные сведения о примере проекта Spring Boot в Docker см. в разделе [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="d6999-205">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="d6999-206">По следующим ссылкам представлены дополнительные сведения о создании приложений Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="d6999-206">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="d6999-207">Дополнительные сведения о создании простого приложения Spring Boot см. на странице Spring Initializr по адресу https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="d6999-207">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="d6999-208">По следующим ссылкам представлены дополнительные сведения об использовании Kubernetes с Azure:</span><span class="sxs-lookup"><span data-stu-id="d6999-208">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="d6999-209">Начало работы с кластером Kubernetes в Службе Azure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d6999-209">Get started with a Kubernetes cluster in Azure Kubernetes Service</span></span>](/azure/aks/intro-kubernetes)

<span data-ttu-id="d6999-210">Дополнительные сведения об использовании интерфейса командной строки Kubernetes доступны в руководстве пользователя **kubectl** по адресу <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="d6999-210">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="d6999-211">На сайте Kubernetes содержится несколько статей, посвященных использованию образов в частных реестрах:</span><span class="sxs-lookup"><span data-stu-id="d6999-211">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="d6999-212">[Configure Service Accounts for Pods] (Настройка учетных записей службы для модулей Pod)</span><span class="sxs-lookup"><span data-stu-id="d6999-212">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="d6999-213">[Namespaces] (Пространства имен)</span><span class="sxs-lookup"><span data-stu-id="d6999-213">[Namespaces]</span></span>
* <span data-ttu-id="d6999-214">[Pull an Image from a Private Registry] (Извлечение образа из частного реестра)</span><span class="sxs-lookup"><span data-stu-id="d6999-214">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="d6999-215">Дополнительные примеры использования пользовательских образов Docker в Azure см. в разделе [Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux].</span><span class="sxs-lookup"><span data-stu-id="d6999-215">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<span data-ttu-id="d6999-216">Дополнительные сведения об итеративном выполнении и отладке контейнеров непосредственно в Службе Azure Kubernetes (AKS) с помощью Azure Dev Spaces см. в разделе [Начало работы в Azure Dev Spaces с использованием Java].</span><span class="sxs-lookup"><span data-stu-id="d6999-216">For more information about iteratively running and debugging containers directly in Azure Kubernetes Service (AKS) with Azure Dev Spaces, see [Get started on Azure Dev Spaces with Java]</span></span>

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Служба Azure Kubernetes (AKS)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure Kubernetes Service (AKS)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure для разработчиков Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/java/ (Работа с Azure DevOps и Java)
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

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- Newly added -->
[Аутентификация с помощью реестра контейнеров Azure из Службы Azure Kubernetes]: /azure/container-registry/container-registry-auth-aks/
[Authenticate with Azure Container Registry from Azure Kubernetes Service]: /azure/container-registry/container-registry-auth-aks/
[Руководства по Java для Visual Studio Code]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Visual Studio Code Java Tutorials]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Начало работы в Azure Dev Spaces с использованием Java]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
[Get started on Azure Dev Spaces with Java]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
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
