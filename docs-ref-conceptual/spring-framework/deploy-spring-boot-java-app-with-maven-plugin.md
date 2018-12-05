---
title: Развертывание приложения Spring Boot в виде файла JAR в облаке с помощью Maven и Azure
description: Узнайте, как развернуть приложение Spring Boot в облаке с помощью подключаемого модуля Maven для веб-приложений Azure на платформе Linux.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: brborges
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: 066ac30697c6adccc0c6a7b9d57205de488bdc53
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339008"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a><span data-ttu-id="680aa-103">Развертывание веб-приложения Spring Boot в виде файла JAR в Службе приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="680aa-103">Deploy a Spring Boot JAR file web app to Azure App Service on Linux</span></span>

<span data-ttu-id="680aa-104">В этой статье показано, как использовать [подключаемый модуль Maven для веб-приложений службы приложений Azure](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme), чтобы развернуть приложение Spring Boot, упакованное в виде файла JAR Java SE, в [Службе приложений Azure на платформе Linux](https://docs.microsoft.com/en-us/azure/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="680aa-104">This article demonstrates using the [Maven Plugin for Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) to deploy a Spring Boot application packaged as a Java SE JAR to [Azure App Service on Linux](https://docs.microsoft.com/en-us/azure/app-service/containers/).</span></span> <span data-ttu-id="680aa-105">Развертывание Java SE является предпочтительным по сравнению с [Tomcat и файлами WAR](/azure/app-service/containers/quickstart-java) в тех случаях, когда нужно объединить зависимости, среду выполнения и файлы конфигурации приложения в единый артефакт, пригодный для развертывания.</span><span class="sxs-lookup"><span data-stu-id="680aa-105">Choose Java SE deployment over [Tomcat and WAR files](/azure/app-service/containers/quickstart-java) when you want to consolidate your app's dependencies, runtime, and configuration into a single deployable artifact.</span></span>


<span data-ttu-id="680aa-106">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="680aa-106">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="680aa-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="680aa-107">Prerequisites</span></span>

<span data-ttu-id="680aa-108">Для выполнения шагов, описанных в этом руководстве, вам понадобиться установить и настроить следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="680aa-108">To complete the steps in this tutorial, you'll need to have the following installed and configured:</span></span>

* <span data-ttu-id="680aa-109">[Azure CLI](/cli/azure/) на локальном компьютере или в [Azure Cloud Shell](https://shell.azure.com).</span><span class="sxs-lookup"><span data-stu-id="680aa-109">The [Azure CLI](/cli/azure/), either locally or through [Azure Cloud Shell](https://shell.azure.com).</span></span>
* <span data-ttu-id="680aa-110">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="680aa-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="680aa-111">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="680aa-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="680aa-112">Apache [Maven](https://maven.apache.org/) версии 3.</span><span class="sxs-lookup"><span data-stu-id="680aa-112">Apache's [Maven](https://maven.apache.org/), Version 3).</span></span>
* <span data-ttu-id="680aa-113">Клиент [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="680aa-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="install-and-sign-in-to-azure-cli"></a><span data-ttu-id="680aa-114">Установка и вход в Azure CLI</span><span class="sxs-lookup"><span data-stu-id="680aa-114">Install and sign in to Azure CLI</span></span>

<span data-ttu-id="680aa-115">[Azure CLI](https://docs.microsoft.com/cli/azure/) — самый простой и наиболее удобный способ развернуть приложение Spring Boot с помощью подключаемого модуля Maven.</span><span class="sxs-lookup"><span data-stu-id="680aa-115">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](https://docs.microsoft.com/cli/azure/).</span></span>

<span data-ttu-id="680aa-116">Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="680aa-116">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
<span data-ttu-id="680aa-117">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="680aa-117">Follow the instructions to complete the sign-in process.</span></span>

## <a name="clone-the-sample-app"></a><span data-ttu-id="680aa-118">Клонирования примера приложения</span><span class="sxs-lookup"><span data-stu-id="680aa-118">Clone the sample app</span></span>

<span data-ttu-id="680aa-119">Из этого раздела вы узнаете, как клонировать готовое приложение Spring Boot и протестировать его на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="680aa-119">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="680aa-120">Откройте командную строку или окно терминала и создайте локальный каталог для размещения приложения Spring Boot, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="680aa-120">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="680aa-121">-- или --</span><span class="sxs-lookup"><span data-stu-id="680aa-121">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="680aa-122">Клонируйте образец проекта [Spring Boot Getting Started] в созданный каталог, например:</span><span class="sxs-lookup"><span data-stu-id="680aa-122">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="680aa-123">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="680aa-123">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="680aa-124">Выполните сборку файла JAR с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="680aa-124">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="680aa-125">При создании веб-приложения запустите веб-приложение с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="680aa-125">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="680aa-126">Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="680aa-126">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="680aa-127">Например, если имеется Curl, можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="680aa-127">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="680aa-128">Должно появиться следующее сообщение: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="680aa-128">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="configure-maven-plugin-for-azure-app-service"></a><span data-ttu-id="680aa-129">Настройка подключаемого модуля Maven для Службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="680aa-129">Configure Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="680aa-130">В этом разделе вы настроите проект Spring Boot `pom.xml`, чтобы развернуть приложение в Службе приложений Azure на платформе Linux с помощью Maven.</span><span class="sxs-lookup"><span data-stu-id="680aa-130">In this section, you will configure the Spring Boot project `pom.xml` so that Maven can deploy the app to Azure App Service on Linux.</span></span>

1. <span data-ttu-id="680aa-131">Откройте файл `pom.xml` в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="680aa-131">Open `pom.xml` in a code editor.</span></span>

2. <span data-ttu-id="680aa-132">В разделе `<build>` файла pom.xml добавьте следующую запись `<plugin>` внутри тега `<plugins>`.</span><span class="sxs-lookup"><span data-stu-id="680aa-132">In the `<build>` section of the pom.xml, add the following `<plugin>` entry inside the `<plugins>` tag.</span></span>

   ```xml
   <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.4.0</version>
    <configuration>
      <deploymentType>jar</deploymentType>

      <!-- configure app to run on port 80, required by App Service -->
      <appSettings>
        <property> 
          <name>JAVA_OPTS</name> 
          <value>-Dserver.port=80</value> 
        </property> 
      </appSettings>

      <!-- Web App information -->
      <resourceGroup>${RESOURCEGROUP_NAME}</resourceGroup>
      <appName>${WEBAPP_NAME}</appName>
      <region>${REGION}</region>  

      <!-- Java Runtime Stack for Web App on Linux-->
      <linuxRuntime>jre8</linuxRuntime>
    </configuration>
   </plugin>
   ```

3. <span data-ttu-id="680aa-133">Укажите нужные значения вместо следующих заполнителей в конфигурации подключаемого модуля:</span><span class="sxs-lookup"><span data-stu-id="680aa-133">Update the following placeholders in the plugin configuration:</span></span>

| <span data-ttu-id="680aa-134">Placeholder</span><span class="sxs-lookup"><span data-stu-id="680aa-134">Placeholder</span></span> | <span data-ttu-id="680aa-135">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="680aa-135">Description</span></span> |
| ----------- | ----------- |
| `RESOURCEGROUP_NAME` | <span data-ttu-id="680aa-136">Имя новой группы ресурсов, в которой создается веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="680aa-136">Name for the new resource group in which to create your web app.</span></span> <span data-ttu-id="680aa-137">Поместив все ресурсы для приложения в группу, вы можете управлять ими совместно.</span><span class="sxs-lookup"><span data-stu-id="680aa-137">By putting all the resources for an app in a group, you can manage them together.</span></span> <span data-ttu-id="680aa-138">Например, при удалении группы ресурсов все ресурсы, связанные с приложением, также удаляются.</span><span class="sxs-lookup"><span data-stu-id="680aa-138">For example, deleting the resource group would delete all resources associated with the app.</span></span> <span data-ttu-id="680aa-139">Укажите вместо этого значения уникальное имя новой группы ресурсов, например *TestResources*.</span><span class="sxs-lookup"><span data-stu-id="680aa-139">Update this value with a unique new resource group name, for example, *TestResources*.</span></span> <span data-ttu-id="680aa-140">Это имя группы ресурсов будет использоваться для удаления всех ресурсов Azure в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="680aa-140">You will use this resource group name to clean up all Azure resources in a later section.</span></span> |
| `WEBAPP_NAME` | <span data-ttu-id="680aa-141">Имя приложения будет частью имени узла для веб-приложения, которое будет развернуто в Azure (WEBAPP_NAME.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="680aa-141">The app name will be part the host name for the web app when deployed to Azure (WEBAPP_NAME.azurewebsites.net).</span></span> <span data-ttu-id="680aa-142">Измените значение этого параметра на уникальное имя нового веб-приложения Azure, в котором будет размещено ваше приложение Java, например *contoso*.</span><span class="sxs-lookup"><span data-stu-id="680aa-142">Update this value with a unique name for the new Azure web app, which will host your Java app, for example *contoso*.</span></span> |
| `REGION` | <span data-ttu-id="680aa-143">Регион Azure, в котором размещено веб-приложение, например `westus2`.</span><span class="sxs-lookup"><span data-stu-id="680aa-143">An Azure region where the web app is hosted, for example `westus2`.</span></span> <span data-ttu-id="680aa-144">Список регионов можно получить из Cloud Shell или CLI с помощью команды `az account list-locations`.</span><span class="sxs-lookup"><span data-stu-id="680aa-144">You can get a list of regions from the Cloud Shell or CLI using the `az account list-locations` command.</span></span> |

<span data-ttu-id="680aa-145">Полный список параметров конфигурации см. в [справочном руководстве по подключаемому модулю Maven на сайте GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).</span><span class="sxs-lookup"><span data-stu-id="680aa-145">A full list of configuration options can be found in the [Maven plugin reference on GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).</span></span>

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="680aa-146">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="680aa-146">Deploy the app to Azure</span></span>

<span data-ttu-id="680aa-147">После настройки всех параметров в предыдущих разделах этой статьи можно приступать к развертыванию веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="680aa-147">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="680aa-148">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="680aa-148">To do so, use the following steps:</span></span>

1. <span data-ttu-id="680aa-149">В командной строке или в окне терминала, которые вы использовали ранее, перестройте JAR-файл, используя Maven, если вы внесли изменения в файл *pom.xml*; например:</span><span class="sxs-lookup"><span data-stu-id="680aa-149">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="680aa-150">Разверните веб-приложение в Azure с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="680aa-150">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="680aa-151">Maven развернет веб-приложение в Azure. Если веб-приложение или план службы приложений отсутствуют, они будут созданы.</span><span class="sxs-lookup"><span data-stu-id="680aa-151">Maven will deploy your web app to Azure; if the web app or web app plan does not already exist, it will be created for you.</span></span>

<span data-ttu-id="680aa-152">После развертывания веб-приложения вы сможете управлять им с помощью [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="680aa-152">When your web has been deployed, you will be able to manage it through the [Azure portal].</span></span>

* <span data-ttu-id="680aa-153">Веб-приложение будет указано в разделе **Службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="680aa-153">Your web app will be listed in **App Services**:</span></span>

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* <span data-ttu-id="680aa-155">URL-адрес веб-приложения будет указан в разделе **Обзор** для вашего веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="680aa-155">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Определение URL-адреса для веб-приложения][AP02]

<span data-ttu-id="680aa-157">Убедитесь, что развертывание прошло успешно, воспользовавшись описанной выше командой cURL. При этом вместо `localhost` введите URL-адрес веб-приложения, указанный на портале.</span><span class="sxs-lookup"><span data-stu-id="680aa-157">Verify that the deployment was successful by using the same cURL command as before, using your web app URL from the Portal instead of `localhost`.</span></span> <span data-ttu-id="680aa-158">Должно появиться следующее сообщение: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="680aa-158">You should see the following message displayed: **Greetings from Spring Boot!**</span></span> 

## <a name="next-steps"></a><span data-ttu-id="680aa-159">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="680aa-159">Next steps</span></span>

<span data-ttu-id="680aa-160">Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="680aa-160">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="680aa-161">[Подключаемый модуль Maven для веб-приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="680aa-161">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="680aa-162">Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="680aa-162">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="680aa-163">Создание субъекта-службы Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="680aa-163">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="680aa-164">Справочник по параметрам Maven</span><span class="sxs-lookup"><span data-stu-id="680aa-164">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[портал Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Подключаемый модуль Maven для веб-приложений Azure]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme
[Maven Plugin for Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
