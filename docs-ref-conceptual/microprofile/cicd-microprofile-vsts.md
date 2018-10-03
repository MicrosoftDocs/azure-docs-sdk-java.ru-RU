---
title: CI/CD для приложений MicroProfile с использованием Azure DevOps
description: Узнайте, как настроить цикл выпуска CI/CD для развертывания приложений MicroProfile в экземпляре Веб-приложения для контейнеров Azure с помощью Azure DevOps
services: Azure DevOps
documentationcenter: MicroProfile
author: ruyakubu
manager: brunoborges
editor: ruyakubu
ms.assetid: ''
ms.author: ruyakubu
ms.date: 09/14/2018
ms.devlang: Java
ms.service: Azure DevOps
ms.tgt_pltfrm: multiple
ms.topic: tutorial
ms.workload: web
ms.openlocfilehash: c2b6bf3370982d26d8d23fede370e0105a70b734
ms.sourcegitcommit: fd67d4088be2cad01c642b9ecf3f9475d9cb4f3c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506589"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a><span data-ttu-id="1f991-103">CI/CD для приложений MicroProfile с использованием Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="1f991-103">CI/CD for MicroProfile applications using Azure DevOps</span></span>

<span data-ttu-id="1f991-104">В этом руководстве объясняется, как разработчики Java EE могут легко настроить цикл выпуска CI/CD, чтобы развернуть приложение [MicroProfile](http://microprofile.io) в экземпляре Веб-приложения для контейнеров Azure с помощью Azure DevOps (прежнее название — VSTS).</span><span class="sxs-lookup"><span data-stu-id="1f991-104">This tutorial will show how Java EE developers can easily setup a CI/CD release cycle to deploy their [MicroProfile](http://microprofile.io) applications to an Azure Web App for Containers using Azure DevOps (formally known as VSTS).</span></span>  <span data-ttu-id="1f991-105">В этом примере мы будем использовать приложение MicroProfile, использующее [Payara Micro](https://www.payara.fish/payara_micro) в качестве базового образа.</span><span class="sxs-lookup"><span data-stu-id="1f991-105">In this example, we’ll be using a MicroProfile application that uses a [Payara Micro](https://www.payara.fish/payara_micro) as a base image.</span></span>   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
<span data-ttu-id="1f991-106">Мы начнем процесс контейнеризации в Azure DevOps с создания образа Docker, а затем отправим образ контейнера в Реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="1f991-106">We will start the Azure DevOps containerize process by building a Docker image and pushing the container image to an Azure Container Register.</span></span>  <span data-ttu-id="1f991-107">После этого мы завершим работу с конвейером выпуска в Azure DevOps, чтобы развернуть образ контейнера в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="1f991-107">Then complete with a Azure DevOps release pipeline to deploy the container image to a Web App.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f991-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1f991-108">Prerequisites</span></span>
- <span data-ttu-id="1f991-109">Скопируйте и сохраните URL-адрес Git из [GitHub](https://github.com/Azure-Samples/microprofile-hello-azure).</span><span class="sxs-lookup"><span data-stu-id="1f991-109">Copy and save the Git url from [Github](https://github.com/Azure-Samples/microprofile-hello-azure)</span></span>
- <span data-ttu-id="1f991-110">Регистрируйтесь или войдите в [Azure DevOps](https://dev.azure.com), используя учетную запись.</span><span class="sxs-lookup"><span data-stu-id="1f991-110">Register or Log into your [Azure DevOps](https://dev.azure.com) account</span></span>
- <span data-ttu-id="1f991-111">Создайте [проект Azure DevOps](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) и **импортируйте репозиторий**, используя скопированный ранее URL-адрес Git.</span><span class="sxs-lookup"><span data-stu-id="1f991-111">Create a new [Azure DevOps project](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) and use the above Git url to **import a repository**</span></span>
- <span data-ttu-id="1f991-112">Создайте экземпляр службы [Реестр контейнеров Azure](https://azure.microsoft.com/en-us/services/container-registry) (ACR).</span><span class="sxs-lookup"><span data-stu-id="1f991-112">Create an [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry) (ACR)</span></span>
- <span data-ttu-id="1f991-113">Создайте экземпляр Веб-приложения для контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="1f991-113">Create an Azure Web App for Container</span></span>
> [!NOTE]
>
> <span data-ttu-id="1f991-114">При подготовке экземпляра веб-приложения выберите "Быстрый запуск" в разделе "Параметры контейнера".</span><span class="sxs-lookup"><span data-stu-id="1f991-114">Select "Quickstart" in the Container Settings when provisioning the Web App instance</span></span>


## <a name="create-a-build-definition"></a><span data-ttu-id="1f991-115">Создание определения сборки</span><span class="sxs-lookup"><span data-stu-id="1f991-115">Create a Build definition</span></span>

<span data-ttu-id="1f991-116">Определение сборки в Azure DevOps обеспечивает автоматическое выполнение всех задач в сборке каждый раз, когда происходит фиксация в исходном приложении Java EE.</span><span class="sxs-lookup"><span data-stu-id="1f991-116">The build definition in Azure DevOps automatically executes all the tasks in the build each time there’s a commit in Java EE application source application.</span></span>  <span data-ttu-id="1f991-117">В этом примере для сборки проекта Java MicroProfile в Azure DevOps мы будем использовать Maven.</span><span class="sxs-lookup"><span data-stu-id="1f991-117">In this example, Azure DevOps will use Maven to build the Java MicroProfile project.</span></span>

1. <span data-ttu-id="1f991-118">Перейдите на вкладку "Сборка и выпуск" в верхней части страницы проекта Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="1f991-118">Click on the "Build and Release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="1f991-119">Затем щелкните ссылку **Сборки**.</span><span class="sxs-lookup"><span data-stu-id="1f991-119">Then, select the **Builds** link</span></span> 

<img src="media/VSTS/Buid-and-Release1.png">

2. <span data-ttu-id="1f991-120">Нажмите кнопку **Новый конвейер** и щелкните **Продолжить**, чтобы приступить к определению задач сборки.</span><span class="sxs-lookup"><span data-stu-id="1f991-120">Click on the **New Pipeline** button, and then **Continue** to start defining your build tasks</span></span>
3. <span data-ttu-id="1f991-121">В списке шаблонов выберите Maven и нажмите кнопку **Применить**, чтобы выполнить сборку проекта Java.</span><span class="sxs-lookup"><span data-stu-id="1f991-121">Select "Maven" from the list of templates, then click on the **Apply** button to build your Java project</span></span>
4. <span data-ttu-id="1f991-122">В раскрывающемся меню поля "Пул агентов" выберите параметр **Hosted Linux Preview** (Размещенная предварительная версия Linux).</span><span class="sxs-lookup"><span data-stu-id="1f991-122">Use the drop-down menu for the Agent pool field to select **Hosted Linux Preview** option.</span></span>
> [!NOTE]
>
> <span data-ttu-id="1f991-123">Таким образом, вы укажете Azure DevOps, какой сервер сборки использовать.</span><span class="sxs-lookup"><span data-stu-id="1f991-123">This informs Azure DevOps which build server to use.</span></span>  <span data-ttu-id="1f991-124">Можно использовать закрытый пользовательский сервер сборки.</span><span class="sxs-lookup"><span data-stu-id="1f991-124">You can use your private customized build server</span></span>

5. <span data-ttu-id="1f991-125">Чтобы настроить сборку для непрерывной интеграции, перейдите на вкладку **Триггеры** и установите флажок **Включить непрерывную интеграцию**.</span><span class="sxs-lookup"><span data-stu-id="1f991-125">To configure your build for continuous integration, select the **Triggers** tab and check the **Enable continuous integration** checkbox.</span></span>  

<img src="media/VSTS/Build-Triggers2.png"> 
 
6. <span data-ttu-id="1f991-126">Выберите вкладку **Задачи**, чтобы вернуться на главную страницу конвейера сборки.</span><span class="sxs-lookup"><span data-stu-id="1f991-126">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
7. <span data-ttu-id="1f991-127">В раскрывающемся меню **Сохранить и поместить в очередь** выберите пункт **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1f991-127">Use the **Save & queue** drop-down menu to select the **Save** option</span></span>
 

## <a name="create-a-docker-build-image"></a><span data-ttu-id="1f991-128">Создание образа сборки Docker</span><span class="sxs-lookup"><span data-stu-id="1f991-128">Create a Docker Build Image</span></span>

<span data-ttu-id="1f991-129">В этой задаче для создания образа Docker в Azure DevOps используется файл Docker с базовым образом из Payara Micro.</span><span class="sxs-lookup"><span data-stu-id="1f991-129">In this task, Azure DevOps uses a Dockerfile with a base image from Payara Micro to create a Docker image.</span></span>  

1. <span data-ttu-id="1f991-130">Выберите вкладку **Задачи**, чтобы вернуться на главную страницу конвейера сборки.</span><span class="sxs-lookup"><span data-stu-id="1f991-130">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
2. <span data-ttu-id="1f991-131">Щелкните значок **+**, чтобы добавить новую задачу в определение сборки.</span><span class="sxs-lookup"><span data-stu-id="1f991-131">Click on the **+** icon to add new task to the build definition</span></span>
 
<img src="media/VSTS/Tasks-add4.png">
 
3. <span data-ttu-id="1f991-132">В списке шаблонов выберите Docker и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1f991-132">Select "Docker" from the list of templates, then click on the **Add** button</span></span>
4. <span data-ttu-id="1f991-133">Введите описательное имя в поле **Отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="1f991-133">Enter a description name for the **Display name** field</span></span>
5. <span data-ttu-id="1f991-134">Убедитесь, что в раскрывающемся меню для поля **Тип реестра контейнеров** выбран пункт **Реестр контейнеров Azure**.</span><span class="sxs-lookup"><span data-stu-id="1f991-134">Verify that **Azure Container Registry** is selected in the drop-down menu for **Container registry type**.</span></span>
> [!NOTE]
>
>  <span data-ttu-id="1f991-135">Если вы используете Docker Hub или другой реестр, выберите "Реестр контейнеров".</span><span class="sxs-lookup"><span data-stu-id="1f991-135">If you are using Docker Hub or another registry, select "Container Registry" instead.</span></span>  <span data-ttu-id="1f991-136">Нажмите кнопку "+Создать", чтобы указать учетные данные и данные подключения для этого реестра.</span><span class="sxs-lookup"><span data-stu-id="1f991-136">Then click on the "+ New" button to provide the credentials and connection information for it.</span></span> <span data-ttu-id="1f991-137">Затем перейдите к разделу "Команды", чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="1f991-137">Then skip to the Commands section to continue.</span></span>

6. <span data-ttu-id="1f991-138">В раскрывающемся меню **Подписка Azure** выберите идентификатор своей подписки.</span><span class="sxs-lookup"><span data-stu-id="1f991-138">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>  <span data-ttu-id="1f991-139">Нажмите кнопку **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="1f991-139">Then click on the **Authorize** button</span></span>
7. <span data-ttu-id="1f991-140">В раскрывающемся меню **Реестр контейнеров Azure** выберите имя реестра, который вы создали в Azure.</span><span class="sxs-lookup"><span data-stu-id="1f991-140">In the **Azure container registry** drop-down menu, select registry name you created in Azure.</span></span>
8. <span data-ttu-id="1f991-141">Убедитесь, что в раскрывающемся меню **Команда** выбран пункт **Сборка**.</span><span class="sxs-lookup"><span data-stu-id="1f991-141">Verify that **build** option is selected in the **Command** drop-down menu.</span></span>
9. <span data-ttu-id="1f991-142">Рядом с текстовым полем **Файл Docker** щелкните значок навигации для выбора пути, чтобы выбрать файл Docker в проекте GitHub.</span><span class="sxs-lookup"><span data-stu-id="1f991-142">For the **Dockerfile**, click on the path navigation icon next to the textbox to select the Dockerfile from the github project.</span></span>  <span data-ttu-id="1f991-143">Затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1f991-143">Then click the **OK** button.</span></span>

<img src="media/VSTS/Dockerfile5.png">

10. <span data-ttu-id="1f991-144">Под полем **Имя образа** установите флажок **Включить последний тег**.</span><span class="sxs-lookup"><span data-stu-id="1f991-144">Under the **Image name**, check the **Include latest tag** checkbox.</span></span> 
11. <span data-ttu-id="1f991-145">В раскрывающемся меню **Сохранить и поместить в очередь** выберите пункт **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1f991-145">Use the **Save & queue** drop-down menu to select the **Save** option.</span></span>

## <a name="push-docker-image-to-acr"></a><span data-ttu-id="1f991-146">Отправка образа Docker в ACR</span><span class="sxs-lookup"><span data-stu-id="1f991-146">Push Docker Image to ACR</span></span>

<span data-ttu-id="1f991-147">В этой задаче Azure DevOps отправит образ Docker в Реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="1f991-147">In this task, Azure DevOps will push the docker image to your Azure Container Registry.</span></span>  <span data-ttu-id="1f991-148">Этот образ будет использоваться для запуска приложения API MicroProfile в качестве контейнерного веб-приложения Java.</span><span class="sxs-lookup"><span data-stu-id="1f991-148">This will be used to run the MicroProfile API application as a containerized Java web app.</span></span>

1. <span data-ttu-id="1f991-149">Так как мы используем Docker в Azure DevOps, создайте новый шаблон Docker, повторив шаги 1–7, приведенные в разделе **Создание образа сборки Docker**.</span><span class="sxs-lookup"><span data-stu-id="1f991-149">Since we are using Docker in Azure DevOps, create a new Docker template by repeating steps 1 - 7 above in the **Create a Docker Build Image** section.</span></span>
2. <span data-ttu-id="1f991-150">В раскрывающемся меню **Команда** выберите **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="1f991-150">Select **push** in the **Command** drop-down menu.</span></span>
3. <span data-ttu-id="1f991-151">Перейдите на вкладку **Сохранить и поместить в очередь** и выберите пункт **Сохранить и поместить в очередь**.</span><span class="sxs-lookup"><span data-stu-id="1f991-151">Click on the **Save & queue** tab, then select **Save & queue** option.</span></span>
4. <span data-ttu-id="1f991-152">Убедитесь, что во всплывающем окне для пула агентов выбрано значение **Hosted Linux Preview** (Размещенная предварительная версия Linux).</span><span class="sxs-lookup"><span data-stu-id="1f991-152">Verify that the **Hosted Linux Preview** is select for the Agent pool on the pop-up window.</span></span>  <span data-ttu-id="1f991-153">Нажмите кнопку **Сохранить и поместить в очередь**.</span><span class="sxs-lookup"><span data-stu-id="1f991-153">Then click on the **Save & queue** button.</span></span>
5. <span data-ttu-id="1f991-154">Щелкните номер сборки, чтобы проверить, успешно ли завершен конвейер сборки для проекта Java.</span><span class="sxs-lookup"><span data-stu-id="1f991-154">Click on the build number to verify that the build pipeline for the Java project completed successfully.</span></span>

<img src="media/VSTS/Build-Number6.png">
 

## <a name="create-a-release-definition-for-a-java-app"></a><span data-ttu-id="1f991-155">Создание определения выпуска для приложения Java</span><span class="sxs-lookup"><span data-stu-id="1f991-155">Create a release definition for a Java app</span></span>

<span data-ttu-id="1f991-156">Конвейер выпуска в Azure DevOps автоматически активирует развертывание артефактов сборки в целевую среду, например Azure, как только процесс сборки успешно завершится.</span><span class="sxs-lookup"><span data-stu-id="1f991-156">The release pipeline in Azure DevOps automatically triggers the deployment of build artifacts to a target environment like Azure as soon as the Build process completes successfully.</span></span>   <span data-ttu-id="1f991-157">Конвейер выпуска можно создавать для сред разработки, тестирования, промежуточной или рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="1f991-157">The release pipeline can be created for dev, test, staging or production environments.</span></span>

1. <span data-ttu-id="1f991-158">Перейдите на вкладку "Сборка и выпуск" в верхней части страницы проекта Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="1f991-158">Click on the "Build and release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="1f991-159">Щелкните ссылку **Выпуски**.</span><span class="sxs-lookup"><span data-stu-id="1f991-159">Then, select the **Releases** link.</span></span>

<img src="media/VSTS/Release-new-pipeline7.png">
 
2. <span data-ttu-id="1f991-160">Нажмите кнопку "Новый конвейер"\*\*.</span><span class="sxs-lookup"><span data-stu-id="1f991-160">Click on the "New pipeline\*\* button</span></span>
3. <span data-ttu-id="1f991-161">В списке шаблонов выберите **Развертывание приложения Java в службе приложений Azure**, а затем нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="1f991-161">Select the **Deploy a Java app to Azure App Service** in the list of templates, then click on the **Apply** button.</span></span>

<img src="media/VSTS/deploy-java-template8.png">
 
4. <span data-ttu-id="1f991-162">Укажите **имя этапа** (например, разработки, тестирования или промежуточного этапа).</span><span class="sxs-lookup"><span data-stu-id="1f991-162">Set a **Stage name** (e.g Dev, Test, Staging or Production).</span></span>  <span data-ttu-id="1f991-163">Нажмите кнопку **X**, чтобы закрыть всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="1f991-163">Then click on the **X** button to close the pop-up window</span></span>
5. <span data-ttu-id="1f991-164">В разделе артефактов нажмите кнопку **+Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1f991-164">Click on the **+ Add** button in the Artifacts section.</span></span>  <span data-ttu-id="1f991-165">Таким образом, вы свяжете артефакты из определения сборки с артефактами из этого определения выпуска.</span><span class="sxs-lookup"><span data-stu-id="1f991-165">This will link artifacts from the build definition to this release definition.</span></span>  
6. <span data-ttu-id="1f991-166">В раскрывающемся меню для поля **Источник (конвейер сборки)** выберите определение сборки.</span><span class="sxs-lookup"><span data-stu-id="1f991-166">Use the drop-down menu for the **Source (build pipeline)** to select your build definition.</span></span> <span data-ttu-id="1f991-167">Нажмите кнопку **Добавить**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="1f991-167">Then click the **Add** button to continue.</span></span>

<img src="media/VSTS/add-artifact9.png">
 
7. <span data-ttu-id="1f991-168">Перейдите на вкладку **Задачи** на странице конвейера.</span><span class="sxs-lookup"><span data-stu-id="1f991-168">Click on the **Tasks** tab on the pipeline.</span></span>  <span data-ttu-id="1f991-169">Выберите имя этапа.</span><span class="sxs-lookup"><span data-stu-id="1f991-169">Then, select your stage name.</span></span>
 
<img src="media/VSTS/release-stage10.png">

8. <span data-ttu-id="1f991-170">В раскрывающемся меню **Подписка Azure** выберите идентификатор своей подписки.</span><span class="sxs-lookup"><span data-stu-id="1f991-170">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>
9. <span data-ttu-id="1f991-171">Выберите тип **Приложение Linux** в раскрывающемся меню **Тип приложения**.</span><span class="sxs-lookup"><span data-stu-id="1f991-171">Select **Linux App** from the **App type** drop-down menu</span></span>
10. <span data-ttu-id="1f991-172">В раскрывающемся меню **Имя службы приложений** выберите имя созданного ранее экземпляра службы "Веб-приложение для контейнеров".</span><span class="sxs-lookup"><span data-stu-id="1f991-172">Select the name of the Web App for Container instance you created above in the **App service name** drop-down menu</span></span>
11. <span data-ttu-id="1f991-173">Введите имя экземпляра службы "Реестр контейнеров Azure" в поле **Registry or Namespaces** (Реестр или пространства имен).</span><span class="sxs-lookup"><span data-stu-id="1f991-173">Enter the name of your azure container registry in the **Registry or Namespaces** field.</span></span>  <span data-ttu-id="1f991-174">Например, **myregistry.azure.io**.</span><span class="sxs-lookup"><span data-stu-id="1f991-174">E.g **myregistry.azure.io**</span></span>
12. <span data-ttu-id="1f991-175">Введите имя реестра в поле **Репозиторий**.</span><span class="sxs-lookup"><span data-stu-id="1f991-175">Enter the registry name in the **Repository** field</span></span>
13. <span data-ttu-id="1f991-176">Щелкните **Deploy Azure App Service** (Развернуть службу приложений Azure).</span><span class="sxs-lookup"><span data-stu-id="1f991-176">Click on **Deploy Azure App Service**.</span></span>  <span data-ttu-id="1f991-177">Введите тег для образа контейнера в текстовом поле **Тег**.</span><span class="sxs-lookup"><span data-stu-id="1f991-177">Enter the tag for the container image in the **Tag** textbox</span></span> 
14. <span data-ttu-id="1f991-178">Щелкните **Запуск на агенте**.</span><span class="sxs-lookup"><span data-stu-id="1f991-178">Click on **Run on agent**.</span></span>  <span data-ttu-id="1f991-179">В раскрывающемся меню пула агента выберите **Hosted Linux Preview** (Размещенная предварительная версия Linux).</span><span class="sxs-lookup"><span data-stu-id="1f991-179">Select **Hosted Linux Preview** in the Agent pool drop-down menu</span></span> 

## <a name="setup-environment-variables"></a><span data-ttu-id="1f991-180">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="1f991-180">Setup Environment Variables</span></span>

1. <span data-ttu-id="1f991-181">Перейдите на вкладку **Переменные**.  Нажмите кнопку **+Добавить**, чтобы определить переменные среды.</span><span class="sxs-lookup"><span data-stu-id="1f991-181">Click on the **Variables** tab.  Then click on the **+ Add** button to define your environment variables</span></span>
2. <span data-ttu-id="1f991-182">Добавьте имя переменной и значения для URL-адреса реестра контейнеров, имя пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="1f991-182">Add the variable name and values for your container registry url, username and password.</span></span>   <span data-ttu-id="1f991-183">В целях безопасности щелкните значок замка, чтобы скрыть значение пароля.</span><span class="sxs-lookup"><span data-stu-id="1f991-183">For security, click on the lock icon to keep the password value hidden.</span></span>

<span data-ttu-id="1f991-184">Например: </span><span class="sxs-lookup"><span data-stu-id="1f991-184">For example:</span></span>
- <span data-ttu-id="1f991-185">registry.password;</span><span class="sxs-lookup"><span data-stu-id="1f991-185">registry.password</span></span>
- <span data-ttu-id="1f991-186">registry.url;</span><span class="sxs-lookup"><span data-stu-id="1f991-186">registry.url</span></span>
- <span data-ttu-id="1f991-187">registry.username.</span><span class="sxs-lookup"><span data-stu-id="1f991-187">registry.username</span></span>

<img src="media/VSTS/environment-variables12.png">

3. <span data-ttu-id="1f991-188">Щелкните вкладку **Задачи**, чтобы вернуться на главную страницу определения конвейера выпуска.</span><span class="sxs-lookup"><span data-stu-id="1f991-188">Click on the **Tasks** tab to return to the main release pipeline definition page</span></span>
4. <span data-ttu-id="1f991-189">Щелкните **Deploy Azure App Service** (Развернуть службу приложений Azure).</span><span class="sxs-lookup"><span data-stu-id="1f991-189">Click on **Deploy Azure App Service**.</span></span> 
5. <span data-ttu-id="1f991-190">Разверните раздел **Параметры приложения и конфигурации**, щелкните значок навигации для выбора пути в поле **Параметры приложения**, чтобы добавить переменную среды для подключения к реестру контейнеров во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="1f991-190">Expand the **Application and Configuration Settings** section, then click on the navigation path for the **App Settings** field to add environments variable to connect to the container registry during deployment.</span></span>
6. <span data-ttu-id="1f991-191">Нажмите кнопку **+Добавить**, чтобы определить следующие параметры приложения и присвоить переменные среды.</span><span class="sxs-lookup"><span data-stu-id="1f991-191">Click on the \*\* + Add\*\* button to define the following app settings and assign the environment variables</span></span>
- <span data-ttu-id="1f991-192">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password).</span><span class="sxs-lookup"><span data-stu-id="1f991-192">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span></span>
- <span data-ttu-id="1f991-193">DOCKER_REGISTRY_SERVER_URL = $(registry.url).</span><span class="sxs-lookup"><span data-stu-id="1f991-193">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span></span>
- <span data-ttu-id="1f991-194">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username).</span><span class="sxs-lookup"><span data-stu-id="1f991-194">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span></span>

<img src="media/VSTS/environment-variables14.png">
 
7. <span data-ttu-id="1f991-195">Нажмите кнопку **ОК**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="1f991-195">Click on the **OK** button to continue</span></span>

## <a name="setup-continious-deployment--deploy-java-application"></a><span data-ttu-id="1f991-196">Настройка непрерывного развертывания и развертывание приложения Java</span><span class="sxs-lookup"><span data-stu-id="1f991-196">Setup Continious Deployment & Deploy Java Application</span></span>

1. <span data-ttu-id="1f991-197">Чтобы включить непрерывное развертывание, перейдите на вкладку **Конвейеры**.</span><span class="sxs-lookup"><span data-stu-id="1f991-197">To enable continuous deployment, click the **Pipelines** tab</span></span>
2. <span data-ttu-id="1f991-198">В разделе "Артефакты" щелкните значок с молнией.</span><span class="sxs-lookup"><span data-stu-id="1f991-198">In the Artifacts section, click on the lightening icon.</span></span>  <span data-ttu-id="1f991-199">Затем задайте для параметра **Триггер непрерывного развертывания** значение "Вкл.".</span><span class="sxs-lookup"><span data-stu-id="1f991-199">Then set the **Continuous deployment trigger** to Enabled.</span></span>

<img src="media/VSTS/release-enable-CD.png">
 
3. <span data-ttu-id="1f991-200">Последовательно нажмите кнопки **Сохранить** и **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1f991-200">Click on the **Save** button, then the **OK** button</span></span> 
4. <span data-ttu-id="1f991-201">Щелкните стрелку раскрывающегося меню **+Выпуск** и выберите ссылку **Создать выпуск**.</span><span class="sxs-lookup"><span data-stu-id="1f991-201">Click on the **+ Release** drop-down menu, then select **Create a release** link</span></span>
5. <span data-ttu-id="1f991-202">В раскрывающемся меню **Stages for a trigger change from automated to manual** (Этапы для изменения автоматической активации на активацию вручную) установите флажок рядом с вашим именем этапа.</span><span class="sxs-lookup"><span data-stu-id="1f991-202">Use the **Stages for a trigger change from automated to manual** drop-down menu to select the checkbox for your stage name</span></span>
6. <span data-ttu-id="1f991-203">Нажмите кнопку **Создать**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="1f991-203">Click the **Create** button to continue</span></span>
7. <span data-ttu-id="1f991-204">Щелкните номер выпуска.</span><span class="sxs-lookup"><span data-stu-id="1f991-204">Click on the release number.</span></span>  <span data-ttu-id="1f991-205">Затем наведите указатель мыши на имя этапа и нажмите кнопку **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="1f991-205">Then hover your mouse cursor over the stage name and click on the **Deploy** button</span></span>
8. <span data-ttu-id="1f991-206">Затем нажмите кнопку **Развернуть** во всплывающем окне, чтобы запустить развертывание в Azure.</span><span class="sxs-lookup"><span data-stu-id="1f991-206">The click on the **Deploy** button on the pop-up window to start the deployment process to Azure</span></span>


## <a name="test-the-java-web-application"></a><span data-ttu-id="1f991-207">Тестирование веб-приложения Java</span><span class="sxs-lookup"><span data-stu-id="1f991-207">Test the Java Web Application</span></span>
1. <span data-ttu-id="1f991-208">Укажите URL-адрес веб-приложения в адресной строке веб-браузера:</span><span class="sxs-lookup"><span data-stu-id="1f991-208">Run the web app url in web browser:</span></span>  
<span data-ttu-id="1f991-209">https://{имя-экземпляра-службы-приложений}.azurewebsites.net/api/hello</span><span class="sxs-lookup"><span data-stu-id="1f991-209">https://{your-app-service-name}.azurewebsites.net/api/hello</span></span>

 
<img src="media/VSTS/web-app16.png">

2. <span data-ttu-id="1f991-210">На веб-странице должно отобразится **Hello Azure!**</span><span class="sxs-lookup"><span data-stu-id="1f991-210">The web page should say **Hello Azure!**</span></span>
 
<img src="media/VSTS/web-api17.png">
