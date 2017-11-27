---
title: "Развертывание приложения Spring Boot с помощью подключаемого модуля Maven Fabric8"
description: "В этом руководстве содержатся пошаговые инструкции по развертыванию приложения Spring Boot для Apache Maven с помощью подключаемого модуля Maven Fabric8 в Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Maven
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/01/2017
ms.author: yuwzho;robmcm
ms.custom: 
ms.openlocfilehash: 6c0e0e233b44b2b54e869b443edf3a255e7fbfb4
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2017
---
# <a name="deploy-a-spring-boot-app-using-the-fabric8-maven-plugin"></a><span data-ttu-id="740e1-104">Развертывание приложения Spring Boot с помощью подключаемого модуля Maven Fabric8</span><span class="sxs-lookup"><span data-stu-id="740e1-104">Deploy a Spring Boot app using the Fabric8 Maven Plugin</span></span>

<span data-ttu-id="740e1-105">**[Fabric8]** — это решение с открытым кодом на базе **[Kubernetes]**, помогающее разработчикам создавать приложения в контейнерах Linux.</span><span class="sxs-lookup"><span data-stu-id="740e1-105">**[Fabric8]** is an open-source solution that is built on **[Kubernetes]**, which helps developers create applications in Linux containers.</span></span>

<span data-ttu-id="740e1-106">В этом руководстве рассматривается применение подключаемого модуля Fabric8 в Maven для разработки и развертывания приложения на узле Linux в [службе контейнеров Azure].</span><span class="sxs-lookup"><span data-stu-id="740e1-106">This tutorial walks you through using the Fabric8 plugin for Maven to develop to deploy an application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="740e1-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="740e1-107">Prerequisites</span></span>

<span data-ttu-id="740e1-108">Для работы с этим руководством требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="740e1-108">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="740e1-109">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="740e1-109">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="740e1-110">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="740e1-110">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="740e1-111">Актуальная версия [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="740e1-111">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="740e1-112">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="740e1-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="740e1-113">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="740e1-113">A [Git] client.</span></span>
* <span data-ttu-id="740e1-114">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="740e1-114">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="740e1-115">С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="740e1-115">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="740e1-116">Создание веб-приложения Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="740e1-116">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="740e1-117">Ниже представлены инструкции по созданию веб-приложения Spring Boot и его локальному тестированию.</span><span class="sxs-lookup"><span data-stu-id="740e1-117">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="740e1-118">Откройте командную строку и создайте локальный каталог для размещения приложения, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-118">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```shell
   md /home/GenaSoto/SpringBoot
   cd /home/GenaSoto/SpringBoot
   ```
   <span data-ttu-id="740e1-119">-- или --</span><span class="sxs-lookup"><span data-stu-id="740e1-119">-- or --</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```

1. <span data-ttu-id="740e1-120">Клонируйте пример проекта [Spring Boot on Docker Getting Started] в каталог.</span><span class="sxs-lookup"><span data-stu-id="740e1-120">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="740e1-121">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-121">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```
   <span data-ttu-id="740e1-122">-- или --</span><span class="sxs-lookup"><span data-stu-id="740e1-122">-- or --</span></span>
   ```shell
   cd gs-spring-boot-docker\complete
   ```

1. <span data-ttu-id="740e1-123">Используйте Maven для создания и запуска примера приложения.</span><span class="sxs-lookup"><span data-stu-id="740e1-123">Use Maven to build and run the sample app.</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```

1. <span data-ttu-id="740e1-124">Чтобы протестировать веб-приложение, перейдите по адресу http://localhost:8080 или введите команду `curl`:</span><span class="sxs-lookup"><span data-stu-id="740e1-124">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="740e1-125">Должно появиться следующее сообщение: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="740e1-125">You should see a **Hello Docker World** message displayed.</span></span>

   ![Локальный просмотр примера приложения][SB01]


## <a name="install-the-kubernetes-command-line-interface-and-create-an-azure-resource-group-using-the-azure-cli"></a><span data-ttu-id="740e1-127">Установка интерфейса командной строки Kubernetes и создание группы ресурсов Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="740e1-127">Install the Kubernetes command-line interface and create an Azure resource group using the Azure CLI</span></span>

1. <span data-ttu-id="740e1-128">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="740e1-128">Open a command prompt.</span></span>

1. <span data-ttu-id="740e1-129">Введите следующую команду, чтобы войти в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="740e1-129">Type the following command to log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="740e1-130">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="740e1-130">Follow the instructions to complete the login process</span></span>
   
   <span data-ttu-id="740e1-131">В интерфейсе командной строки Azure отобразится список учетных записей, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-131">The Azure CLI will display a list of your accounts; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "00000000-0000-0000-0000-000000000000",
       "isDefault": false,
       "name": "Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "00000000-0000-0000-0000-000000000000",
       "user": {
         "name": "Gena.Soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```

1. <span data-ttu-id="740e1-132">Если интерфейс командной строки Kubernetes еще не установлен (`kubectl`), можно установить его с помощью Azure CLI, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-132">If you do not already have the Kubernetes command-line interface (`kubectl`) installed, you can install using the Azure CLI; for example:</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="740e1-133">Пользователи Linux могут добавить к этой команде префикс `sudo`, так как она развертывает интерфейс командной строки Kubernetes в `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="740e1-133">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   >
   > <span data-ttu-id="740e1-134">Если `kubectl` уже установлен и ваша версия `kubectl` устарела, при попытке выполнить действия, приведенные далее в этой статье, может появиться сообщение об ошибке (как в следующем примере).</span><span class="sxs-lookup"><span data-stu-id="740e1-134">If you already have `kubectl`) installed and your version of `kubectl` is too old, you may see an error message similar to the following example when you attempt to complete the steps listed later in this article:</span></span>
   >
   > ```
   > error: group map[autoscaling:0x0000000000 batch:0x0000000000 certificates.k8s.io
   > :0x0000000000 extensions:0x0000000000 storage.k8s.io:0x0000000000 apps:0x0000000
   > 000 authentication.k8s.io:0x0000000000 policy:0x0000000000 rbac.authorization.k8
   > s.io:0x0000000000 federation:0x0000000000 authorization.k8s.io:0x0000000000 comp
   > onentconfig:0x0000000000] is already registered
   > ```
   >
   > <span data-ttu-id="740e1-135">В этом случае необходимо переустановить `kubectl`, чтобы обновить версию.</span><span class="sxs-lookup"><span data-stu-id="740e1-135">If this happens, you will need to reinstall `kubectl` to update your version.</span></span>
   >

1. <span data-ttu-id="740e1-136">Создайте группу ресурсов Azure, используемых в этой статье, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-136">Create a resource group for the Azure resources that you will use in this tutorial; for example:</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=westeurope
   ```
   <span data-ttu-id="740e1-137">Описание</span><span class="sxs-lookup"><span data-stu-id="740e1-137">Where:</span></span>  
      * <span data-ttu-id="740e1-138">*wingtiptoys-kubernetes* — уникальное имя для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="740e1-138">*wingtiptoys-kubernetes* is a unique name for your resource group</span></span>  
      * <span data-ttu-id="740e1-139">*westeurope* — соответствующее географическое расположение для приложения.</span><span class="sxs-lookup"><span data-stu-id="740e1-139">*westeurope* is an appropriate geographic location for your application</span></span>  

   <span data-ttu-id="740e1-140">В Azure CLI отобразятся результаты созданной группы ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-140">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes",
     "location": "westeurope",
     "managedBy": null,
     "name": "wingtiptoys-kubernetes",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```


## <a name="create-a-kubernetes-cluster-using-the-azure-cli"></a><span data-ttu-id="740e1-141">Создание кластера Kubernetes с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="740e1-141">Create a Kubernetes cluster using the Azure CLI</span></span>

1. <span data-ttu-id="740e1-142">Создайте кластер Kubernetes в новой группе ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-142">Create a Kubernetes cluster in your new resource group; for example:</span></span>  
   ```azurecli 
   az acs create --orchestrator-type kubernetes --resource-group wingtiptoys-kubernetes --name wingtiptoys-cluster --generate-ssh-keys --dns-prefix=wingtiptoys
   ```
   <span data-ttu-id="740e1-143">Описание</span><span class="sxs-lookup"><span data-stu-id="740e1-143">Where:</span></span>  
      * <span data-ttu-id="740e1-144">*wingtiptoys-kubernetes* — имя группы ресурсов, описанной в этой статье.</span><span class="sxs-lookup"><span data-stu-id="740e1-144">*wingtiptoys-kubernetes* is the name of your resource group from earlier in this article</span></span>  
      * <span data-ttu-id="740e1-145">*wingtiptoys-cluster* — уникальное имя для кластера Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="740e1-145">*wingtiptoys-cluster* is a unique name for your Kubernetes cluster</span></span>
      * <span data-ttu-id="740e1-146">*wingtiptoys* — уникальное имя DNS-имени для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="740e1-146">*wingtiptoys* is a unique name DNS name for your application</span></span>

   <span data-ttu-id="740e1-147">В Azure CLI отобразятся результаты создания кластера, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-147">The Azure CLI will display the results of your cluster creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.Resources/deployments/azurecli0000000000.00000000000",
     "name": "azurecli0000000000.00000000000",
     "properties": {
       "correlationId": "00000000-0000-0000-0000-000000000000",
       "debugSetting": null,
       "dependencies": [],
       "mode": "Incremental",
       "outputs": {
         "masterFQDN": {
           "type": "String",
           "value": "wingtiptoysmgmt.westeurope.cloudapp.azure.com"
         },
         "sshMaster0": {
           "type": "String",
           "value": "ssh azureuser@wingtiptoysmgmt.westeurope.cloudapp.azure.com -A -p 22"
         }
       },
       "parameters": {
         "clientSecret": {
           "type": "SecureString"
         }
       },
       "parametersLink": null,
       "providers": [
         {
           "id": null,
           "namespace": "Microsoft.ContainerService",
           "registrationState": null,
           "resourceTypes": [
             {
               "aliases": null,
               "apiVersions": null,
               "locations": [
                 "westeurope"
               ],
               "properties": null,
               "resourceType": "containerServices"
             }
           ]
         }
       ],
       "provisioningState": "Succeeded",
       "template": null,
       "templateLink": null,
       "timestamp": "2017-09-15T01:00:00.000000+00:00"
     },
     "resourceGroup": "wingtiptoys-kubernetes"
   }
   ```

1. <span data-ttu-id="740e1-148">Скачайте учетные данные для нового кластера Kubernetes, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-148">Download your credentials for your new Kubernetes cluster; for example:</span></span>  
   ```azurecli 
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes --name wingtiptoys-cluster
   ```

1. <span data-ttu-id="740e1-149">Проверьте подключение с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="740e1-149">Verify your connection with the following command:</span></span>
   ```shell 
   kubectl get nodes
   ```

   <span data-ttu-id="740e1-150">Появится список узлов и состояний, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="740e1-150">You should see a list of nodes and statuses like the following example:</span></span>

   ```shell
   NAME                    STATUS                     AGE       VERSION
   k8s-agent-00000000-0    Ready                      5h        v1.6.6
   k8s-agent-00000000-1    Ready                      5h        v1.6.6
   k8s-agent-00000000-2    Ready                      5h        v1.6.6
   k8s-master-00000000-0   Ready,SchedulingDisabled   5h        v1.6.6
   ```


## <a name="create-a-private-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="740e1-151">Создание закрытого реестра контейнеров Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="740e1-151">Create a private Azure container registry using the Azure CLI</span></span>

1. <span data-ttu-id="740e1-152">Создайте закрытый реестр контейнеров Azure в группе ресурсов для размещения образа Docker, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-152">Create a private Azure container registry in your resource group to host your Docker image; for example:</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes --location westeurope --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="740e1-153">Описание</span><span class="sxs-lookup"><span data-stu-id="740e1-153">Where:</span></span>  
      * <span data-ttu-id="740e1-154">*wingtiptoys-kubernetes* — имя группы ресурсов, описанной в этой статье.</span><span class="sxs-lookup"><span data-stu-id="740e1-154">*wingtiptoys-kubernetes* is the name of your resource group from earlier in this article</span></span>  
      * <span data-ttu-id="740e1-155">*wingtiptoysregistry* — уникальное имя для частного реестра</span><span class="sxs-lookup"><span data-stu-id="740e1-155">*wingtiptoysregistry* is a unique name for your private registry</span></span>
      * <span data-ttu-id="740e1-156">*westeurope* — соответствующее географическое расположение для приложения.</span><span class="sxs-lookup"><span data-stu-id="740e1-156">*westeurope* is an appropriate geographic location for your application</span></span>  

   <span data-ttu-id="740e1-157">В Azure CLI отобразятся результаты создания реестра, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-157">The Azure CLI will display the results of your registry creation; for example:</span></span>  

   ```json
   {
     "adminUserEnabled": true,
     "creationDate": "2017-09-15T01:00:00.000000+00:00",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.ContainerRegistry/registries/wingtiptoysregistry",
     "location": "westeurope",
     "loginServer": "wingtiptoysregistry.azurecr.io",
     "name": "wingtiptoysregistry",
     "provisioningState": "Succeeded",
     "resourceGroup": "wingtiptoys-kubernetes",
     "sku": {
       "name": "Basic",
       "tier": "Basic"
     },
     "storageAccount": {
       "name": "wingtiptoysregistr000000"
     },
     "tags": {},
     "type": "Microsoft.ContainerRegistry/registries"
   }
   ```

1. <span data-ttu-id="740e1-158">Получите пароль для реестра контейнеров из Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="740e1-158">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   <span data-ttu-id="740e1-159">В Azure CLI отобразится пароль для реестра, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-159">The Azure CLI will display the password for your registry; for example:</span></span>  

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="740e1-160">Перейдите в каталог конфигурации для установки Maven (по умолчанию ~/.m2/ или C:\Users\username\.m2) и откройте файл *settings.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="740e1-160">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="740e1-161">Добавьте URL-адрес, имя пользователя и пароль реестра контейнеров Azure для новой коллекции `<server>` в файле *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="740e1-161">Add your Azure Container Registry URL, username and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="740e1-162">`id` и `username` — это имена реестра.</span><span class="sxs-lookup"><span data-stu-id="740e1-162">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="740e1-163">Используйте значение `password` из предыдущей команды (без кавычек).</span><span class="sxs-lookup"><span data-stu-id="740e1-163">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry.azurecr.io</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="740e1-164">Перейдите в каталог завершенного проекта для приложения Spring Boot (например, *C:\SpringBoot\gs-spring-boot-docker\complete* или */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*) и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="740e1-164">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="740e1-165">Обновите коллекцию `<properties>` в файле *pom.xml*, добавив значение сервера входа для реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="740e1-165">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="740e1-166">Обновите коллекцию `<plugins>` в файле *pom.xml* таким образом, чтобы в `<plugin>` содержались адрес сервера входа и имя реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="740e1-166">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
     <groupId>com.spotify</groupId>
     <artifactId>dockerfile-maven-plugin</artifactId>
     <version>1.3.4</version>
     <configuration>
       <repository>${docker.image.prefix}/${project.artifactId}</repository>
       <serverId>${docker.image.prefix}</serverId>
       <registryUrl>https://${docker.image.prefix}</registryUrl>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="740e1-167">Перейдите в каталог завершенного проекта для приложения Spring Boot и выполните указанную ниже команду Maven для создания контейнера Docker и отправки образа в реестр:</span><span class="sxs-lookup"><span data-stu-id="740e1-167">Navigate to the completed project directory for your Spring Boot application, and run the following Maven command to build the Docker container and push the image to your registry:</span></span>

   ```shell
   mvn package dockerfile:build -DpushImage
   ```

   <span data-ttu-id="740e1-168">В Maven отобразятся результаты создания, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-168">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 38.113 s
   [INFO] Finished at: 2017-09-15T02:00:00-07:00
   [INFO] Final Memory: 47M/338M
   [INFO] ----------------------------------------------------
   ```


## <a name="configure-your-spring-boot-app-to-use-the-fabric8-maven-plugin"></a><span data-ttu-id="740e1-169">Настройка приложения Spring Boot для использования подключаемого модуля Maven Fabric8</span><span class="sxs-lookup"><span data-stu-id="740e1-169">Configure your Spring Boot app to use the Fabric8 Maven plugin</span></span>

1. <span data-ttu-id="740e1-170">Перейдите в каталог завершенного проекта для приложения Spring Boot (например, *C:\SpringBoot\gs-spring-boot-docker\complete* или */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*) и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="740e1-170">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="740e1-171">Обновите коллекцию `<plugins>` в файле *pom.xml*, чтобы добавить подключаемый модуль Maven Fabric8.</span><span class="sxs-lookup"><span data-stu-id="740e1-171">Update the `<plugins>` collection in the *pom.xml* file to add the Fabric8 Maven plugin:</span></span>

   ```xml
   <plugin>
     <groupId>io.fabric8</groupId>
     <artifactId>fabric8-maven-plugin</artifactId>
     <version>3.5.30</version>
     <configuration>
       <ignoreServices>false</ignoreServices>
       <registry>${docker.image.prefix}</registry>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="740e1-172">Перейдите в основной исходный каталог для приложения Spring Boot (например, *C:\SpringBoot\gs-spring-boot-docker\complete\src\main* или */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*) и создайте папку с именем *fabric8*.</span><span class="sxs-lookup"><span data-stu-id="740e1-172">Navigate to the main source directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete\src\main*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*"), and create a new folder named "*fabric8*".</span></span>

1. <span data-ttu-id="740e1-173">Создайте три файла фрагмента YAML в новой папке *fabric8*.</span><span class="sxs-lookup"><span data-stu-id="740e1-173">Create three YAML fragment files in the new *fabric8* folder:</span></span>

   <span data-ttu-id="740e1-174">а.</span><span class="sxs-lookup"><span data-stu-id="740e1-174">a.</span></span> <span data-ttu-id="740e1-175">Создайте файл с именем **deployment.yml** со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="740e1-175">Create a file named **deployment.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: extensions/v1beta1
      kind: Deployment
      metadata:
        name: ${project.artifactId}
        labels:
          run: gs-spring-boot-docker
      spec:
        replicas: 1
        selector:
          matchLabels:
            run: gs-spring-boot-docker
        strategy:
          rollingUpdate:
            maxSurge: 1
            maxUnavailable: 1
          type: RollingUpdate
        template:
          metadata:
            labels:
              run: gs-spring-boot-docker
          spec:
            containers:
            - image: ${docker.image.prefix}/${project.artifactId}:latest
              name: gs-spring-boot-docker
              imagePullPolicy: Always
              ports:
              - containerPort: 8080
            imagePullSecrets:
              - name: mysecrets
      ```

   <span data-ttu-id="740e1-176">b.</span><span class="sxs-lookup"><span data-stu-id="740e1-176">b.</span></span> <span data-ttu-id="740e1-177">Создайте файл с именем **secrets.yml** со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="740e1-177">Create a file named **secrets.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: v1
      kind: Secret
      metadata:
        name: mysecrets
        namespace: default
        annotations:
          maven.fabric8.io/dockerServerId:  ${docker.image.prefix}
      type: kubernetes.io/dockercfg
      ```

   <span data-ttu-id="740e1-178">c.</span><span class="sxs-lookup"><span data-stu-id="740e1-178">c.</span></span> <span data-ttu-id="740e1-179">Создайте файл с именем **service.yml** со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="740e1-179">Create a file named **service.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: v1
      kind: Service
      metadata:
        name: ${project.artifactId}
        labels:
          expose: "true"
      spec:
        ports:
        - port: 80
          targetPort: 8080
        type: LoadBalancer
      ```

1. <span data-ttu-id="740e1-180">Запустите следующую команду Maven, чтобы создать файл списка ресурсов Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="740e1-180">Run the following Maven command to build the Kubernetes resource list file:</span></span>

   ```shell
   mvn fabric8:resource
   ```

   <span data-ttu-id="740e1-181">Эта команда объединяет все файлы YAML ресурсов Kubernetes в папке *src/main/fabric8* в файл YAML, содержащий список ресурсов Kubernetes, который можно применить непосредственно к кластеру Kubernetes или экспортировать в чарт Helm.</span><span class="sxs-lookup"><span data-stu-id="740e1-181">This command merges all Kubernetes resource yaml files under the *src/main/fabric8* folder to a YAML file that contains a Kubernetes resource list, which can be applied to Kubernetes cluster directly or export to a helm chart.</span></span>

   <span data-ttu-id="740e1-182">В Maven отобразятся результаты создания, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-182">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 16.744 s
   [INFO] Finished at: 2017-09-15T02:35:00-07:00
   [INFO] Final Memory: 30M/290M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="740e1-183">Выполните следующую команду Maven, чтобы применить файл списка ресурсов к кластеру Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="740e1-183">Run the following Maven command to apply the resource list file to your Kubernetes cluster:</span></span>

   ```shell
   mvn fabric8:apply
   ```

   <span data-ttu-id="740e1-184">В Maven отобразятся результаты создания, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-184">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 14.814 s
   [INFO] Finished at: 2017-09-15T02:41:00-07:00
   [INFO] Final Memory: 35M/288M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="740e1-185">После развертывания приложения в кластере отправьте запрос к внешнему IP-адресу с помощью приложения `kubectl`, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-185">Once the app is deployed to the cluster, query the external IP address using the `kubectl` application; for example:</span></span>
   ```shell
   kubectl get svc -w
   ```

   <span data-ttu-id="740e1-186">В `kubectl` отобразятся внутренний и внешний IP-адреса, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-186">`kubectl` will display your internal and external IP addresses; for example:</span></span>
   
   ```shell
   NAME                    CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
   kubernetes              10.0.0.1     <none>        443/TCP        19h
   gs-spring-boot-docker   10.0.242.8   13.65.196.3   80:31215/TCP   3m
   ```
   
   <span data-ttu-id="740e1-187">Вы можете использовать внешний IP-адрес, чтобы открыть приложение в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="740e1-187">You can use the external IP address to open your application in a web browser.</span></span>

   ![Просмотр примера приложения извне][SB02]

## <a name="delete-your-kubernetes-cluster"></a><span data-ttu-id="740e1-189">Удаление кластера Kubernetes</span><span class="sxs-lookup"><span data-stu-id="740e1-189">Delete your Kubernetes cluster</span></span>

<span data-ttu-id="740e1-190">Если кластер Kubernetes больше не нужен, можно использовать команду `az group delete`, чтобы удалить группу ресурсов, что приведет к удалению всех связанных ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="740e1-190">When your Kubernetes cluster is no longer needed, you can use the `az group delete` command to remove the resource group, which will remove all of its related resources; for example:</span></span>

   ```azurecli
   az group delete --name wingtiptoys-kubernetes --yes --no-wait
   ```

## <a name="next-steps"></a><span data-ttu-id="740e1-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="740e1-191">Next steps</span></span>

<span data-ttu-id="740e1-192">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="740e1-192">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="740e1-193">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="740e1-193">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="740e1-194">Развертывание приложения Spring Boot в Linux в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="740e1-194">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)
* [<span data-ttu-id="740e1-195">Развертывание приложения Spring Boot в кластере Kubernetes в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="740e1-195">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="740e1-196">Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [инструментов Java для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="740e1-196">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="740e1-197">Дополнительные сведения о Spring Boot в образце проекта Docker см. в разделе [Spring Boot on Docker Getting Started] (Начало работы с Spring Boot в Docker).</span><span class="sxs-lookup"><span data-stu-id="740e1-197">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="740e1-198">Справку по началу работы с собственными приложениями Spring Boot см. на странице **Spring Initializr** по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="740e1-198">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at <https://start.spring.io/>.</span></span>

<span data-ttu-id="740e1-199">Дополнительные сведения о начале создания простого приложения Spring Boot см. на странице Spring Initializr по адресу <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="740e1-199">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at <https://start.spring.io/>.</span></span>

<span data-ttu-id="740e1-200">Дополнительные примеры использования пользовательских образов Docker в Azure см. в разделе [Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux].</span><span class="sxs-lookup"><span data-stu-id="740e1-200">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[службе контейнеров Azure]: https://azure.microsoft.com/services/container-service/
[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Fabric8]: https://fabric8.io/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[инструментов Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Kubernetes]: https://kubernetes.io/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB02.png
