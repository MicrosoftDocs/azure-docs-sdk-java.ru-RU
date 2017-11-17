---
title: "Настройка развертываний веб-приложений с использованием Java | Документация Майкрософт"
description: "Пример кода Java для настройки развертываний Git или FTP в службе приложений Azure с использованием пакета Azure SDK для Java"
author: rloutlaw
manager: douge
ms.assetid: 833e9c78-1e50-4c23-a611-f73a2f0c2983
ms.service: Azure
ms.devlang: java
ms.topic: article
ms.date: 03/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 910d1e43c9942d6402aeccb8757ba819b7453dab
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
# <a name="configure-azure-app-service-deployment-sources-from-your-java-applications"></a><span data-ttu-id="f0f95-103">Настройка источников развертывания в службе приложений Azure из приложений Java</span><span class="sxs-lookup"><span data-stu-id="f0f95-103">Configure Azure App Service deployment sources from your Java applications</span></span>

<span data-ttu-id="f0f95-104">В [этом примере](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) развертывается код для четырех приложений в рамках одного плана [службы приложений Azure](https://docs.microsoft.com/azure/app-service/). Для каждого приложения используется отдельный источник развертывания.</span><span class="sxs-lookup"><span data-stu-id="f0f95-104">[This sample](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) deploys code to four applications in a single [Azure App Service](https://docs.microsoft.com/azure/app-service/) plan, each using a different deployment source.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="f0f95-105">Запуск примера</span><span class="sxs-lookup"><span data-stu-id="f0f95-105">Run the sample</span></span>

<span data-ttu-id="f0f95-106">Создайте [файл проверки подлинности](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md), задайте переменную среды `AZURE_AUTH_LOCATION` и укажите полный путь к файлу на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f0f95-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="f0f95-107">Далее выполните:</span><span class="sxs-lookup"><span data-stu-id="f0f95-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps.git
cd app-service-java-configure-deployment-sources-for-web-apps
mvn clean compile exec:java
```

<span data-ttu-id="f0f95-108">См. [полный пример кода на GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java).</span><span class="sxs-lookup"><span data-stu-id="f0f95-108">View the [complete sample code on GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="f0f95-109">Проверка подлинности с помощью Azure</span><span class="sxs-lookup"><span data-stu-id="f0f95-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-app-service-app-running-apache-tomcat"></a><span data-ttu-id="f0f95-110">Создание приложения службы приложений под управлением Apache Tomcat</span><span class="sxs-lookup"><span data-stu-id="f0f95-110">Create a App Service app running Apache Tomcat</span></span>

```java
// create a new Standard app service plan and create a single Java 8/Tomcat 8 app in it
WebApp app1 = azure.webApps().define(app1Name)
             .withNewResourceGroup(rgName)
             .withNewAppServicePlan(planName)
             .withRegion(Region.US_WEST)
             .withPricingTier(AppServicePricingTier.STANDARD_S1)
             .withJavaVersion(JavaVersion.JAVA_8_NEWEST)
             .withWebContainer(WebContainer.TOMCAT_8_0_NEWEST)
             .create();
```

<span data-ttu-id="f0f95-111">`withJavaVersion()` и `withWebContainer()` настраивают службу приложений для обслуживания HTTP-запросов с использованием Tomcat 8.</span><span class="sxs-lookup"><span data-stu-id="f0f95-111">`withJavaVersion()` and `withWebContainer()` configure App Service to serve HTTP requests using Tomcat 8.</span></span>

## <a name="deploy-a-java-application-using-ftp"></a><span data-ttu-id="f0f95-112">Развертывание приложения Java с использованием протокола FTP</span><span class="sxs-lookup"><span data-stu-id="f0f95-112">Deploy a Java application using FTP</span></span>
```java
// pass the PublishingProfile that contains FTP information to a helper method 
uploadFileToFtp(app1.getPublishingProfile(), "helloworld.war", 
      ManageWebAppSourceControl.class.getResourceAsStream("/helloworld.war"));

// Use the FTP classes in the Apache Commons library to connect to Azure using 
// the information from the PublishingProfile
private static void uploadFileToFtp(PublishingProfile profile, String fileName, InputStream file) throws Exception {
        FTPClient ftpClient = new FTPClient();
        String[] ftpUrlSegments = profile.ftpUrl().split("/", 2);
        String server = ftpUrlSegments[0];
        // Tomcat will deploy WAR files uploaded to this directory.
        String path = "./site/wwwroot/webapps"; 

        // FTP the build WAR to Azure
        ftpClient.connect(server);
        ftpClient.login(profile.ftpUsername(), profile.ftpPassword());
        ftpClient.setFileType(FTP.BINARY_FILE_TYPE);
        ftpClient.changeWorkingDirectory(path);
        ftpClient.storeFile(fileName, file);
        ftpClient.disconnect();
}
```

<span data-ttu-id="f0f95-113">Этот код передает WAR-файл в каталог `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="f0f95-113">This code uploads a WAR file to the `/site/wwwroot/webapps` directory.</span></span> <span data-ttu-id="f0f95-114">Tomcat развертывает WAR-файлы, по умолчанию помещенные в эту папку в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="f0f95-114">Tomcat deploys WAR files placed in this directory by default in App Service.</span></span>

## <a name="deploy-a-java-application-from-a-local-git-repo"></a><span data-ttu-id="f0f95-115">Развертывание приложения Java из локального репозитория Git</span><span class="sxs-lookup"><span data-stu-id="f0f95-115">Deploy a Java application from a local Git repo</span></span>

```java
// get the publishing profile from the App Service webapp
PublishingProfile profile = app2.getPublishingProfile();

// create a new Git repo in the sample directory under src/main/resources 
Git git = Git
    .init()
    .setDirectory(new File(ManageWebAppSourceControl.class.getResource("/azure-samples-appservice-helloworld/").getPath()))
    .call();
git.add().addFilepattern(".").call();
// add the files in the sample app to an initial commit
git.commit().setMessage("Initial commit").call(); 

// push the commit using the Azure Git remote URL and credentials in the publishing profile
PushCommand command = git.push();
command.setRemote(profile.gitUrl()); 
command.setCredentialsProvider(new UsernamePasswordCredentialsProvider(profile.gitUsername(), profile.gitPassword()));
command.setRefSpecs(new RefSpec("master:master")); 
command.setForce(true);
command.call();
```      

<span data-ttu-id="f0f95-116">Этот код использует библиотеки [JGit](https://eclipse.org/jgit/), чтобы создать репозиторий Git в папке `src/main/resources/azure-samples-appservice-helloworld`.</span><span class="sxs-lookup"><span data-stu-id="f0f95-116">This code uses the [JGit](https://eclipse.org/jgit/) libraries to create a new Git repo in the `src/main/resources/azure-samples-appservice-helloworld` folder.</span></span> <span data-ttu-id="f0f95-117">Затем в примере все файлы добавляются в папку для начальной фиксации. Фиксация отправляется в Azure с использованием сведений о развертывании Git из `PublishingProfile` веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f0f95-117">The sample then adds all files in the folder to an initial commit and pushes the commit to Azure using Git deployment information from the webapp's `PublishingProfile`.</span></span> 

>[!NOTE]
> <span data-ttu-id="f0f95-118">Макет файлов в репозитории должен точно соответствовать предполагаемому способу их развертывания в каталоге `/site/wwwroot/` в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="f0f95-118">The layout of the files in the repo must match exactly how you want the files deployed under the `/site/wwwroot/` directory in Azure App Service.</span></span>

## <a name="deploy-an-application-from-a-public-git-repo"></a><span data-ttu-id="f0f95-119">Развертывание приложения из общедоступного репозитория Git</span><span class="sxs-lookup"><span data-stu-id="f0f95-119">Deploy an application from a public Git repo</span></span>

```java
// deploy a .NET sample app from a public GitHub repo into a new webapp
WebApp app3 = azure.webApps().define(app3Name)
                .withNewResourceGroup(rgName)
                .withExistingAppServicePlan(plan)
                .defineSourceControl()
                .withPublicGitRepository(
                   "https://github.com/Azure-Samples/app-service-web-dotnet-get-started")
                .withBranch("master")
                .attach()
                .create();
 ```

 <span data-ttu-id="f0f95-120">Среда выполнения службы приложений автоматически собирает и развертывает проект .NET с использованием последней версии кода в ветви `master` репозитория.</span><span class="sxs-lookup"><span data-stu-id="f0f95-120">The App Service runtime automatically builds and deploys the .NET project using the latest code on the `master` branch of the repo.</span></span>

## <a name="continuous-deployment-from-a-github-repo"></a><span data-ttu-id="f0f95-121">Непрерывное развертывание из репозитория GitHub</span><span class="sxs-lookup"><span data-stu-id="f0f95-121">Continuous deployment from a GitHub repo</span></span>

```java
// deploy the application whenever you push a new commit or merge a pull request into your master branch
WebApp app4 = azure.webApps()
                    .define(app4Name)
                    .withExistingResourceGroup(rgName)
                    .withExistingAppServicePlan(plan)
                    // Uncomment the following lines to turn on continuous deployment scenario
                    //.defineSourceControl()
                    //    .withContinuouslyIntegratedGitHubRepository("username", "reponame")
                    //    .withBranch("master")
                    //    .withGitHubAccessToken("YOUR GITHUB PERSONAL TOKEN")
                    //    .attach()
                    .create();
```  

<span data-ttu-id="f0f95-122">`username` и `reponame` — значения, использующиеся в GitHub.</span><span class="sxs-lookup"><span data-stu-id="f0f95-122">The `username` and `reponame` values are the ones used in GitHub.</span></span> <span data-ttu-id="f0f95-123">[Создайте личный маркер доступа GitHub](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) с разрешениями на чтение в репозитории, а затем передайте его в `withGitHubAccessToken`.</span><span class="sxs-lookup"><span data-stu-id="f0f95-123">[Create a GitHub personal access token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) with repo read permissions and pass it to `withGitHubAccessToken`.</span></span> 


## <a name="sample-explanation"></a><span data-ttu-id="f0f95-124">Описание примера</span><span class="sxs-lookup"><span data-stu-id="f0f95-124">Sample explanation</span></span>

<span data-ttu-id="f0f95-125">В примере создается первое приложение с помощью Java 8 и Tomcat 8. Оно выполняется в созданном плане службы приложений [Стандартный](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span><span class="sxs-lookup"><span data-stu-id="f0f95-125">The sample creates the first application using Java 8 and Tomcat 8 running in a newly created [Standard](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) App Service plan.</span></span> <span data-ttu-id="f0f95-126">Затем код передает WAR-файл по протоколу FTP, используя сведения в объекте `PublishingProfile`, а Tomcat развертывает его.</span><span class="sxs-lookup"><span data-stu-id="f0f95-126">The code then FTPs a WAR file using the information in the `PublishingProfile` object and Tomcat deploys it.</span></span>

<span data-ttu-id="f0f95-127">Второе приложение используется в рамках того же плана, что и первое. Оно также настраивается как приложение Java 8 и Tomcat 8.</span><span class="sxs-lookup"><span data-stu-id="f0f95-127">The second application uses in the same plan as the first and is also configured as a Java 8/Tomcat 8 application.</span></span> <span data-ttu-id="f0f95-128">Библиотеки JGit создают репозиторий Git в папке с распакованным веб-приложением Java в структуре каталогов, которая сопоставляется с данными службы приложений.</span><span class="sxs-lookup"><span data-stu-id="f0f95-128">The JGit libraries create a new Git repository in a folder that contains an unpacked Java web application in a directory structure that maps to App Service.</span></span> <span data-ttu-id="f0f95-129">Новая фиксация добавляет файлы в папке в новый репозиторий Git. Git отправляет фиксацию в Azure с использованием URL-адреса удаленного объекта, а также имени пользователя и пароля, указанных в `PublishingProfile` веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f0f95-129">A new commit adds the files in the folder to the new Git repo, and Git pushes the commit to Azure with a remote URL and username/password provided by the webapp's `PublishingProfile`.</span></span>

<span data-ttu-id="f0f95-130">Третье приложение не настраивается для Java и Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f0f95-130">The third application is not configured for Java and Tomcat.</span></span> <span data-ttu-id="f0f95-131">Вместо этого пример .NET развертывается в общедоступном репозитории GitHub непосредственно из источника.</span><span class="sxs-lookup"><span data-stu-id="f0f95-131">Instead, a .NET sample in a public GitHub repo is deployed directly from source.</span></span>

<span data-ttu-id="f0f95-132">Четвертое приложение развертывает код в главной ветви при каждой отправке изменений или слиянии запроса на вытягивание в главной ветви репозитория GitHub.</span><span class="sxs-lookup"><span data-stu-id="f0f95-132">The fourth application deploys the code in your master branch every time you push changes or merge a pull request into the GitHub repo's master branch.</span></span>

| <span data-ttu-id="f0f95-133">Класс, используемый в примере</span><span class="sxs-lookup"><span data-stu-id="f0f95-133">Class used in sample</span></span> | <span data-ttu-id="f0f95-134">Примечания</span><span class="sxs-lookup"><span data-stu-id="f0f95-134">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="f0f95-135">WebApp</span><span class="sxs-lookup"><span data-stu-id="f0f95-135">WebApp</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_app) | <span data-ttu-id="f0f95-136">Создается из текучей цепочки `azure.webApps().define()....create()`.</span><span class="sxs-lookup"><span data-stu-id="f0f95-136">Created from the `azure.webApps().define()....create()` fluent chain.</span></span> <span data-ttu-id="f0f95-137">Создает веб-приложение службы приложений и любые ресурсы, требующиеся для приложения.</span><span class="sxs-lookup"><span data-stu-id="f0f95-137">Creates a App Service web app and any resources needed for the app.</span></span> <span data-ttu-id="f0f95-138">Большинство методов обращаются к объекту, чтобы получить сведения о конфигурации. Но методы команд, например `restart()`, изменяют состояние веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f0f95-138">Most methods query the object for configuration details, but verb methods like `restart()` change the state of the webapp.</span></span>
| [<span data-ttu-id="f0f95-139">WebContainer</span><span class="sxs-lookup"><span data-stu-id="f0f95-139">WebContainer</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_container) | <span data-ttu-id="f0f95-140">Класс со статическими общедоступными полями, которые используются в качестве параметров для `withWebContainer()` при определении WebApp для выполнения в веб-контейнере Java.</span><span class="sxs-lookup"><span data-stu-id="f0f95-140">Class with static public fields used as paramters to `withWebContainer()` when defining a WebApp running a Java webcontainer.</span></span> <span data-ttu-id="f0f95-141">Содержит варианты для версий Tomcat и Jetty.</span><span class="sxs-lookup"><span data-stu-id="f0f95-141">Has choices for both Jetty and Tomcat versions.</span></span>
| [<span data-ttu-id="f0f95-142">PublishingProfile</span><span class="sxs-lookup"><span data-stu-id="f0f95-142">PublishingProfile</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._publishing_profile) | <span data-ttu-id="f0f95-143">Класс, получаемый с помощью объекта WebApp с использованием метода `getPublishingProfile()`.</span><span class="sxs-lookup"><span data-stu-id="f0f95-143">Obtained through a WebApp object using the `getPublishingProfile()` method.</span></span> <span data-ttu-id="f0f95-144">Содержит сведения о развертывании FTP и Git, включая имя пользователя и пароль для развертывания (отличные от данных учетной записи Azure или учетных данных субъекта-службы).</span><span class="sxs-lookup"><span data-stu-id="f0f95-144">Contains FTP and Git deployment information, including deployment username and password (which is separate from Azure account or service principal credentials).</span></span>
| [<span data-ttu-id="f0f95-145">AppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f0f95-145">AppServicePlan</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_plan) | <span data-ttu-id="f0f95-146">Класс, возвращаемый `azure.appServices().appServicePlans().getByResourceGroup()`.</span><span class="sxs-lookup"><span data-stu-id="f0f95-146">Returned by `azure.appServices().appServicePlans().getByResourceGroup()`.</span></span> <span data-ttu-id="f0f95-147">Доступны методы для проверки производительности, уровня и числа веб-приложений, выполняющихся в плане.</span><span class="sxs-lookup"><span data-stu-id="f0f95-147">Methods are availble to check the capacity, tier, and number of web apps running in the plan.</span></span>
| [<span data-ttu-id="f0f95-148">AppServicePricingTier</span><span class="sxs-lookup"><span data-stu-id="f0f95-148">AppServicePricingTier</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_pricing_tier) | <span data-ttu-id="f0f95-149">Класс со статическими общедоступными полями, которые представляют уровни службы приложений.</span><span class="sxs-lookup"><span data-stu-id="f0f95-149">Class with static public fields representing App Service tiers.</span></span> <span data-ttu-id="f0f95-150">Используется для определения встроенного уровня плана при создании приложения с использованием `withPricingTier()` или непосредственно при определении плана с помощью `azure.appServices().appServicePlans().define()`.</span><span class="sxs-lookup"><span data-stu-id="f0f95-150">Used to define a plan tier in-line during app creation with `withPricingTier()` or directly when defining a plan via `azure.appServices().appServicePlans().define()`</span></span>
| [<span data-ttu-id="f0f95-151">JavaVersion</span><span class="sxs-lookup"><span data-stu-id="f0f95-151">JavaVersion</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._java_version) | <span data-ttu-id="f0f95-152">Класс со статическими общедоступными полями, которые представляют версии Java, поддерживаемые службой приложений.</span><span class="sxs-lookup"><span data-stu-id="f0f95-152">Class with static public fields representing Java versions supported by App Service.</span></span> <span data-ttu-id="f0f95-153">Используется с `withJavaVersion()` во время выполнения цепочки `define()...create()` при создании нового веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f0f95-153">Used with `withJavaVersion()` during the `define()...create()` chain when creating a new webapp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0f95-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f0f95-154">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]