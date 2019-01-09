---
title: Развертывание приложения Spring Boot с помощью подключаемого модуля Maven Fabric8
description: В этом руководстве содержатся пошаговые инструкции по развертыванию приложения Spring Boot для Apache Maven с помощью подключаемого модуля Maven Fabric8 в Microsoft Azure.
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
ms.openlocfilehash: 72eb49a764bdf15339e6cd17c6a7f997495dcf09
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991608"
---
# <a name="deploy-a-spring-boot-app-using-the-fabric8-maven-plugin"></a><span data-ttu-id="55311-103">Развертывание приложения Spring Boot с помощью подключаемого модуля Maven Fabric8</span><span class="sxs-lookup"><span data-stu-id="55311-103">Deploy a Spring Boot app using the Fabric8 Maven Plugin</span></span>

<span data-ttu-id="55311-104">**[Fabric8]**  — это решение с открытым кодом на базе **[Kubernetes]**, помогающее разработчикам создавать приложения в контейнерах Linux.</span><span class="sxs-lookup"><span data-stu-id="55311-104">**[Fabric8]** is an open-source solution that is built on **[Kubernetes]**, which helps developers create applications in Linux containers.</span></span>

<span data-ttu-id="55311-105">В этом руководстве рассматривается применение подключаемого модуля Fabric8 в Maven для разработки и развертывания приложения на узле Linux в [Служба контейнеров Azure].</span><span class="sxs-lookup"><span data-stu-id="55311-105">This tutorial walks you through using the Fabric8 plugin for Maven to develop to deploy an application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55311-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="55311-106">Prerequisites</span></span>

<span data-ttu-id="55311-107">Для работы с этим руководством требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="55311-107">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="55311-108">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="55311-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="55311-109">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="55311-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="55311-110">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="55311-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="55311-111">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="55311-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="55311-112">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="55311-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="55311-113">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="55311-113">A [Git] client.</span></span>
* <span data-ttu-id="55311-114">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="55311-114">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="55311-115">С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="55311-115">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="55311-116">Создание веб-приложения Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="55311-116">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="55311-117">Ниже представлены инструкции по созданию веб-приложения Spring Boot и его локальному тестированию.</span><span class="sxs-lookup"><span data-stu-id="55311-117">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="55311-118">Откройте командную строку и создайте локальный каталог для размещения приложения, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="55311-118">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```shell
   md /home/GenaSoto/SpringBoot
   cd /home/GenaSoto/SpringBoot
   ```
   <span data-ttu-id="55311-119">-- или --</span><span class="sxs-lookup"><span data-stu-id="55311-119">-- or --</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```

1. <span data-ttu-id="55311-120">Клонируйте пример проекта [Spring Boot on Docker Getting Started] в каталог.</span><span class="sxs-lookup"><span data-stu-id="55311-120">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="55311-121">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="55311-121">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```
   <span data-ttu-id="55311-122">-- или --</span><span class="sxs-lookup"><span data-stu-id="55311-122">-- or --</span></span>
   ```shell
   cd gs-spring-boot-docker\complete
   ```

1. <span data-ttu-id="55311-123">Используйте Maven для создания и запуска примера приложения.</span><span class="sxs-lookup"><span data-stu-id="55311-123">Use Maven to build and run the sample app.</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```

1. <span data-ttu-id="55311-124">Чтобы протестировать веб-приложение, перейдите по адресу http://localhost:8080 или введите такую команду `curl`:</span><span class="sxs-lookup"><span data-stu-id="55311-124">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="55311-125">Должно появиться следующее сообщение: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="55311-125">You should see a **Hello Docker World** message displayed.</span></span>

   ![Локальный просмотр примера приложения][SB01]


## <a name="install-the-kubernetes-command-line-interface-and-create-an-azure-resource-group-using-the-azure-cli"></a><span data-ttu-id="55311-127">Установка интерфейса командной строки Kubernetes и создание группы ресурсов Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="55311-127">Install the Kubernetes command-line interface and create an Azure resource group using the Azure CLI</span></span>

1. <span data-ttu-id="55311-128">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="55311-128">Open a command prompt.</span></span>

1. <span data-ttu-id="55311-129">Введите следующую команду, чтобы войти в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="55311-129">Type the following command to log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="55311-130">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="55311-130">Follow the instructions to complete the login process</span></span>

   <span data-ttu-id="55311-131">В интерфейсе командной строки Azure отобразится список учетных записей, например:</span><span class="sxs-lookup"><span data-stu-id="55311-131">The Azure CLI will display a list of your accounts; for example:</span></span>

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

1. <span data-ttu-id="55311-132">Если интерфейс командной строки Kubernetes еще не установлен (`kubectl`), можно установить его с помощью Azure CLI, например:</span><span class="sxs-lookup"><span data-stu-id="55311-132">If you do not already have the Kubernetes command-line interface (`kubectl`) installed, you can install using the Azure CLI; for example:</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="55311-133">Пользователи Linux могут добавить к этой команде префикс `sudo`, так как она развертывает интерфейс командной строки Kubernetes в `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="55311-133">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   >
   > <span data-ttu-id="55311-134">Если `kubectl` уже установлен и ваша версия `kubectl` устарела, при попытке выполнить действия, приведенные далее в этой статье, может появиться сообщение об ошибке (как в следующем примере).</span><span class="sxs-lookup"><span data-stu-id="55311-134">If you already have `kubectl`) installed and your version of `kubectl` is too old, you may see an error message similar to the following example when you attempt to complete the steps listed later in this article:</span></span>
   >
   > ```
   > error: group map[autoscaling:0x0000000000 batch:0x0000000000 certificates.k8s.io
   > :0x0000000000 extensions:0x0000000000 storage.k8s.io:0x0000000000 apps:0x0000000
   > 000 authentication.k8s.io:0x0000000000 policy:0x0000000000 rbac.authorization.k8
   > s.io:0x0000000000 federation:0x0000000000 authorization.k8s.io:0x0000000000 comp
   > onentconfig:0x0000000000] is already registered
   > ```
   >
   > <span data-ttu-id="55311-135">В этом случае необходимо переустановить `kubectl`, чтобы обновить версию.</span><span class="sxs-lookup"><span data-stu-id="55311-135">If this happens, you will need to reinstall `kubectl` to update your version.</span></span>
   >

1. <span data-ttu-id="55311-136">Создайте группу ресурсов Azure, используемых в этой статье, например:</span><span class="sxs-lookup"><span data-stu-id="55311-136">Create a resource group for the Azure resources that you will use in this tutorial; for example:</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=westeurope
   ```
   <span data-ttu-id="55311-137">Описание</span><span class="sxs-lookup"><span data-stu-id="55311-137">Where:</span></span>  
      * <span data-ttu-id="55311-138">*wingtiptoys-kubernetes* — уникальное имя для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="55311-138">*wingtiptoys-kubernetes* is a unique name for your resource group</span></span>  
      * <span data-ttu-id="55311-139">*westeurope* — соответствующее географическое расположение для приложения.</span><span class="sxs-lookup"><span data-stu-id="55311-139">*westeurope* is an appropriate geographic location for your application</span></span>  

   <span data-ttu-id="55311-140">В Azure CLI отобразятся результаты созданной группы ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="55311-140">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

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


## <a name="create-a-kubernetes-cluster-using-the-azure-cli"></a><span data-ttu-id="55311-141">Создание кластера Kubernetes с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="55311-141">Create a Kubernetes cluster using the Azure CLI</span></span>

1. <span data-ttu-id="55311-142">Создайте кластер Kubernetes в новой группе ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="55311-142">Create a Kubernetes cluster in your new resource group; for example:</span></span>  
   ```azurecli 
   az acs create --orchestrator-type kubernetes --resource-group wingtiptoys-kubernetes --name wingtiptoys-cluster --generate-ssh-keys --dns-prefix=wingtiptoys
   ```
   <span data-ttu-id="55311-143">Описание</span><span class="sxs-lookup"><span data-stu-id="55311-143">Where:</span></span>  
      * <span data-ttu-id="55311-144">*wingtiptoys-kubernetes* — имя группы ресурсов, описанной в этой статье.</span><span class="sxs-lookup"><span data-stu-id="55311-144">*wingtiptoys-kubernetes* is the name of your resource group from earlier in this article</span></span>  
      * <span data-ttu-id="55311-145">*wingtiptoys-cluster* — уникальное имя для кластера Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="55311-145">*wingtiptoys-cluster* is a unique name for your Kubernetes cluster</span></span>
      * <span data-ttu-id="55311-146">*wingtiptoys* — уникальное имя DNS-имени для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="55311-146">*wingtiptoys* is a unique name DNS name for your application</span></span>

   <span data-ttu-id="55311-147">В Azure CLI отобразятся результаты создания кластера, например:</span><span class="sxs-lookup"><span data-stu-id="55311-147">The Azure CLI will display the results of your cluster creation; for example:</span></span>  

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

1. <span data-ttu-id="55311-148">Скачайте учетные данные для нового кластера Kubernetes, например:</span><span class="sxs-lookup"><span data-stu-id="55311-148">Download your credentials for your new Kubernetes cluster; for example:</span></span>  
   ```azurecli 
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes --name wingtiptoys-cluster
   ```

1. <span data-ttu-id="55311-149">Проверьте подключение с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="55311-149">Verify your connection with the following command:</span></span>
   ```shell 
   kubectl get nodes
   ```

   <span data-ttu-id="55311-150">Появится список узлов и состояний, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="55311-150">You should see a list of nodes and statuses like the following example:</span></span>

   ```shell
   NAME                    STATUS                     AGE       VERSION
   k8s-agent-00000000-0    Ready                      5h        v1.6.6
   k8s-agent-00000000-1    Ready                      5h        v1.6.6
   k8s-agent-00000000-2    Ready                      5h        v1.6.6
   k8s-master-00000000-0   Ready,SchedulingDisabled   5h        v1.6.6
   ```


## <a name="create-a-private-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="55311-151">Создание закрытого реестра контейнеров Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="55311-151">Create a private Azure container registry using the Azure CLI</span></span>

1. <span data-ttu-id="55311-152">Создайте закрытый реестр контейнеров Azure в группе ресурсов для размещения образа Docker, например:</span><span class="sxs-lookup"><span data-stu-id="55311-152">Create a private Azure container registry in your resource group to host your Docker image; for example:</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes --location westeurope --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="55311-153">Описание</span><span class="sxs-lookup"><span data-stu-id="55311-153">Where:</span></span>

   | <span data-ttu-id="55311-154">Параметр</span><span class="sxs-lookup"><span data-stu-id="55311-154">Parameter</span></span> | <span data-ttu-id="55311-155">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="55311-155">Description</span></span> |
   |---|---|
   | `wingtiptoys-kubernetes` | <span data-ttu-id="55311-156">Определяет имя группы ресурсов, описанной в этой статье.</span><span class="sxs-lookup"><span data-stu-id="55311-156">Specifies the name of your resource group from earlier in this article.</span></span> |
   | `wingtiptoysregistry` | <span data-ttu-id="55311-157">Определяет уникальное имя для закрытого реестра.</span><span class="sxs-lookup"><span data-stu-id="55311-157">Specifies a unique name for your private registry.</span></span> |
   | `westeurope` | <span data-ttu-id="55311-158">Определяет соответствующее географическое расположение для приложения.</span><span class="sxs-lookup"><span data-stu-id="55311-158">Specifies an appropriate geographic location for your application.</span></span> |

   <span data-ttu-id="55311-159">В Azure CLI отобразятся результаты создания реестра, например:</span><span class="sxs-lookup"><span data-stu-id="55311-159">The Azure CLI will display the results of your registry creation; for example:</span></span>  

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

2. <span data-ttu-id="55311-160">Получите пароль для реестра контейнеров из Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="55311-160">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   <span data-ttu-id="55311-161">В Azure CLI отобразится пароль для реестра, например:</span><span class="sxs-lookup"><span data-stu-id="55311-161">The Azure CLI will display the password for your registry; for example:</span></span>  

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

3. <span data-ttu-id="55311-162">Перейдите в каталог конфигурации для установки Maven (по умолчанию ~/.m2/ или C:\Users\username\.m2) и откройте файл *settings.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="55311-162">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

4. <span data-ttu-id="55311-163">Добавьте URL-адрес, имя пользователя и пароль реестра контейнеров Azure для новой коллекции `<server>` в файле *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="55311-163">Add your Azure Container Registry URL, username and password to a new `<server>` collection in the *settings.xml* file.</span></span>
   <span data-ttu-id="55311-164">`id` и `username` — это имена реестра.</span><span class="sxs-lookup"><span data-stu-id="55311-164">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="55311-165">Используйте значение `password` из предыдущей команды (без кавычек).</span><span class="sxs-lookup"><span data-stu-id="55311-165">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry.azurecr.io</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

5. <span data-ttu-id="55311-166">Перейдите в каталог завершенного проекта для приложения Spring Boot (например, *C:\SpringBoot\gs-spring-boot-docker\complete* или */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*) и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="55311-166">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

6. <span data-ttu-id="55311-167">Обновите коллекцию `<properties>` в файле *pom.xml*, добавив значение сервера входа для реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="55311-167">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

7. <span data-ttu-id="55311-168">Обновите коллекцию `<plugins>` в файле *pom.xml* таким образом, чтобы в `<plugin>` содержались адрес сервера входа и имя реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="55311-168">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

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

8. <span data-ttu-id="55311-169">Перейдите в каталог завершенного проекта для приложения Spring Boot и выполните указанную ниже команду Maven для создания контейнера Docker и отправки образа в реестр:</span><span class="sxs-lookup"><span data-stu-id="55311-169">Navigate to the completed project directory for your Spring Boot application, and run the following Maven command to build the Docker container and push the image to your registry:</span></span>

   ```shell
   mvn package dockerfile:build -DpushImage
   ```

   <span data-ttu-id="55311-170">В Maven отобразятся результаты создания, например:</span><span class="sxs-lookup"><span data-stu-id="55311-170">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 38.113 s
   [INFO] Finished at: 2017-09-15T02:00:00-07:00
   [INFO] Final Memory: 47M/338M
   [INFO] ----------------------------------------------------
   ```


## <a name="configure-your-spring-boot-app-to-use-the-fabric8-maven-plugin"></a><span data-ttu-id="55311-171">Настройка приложения Spring Boot для использования подключаемого модуля Maven Fabric8</span><span class="sxs-lookup"><span data-stu-id="55311-171">Configure your Spring Boot app to use the Fabric8 Maven plugin</span></span>

1. <span data-ttu-id="55311-172">Перейдите в каталог завершенного проекта для приложения Spring Boot (например *C:\SpringBoot\gs-spring-boot-docker\complete* или */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*) и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="55311-172">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="55311-173">Обновите коллекцию `<plugins>` в файле *pom.xml*, чтобы добавить подключаемый модуль Maven Fabric8.</span><span class="sxs-lookup"><span data-stu-id="55311-173">Update the `<plugins>` collection in the *pom.xml* file to add the Fabric8 Maven plugin:</span></span>

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

1. <span data-ttu-id="55311-174">Перейдите в основной исходный каталог для приложения Spring Boot (например *C:\SpringBoot\gs-spring-boot-docker\complete\src\main* или */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*) и создайте папку с именем *fabric8*.</span><span class="sxs-lookup"><span data-stu-id="55311-174">Navigate to the main source directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete\src\main*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*"), and create a new folder named "*fabric8*".</span></span>

1. <span data-ttu-id="55311-175">Создайте три файла фрагмента YAML в новой папке *fabric8*.</span><span class="sxs-lookup"><span data-stu-id="55311-175">Create three YAML fragment files in the new *fabric8* folder:</span></span>

   <span data-ttu-id="55311-176">a.</span><span class="sxs-lookup"><span data-stu-id="55311-176">a.</span></span> <span data-ttu-id="55311-177">Создайте файл с именем **deployment.yml** со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="55311-177">Create a file named **deployment.yml** with the following contents:</span></span>
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

   <span data-ttu-id="55311-178">b.</span><span class="sxs-lookup"><span data-stu-id="55311-178">b.</span></span> <span data-ttu-id="55311-179">Создайте файл с именем **secrets.yml** со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="55311-179">Create a file named **secrets.yml** with the following contents:</span></span>
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

   <span data-ttu-id="55311-180">c.</span><span class="sxs-lookup"><span data-stu-id="55311-180">c.</span></span> <span data-ttu-id="55311-181">Создайте файл с именем **service.yml** со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="55311-181">Create a file named **service.yml** with the following contents:</span></span>
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

1. <span data-ttu-id="55311-182">Запустите следующую команду Maven, чтобы создать файл списка ресурсов Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="55311-182">Run the following Maven command to build the Kubernetes resource list file:</span></span>

   ```shell
   mvn fabric8:resource
   ```

   <span data-ttu-id="55311-183">Эта команда объединяет все файлы YAML ресурсов Kubernetes в папке *src/main/fabric8* в файл YAML, содержащий список ресурсов Kubernetes, который можно применить непосредственно к кластеру Kubernetes или экспортировать в чарт Helm.</span><span class="sxs-lookup"><span data-stu-id="55311-183">This command merges all Kubernetes resource yaml files under the *src/main/fabric8* folder to a YAML file that contains a Kubernetes resource list, which can be applied to Kubernetes cluster directly or export to a helm chart.</span></span>

   <span data-ttu-id="55311-184">В Maven отобразятся результаты создания, например:</span><span class="sxs-lookup"><span data-stu-id="55311-184">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 16.744 s
   [INFO] Finished at: 2017-09-15T02:35:00-07:00
   [INFO] Final Memory: 30M/290M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="55311-185">Выполните следующую команду Maven, чтобы применить файл списка ресурсов к кластеру Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="55311-185">Run the following Maven command to apply the resource list file to your Kubernetes cluster:</span></span>

   ```shell
   mvn fabric8:apply
   ```

   <span data-ttu-id="55311-186">В Maven отобразятся результаты создания, например:</span><span class="sxs-lookup"><span data-stu-id="55311-186">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 14.814 s
   [INFO] Finished at: 2017-09-15T02:41:00-07:00
   [INFO] Final Memory: 35M/288M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="55311-187">После развертывания приложения в кластере отправьте запрос к внешнему IP-адресу с помощью приложения `kubectl`, например:</span><span class="sxs-lookup"><span data-stu-id="55311-187">Once the app is deployed to the cluster, query the external IP address using the `kubectl` application; for example:</span></span>
   ```shell
   kubectl get svc -w
   ```

   <span data-ttu-id="55311-188">В `kubectl` отобразятся внутренний и внешний IP-адреса, например:</span><span class="sxs-lookup"><span data-stu-id="55311-188">`kubectl` will display your internal and external IP addresses; for example:</span></span>

   ```shell
   NAME                    CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
   kubernetes              10.0.0.1     <none>        443/TCP        19h
   gs-spring-boot-docker   10.0.242.8   13.65.196.3   80:31215/TCP   3m
   ```

   <span data-ttu-id="55311-189">Вы можете использовать внешний IP-адрес, чтобы открыть приложение в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="55311-189">You can use the external IP address to open your application in a web browser.</span></span>

   ![Просмотр примера приложения извне][SB02]

## <a name="delete-your-kubernetes-cluster"></a><span data-ttu-id="55311-191">Удаление кластера Kubernetes</span><span class="sxs-lookup"><span data-stu-id="55311-191">Delete your Kubernetes cluster</span></span>

<span data-ttu-id="55311-192">Если кластер Kubernetes больше не нужен, можно использовать команду `az group delete`, чтобы удалить группу ресурсов, что приведет к удалению всех связанных ресурсов, например:</span><span class="sxs-lookup"><span data-stu-id="55311-192">When your Kubernetes cluster is no longer needed, you can use the `az group delete` command to remove the resource group, which will remove all of its related resources; for example:</span></span>

   ```azurecli
   az group delete --name wingtiptoys-kubernetes --yes --no-wait
   ```

## <a name="next-steps"></a><span data-ttu-id="55311-193">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="55311-193">Next steps</span></span>

<span data-ttu-id="55311-194">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="55311-194">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="55311-195">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="55311-195">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="55311-196">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="55311-196">Additional Resources</span></span>

<span data-ttu-id="55311-197">Дополнительные сведения об использовании приложений Spring Boot в Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="55311-197">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="55311-198">Развертывание приложения Spring Boot Application в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="55311-198">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="55311-199">Развертывание приложения Spring Boot в Linux в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="55311-199">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)
* [<span data-ttu-id="55311-200">Развертывание приложения Spring Boot в кластере Kubernetes в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="55311-200">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="55311-201">Дополнительные сведения об использовании Java в Azure см. в статьях [Azure для разработчиков Java] и [Working with Azure DevOps and Java] (Работа с Azure DevOps и Java).</span><span class="sxs-lookup"><span data-stu-id="55311-201">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="55311-202">Дополнительные сведения о Spring Boot в образце проекта Docker см. в разделе [Spring Boot on Docker Getting Started] (Начало работы с Spring Boot в Docker).</span><span class="sxs-lookup"><span data-stu-id="55311-202">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="55311-203">Справку по началу работы с собственными приложениями Spring Boot см. на странице **Spring Initializr**: <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="55311-203">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at <https://start.spring.io/>.</span></span>

<span data-ttu-id="55311-204">Дополнительные сведения о создании простого приложения Spring Boot см. на странице Spring Initializr: <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="55311-204">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at <https://start.spring.io/>.</span></span>

<span data-ttu-id="55311-205">Дополнительные примеры использования пользовательских образов Docker в Azure см. в разделе [Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux].</span><span class="sxs-lookup"><span data-stu-id="55311-205">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Служба контейнеров Azure]: https://azure.microsoft.com/services/container-service/
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure для разработчиков Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Fabric8]: https://fabric8.io/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/java/ (Работа с Azure DevOps и Java)
[Kubernetes]: https://kubernetes.io/
[Maven]: http://maven.apache.org/
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB02.png
