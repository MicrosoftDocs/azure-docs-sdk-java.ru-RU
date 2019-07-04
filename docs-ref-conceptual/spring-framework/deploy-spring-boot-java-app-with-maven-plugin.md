---
title: Развертывание приложения Spring Boot в виде файла JAR в облаке с помощью Maven и Azure
description: Узнайте, как развернуть приложение Spring Boot в облаке с помощью подключаемого модуля Maven для веб-приложений Azure на платформе Linux.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: brborges
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: b133290d1f14429cbf36d6ed5a67d27e1a637593
ms.sourcegitcommit: 599405a9ce892d75073ef0776befa2fa22407b4c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/19/2019
ms.locfileid: "67237599"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a><span data-ttu-id="c66b5-103">Развертывание веб-приложения Spring Boot в виде файла JAR в Службе приложений Azure на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="c66b5-103">Deploy a Spring Boot JAR file web app to Azure App Service on Linux</span></span>

<span data-ttu-id="c66b5-104">В этой статье показано, как использовать [подключаемый модуль Maven для веб-приложений службы приложений Azure](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme), чтобы развернуть приложение Spring Boot, упакованное в виде файла JAR Java SE, в [Службе приложений Azure на платформе Linux](/azure/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="c66b5-104">This article demonstrates using the [Maven Plugin for Azure App Service Web Apps](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) to deploy a Spring Boot application packaged as a Java SE JAR to [Azure App Service on Linux](/azure/app-service/containers/).</span></span> <span data-ttu-id="c66b5-105">Развертывание Java SE является предпочтительным по сравнению с [Tomcat и файлами WAR](/azure/app-service/containers/quickstart-java) в тех случаях, когда нужно объединить зависимости, среду выполнения и файлы конфигурации приложения в единый артефакт, пригодный для развертывания.</span><span class="sxs-lookup"><span data-stu-id="c66b5-105">Choose Java SE deployment over [Tomcat and WAR files](/azure/app-service/containers/quickstart-java) when you want to consolidate your app's dependencies, runtime, and configuration into a single deployable artifact.</span></span>


<span data-ttu-id="c66b5-106">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="c66b5-106">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c66b5-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c66b5-107">Prerequisites</span></span>

<span data-ttu-id="c66b5-108">Для выполнения шагов, описанных в этом руководстве, вам понадобиться установить и настроить следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="c66b5-108">To complete the steps in this tutorial, you'll need to have the following installed and configured:</span></span>

* <span data-ttu-id="c66b5-109">[Azure CLI](/cli/azure/) на локальном компьютере или в [Azure Cloud Shell](https://shell.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c66b5-109">The [Azure CLI](/cli/azure/), either locally or through [Azure Cloud Shell](https://shell.azure.com).</span></span>
* <span data-ttu-id="c66b5-110">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="c66b5-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="c66b5-111">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="c66b5-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="c66b5-112">Apache [Maven](https://maven.apache.org/) версии 3.</span><span class="sxs-lookup"><span data-stu-id="c66b5-112">Apache's [Maven](https://maven.apache.org/), Version 3).</span></span>
* <span data-ttu-id="c66b5-113">Клиент [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="c66b5-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="install-and-sign-in-to-azure-cli"></a><span data-ttu-id="c66b5-114">Установка и вход в Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c66b5-114">Install and sign in to Azure CLI</span></span>

<span data-ttu-id="c66b5-115">[Azure CLI](/cli/azure/) — самый простой и наиболее удобный способ развернуть приложение Spring Boot с помощью подключаемого модуля Maven.</span><span class="sxs-lookup"><span data-stu-id="c66b5-115">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](/cli/azure/).</span></span>

<span data-ttu-id="c66b5-116">Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="c66b5-116">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
<span data-ttu-id="c66b5-117">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="c66b5-117">Follow the instructions to complete the sign-in process.</span></span>

## <a name="clone-the-sample-app"></a><span data-ttu-id="c66b5-118">Клонирования примера приложения</span><span class="sxs-lookup"><span data-stu-id="c66b5-118">Clone the sample app</span></span>

<span data-ttu-id="c66b5-119">Из этого раздела вы узнаете, как клонировать готовое приложение Spring Boot и протестировать его на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="c66b5-119">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="c66b5-120">Откройте командную строку или окно терминала и создайте локальный каталог для размещения приложения Spring Boot, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="c66b5-120">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="c66b5-121">-- или --</span><span class="sxs-lookup"><span data-stu-id="c66b5-121">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="c66b5-122">Клонируйте образец проекта [Spring Boot Getting Started] в созданный каталог, например:</span><span class="sxs-lookup"><span data-stu-id="c66b5-122">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="c66b5-123">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="c66b5-123">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="c66b5-124">Выполните сборку файла JAR с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="c66b5-124">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c66b5-125">При создании веб-приложения запустите веб-приложение с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="c66b5-125">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="c66b5-126">Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="c66b5-126">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="c66b5-127">Например, если имеется Curl, можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c66b5-127">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="c66b5-128">Должно появиться следующее сообщение: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="c66b5-128">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="configure-maven-plugin-for-azure-app-service"></a><span data-ttu-id="c66b5-129">Настройка подключаемого модуля Maven для Службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="c66b5-129">Configure Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="c66b5-130">В этом разделе вы настроите проект Spring Boot `pom.xml`, чтобы развернуть приложение в Службе приложений Azure на платформе Linux с помощью Maven.</span><span class="sxs-lookup"><span data-stu-id="c66b5-130">In this section, you will configure the Spring Boot project `pom.xml` so that Maven can deploy the app to Azure App Service on Linux.</span></span>

1. <span data-ttu-id="c66b5-131">Откройте файл `pom.xml` в редакторе кода.</span><span class="sxs-lookup"><span data-stu-id="c66b5-131">Open `pom.xml` in a code editor.</span></span>

2. <span data-ttu-id="c66b5-132">В разделе `<build>` файла pom.xml добавьте следующую запись `<plugin>` внутри тега `<plugins>`.</span><span class="sxs-lookup"><span data-stu-id="c66b5-132">In the `<build>` section of the pom.xml, add the following `<plugin>` entry inside the `<plugins>` tag.</span></span>

   ```xml
   <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.6.0</version>
   </plugin>
   ```

3. <span data-ttu-id="c66b5-133">Затем можно настроить развертывание, выполнить в командной строке команду Maven `mvn azure-webapp:config` и с помощью **number** выбрать параметры в командной строке:</span><span class="sxs-lookup"><span data-stu-id="c66b5-133">Then you can configure the deployment, run the maven command `mvn azure-webapp:config` in the Command Prompt and use the **number** to choose these options in the prompt:</span></span>
    * <span data-ttu-id="c66b5-134">**OS**: linux;</span><span class="sxs-lookup"><span data-stu-id="c66b5-134">**OS**: linux</span></span>  
    * <span data-ttu-id="c66b5-135">**javaVersion**: jre8;</span><span class="sxs-lookup"><span data-stu-id="c66b5-135">**javaVersion**: jre8</span></span>
    * <span data-ttu-id="c66b5-136">**runtimeStack**: jre8.</span><span class="sxs-lookup"><span data-stu-id="c66b5-136">**runtimeStack**: jre8</span></span>

<span data-ttu-id="c66b5-137">Если вы получите запрос **Confirm (Y/N)** , нажмите клавишу **y** для подтверждения. Настройка завершена.</span><span class="sxs-lookup"><span data-stu-id="c66b5-137">When you get the **Confirm (Y/N)** prompt, press **'y'** and the configuration is done.</span></span>

```cmd
~@Azure:~/gs-spring-boot/complete$ mvn azure-webapp:config
[INFO] Scanning for projects...
[INFO]
[INFO] -----------------< org.springframework:gs-spring-boot >-----------------
[INFO] Building gs-spring-boot 0.1.0
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- azure-webapp-maven-plugin:1.6.0:config (default-cli) @ gs-spring-boot ---
[WARNING] The plugin may not work if you change the os of an existing webapp.
Define value for OS(Default: Linux):
1. linux [*]
2. windows
3. docker
Enter index to use:
Define value for javaVersion(Default: jre8):
1. jre8 [*]
2. java11
Enter index to use:
Define value for runtimeStack(Default: TOMCAT 8.5):
1. TOMCAT 9.0
2. jre8
3. TOMCAT 8.5 [*]
4. WILDFLY 14
Enter index to use: 2
Please confirm webapp properties
AppName : gs-spring-boot-1559091271202
ResourceGroup : gs-spring-boot-1559091271202-rg
Region : westeurope
PricingTier : Premium_P1V2
OS : Linux
RuntimeStack : JAVA 8-jre8
Deploy to slot : false
Confirm (Y/N)? : Y
```

4. <span data-ttu-id="c66b5-138">Добавьте раздел `<appSettings>` в раздел `<configuration>` в `<azure-webapp-maven-plugin>` для прослушивания порта *80*.</span><span class="sxs-lookup"><span data-stu-id="c66b5-138">Add the `<appSettings>` section to the `<configuration>` section of `<azure-webapp-maven-plugin>` to listen on the *80* port.</span></span>

    ```xml
   <plugin>
       <groupId>com.microsoft.azure</groupId>
       <artifactId>azure-webapp-maven-plugin</artifactId>
       <version>1.6.0</version>
       <configuration>
          <schemaVersion>V2</schemaVersion>
          <resourceGroup>gs-spring-boot-1559091271202-rg</resourceGroup>
          <appName>gs-spring-boot-1559091271202</appName>
          <region>westeurope</region>
          <pricingTier>P1V2</pricingTier>

          <!-- Begin of App Settings  -->
          <appSettings>
             <property>
                   <name>JAVA_OPTS</name>
                   <value>-Dserver.port=80</value>
             </property>
          </appSettings>
          <!-- End of App Settings  -->
          ...
         </configuration>
   </plugin>
   ```

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="c66b5-139">Развертывание приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="c66b5-139">Deploy the app to Azure</span></span>

<span data-ttu-id="c66b5-140">После настройки всех параметров в предыдущих разделах этой статьи можно приступать к развертыванию веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="c66b5-140">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="c66b5-141">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c66b5-141">To do so, use the following steps:</span></span>

1. <span data-ttu-id="c66b5-142">В командной строке или в окне терминала, которые вы использовали ранее, перестройте JAR-файл, используя Maven, если вы внесли изменения в файл *pom.xml*; например:</span><span class="sxs-lookup"><span data-stu-id="c66b5-142">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c66b5-143">Разверните веб-приложение в Azure с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="c66b5-143">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="c66b5-144">Maven развернет веб-приложение в Azure. Если веб-приложение или план службы приложений отсутствуют, они будут созданы.</span><span class="sxs-lookup"><span data-stu-id="c66b5-144">Maven will deploy your web app to Azure; if the web app or web app plan does not already exist, it will be created for you.</span></span>

<span data-ttu-id="c66b5-145">После развертывания веб-приложения вы сможете управлять им с помощью [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="c66b5-145">When your web has been deployed, you will be able to manage it through the [Azure portal].</span></span>

* <span data-ttu-id="c66b5-146">Веб-приложение будет указано в разделе **Службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="c66b5-146">Your web app will be listed in **App Services**:</span></span>

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* <span data-ttu-id="c66b5-148">URL-адрес веб-приложения будет указан в разделе **Обзор** для вашего веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="c66b5-148">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Определение URL-адреса для веб-приложения][AP02]

<span data-ttu-id="c66b5-150">Убедитесь, что развертывание прошло успешно, воспользовавшись описанной выше командой cURL. При этом вместо `localhost` введите URL-адрес веб-приложения, указанный на портале.</span><span class="sxs-lookup"><span data-stu-id="c66b5-150">Verify that the deployment was successful by using the same cURL command as before, using your web app URL from the Portal instead of `localhost`.</span></span> <span data-ttu-id="c66b5-151">Должно появиться следующее сообщение: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="c66b5-151">You should see the following message displayed: **Greetings from Spring Boot!**</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c66b5-152">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="c66b5-152">Next steps</span></span>

<span data-ttu-id="c66b5-153">Дополнительные сведения о Spring и Azure см. в центре документации об использовании Spring в Azure.</span><span class="sxs-lookup"><span data-stu-id="c66b5-153">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c66b5-154">Spring в Azure</span><span class="sxs-lookup"><span data-stu-id="c66b5-154">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="c66b5-155">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c66b5-155">Additional Resources</span></span>

<span data-ttu-id="c66b5-156">Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="c66b5-156">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="c66b5-157">[Подключаемый модуль Maven для веб-приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="c66b5-157">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="c66b5-158">Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="c66b5-158">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="c66b5-159">Создание субъекта-службы Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c66b5-159">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="c66b5-160">Справочник по параметрам Maven</span><span class="sxs-lookup"><span data-stu-id="c66b5-160">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: /java/azure/
[портал Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Подключаемый модуль Maven для веб-приложений Azure]: /java/api/overview/azure/maven/azure-webapp-maven-plugin/readme
[Maven Plugin for Azure Web Apps]: /java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
