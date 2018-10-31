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
ms.openlocfilehash: 818e37291fa47f99cb161c63a86062bddbf6248c
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799940"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a><span data-ttu-id="0ad79-103">CI/CD для приложений MicroProfile с использованием Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="0ad79-103">CI/CD for MicroProfile applications using Azure DevOps</span></span>

<span data-ttu-id="0ad79-104">В этом руководстве объясняется, как разработчики Java EE могут легко настроить цикл выпуска CI/CD, чтобы развернуть приложение [MicroProfile](http://microprofile.io) в экземпляре Веб-приложения для контейнеров Azure с помощью Azure DevOps (прежнее название — VSTS).</span><span class="sxs-lookup"><span data-stu-id="0ad79-104">This tutorial will show how Java EE developers can easily setup a CI/CD release cycle to deploy their [MicroProfile](http://microprofile.io) applications to an Azure Web App for Containers using Azure DevOps (formally known as VSTS).</span></span>  <span data-ttu-id="0ad79-105">В этом примере мы будем использовать приложение MicroProfile, использующее [Payara Micro](https://www.payara.fish/payara_micro) в качестве базового образа.</span><span class="sxs-lookup"><span data-stu-id="0ad79-105">In this example, we’ll be using a MicroProfile application that uses a [Payara Micro](https://www.payara.fish/payara_micro) as a base image.</span></span>   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
<span data-ttu-id="0ad79-106">Мы начнем процесс контейнеризации в Azure DevOps с создания образа Docker, а затем отправим образ контейнера в Реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="0ad79-106">We will start the Azure DevOps containerize process by building a Docker image and pushing the container image to an Azure Container Register.</span></span>  <span data-ttu-id="0ad79-107">После этого мы завершим работу с конвейером выпуска в Azure DevOps, чтобы развернуть образ контейнера в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="0ad79-107">Then complete with a Azure DevOps release pipeline to deploy the container image to a Web App.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ad79-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0ad79-108">Prerequisites</span></span>
- <span data-ttu-id="0ad79-109">Скопируйте и сохраните URL-адрес Git из [GitHub](https://github.com/Azure-Samples/microprofile-hello-azure).</span><span class="sxs-lookup"><span data-stu-id="0ad79-109">Copy and save the Git url from [Github](https://github.com/Azure-Samples/microprofile-hello-azure)</span></span>
- <span data-ttu-id="0ad79-110">Регистрируйтесь или войдите в [Azure DevOps](https://dev.azure.com), используя учетную запись.</span><span class="sxs-lookup"><span data-stu-id="0ad79-110">Register or Log into your [Azure DevOps](https://dev.azure.com) account</span></span>
- <span data-ttu-id="0ad79-111">Создайте [проект Azure DevOps](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) и **импортируйте репозиторий**, используя скопированный ранее URL-адрес Git.</span><span class="sxs-lookup"><span data-stu-id="0ad79-111">Create a new [Azure DevOps project](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) and use the above Git url to **import a repository**</span></span>
- <span data-ttu-id="0ad79-112">Создайте экземпляр службы [Реестр контейнеров Azure](https://azure.microsoft.com/en-us/services/container-registry) (ACR).</span><span class="sxs-lookup"><span data-stu-id="0ad79-112">Create an [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry) (ACR)</span></span>
- <span data-ttu-id="0ad79-113">Создайте экземпляр Веб-приложения для контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="0ad79-113">Create an Azure Web App for Container</span></span>
  > [!NOTE]
  >
  > <span data-ttu-id="0ad79-114">При подготовке экземпляра веб-приложения выберите "Быстрый запуск" в разделе "Параметры контейнера".</span><span class="sxs-lookup"><span data-stu-id="0ad79-114">Select "Quickstart" in the Container Settings when provisioning the Web App instance</span></span>


## <a name="create-a-build-definition"></a><span data-ttu-id="0ad79-115">Создание определения сборки</span><span class="sxs-lookup"><span data-stu-id="0ad79-115">Create a Build definition</span></span>

<span data-ttu-id="0ad79-116">Определение сборки в Azure DevOps обеспечивает автоматическое выполнение всех задач в сборке каждый раз, когда происходит фиксация в исходном приложении Java EE.</span><span class="sxs-lookup"><span data-stu-id="0ad79-116">The build definition in Azure DevOps automatically executes all the tasks in the build each time there’s a commit in Java EE application source application.</span></span>  <span data-ttu-id="0ad79-117">В этом примере для сборки проекта Java MicroProfile в Azure DevOps мы будем использовать Maven.</span><span class="sxs-lookup"><span data-stu-id="0ad79-117">In this example, Azure DevOps will use Maven to build the Java MicroProfile project.</span></span>

1. <span data-ttu-id="0ad79-118">Перейдите на вкладку "Сборка и выпуск" в верхней части страницы проекта Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="0ad79-118">Click on the "Build and Release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="0ad79-119">Затем щелкните ссылку **Сборки**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-119">Then, select the **Builds** link</span></span> 

<img src="media/VSTS/Buid-and-Release1.png">

2. <span data-ttu-id="0ad79-120">Нажмите кнопку **Новый конвейер** и щелкните **Продолжить**, чтобы приступить к определению задач сборки.</span><span class="sxs-lookup"><span data-stu-id="0ad79-120">Click on the **New Pipeline** button, and then **Continue** to start defining your build tasks</span></span>
3. <span data-ttu-id="0ad79-121">В списке шаблонов выберите Maven и нажмите кнопку **Применить**, чтобы выполнить сборку проекта Java.</span><span class="sxs-lookup"><span data-stu-id="0ad79-121">Select "Maven" from the list of templates, then click on the **Apply** button to build your Java project</span></span>
4. <span data-ttu-id="0ad79-122">В раскрывающемся меню поля "Пул агентов" выберите параметр **Hosted Linux Preview** (Размещенная предварительная версия Linux).</span><span class="sxs-lookup"><span data-stu-id="0ad79-122">Use the drop-down menu for the Agent pool field to select **Hosted Linux Preview** option.</span></span>
   > [!NOTE]
   >
   > <span data-ttu-id="0ad79-123">Таким образом, вы укажете Azure DevOps, какой сервер сборки использовать.</span><span class="sxs-lookup"><span data-stu-id="0ad79-123">This informs Azure DevOps which build server to use.</span></span>  <span data-ttu-id="0ad79-124">Можно использовать закрытый пользовательский сервер сборки.</span><span class="sxs-lookup"><span data-stu-id="0ad79-124">You can use your private customized build server</span></span>

5. <span data-ttu-id="0ad79-125">Чтобы настроить сборку для непрерывной интеграции, перейдите на вкладку **Триггеры** и установите флажок **Включить непрерывную интеграцию**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-125">To configure your build for continuous integration, select the **Triggers** tab and check the **Enable continuous integration** checkbox.</span></span>  

<img src="media/VSTS/Build-Triggers2.png"> 

6. <span data-ttu-id="0ad79-126">Выберите вкладку <strong>Задачи</strong>, чтобы вернуться на главную страницу конвейера сборки.</span><span class="sxs-lookup"><span data-stu-id="0ad79-126">Select the <strong>Tasks</strong> tab to return back to the main build pipeline page</span></span>
7. <span data-ttu-id="0ad79-127">В раскрывающемся меню <strong>Сохранить и поместить в очередь</strong> выберите пункт <strong>Сохранить</strong>.</span><span class="sxs-lookup"><span data-stu-id="0ad79-127">Use the <strong>Save &amp; queue</strong> drop-down menu to select the <strong>Save</strong> option</span></span>


## <a name="create-a-docker-build-image"></a><span data-ttu-id="0ad79-128">Создание образа сборки Docker</span><span class="sxs-lookup"><span data-stu-id="0ad79-128">Create a Docker Build Image</span></span>

<span data-ttu-id="0ad79-129">В этой задаче для создания образа Docker в Azure DevOps используется файл Docker с базовым образом из Payara Micro.</span><span class="sxs-lookup"><span data-stu-id="0ad79-129">In this task, Azure DevOps uses a Dockerfile with a base image from Payara Micro to create a Docker image.</span></span>  

1. <span data-ttu-id="0ad79-130">Выберите вкладку **Задачи**, чтобы вернуться на главную страницу конвейера сборки.</span><span class="sxs-lookup"><span data-stu-id="0ad79-130">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
2. <span data-ttu-id="0ad79-131">Щелкните значок **+**, чтобы добавить новую задачу в определение сборки.</span><span class="sxs-lookup"><span data-stu-id="0ad79-131">Click on the **+** icon to add new task to the build definition</span></span>

<img src="media/VSTS/Tasks-add4.png">

3. <span data-ttu-id="0ad79-132">В списке шаблонов выберите &quot;Docker&quot; и нажмите кнопку <strong>Добавить</strong>.</span><span class="sxs-lookup"><span data-stu-id="0ad79-132">Select &quot;Docker&quot; from the list of templates, then click on the <strong>Add</strong> button</span></span>
4. <span data-ttu-id="0ad79-133">Введите описательное имя в поле <strong>Отображаемое имя</strong>.</span><span class="sxs-lookup"><span data-stu-id="0ad79-133">Enter a description name for the <strong>Display name</strong> field</span></span>
5. <span data-ttu-id="0ad79-134">Убедитесь, что в раскрывающемся меню для поля <strong>Тип реестра контейнеров</strong> выбран пункт <strong>Реестр контейнеров Azure</strong>.</span><span class="sxs-lookup"><span data-stu-id="0ad79-134">Verify that <strong>Azure Container Registry</strong> is selected in the drop-down menu for <strong>Container registry type</strong>.</span></span>
<span data-ttu-id="0ad79-135">&gt;</span><span class="sxs-lookup"><span data-stu-id="0ad79-135">&gt;</span></span> [!NOTE]
<span data-ttu-id="0ad79-136">&gt; &gt; Если вы используете Docker Hub или другой реестр, выберите &quot;Реестр контейнеров&quot;.</span><span class="sxs-lookup"><span data-stu-id="0ad79-136">&gt; &gt;  If you are using Docker Hub or another registry, select &quot;Container Registry&quot; instead.</span></span>  <span data-ttu-id="0ad79-137">Нажмите кнопку &quot;+ Создать&quot;, чтобы указать учетные данные и данные подключения для этого реестра.</span><span class="sxs-lookup"><span data-stu-id="0ad79-137">Then click on the &quot;+ New&quot; button to provide the credentials and connection information for it.</span></span> <span data-ttu-id="0ad79-138">Затем перейдите к разделу "Команды", чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="0ad79-138">Then skip to the Commands section to continue.</span></span>

6. <span data-ttu-id="0ad79-139">В раскрывающемся меню **Подписка Azure** выберите идентификатор своей подписки.</span><span class="sxs-lookup"><span data-stu-id="0ad79-139">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>  <span data-ttu-id="0ad79-140">Нажмите кнопку **Авторизовать**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-140">Then click on the **Authorize** button</span></span>
7. <span data-ttu-id="0ad79-141">В раскрывающемся меню **Реестр контейнеров Azure** выберите имя реестра, который вы создали в Azure.</span><span class="sxs-lookup"><span data-stu-id="0ad79-141">In the **Azure container registry** drop-down menu, select registry name you created in Azure.</span></span>
8. <span data-ttu-id="0ad79-142">Убедитесь, что в раскрывающемся меню **Команда** выбран пункт **Сборка**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-142">Verify that **build** option is selected in the **Command** drop-down menu.</span></span>
9. <span data-ttu-id="0ad79-143">Рядом с текстовым полем **Файл Docker** щелкните значок навигации для выбора пути, чтобы выбрать файл Docker в проекте GitHub.</span><span class="sxs-lookup"><span data-stu-id="0ad79-143">For the **Dockerfile**, click on the path navigation icon next to the textbox to select the Dockerfile from the github project.</span></span>  <span data-ttu-id="0ad79-144">Затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-144">Then click the **OK** button.</span></span>

<img src="media/VSTS/Dockerfile5.png">

10. <span data-ttu-id="0ad79-145">Под полем **Имя образа** установите флажок **Включить последний тег**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-145">Under the **Image name**, check the **Include latest tag** checkbox.</span></span> 
11. <span data-ttu-id="0ad79-146">В раскрывающемся меню **Сохранить и поместить в очередь** выберите пункт **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-146">Use the **Save & queue** drop-down menu to select the **Save** option.</span></span>

## <a name="push-docker-image-to-acr"></a><span data-ttu-id="0ad79-147">Отправка образа Docker в ACR</span><span class="sxs-lookup"><span data-stu-id="0ad79-147">Push Docker Image to ACR</span></span>

<span data-ttu-id="0ad79-148">В этой задаче Azure DevOps отправит образ Docker в Реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="0ad79-148">In this task, Azure DevOps will push the docker image to your Azure Container Registry.</span></span>  <span data-ttu-id="0ad79-149">Этот образ будет использоваться для запуска приложения API MicroProfile в качестве контейнерного веб-приложения Java.</span><span class="sxs-lookup"><span data-stu-id="0ad79-149">This will be used to run the MicroProfile API application as a containerized Java web app.</span></span>

1. <span data-ttu-id="0ad79-150">Так как мы используем Docker в Azure DevOps, создайте новый шаблон Docker, повторив шаги 1–7, приведенные в разделе **Создание образа сборки Docker**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-150">Since we are using Docker in Azure DevOps, create a new Docker template by repeating steps 1 - 7 above in the **Create a Docker Build Image** section.</span></span>
2. <span data-ttu-id="0ad79-151">В раскрывающемся меню **Команда** выберите **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-151">Select **push** in the **Command** drop-down menu.</span></span>
3. <span data-ttu-id="0ad79-152">Перейдите на вкладку **Сохранить и поместить в очередь** и выберите пункт **Сохранить и поместить в очередь**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-152">Click on the **Save & queue** tab, then select **Save & queue** option.</span></span>
4. <span data-ttu-id="0ad79-153">Убедитесь, что во всплывающем окне для пула агентов выбрано значение **Hosted Linux Preview** (Размещенная предварительная версия Linux).</span><span class="sxs-lookup"><span data-stu-id="0ad79-153">Verify that the **Hosted Linux Preview** is select for the Agent pool on the pop-up window.</span></span>  <span data-ttu-id="0ad79-154">Нажмите кнопку **Сохранить и поместить в очередь**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-154">Then click on the **Save & queue** button.</span></span>
5. <span data-ttu-id="0ad79-155">Щелкните номер сборки, чтобы проверить, успешно ли завершен конвейер сборки для проекта Java.</span><span class="sxs-lookup"><span data-stu-id="0ad79-155">Click on the build number to verify that the build pipeline for the Java project completed successfully.</span></span>

<img src="media/VSTS/Build-Number6.png">


## <a name="create-a-release-definition-for-a-java-app"></a><span data-ttu-id="0ad79-156">Создание определения выпуска для приложения Java</span><span class="sxs-lookup"><span data-stu-id="0ad79-156">Create a release definition for a Java app</span></span>

<span data-ttu-id="0ad79-157">Конвейер выпуска в Azure DevOps автоматически активирует развертывание артефактов сборки в целевую среду, например Azure, как только процесс сборки успешно завершится.</span><span class="sxs-lookup"><span data-stu-id="0ad79-157">The release pipeline in Azure DevOps automatically triggers the deployment of build artifacts to a target environment like Azure as soon as the Build process completes successfully.</span></span>   <span data-ttu-id="0ad79-158">Конвейер выпуска можно создавать для сред разработки, тестирования, промежуточной или рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="0ad79-158">The release pipeline can be created for dev, test, staging or production environments.</span></span>

1. <span data-ttu-id="0ad79-159">Перейдите на вкладку "Сборка и выпуск" в верхней части страницы проекта Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="0ad79-159">Click on the "Build and release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="0ad79-160">Щелкните ссылку **Выпуски**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-160">Then, select the **Releases** link.</span></span>

<img src="media/VSTS/Release-new-pipeline7.png">

2. <span data-ttu-id="0ad79-161">Нажмите кнопку &quot;Новый конвейер\*\*.</span><span class="sxs-lookup"><span data-stu-id="0ad79-161">Click on the &quot;New pipeline\*\* button</span></span>
3. <span data-ttu-id="0ad79-162">В списке шаблонов выберите <strong>Развертывание приложения Java в службе приложений Azure</strong>, а затем нажмите кнопку <strong>Применить</strong>.</span><span class="sxs-lookup"><span data-stu-id="0ad79-162">Select the <strong>Deploy a Java app to Azure App Service</strong> in the list of templates, then click on the <strong>Apply</strong> button.</span></span>

<img src="media/VSTS/deploy-java-template8.png">

4. <span data-ttu-id="0ad79-163">Укажите <strong>имя этапа</strong> (например, разработки, тестирования или промежуточного этапа).</span><span class="sxs-lookup"><span data-stu-id="0ad79-163">Set a <strong>Stage name</strong> (e.g Dev, Test, Staging or Production).</span></span>  <span data-ttu-id="0ad79-164">Нажмите кнопку <strong>X</strong>, чтобы закрыть всплывающее окно.</span><span class="sxs-lookup"><span data-stu-id="0ad79-164">Then click on the <strong>X</strong> button to close the pop-up window</span></span>
5. <span data-ttu-id="0ad79-165">В разделе артефактов нажмите кнопку <strong>+Добавить</strong>.</span><span class="sxs-lookup"><span data-stu-id="0ad79-165">Click on the <strong>+ Add</strong> button in the Artifacts section.</span></span>  <span data-ttu-id="0ad79-166">Таким образом, вы свяжете артефакты из определения сборки с артефактами из этого определения выпуска.</span><span class="sxs-lookup"><span data-stu-id="0ad79-166">This will link artifacts from the build definition to this release definition.</span></span><br/><span data-ttu-id="0ad79-167">6. В раскрывающемся меню для поля <strong>Источник (конвейер сборки)</strong> выберите определение сборки.</span><span class="sxs-lookup"><span data-stu-id="0ad79-167">6. Use the drop-down menu for the <strong>Source (build pipeline)</strong> to select your build definition.</span></span> <span data-ttu-id="0ad79-168">Нажмите кнопку <strong>Добавить</strong>, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="0ad79-168">Then click the <strong>Add</strong> button to continue.</span></span>

<img src="media/VSTS/add-artifact9.png">

7. <span data-ttu-id="0ad79-169">Перейдите на вкладку <strong>Задачи</strong> на странице конвейера.</span><span class="sxs-lookup"><span data-stu-id="0ad79-169">Click on the <strong>Tasks</strong> tab on the pipeline.</span></span>  <span data-ttu-id="0ad79-170">Выберите имя этапа.</span><span class="sxs-lookup"><span data-stu-id="0ad79-170">Then, select your stage name.</span></span>

<img src="media/VSTS/release-stage10.png">

8. <span data-ttu-id="0ad79-171">В раскрывающемся меню **Подписка Azure** выберите идентификатор своей подписки.</span><span class="sxs-lookup"><span data-stu-id="0ad79-171">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>
9. <span data-ttu-id="0ad79-172">Выберите тип **Приложение Linux** в раскрывающемся меню **Тип приложения**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-172">Select **Linux App** from the **App type** drop-down menu</span></span>
10. <span data-ttu-id="0ad79-173">В раскрывающемся меню **Имя службы приложений** выберите имя созданного ранее экземпляра службы "Веб-приложение для контейнеров".</span><span class="sxs-lookup"><span data-stu-id="0ad79-173">Select the name of the Web App for Container instance you created above in the **App service name** drop-down menu</span></span>
11. <span data-ttu-id="0ad79-174">Введите имя экземпляра службы "Реестр контейнеров Azure" в поле **Registry or Namespaces** (Реестр или пространства имен).</span><span class="sxs-lookup"><span data-stu-id="0ad79-174">Enter the name of your azure container registry in the **Registry or Namespaces** field.</span></span>  <span data-ttu-id="0ad79-175">Например, **myregistry.azure.io**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-175">E.g **myregistry.azure.io**</span></span>
12. <span data-ttu-id="0ad79-176">Введите имя реестра в поле **Репозиторий**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-176">Enter the registry name in the **Repository** field</span></span>
13. <span data-ttu-id="0ad79-177">Щелкните **Deploy Azure App Service** (Развернуть службу приложений Azure).</span><span class="sxs-lookup"><span data-stu-id="0ad79-177">Click on **Deploy Azure App Service**.</span></span>  <span data-ttu-id="0ad79-178">Введите тег для образа контейнера в текстовом поле **Тег**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-178">Enter the tag for the container image in the **Tag** textbox</span></span> 
14. <span data-ttu-id="0ad79-179">Щелкните **Запуск на агенте**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-179">Click on **Run on agent**.</span></span>  <span data-ttu-id="0ad79-180">В раскрывающемся меню пула агента выберите **Hosted Linux Preview** (Размещенная предварительная версия Linux).</span><span class="sxs-lookup"><span data-stu-id="0ad79-180">Select **Hosted Linux Preview** in the Agent pool drop-down menu</span></span> 

## <a name="setup-environment-variables"></a><span data-ttu-id="0ad79-181">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="0ad79-181">Setup Environment Variables</span></span>

1. <span data-ttu-id="0ad79-182">Перейдите на вкладку **Переменные**.  Нажмите кнопку **+Добавить**, чтобы определить переменные среды.</span><span class="sxs-lookup"><span data-stu-id="0ad79-182">Click on the **Variables** tab.  Then click on the **+ Add** button to define your environment variables</span></span>
2. <span data-ttu-id="0ad79-183">Добавьте имя переменной и значения для URL-адреса реестра контейнеров, имя пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="0ad79-183">Add the variable name and values for your container registry url, username and password.</span></span>   <span data-ttu-id="0ad79-184">В целях безопасности щелкните значок замка, чтобы скрыть значение пароля.</span><span class="sxs-lookup"><span data-stu-id="0ad79-184">For security, click on the lock icon to keep the password value hidden.</span></span>

<span data-ttu-id="0ad79-185">Например: </span><span class="sxs-lookup"><span data-stu-id="0ad79-185">For example:</span></span>
- <span data-ttu-id="0ad79-186">registry.password;</span><span class="sxs-lookup"><span data-stu-id="0ad79-186">registry.password</span></span>
- <span data-ttu-id="0ad79-187">registry.url;</span><span class="sxs-lookup"><span data-stu-id="0ad79-187">registry.url</span></span>
- <span data-ttu-id="0ad79-188">registry.username.</span><span class="sxs-lookup"><span data-stu-id="0ad79-188">registry.username</span></span>

<img src="media/VSTS/environment-variables12.png">

3. <span data-ttu-id="0ad79-189">Щелкните вкладку **Задачи**, чтобы вернуться на главную страницу определения конвейера выпуска.</span><span class="sxs-lookup"><span data-stu-id="0ad79-189">Click on the **Tasks** tab to return to the main release pipeline definition page</span></span>
4. <span data-ttu-id="0ad79-190">Щелкните **Deploy Azure App Service** (Развернуть службу приложений Azure).</span><span class="sxs-lookup"><span data-stu-id="0ad79-190">Click on **Deploy Azure App Service**.</span></span> 
5. <span data-ttu-id="0ad79-191">Разверните раздел **Параметры приложения и конфигурации**, щелкните значок навигации для выбора пути в поле **Параметры приложения**, чтобы добавить переменную среды для подключения к реестру контейнеров во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="0ad79-191">Expand the **Application and Configuration Settings** section, then click on the navigation path for the **App Settings** field to add environments variable to connect to the container registry during deployment.</span></span>
6. <span data-ttu-id="0ad79-192">Нажмите кнопку **+Добавить**, чтобы определить следующие параметры приложения и присвоить переменные среды.</span><span class="sxs-lookup"><span data-stu-id="0ad79-192">Click on the \*\* + Add\*\* button to define the following app settings and assign the environment variables</span></span>
7. <span data-ttu-id="0ad79-193">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password).</span><span class="sxs-lookup"><span data-stu-id="0ad79-193">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span></span>
8. <span data-ttu-id="0ad79-194">DOCKER_REGISTRY_SERVER_URL = $(registry.url).</span><span class="sxs-lookup"><span data-stu-id="0ad79-194">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span></span>
9. <span data-ttu-id="0ad79-195">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username).</span><span class="sxs-lookup"><span data-stu-id="0ad79-195">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span></span>

<img src="media/VSTS/environment-variables14.png">

7. <span data-ttu-id="0ad79-196">Нажмите кнопку <strong>ОК</strong>, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="0ad79-196">Click on the <strong>OK</strong> button to continue</span></span>

## <a name="setup-continious-deployment--deploy-java-application"></a><span data-ttu-id="0ad79-197">Настройка непрерывного развертывания и развертывание приложения Java</span><span class="sxs-lookup"><span data-stu-id="0ad79-197">Setup Continious Deployment & Deploy Java Application</span></span>

1. <span data-ttu-id="0ad79-198">Чтобы включить непрерывное развертывание, перейдите на вкладку **Конвейеры**.</span><span class="sxs-lookup"><span data-stu-id="0ad79-198">To enable continuous deployment, click the **Pipelines** tab</span></span>
2. <span data-ttu-id="0ad79-199">В разделе "Артефакты" щелкните значок с молнией.</span><span class="sxs-lookup"><span data-stu-id="0ad79-199">In the Artifacts section, click on the lightening icon.</span></span>  <span data-ttu-id="0ad79-200">Затем задайте для параметра **Триггер непрерывного развертывания** значение "Вкл.".</span><span class="sxs-lookup"><span data-stu-id="0ad79-200">Then set the **Continuous deployment trigger** to Enabled.</span></span>

<img src="media/VSTS/release-enable-CD.png">

3. <span data-ttu-id="0ad79-201">Последовательно нажмите кнопки <strong>Сохранить</strong> и <strong>ОК</strong>.</span><span class="sxs-lookup"><span data-stu-id="0ad79-201">Click on the <strong>Save</strong> button, then the <strong>OK</strong> button</span></span> 
4. <span data-ttu-id="0ad79-202">Щелкните стрелку раскрывающегося меню <strong>+Выпуск</strong> и выберите ссылку <strong>Создать выпуск</strong>.</span><span class="sxs-lookup"><span data-stu-id="0ad79-202">Click on the <strong>+ Release</strong> drop-down menu, then select <strong>Create a release</strong> link</span></span>
5. <span data-ttu-id="0ad79-203">В раскрывающемся меню <strong>Stages for a trigger change from automated to manual</strong> (Этапы для изменения автоматической активации на активацию вручную) установите флажок рядом с вашим именем этапа.</span><span class="sxs-lookup"><span data-stu-id="0ad79-203">Use the <strong>Stages for a trigger change from automated to manual</strong> drop-down menu to select the checkbox for your stage name</span></span>
6. <span data-ttu-id="0ad79-204">Нажмите кнопку <strong>Создать</strong>, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="0ad79-204">Click the <strong>Create</strong> button to continue</span></span>
7. <span data-ttu-id="0ad79-205">Щелкните номер выпуска.</span><span class="sxs-lookup"><span data-stu-id="0ad79-205">Click on the release number.</span></span>  <span data-ttu-id="0ad79-206">Затем наведите указатель мыши на имя этапа и нажмите кнопку <strong>Развернуть</strong>.</span><span class="sxs-lookup"><span data-stu-id="0ad79-206">Then hover your mouse cursor over the stage name and click on the <strong>Deploy</strong> button</span></span>
8. <span data-ttu-id="0ad79-207">Затем нажмите кнопку <strong>Развернуть</strong> во всплывающем окне, чтобы запустить развертывание в Azure.</span><span class="sxs-lookup"><span data-stu-id="0ad79-207">The click on the <strong>Deploy</strong> button on the pop-up window to start the deployment process to Azure</span></span>


## <a name="test-the-java-web-application"></a><span data-ttu-id="0ad79-208">Тестирование веб-приложения Java</span><span class="sxs-lookup"><span data-stu-id="0ad79-208">Test the Java Web Application</span></span>
1. <span data-ttu-id="0ad79-209">Укажите URL-адрес веб-приложения в адресной строке веб-браузера:</span><span class="sxs-lookup"><span data-stu-id="0ad79-209">Run the web app url in web browser:</span></span>  
   <span data-ttu-id="0ad79-210">https://{имя-экземпляра-службы-приложений}.azurewebsites.net/api/hello</span><span class="sxs-lookup"><span data-stu-id="0ad79-210">https://{your-app-service-name}.azurewebsites.net/api/hello</span></span>


<img src="media/VSTS/web-app16.png">

2. <span data-ttu-id="0ad79-211">На веб-странице должно отобразится **Hello Azure!**</span><span class="sxs-lookup"><span data-stu-id="0ad79-211">The web page should say **Hello Azure!**</span></span>

<img src="media/VSTS/web-api17.png">
