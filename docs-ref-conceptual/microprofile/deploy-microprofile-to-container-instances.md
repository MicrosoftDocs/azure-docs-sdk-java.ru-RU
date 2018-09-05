---
title: Развертывание приложения MicroProfile в облаке с помощью Docker и Azure
description: Узнайте, как развернуть приложение MicroProfile в облаке с помощью Docker и службы "Экземпляры контейнеров Azure".
services: container-instances;container-retistry
documentationcenter: java
author: brborges
manager: routlaw
editor: brborges
ms.assetid: ''
ms.author: brborges
ms.date: 07/30/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: c6254d11ee1596a23076931c9a2a2370b5f52409
ms.sourcegitcommit: 3d0896f821907278547c283c54b53fbd7f4f30f0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2018
ms.locfileid: "43153864"
---
# <a name="deploy-a-microprofile-application-to-the-cloud-with-docker-and-azure"></a><span data-ttu-id="60a2e-103">Развертывание приложения MicroProfile в облаке с помощью Docker и Azure</span><span class="sxs-lookup"><span data-stu-id="60a2e-103">Deploy a MicroProfile application to the cloud with Docker and Azure</span></span>

<span data-ttu-id="60a2e-104">В этой статье показано, как упаковать приложение [MicroProfile.io] в контейнер Docker и запустить его в службе "Экземпляры контейнеров Azure".</span><span class="sxs-lookup"><span data-stu-id="60a2e-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
>
> <span data-ttu-id="60a2e-105">Эта процедура подходит для любой реализации MicroProfile.io при условии, что образ контейнера Docker является самовыполняющимся (т. е. включает среду выполнения).</span><span class="sxs-lookup"><span data-stu-id="60a2e-105">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60a2e-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="60a2e-106">Prerequisites</span></span>

<span data-ttu-id="60a2e-107">Для работы с этим руководством требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="60a2e-107">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="60a2e-108">Подписка Azure. Если у вас ее еще нет, создайте [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="60a2e-108">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="60a2e-109">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="60a2e-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="60a2e-110">Актуальный [пакет разработчиков Java (JDK)] версии 1.8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="60a2e-110">An up-to-date [Java Development Kit (JDK)], version 1.8 or later.</span></span>
* <span data-ttu-id="60a2e-111">Средство сборки [Maven] от Apache (версии 3 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="60a2e-111">Apache's [Maven] build tool (version 3+).</span></span>
* <span data-ttu-id="60a2e-112">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="60a2e-112">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="60a2e-113">Пример приложения MicroProfile Hello Azure</span><span class="sxs-lookup"><span data-stu-id="60a2e-113">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="60a2e-114">В этой статье мы используем пример приложения [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure):</span><span class="sxs-lookup"><span data-stu-id="60a2e-114">For this article, we will use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample:</span></span>

### <a name="clone-build-and-run-locally"></a><span data-ttu-id="60a2e-115">Клонирование, сборка и локальный запуск</span><span class="sxs-lookup"><span data-stu-id="60a2e-115">Clone, build, and run locally</span></span>

```bash
$ git clone https://github.com/Azure-Samples/microprofile-hello-azure.git
$ mvn clean package
...
[INFO] BUILD SUCCESS
...
$ mvn payara-micro:start
...
[2018-07-30T13:34:51.553-0700] [] [INFO] [] [PayaraMicro] [tid: _ThreadID=1 _ThreadName=main] [timeMillis: 1532982891553] [levelValue: 800] Payara Micro  5.182 #badassmicrofish (build 303) ready in 10,304 (ms)
...
```

<span data-ttu-id="60a2e-116">Приложение можно протестировать с помощью команды `curl` или [веб-браузера](http://localhost:8080/api/hello):</span><span class="sxs-lookup"><span data-stu-id="60a2e-116">You can test the application by calling `curl` or visiting through a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-to-azure"></a><span data-ttu-id="60a2e-117">Развертывание в Azure</span><span class="sxs-lookup"><span data-stu-id="60a2e-117">Deploy to Azure</span></span>

<span data-ttu-id="60a2e-118">Теперь развернем это приложение в облаке с помощью служб [Экземпляры контейнеров Azure] и [Реестр контейнеров Azure].</span><span class="sxs-lookup"><span data-stu-id="60a2e-118">Now let's bring this application to the cloud using [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="60a2e-119">Создание образа Docker</span><span class="sxs-lookup"><span data-stu-id="60a2e-119">Build a Docker image</span></span>

<span data-ttu-id="60a2e-120">Пример проекта уже содержит файл Dockerfile, который можно использовать.</span><span class="sxs-lookup"><span data-stu-id="60a2e-120">The sample project already provides a Dockerfile you can use.</span></span> <span data-ttu-id="60a2e-121">Вам не нужно устанавливать Docker, так как мы воспользуемся службой "Сборка Реестра контейнеров Azure" для сборки образа в облаке.</span><span class="sxs-lookup"><span data-stu-id="60a2e-121">You don't need Docker installed though, as we will use Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="60a2e-122">Для сборки образа и его подготовки к запуску в Azure выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="60a2e-122">To build the image and be ready to run on Azure, you will have to follow these steps:</span></span>

1. <span data-ttu-id="60a2e-123">Установите Azure CLI и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="60a2e-123">Install and log in with Azure CLI</span></span>
1. <span data-ttu-id="60a2e-124">Создайте группу ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="60a2e-124">Create an Azure Resource Group</span></span>
1. <span data-ttu-id="60a2e-125">Создайте Реестр контейнеров Azure (ACR).</span><span class="sxs-lookup"><span data-stu-id="60a2e-125">Create an Azure Container Registry (ACR)</span></span>
1. <span data-ttu-id="60a2e-126">Соберите образ Docker.</span><span class="sxs-lookup"><span data-stu-id="60a2e-126">Build the Docker image</span></span>
1. <span data-ttu-id="60a2e-127">Опубликуйте образ Docker в созданном ранее реестре ACR.</span><span class="sxs-lookup"><span data-stu-id="60a2e-127">Publish the Docker image to the ACR created before</span></span>
1. <span data-ttu-id="60a2e-128">Дополнительно: выполните сборку образа и опубликуйте его в ACR с помощью одной команды.</span><span class="sxs-lookup"><span data-stu-id="60a2e-128">(Optionally) Build and publish to ACR in one command</span></span>


#### <a name="set-up-azure-cli"></a><span data-ttu-id="60a2e-129">Настройка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="60a2e-129">Set up Azure CLI</span></span>

<span data-ttu-id="60a2e-130">Убедитесь, что у вас есть подписка на Azure, установлен [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) и вы выполнили проверку подлинности в своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="60a2e-130">Make sure you have an Azure subscription, [Azure CLI installed](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you are authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="60a2e-131">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="60a2e-131">Create a Resource Group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="60a2e-132">Создание экземпляра Реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="60a2e-132">Create an Azure Container Registry instance</span></span>

<span data-ttu-id="60a2e-133">С помощью этой команды должен быть создан глобально уникальный реестр контейнеров с использованием базового имени и случайного числа.</span><span class="sxs-lookup"><span data-stu-id="60a2e-133">This command will create a globally unique (hopefully) container registry using a basic name with a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="60a2e-134">Создание образа Docker</span><span class="sxs-lookup"><span data-stu-id="60a2e-134">Build the Docker image</span></span>

<span data-ttu-id="60a2e-135">Хотя можно легко выполнить сборку образа Docker локально с помощью самого средства Docker, рекомендуем выполнить ее в облаке по ряду причин:</span><span class="sxs-lookup"><span data-stu-id="60a2e-135">While you can easily build the Docker image locally using Docker itself, you may want to consider building it in the Cloud for few reasons:</span></span>

1. <span data-ttu-id="60a2e-136">Нет необходимости устанавливать Docker локально.</span><span class="sxs-lookup"><span data-stu-id="60a2e-136">No need to install Docker locally</span></span>
1. <span data-ttu-id="60a2e-137">Скорость значительно увеличивается, потому что сборка выполняется в другом расположении (это не влияет на время, требующееся для отправки контекста).</span><span class="sxs-lookup"><span data-stu-id="60a2e-137">Much faster since build will happen elsewhere (except for context upload time)</span></span>
1. <span data-ttu-id="60a2e-138">Для процесса в облаке используется более скоростной интернет-канал, и загрузка происходит быстрее.</span><span class="sxs-lookup"><span data-stu-id="60a2e-138">Process in the Cloud has access to faster Internet, therefore faster downloads</span></span>
1. <span data-ttu-id="60a2e-139">Образ попадает непосредственно в Реестр контейнеров.</span><span class="sxs-lookup"><span data-stu-id="60a2e-139">Image goes directly into the Container Registry</span></span>

<span data-ttu-id="60a2e-140">Поэтому мы выполним сборку образа с помощью службы [Служба "Сборка Реестра контейнеров Azure"]:</span><span class="sxs-lookup"><span data-stu-id="60a2e-140">Because of these reasons, we will build the image using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-docker-image-from-azure-container-registry-acr-into-container-instances-aci"></a><span data-ttu-id="60a2e-141">Развертывание образа Docker из Реестра контейнеров Azure (ACR) в службе "Экземпляры контейнеров Azure (ACI)"</span><span class="sxs-lookup"><span data-stu-id="60a2e-141">Deploy Docker Image from Azure Container Registry (ACR) into Container Instances (ACI)</span></span>

<span data-ttu-id="60a2e-142">Теперь, когда образ доступен в ACR, отправим его в службу ACI и создадим там экземпляр контейнера.</span><span class="sxs-lookup"><span data-stu-id="60a2e-142">Now that the image is available on your ACR, let's push and instanciate a container instance on ACI.</span></span> <span data-ttu-id="60a2e-143">Но сначала нужно убедиться, что мы можем выполнить проверку подлинности в ACR:</span><span class="sxs-lookup"><span data-stu-id="60a2e-143">But first, we need to make sure we can authenticate into the ACR:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="60a2e-144">Тестирование развернутого приложения MicroProfile</span><span class="sxs-lookup"><span data-stu-id="60a2e-144">Test Your Deployed MicroProfile Application</span></span>

<span data-ttu-id="60a2e-145">На этом этапе ваше приложение должно быть запущено.</span><span class="sxs-lookup"><span data-stu-id="60a2e-145">Your application should now be up and running.</span></span> <span data-ttu-id="60a2e-146">Чтобы протестировать его, попробуйте выполнить следующую команду:</span><span class="sxs-lookup"><span data-stu-id="60a2e-146">To test it from the command-line, try the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="60a2e-147">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="60a2e-147">Congratulations!</span></span> <span data-ttu-id="60a2e-148">Вы успешно собрали и развернули приложение MicroProfile в виде контейнера Docker в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="60a2e-148">You have successfuly built and deployed a MicroProfile application as a Docker container onto Microsoft Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60a2e-149">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="60a2e-149">Next steps</span></span>

<span data-ttu-id="60a2e-150">Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="60a2e-150">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* [<span data-ttu-id="60a2e-151">Вход в Azure из интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="60a2e-151">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

<!-- URL List -->

[Служба "Сборка Реестра контейнеров Azure"]: https://docs.microsoft.com/en-us/azure/container-registry/container-registry-build-overview
[Azure Container Registry Build]: https://docs.microsoft.com/en-us/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Maven]: http://maven.apache.org/
