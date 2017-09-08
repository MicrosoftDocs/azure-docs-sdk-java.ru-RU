---
title: "Развертывание веб-приложения Java в Azure за пять минут с помощью Maven | Документация Майкрософт"
description: "Создание и развертывание приложения Java, созданного с помощью Maven, в Azure"
services: app-service\web
documentationcenter: 
author: rloutlaw
manager: douge
editor: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: routlaw
ms.openlocfilehash: 9c3d39e12b00dd1dd3d5f76162ce0f387c7a947c
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/28/2017
---
# <a name="create-and-deploy-a-java-app-to-azure-with-maven"></a><span data-ttu-id="f14d3-103">Создание и развертывание приложения Java в Azure с помощью Maven</span><span class="sxs-lookup"><span data-stu-id="f14d3-103">Create and deploy a Java app to Azure with Maven</span></span>

<span data-ttu-id="f14d3-104">Это краткое руководство поможет вам создать и развернуть простое веб-приложение Java в [службе приложений Azure](/azure/app-service/app-service-value-prop-what-is) с использованием [Apache Maven](http://maven.apache.org) и интерфейса командной строки Azure за считаные минуты.</span><span class="sxs-lookup"><span data-stu-id="f14d3-104">This quickstart helps you create and deploy a simple Java web app to [Azure App Service](/azure/app-service/app-service-value-prop-what-is) in just a few minutes using [Apache Maven](http://maven.apache.org) and the Azure CLI.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f14d3-105">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="f14d3-105">Before you begin</span></span>

<span data-ttu-id="f14d3-106">Прежде чем начать, настройте следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="f14d3-106">Before you start, set up the following:</span></span>

- [<span data-ttu-id="f14d3-107">Git.</span><span class="sxs-lookup"><span data-stu-id="f14d3-107">Git</span></span>](https://git-scm.com/)
- <span data-ttu-id="f14d3-108">[Java 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html);</span><span class="sxs-lookup"><span data-stu-id="f14d3-108">[Java 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html)</span></span>
- [<span data-ttu-id="f14d3-109">Maven 3</span><span class="sxs-lookup"><span data-stu-id="f14d3-109">Maven 3</span></span>](http://maven.apache.org/download.cgi)
- [<span data-ttu-id="f14d3-110">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f14d3-110">Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-az-cli2)

<span data-ttu-id="f14d3-111">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="f14d3-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="get-the-sample-code"></a><span data-ttu-id="f14d3-112">Получение кода примера</span><span class="sxs-lookup"><span data-stu-id="f14d3-112">Get the sample code</span></span>

<span data-ttu-id="f14d3-113">Клонируйте репозиторий с примером приложения на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="f14d3-113">Clone the sample app repository to your local machine.</span></span> <span data-ttu-id="f14d3-114">Пример представляет собой простое приложение JSP с дополнительной конфигурацией Maven в проекте `pom.xml` для локального тестирования приложения и развертывания примера в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="f14d3-114">The sample is a simple JSP application with additional Maven configuration in the project `pom.xml` to test the app locally and help deploy the sample to Azure App Service.</span></span>

```
git clone https://github.com/Azure-Samples/app-service-maven
```

## <a name="run-the-app-locally"></a><span data-ttu-id="f14d3-115">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="f14d3-115">Run the app locally</span></span>

<span data-ttu-id="f14d3-116">Откройте командную строку, с помощью Maven выполните сборку приложения и запустите его в локальном веб-контейнере [Tomcat](https://tomcat.apache.org).</span><span class="sxs-lookup"><span data-stu-id="f14d3-116">Open a command prompt and use Maven to build the app and run it in a local [Tomcat](https://tomcat.apache.org) web container.</span></span> 

```
cd app-service-maven
mvn package
mvn tomcat7:run-war
```

<span data-ttu-id="f14d3-117">Откройте веб-браузер и перейдите по адресу http://localhost:8080, чтобы просмотреть приложение:</span><span class="sxs-lookup"><span data-stu-id="f14d3-117">Open a web browser and navigate to http://localhost:8080 to preview the app:</span></span>

  ![Выходные данные Hello World из примера приложения Java](media/maven-quickstart/java-app-hello-world-output.png)

## <a name="log-in-to-azure"></a><span data-ttu-id="f14d3-119">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="f14d3-119">Log in to Azure</span></span>

<span data-ttu-id="f14d3-120">Войдите в интерфейс командной строки Azure с помощью команды `az login`.</span><span class="sxs-lookup"><span data-stu-id="f14d3-120">Log in to the Azure CLI with `az login`.</span></span> <span data-ttu-id="f14d3-121">В этом руководстве интерфейс командной строки используется для запроса и создания ресурсов Azure, необходимых для размещения приложения.</span><span class="sxs-lookup"><span data-stu-id="f14d3-121">This quickstart uses the CLI to query and create the Azure resources needed to host the app.</span></span>
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="f14d3-122">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="f14d3-122">Create a resource group</span></span>   

<span data-ttu-id="f14d3-123">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f14d3-123">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f14d3-124">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="f14d3-124">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

```azurecli
az group create --location "East US" --name myResourceGroup
```

<span data-ttu-id="f14d3-125">Чтобы увидеть другие доступные значения для `---location`, выполните команду [az appservice list-locations](/cli/azure/appservice#list-locations).</span><span class="sxs-lookup"><span data-stu-id="f14d3-125">To see other possible values you can use for `---location`, use [az appservice list-locations](/cli/azure/appservice#list-locations)</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="f14d3-126">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="f14d3-126">Create an App Service plan</span></span>

<span data-ttu-id="f14d3-127">Создайте **бесплатный** [план службы приложений](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview), выполнив команду [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="f14d3-127">Create a **FREE** [App Service plan](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) using [az appservice plan create](/cli/azure/appservice/plan#create).</span></span> <span data-ttu-id="f14d3-128">Планы службы приложений распределяют ресурсы, которые совместно используются всеми веб-приложениями, работающими в плане.</span><span class="sxs-lookup"><span data-stu-id="f14d3-128">App Service plans allocate resources shared across all web apps running in the plan.</span></span>


```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="f14d3-129">Когда план службы приложений будет готов, в интерфейсе командной строки Azure отобразятся следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="f14d3-129">When the App Service Plan is ready, the Azure CLI shows information similar to the following example:</span></span>

```json
{
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "location": "East US",
    "sku": {
    "capacity": 1,
    "family": "S",
    "name": "S1",
    "tier": "Standard"
    },
    "status": "Ready",
    "type": "Microsoft.Web/serverfarms"
}
```


## <a name="create-a-web-app"></a><span data-ttu-id="f14d3-130">Создание веб-приложения</span><span class="sxs-lookup"><span data-stu-id="f14d3-130">Create a web app</span></span>

<span data-ttu-id="f14d3-131">Создайте веб-приложение, использующее ресурсы плана, с помощью команды интерфейса командной строки Azure [az webapp create](/cli/azure/appservice/web#create).</span><span class="sxs-lookup"><span data-stu-id="f14d3-131">Create a web app that uses the plan's resources using the Azure CLI [az webapp create](/cli/azure/appservice/web#create) command.</span></span> <span data-ttu-id="f14d3-132">В определении веб-приложения указано место для развертывания кода и URL-адрес для доступа к приложению после его запуска.</span><span class="sxs-lookup"><span data-stu-id="f14d3-132">The web app definition provides a space to deploy the code to and a URL to access the app once it's running.</span></span>

<span data-ttu-id="f14d3-133">В приведенной ниже команде замените заполнитель <appname> уникальным именем приложения.</span><span class="sxs-lookup"><span data-stu-id="f14d3-133">In the command below substitute your own unique app name where you see the <appname> placeholder.</span></span> <span data-ttu-id="f14d3-134">В качестве узла по умолчанию для веб-приложения используется <appname>.</span><span class="sxs-lookup"><span data-stu-id="f14d3-134">The <appname> is used in the default hostname for the web app.</span></span> <span data-ttu-id="f14d3-135">Если <appname> не является уникальным, вы получите сообщение об ошибке "Веб-сайт с указанным именем уже существует".</span><span class="sxs-lookup"><span data-stu-id="f14d3-135">If <appname> is not unique, you get the friendly error message "Website with given name already exists."</span></span>

```azurecli
az webapp create --name appname --resource-group myResourceGroup --plan my-free-appservice-plan
```

<span data-ttu-id="f14d3-136">После создания веб-приложения в Azure CLI отобразятся примерно такие сведения:</span><span class="sxs-lookup"><span data-stu-id="f14d3-136">When the Web App has been created, the Azure CLI shows information similar to the following example.1</span></span>

```json
{
    "clientAffinityEnabled": true,
    "defaultHostName": "<appname>.azurewebsites.net",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<appname>",
    "isDefaultContainer": null,
    "kind": "app",
    "location": "East US",
    "name": "<app_name>",
    "repositorySiteName": "<app_name>",
    "reserved": true,
    "resourceGroup": "myResourceGroup",
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "state": "Running",
    "type": "Microsoft.Web/sites",
}
```

## <a name="configure-java-and-tomcat"></a><span data-ttu-id="f14d3-137">Настройка Java и Tomcat</span><span class="sxs-lookup"><span data-stu-id="f14d3-137">Configure Java and Tomcat</span></span>

<span data-ttu-id="f14d3-138">Выполните команду Azure CLI [az webapp config](/cli/azure/appservice/web#config), чтобы настроить веб-приложение для использования Java и Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f14d3-138">Configure the web app to use Java and Tomcat using the Azure CLI's [az webapp config](/cli/azure/appservice/web#config) command.</span></span> <span data-ttu-id="f14d3-139">Приведенный ниже пример кода настраивает в службе приложений Java 8 и [Apache Tomcat 8.5](http://tomcat.apache.org/) для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="f14d3-139">The example below configures App Service to run Java 8 and [Apache Tomcat 8.5](http://tomcat.apache.org/) to run the app.</span></span>

```azurecli
az webapp config set \ 
--name appname \
--resource-group myResourceGroup \
--java-container TOMCAT \
--java-version 1.8.0_73  \
--java-container-version 8.5
```

## <a name="configure-maven"></a><span data-ttu-id="f14d3-140">Настройка Maven</span><span class="sxs-lookup"><span data-stu-id="f14d3-140">Configure Maven</span></span> 

<span data-ttu-id="f14d3-141">Пример файла Maven `pom.xml` включает конфигурацию, которая передает пример в Azure по протоколу FTP. Но для развертывания веб-приложения это файл необходимо настроить.</span><span class="sxs-lookup"><span data-stu-id="f14d3-141">The sample's Maven `pom.xml` includes configuration to FTP the sample into Azure, but you'll need to customize it to deploy to your own web app.</span></span> <span data-ttu-id="f14d3-142">Получите учетные данные службы приложений с помощью команды [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles):</span><span class="sxs-lookup"><span data-stu-id="f14d3-142">Retreive your App Seevice credentials with [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles):</span></span>

```azurecli
az webapp deployment list-publishing-profiles  \
--name appname \ 
--resource-group myResourceGroup  \
--query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" 
```

```json
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "appname\\$appname"
  }
]
```

<span data-ttu-id="f14d3-143">Замените заполнители в файле `az-settings.xml` паролем, именем пользователя и именем узла FTP из выходных данных.</span><span class="sxs-lookup"><span data-stu-id="f14d3-143">Replace the placeholders in the `az-settings.xml` file with password, username, and FTP hostname from the output.</span></span> <span data-ttu-id="f14d3-144">В имени пользователя используйте только один символ `\` вместо экранированного значения из выходных данных интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="f14d3-144">Make sure to only use one `\` character in the username instead of the escaped value from the CLI output.</span></span>
   
```XML
...
    <server>
      <id>azure-hello-world</id>
      <username>appname\$appname</username>
      <password>aBcDeFgHiJkLmNoPqRsTuVwXyZ</password>
    </server>
...
   <configuration>
     <fromFile>${basedir}/target/AzureAppDemo-0.0.1-SNAPSHOT.war</fromFile>
     <url>ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot</url>
     <toFile>webapps/ROOT.war</toFile>
     <serverId>azure-hello-world</serverId>
   </configuration>
...
```

## <a name="deploy-the-sample-application"></a><span data-ttu-id="f14d3-145">Развертывание примера приложения</span><span class="sxs-lookup"><span data-stu-id="f14d3-145">Deploy the sample application</span></span>

<span data-ttu-id="f14d3-146">Разверните пример в Azure с помощью параметра Maven `-s` для использования конфигурации в файле `az-settings.xml`.</span><span class="sxs-lookup"><span data-stu-id="f14d3-146">Deploy with sample to Azure, using Maven's `-s` parameter to use the configuration in the `az-settings.xml` file.</span></span>

```
mvn install -s az-settings.xml
```

## <a name="browse-to-web-app"></a><span data-ttu-id="f14d3-147">Перейдите к веб-приложению</span><span class="sxs-lookup"><span data-stu-id="f14d3-147">Browse to web app</span></span>

<span data-ttu-id="f14d3-148">Просмотрите пример, запущенный в Azure:</span><span class="sxs-lookup"><span data-stu-id="f14d3-148">View the sample running in Azure:</span></span>

```azurecli
az webapp browse --name appname --resource-group myResourceGroup
```

## <a name="update-the-app"></a><span data-ttu-id="f14d3-149">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="f14d3-149">Update the app</span></span>

<span data-ttu-id="f14d3-150">В текстовом редакторе откройте файл `src/main/webapp/index.jsp` и замените существующий JSP-элемент приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="f14d3-150">Using a text editor, open `src/main/webapp/index.jsp`, and replace the existing JSP with the one below.</span></span>

```html
<%--
  Copyright (c) Microsoft Corporation. All rights reserved.
  Licensed under the MIT License. See License.txt in the project root for
  license information.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java"  import="java.util.Date" %>
<html>
<head>
  <title>Azure Samples Hello World</title>
</head>
<body>
  <H1>Hello Azure!</H1>
   Current time is: <%= new Date() %>
</body>
</html>
```

<span data-ttu-id="f14d3-151">Разверните обновление с помощью Maven:</span><span class="sxs-lookup"><span data-stu-id="f14d3-151">Deploy the update with Maven:</span></span>

```
mvn clean package
mvn install -s az-settings.xml
```

<span data-ttu-id="f14d3-152">Обновите страницу в браузере после повторного развертывания приложения, чтобы увидеть изменения.</span><span class="sxs-lookup"><span data-stu-id="f14d3-152">Refresh your browser after the app redeploys to view your changes.</span></span>

## <a name="manage-your-new-azure-app"></a><span data-ttu-id="f14d3-153">Управление новым приложением Azure</span><span class="sxs-lookup"><span data-stu-id="f14d3-153">Manage your new Azure app</span></span>

<span data-ttu-id="f14d3-154">Перейдите на портал Azure, чтобы просмотреть созданное приложение.</span><span class="sxs-lookup"><span data-stu-id="f14d3-154">Go to the Azure portal to take a look at the web app you just created.</span></span>

<span data-ttu-id="f14d3-155">Для этого войдите на портал [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f14d3-155">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="f14d3-156">В меню слева выберите **Служба приложений**, а затем щелкните имя своего веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="f14d3-156">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

 ![Выбор приложения из списка веб-приложений на портале](media/azure-app-service-portal.png)

<span data-ttu-id="f14d3-158">Протестируйте компонент мониторинга, выполнив команду `curl` в приложении, чтобы отправить трафик.</span><span class="sxs-lookup"><span data-stu-id="f14d3-158">Test the monitoring by running `curl` against the app to send some traffic.</span></span>

```bash
curl http://<appname>.azurewebsites.net/?[1-30]
```

<span data-ttu-id="f14d3-159">Через несколько минут в компоненте мониторинга отобразится действие запроса.</span><span class="sxs-lookup"><span data-stu-id="f14d3-159">You'll see the request activity in the monitoring after a couple of minutes.</span></span>

 ![Мониторинг на портале Azure](media/java-app-monitoring.png)

## <a name="clean-up-resources"></a><span data-ttu-id="f14d3-161">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="f14d3-161">Clean up resources</span></span>

<span data-ttu-id="f14d3-162">Чтобы удалить все ресурсы, созданные в этом руководстве, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f14d3-162">To remove all the resources created in this guide, run the following command:</span></span>

```azurecli
az group delete --name myResrouceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f14d3-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f14d3-163">Next steps</span></span>

<span data-ttu-id="f14d3-164">Просмотрите полный список [примеров кода Java для Azure](https://azure.microsoft.com/resources/samples/?term=java).</span><span class="sxs-lookup"><span data-stu-id="f14d3-164">Browse the full list of [Azure Java samples](https://azure.microsoft.com/resources/samples/?term=java).</span></span>