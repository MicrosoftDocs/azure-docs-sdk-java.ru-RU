---
title: Развертывание приложения MicroProfile в облаке с помощью Docker и Azure
description: Узнайте, как развернуть приложение MicroProfile в облаке с помощью Docker и службы "Экземпляры контейнеров Azure".
services: container-instances;container-registry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 6ba12bb183969103676fa988199603df6cf36bba
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533606"
---
# <a name="deploy-a-microprofile-app-to-the-cloud-by-using-docker-and-azure"></a><span data-ttu-id="8a704-103">Развертывание приложения MicroProfile в облаке с помощью Docker и Azure</span><span class="sxs-lookup"><span data-stu-id="8a704-103">Deploy a MicroProfile app to the cloud by using Docker and Azure</span></span>

<span data-ttu-id="8a704-104">В этой статье показано, как упаковать приложение [MicroProfile.io] в контейнер Docker и запустить его в службе "Экземпляры контейнеров Azure".</span><span class="sxs-lookup"><span data-stu-id="8a704-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
> <span data-ttu-id="8a704-105">Эта процедура подходит для любой реализации MicroProfile.io при условии, что образ контейнера Docker является самовыполняющимся (т. е. образ содержит среду выполнения).</span><span class="sxs-lookup"><span data-stu-id="8a704-105">This procedure works with any implementation of MicroProfile.io, as long as the Docker container image is self-executable (that is, the image includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a704-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8a704-106">Prerequisites</span></span>

<span data-ttu-id="8a704-107">Для работы с данным руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="8a704-107">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="8a704-108">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="8a704-108">An Azure subscription.</span></span> <span data-ttu-id="8a704-109">Если у вас ее еще нет, создайте [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="8a704-109">If you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="8a704-110">Установленный [Интерфейс командной строки Azure].</span><span class="sxs-lookup"><span data-stu-id="8a704-110">The [Azure CLI], installed.</span></span>
* <span data-ttu-id="8a704-111">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="8a704-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="8a704-112">Дополнительные сведения о пакетах JDK, которые можно использовать при разработке в Azure, см. в статье [Долгосрочная поддержка Java для Azure и Azure Stack](https://aka.ms/azure-jdks).</span><span class="sxs-lookup"><span data-stu-id="8a704-112">For more information about the JDKs that are available to use when you develop on Azure, see [Java long-term support for Azure and Azure Stack](https://aka.ms/azure-jdks).</span></span>
* <span data-ttu-id="8a704-113">Средство сборки [Apache Maven] (версии 3 или более поздней).</span><span class="sxs-lookup"><span data-stu-id="8a704-113">The [Apache Maven] build tool (version 3 or later).</span></span>
* <span data-ttu-id="8a704-114">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="8a704-114">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="8a704-115">Пример приложения MicroProfile Hello Azure</span><span class="sxs-lookup"><span data-stu-id="8a704-115">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="8a704-116">В этой статье мы используем пример приложения [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure).</span><span class="sxs-lookup"><span data-stu-id="8a704-116">In this article, you use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample.</span></span> <span data-ttu-id="8a704-117">Клонируйте это приложение, выполните его сборку и запустите локально с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="8a704-117">Clone, build, and run it locally by using the following commands:</span></span>

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

<span data-ttu-id="8a704-118">Приложение можно протестировать с помощью команды `curl` или [веб-браузера](http://localhost:8080/api/hello):</span><span class="sxs-lookup"><span data-stu-id="8a704-118">You can test the application by calling `curl` or by using a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="8a704-119">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="8a704-119">Deploy the app to Azure</span></span>

<span data-ttu-id="8a704-120">Теперь развернем это приложение в Azure с помощью служб [Экземпляры контейнеров Azure] и [Реестр контейнеров Azure].</span><span class="sxs-lookup"><span data-stu-id="8a704-120">Now bring this application to Azure by using the [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="8a704-121">Создание образа Docker</span><span class="sxs-lookup"><span data-stu-id="8a704-121">Build a Docker image</span></span>

<span data-ttu-id="8a704-122">Пример проекта содержит файл Dockerfile, который можно использовать.</span><span class="sxs-lookup"><span data-stu-id="8a704-122">The sample project provides a Dockerfile that you can use.</span></span> <span data-ttu-id="8a704-123">Вам не нужно устанавливать Docker, так как мы воспользуемся функцией сборки Реестра контейнеров Azure для выполнения сборки образа в облаке.</span><span class="sxs-lookup"><span data-stu-id="8a704-123">You don't need to have Docker installed, though, because you'll use the Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="8a704-124">Чтобы создать образ и подготовить его для запуска в Azure, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="8a704-124">To build the image and prepare to run it on Azure, do the following:</span></span>

1. <span data-ttu-id="8a704-125">Установите Azure CLI и войдите в его систему.</span><span class="sxs-lookup"><span data-stu-id="8a704-125">Install and sign in to the Azure CLI.</span></span>
1. <span data-ttu-id="8a704-126">Создание группы ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="8a704-126">Create an Azure resource group.</span></span>
1. <span data-ttu-id="8a704-127">Создайте экземпляр Реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="8a704-127">Create an Azure container registry instance.</span></span>
1. <span data-ttu-id="8a704-128">Создайте образ Docker.</span><span class="sxs-lookup"><span data-stu-id="8a704-128">Build a Docker image.</span></span>
1. <span data-ttu-id="8a704-129">Опубликуйте образ Docker в ранее созданном экземпляре реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="8a704-129">Publish the Docker image to the previously created container registry instance.</span></span>
1. <span data-ttu-id="8a704-130">(Необязательно.) Выполните сборку образа и опубликуйте его в экземпляре реестра контейнеров с помощью одной команды.</span><span class="sxs-lookup"><span data-stu-id="8a704-130">(Optional) Build and publish the image to the container registry instance in one command.</span></span>


#### <a name="set-up-the-azure-cli"></a><span data-ttu-id="8a704-131">Настройка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8a704-131">Set up the Azure CLI</span></span>

<span data-ttu-id="8a704-132">Убедитесь, что у вас есть подписка Azure, установлен [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) и вы выполнили проверку подлинности в своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="8a704-132">Make sure that you have an Azure subscription, that you've installed [the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you're authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="8a704-133">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="8a704-133">Create a resource group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-a-container-registry-instance"></a><span data-ttu-id="8a704-134">Создание экземпляра реестра контейнеров</span><span class="sxs-lookup"><span data-stu-id="8a704-134">Create a container registry instance</span></span>

<span data-ttu-id="8a704-135">С помощью этой команды должен быть создан глобальный уникальный экземпляр реестра контейнеров с простым именем и случайным числом.</span><span class="sxs-lookup"><span data-stu-id="8a704-135">This command should create a globally unique container registry instance with a basic name and a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="8a704-136">Создание образа Docker</span><span class="sxs-lookup"><span data-stu-id="8a704-136">Build the Docker image</span></span>

<span data-ttu-id="8a704-137">Хотя можно легко выполнить сборку образа Docker локально с помощью самого средства Docker, рекомендуем выполнить ее в облаке по ряду причин:</span><span class="sxs-lookup"><span data-stu-id="8a704-137">Although you can easily build the Docker image locally by using Docker itself, you might consider building it in the cloud for few reasons:</span></span>

* <span data-ttu-id="8a704-138">Нет необходимости устанавливать Docker локально.</span><span class="sxs-lookup"><span data-stu-id="8a704-138">You don't have to install Docker locally.</span></span>
* <span data-ttu-id="8a704-139">Скорость значительно увеличивается, потому что сборка выполняется в другом расположении (это не влияет на время, требующееся для отправки контекста).</span><span class="sxs-lookup"><span data-stu-id="8a704-139">It's much faster, because the build happens elsewhere (except for context upload time).</span></span>
* <span data-ttu-id="8a704-140">Для процесса в облаке используется более скоростной интернет-канал, вследствие чего загрузка происходит быстрее.</span><span class="sxs-lookup"><span data-stu-id="8a704-140">The process in the cloud has faster access to the internet and, therefore, faster downloads.</span></span>
* <span data-ttu-id="8a704-141">Образ попадает непосредственно в экземпляр реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="8a704-141">The image goes directly into the container registry instance.</span></span>

<span data-ttu-id="8a704-142">Поэтому мы выполнили сборку образа с помощью функции сборки [Служба "Сборка Реестра контейнеров Azure"]:</span><span class="sxs-lookup"><span data-stu-id="8a704-142">For these reasons, you build the image by using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-the-docker-image-from-the-azure-container-registry-instance-to-container-instances"></a><span data-ttu-id="8a704-143">Развертывание образа Docker из экземпляра Реестра контейнеров Azure в службе "Экземпляры контейнеров"</span><span class="sxs-lookup"><span data-stu-id="8a704-143">Deploy the Docker image from the Azure container registry instance to Container Instances</span></span>

<span data-ttu-id="8a704-144">Теперь, когда этот образ доступен в экземпляре реестра контейнеров, отправьте его и создайте экземпляр контейнера в службе "Экземпляры контейнеров".</span><span class="sxs-lookup"><span data-stu-id="8a704-144">Now that the image is available on your container registry instance, push and instantiate a container instance on Container Instances.</span></span> <span data-ttu-id="8a704-145">Но сначала убедитесь, что вы можете выполнить проверку подлинности в экземпляре реестра контейнеров:</span><span class="sxs-lookup"><span data-stu-id="8a704-145">But first, make sure that you can authenticate into the container registry instance:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="8a704-146">Тестирование развернутого приложения MicroProfile</span><span class="sxs-lookup"><span data-stu-id="8a704-146">Test your deployed MicroProfile application</span></span>

<span data-ttu-id="8a704-147">На этом этапе ваше приложение должно быть запущено.</span><span class="sxs-lookup"><span data-stu-id="8a704-147">Your application should now be up and running.</span></span> <span data-ttu-id="8a704-148">Чтобы протестировать его с помощью интерфейса командной строки, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8a704-148">To test it from the command-line interface, use the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="8a704-149">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="8a704-149">Congratulations!</span></span> <span data-ttu-id="8a704-150">Вы успешно собрали приложение MicroProfile в виде контейнера Docker и развернули его в Azure.</span><span class="sxs-lookup"><span data-stu-id="8a704-150">You've successfully built a MicroProfile application as a Docker container and deployed it to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a704-151">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="8a704-151">Next steps</span></span>

<span data-ttu-id="8a704-152">Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="8a704-152">For more information about the various technologies discussed in this article, see:</span></span>

* [<span data-ttu-id="8a704-153">Вход в Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8a704-153">Sign in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

<!-- URL List -->

[Служба "Сборка Реестра контейнеров Azure"]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Интерфейс командной строки Azure]: /cli/azure/overview
[Azure CLI]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Apache Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Экземпляры контейнеров Azure]: https://docs.microsoft.com/azure/container-instances/;
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Реестр контейнеров Azure]:  https://docs.microsoft.com/azure/container-registry
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry
