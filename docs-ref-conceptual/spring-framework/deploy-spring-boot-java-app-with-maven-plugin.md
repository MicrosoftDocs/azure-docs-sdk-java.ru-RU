---
title: Развертывание приложения Spring Boot в облаке с помощью Maven и Azure
description: Узнайте, как развернуть приложение Spring Boot в облаке с помощью подключаемого модуля Maven для веб-приложений Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.assetid: ''
ms.author: robmcm;kevinzha;brborges
ms.date: 06/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: d58cafe3456150069ec8572c101c62d1b2c29c5d
ms.sourcegitcommit: e1a5d9687e006e8bf12d11747d45cf130a2c82af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/09/2018
ms.locfileid: "42703358"
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-app-service"></a><span data-ttu-id="21cbf-103">Развертывание приложения Spring Boot в облаке с помощью подключаемого модуля Maven для Службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="21cbf-103">Deploy a Spring Boot app to the cloud using the Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="21cbf-104">В этой статье демонстрируется использование подключаемого модуля Maven для Веб-приложений Службы приложений Azure с целью развертывания примера приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="21cbf-104">This article demonstrates using the Maven Plugin for Azure App Service Web Apps to deploy a sample Spring Boot application.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="21cbf-105">[Подключаемый модуль Maven для Веб-приложений Службы приложений Azure](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) для [Apache Maven](http://maven.apache.org/) обеспечивает эффективную интеграцию Службы приложений Azure в проекты Maven и упрощает разработчикам развертывание веб-приложений в этой службе.</span><span class="sxs-lookup"><span data-stu-id="21cbf-105">The [Maven Plugin for Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>

<span data-ttu-id="21cbf-106">Прежде чем использовать подключаемый модуль Maven, проверьте центральный репозиторий Maven на наличие новой версии: [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22).</span><span class="sxs-lookup"><span data-stu-id="21cbf-106">Before using the Maven plugin, check on Maven Central for the latest available version of the plugin: [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22)</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="21cbf-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="21cbf-107">Prerequisites</span></span>

<span data-ttu-id="21cbf-108">Для работы с этим руководством требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="21cbf-108">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="21cbf-109">Подписка Azure. Если у вас ее еще нет, создайте [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="21cbf-109">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="21cbf-110">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="21cbf-110">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="21cbf-111">Актуальный [пакет разработчиков Java (JDK)] версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="21cbf-111">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="21cbf-112">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="21cbf-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="21cbf-113">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="21cbf-113">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="21cbf-114">Клонирование примера "Веб-приложение Spring Boot"</span><span class="sxs-lookup"><span data-stu-id="21cbf-114">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="21cbf-115">Из этого раздела вы узнаете, как клонировать готовое приложение Spring Boot и протестировать его на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="21cbf-115">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="21cbf-116">Откройте командную строку или окно терминала и создайте локальный каталог для размещения приложения Spring Boot, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="21cbf-116">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="21cbf-117">-- или --</span><span class="sxs-lookup"><span data-stu-id="21cbf-117">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="21cbf-118">Клонируйте образец проекта [Spring Boot Getting Started] в созданный каталог, например:</span><span class="sxs-lookup"><span data-stu-id="21cbf-118">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="21cbf-119">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="21cbf-119">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="21cbf-120">Выполните сборку файла JAR с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="21cbf-120">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="21cbf-121">При создании веб-приложения запустите веб-приложение с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="21cbf-121">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="21cbf-122">Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="21cbf-122">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="21cbf-123">Например, если имеется Curl, можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="21cbf-123">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="21cbf-124">Должно появиться следующее сообщение: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="21cbf-124">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="adjust-project-for-war-based-deployment-on-azure-app-service"></a><span data-ttu-id="21cbf-125">Настройка проекта для развертывания из WAR-файла в Службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="21cbf-125">Adjust project for WAR-based deployment on Azure App Service</span></span>

<span data-ttu-id="21cbf-126">В этом разделе мы быстро настроим развертывание проекта Spring Boot в Службе приложений Azure из WAR-файла. По умолчанию используется среда выполнения Tomcat.</span><span class="sxs-lookup"><span data-stu-id="21cbf-126">In this section we will quickly adjust the Spring Boot project to be deployed as a WAR file on Azure App Service, which provides Tomcat as the runtime by default.</span></span> <span data-ttu-id="21cbf-127">Для этого нам нужно изменить два файла:</span><span class="sxs-lookup"><span data-stu-id="21cbf-127">For this to work, there are two files to be modified:</span></span>

- <span data-ttu-id="21cbf-128">файл Maven `pom.xml`;</span><span class="sxs-lookup"><span data-stu-id="21cbf-128">The Maven `pom.xml` file</span></span>
- <span data-ttu-id="21cbf-129">класс Java `Application`.</span><span class="sxs-lookup"><span data-stu-id="21cbf-129">The `Application` Java class</span></span>

<span data-ttu-id="21cbf-130">Начнем с настроек Maven.</span><span class="sxs-lookup"><span data-stu-id="21cbf-130">Let's start with the Maven settings:</span></span>

1. <span data-ttu-id="21cbf-131">Откройте файл `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="21cbf-131">Open `pom.xml`</span></span>

1. <span data-ttu-id="21cbf-132">В начале файла сразу после определения `<artifactId>` добавьте `<packaging>war</packaging>`.</span><span class="sxs-lookup"><span data-stu-id="21cbf-132">Add `<packaging>war</packaging>` right after the `<artifactId>` definition at the top:</span></span>
   ```xml
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.springframework</groupId>
    <artifactId>gs-spring-boot</artifactId>

    <packaging>war</packaging>
   ```

1. <span data-ttu-id="21cbf-133">Добавьте следующую зависимость:</span><span class="sxs-lookup"><span data-stu-id="21cbf-133">Add the following dependency:</span></span>
   ```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
   ```

<span data-ttu-id="21cbf-134">Теперь откройте класс `Application` (будем надеяться, что интегрированная среда разработки уже считала новые зависимости) и внесите в него следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="21cbf-134">Now open the class `Application`, hopefully after your IDE has already picked up the new dependencies, and proceed with the following modifications:</span></span>

1. <span data-ttu-id="21cbf-135">Сделайте класс Application подклассом `SpringBootServletInitializer`.</span><span class="sxs-lookup"><span data-stu-id="21cbf-135">Make class Application a subclass of `SpringBootServletInitializer`:</span></span>
   ```java
   @SpringBootApplication
   public class Application extends SpringBootServletInitializer {
     // ...
   }
   ```

1. <span data-ttu-id="21cbf-136">Добавьте в класс Application следующий метод:</span><span class="sxs-lookup"><span data-stu-id="21cbf-136">Add the following method to the Application class:</span></span>
   ```java
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
           return application.sources(Application.class);
       }
   ```

<span data-ttu-id="21cbf-137">Теперь ваше приложение готово к развертыванию в Tomcat или любой другой среде выполнения сервлетов (например, Jetty).</span><span class="sxs-lookup"><span data-stu-id="21cbf-137">Your application is now ready to be deployed to Tomcat and any other Servlet runtime (e.g. Jetty).</span></span>

## <a name="add-the-maven-plugin-for-azure-app-service-web-apps"></a><span data-ttu-id="21cbf-138">Добавление подключаемого модуля Maven для Веб-приложений Службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="21cbf-138">Add the Maven Plugin for Azure App Service Web Apps</span></span>

<span data-ttu-id="21cbf-139">В этом разделе мы добавим подключаемый модуль Maven, который автоматизирует весь процесс развертывания этого приложения в Веб-приложения Службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="21cbf-139">In this section, we will add a Maven plugin that will automate the entire deployment of this application into Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="21cbf-140">Откройте файл `pom.xml` еще раз.</span><span class="sxs-lookup"><span data-stu-id="21cbf-140">Open `pom.xml` once again.</span></span>

1. <span data-ttu-id="21cbf-141">В элементе `<properties>` укажите настраиваемый формат метки времени, используя свойство `maven.build.timestamp.format`.</span><span class="sxs-lookup"><span data-stu-id="21cbf-141">Inside `<properties>`, set a custom timestamp format with the property `maven.build.timestamp.format`.</span></span> <span data-ttu-id="21cbf-142">Так как Служба приложений Azure создает для вашего приложения общедоступный URL-адрес, этот параметр будет использоваться для создания имени развертывания, что позволит избежать конфликтов с развертываниями других пользователей.</span><span class="sxs-lookup"><span data-stu-id="21cbf-142">Because Azure App Service creates a public URL for your application, this setting will be used to generate the name of your deployment, and avoid conflict with other users' live deployments.</span></span>
   ```xml
    <properties>
        <java.version>1.8</java.version>
        <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
    </properties>
   ```

1. <span data-ttu-id="21cbf-143">В элементе `<plugins>` добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="21cbf-143">In the `<plugins>` element, add the following:</span></span>
   ```xml
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
    </plugin>
   ```

<span data-ttu-id="21cbf-144">С такими параметрами проект Maven можно развертывать в Веб-приложениях Службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="21cbf-144">With these settings, your Maven project is now ready for live deployment to Azure App Service Web App.</span></span>

## <a name="install-and-log-in-to-azure-cli"></a><span data-ttu-id="21cbf-145">Установка и вход в Azure CLI</span><span class="sxs-lookup"><span data-stu-id="21cbf-145">Install and log in to Azure CLI</span></span>

<span data-ttu-id="21cbf-146">[Azure CLI](https://docs.microsoft.com/cli/azure/) — самый простой и наиболее удобный способ развернуть приложение Spring Boot с помощью подключаемого модуля Maven.</span><span class="sxs-lookup"><span data-stu-id="21cbf-146">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](https://docs.microsoft.com/cli/azure/).</span></span> <span data-ttu-id="21cbf-147">Установите этот компонент.</span><span class="sxs-lookup"><span data-stu-id="21cbf-147">Make sure you have it installed.</span></span>

1. <span data-ttu-id="21cbf-148">Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="21cbf-148">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
   <span data-ttu-id="21cbf-149">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="21cbf-149">Follow the instructions to complete the sign-in process.</span></span>

## <a name="optionally-customize-pomxml-before-deploying"></a><span data-ttu-id="21cbf-150">Настройка файла pom.xml перед развертыванием (необязательный этап)</span><span class="sxs-lookup"><span data-stu-id="21cbf-150">Optionally, customize pom.xml before deploying</span></span>

<span data-ttu-id="21cbf-151">Откройте файл `pom.xml` для приложения Spring Boot в текстовом редакторе, а затем найдите элемент `<plugin>` для `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="21cbf-151">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="21cbf-152">Этот элемент должен выглядеть примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="21cbf-152">This element should resemble the following example:</span></span>

   ```xml
  <plugins>
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
      <configuration>
         <resourceGroup>maven-projects</resourceGroup>
         <appName>${project.artifactId}-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>war</deploymentType>
      </configuration>
    </plugin>
  </plugins>
   ```

<span data-ttu-id="21cbf-153">Существует несколько значений, которые можно изменить для подключаемого модуля Maven. Подробное описание каждого из этих элементов см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="21cbf-153">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="21cbf-154">Существует ряд значений, на которые следует обратить внимание в этой статье.</span><span class="sxs-lookup"><span data-stu-id="21cbf-154">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="21cbf-155">Элемент</span><span class="sxs-lookup"><span data-stu-id="21cbf-155">Element</span></span> | <span data-ttu-id="21cbf-156">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="21cbf-156">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="21cbf-157">Версия [Подключаемый модуль Maven для веб-приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="21cbf-157">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="21cbf-158">Чтобы убедиться, что вы используете актуальную версию, проверьте, какая версия указана в списке версий в [центральном репозитории Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22).</span><span class="sxs-lookup"><span data-stu-id="21cbf-158">Verify the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="21cbf-159">Целевая группа ресурсов, которой в этом примере является `maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="21cbf-159">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="21cbf-160">Если эта группа ресурсов не существует, она создается во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="21cbf-160">The resource group is created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="21cbf-161">Целевое имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="21cbf-161">Specifies the target name for your web app.</span></span> <span data-ttu-id="21cbf-162">В этом примере целевое имя — `maven-web-app-${maven.build.timestamp}`, к которому в этом примере добавлен суффикс `${maven.build.timestamp}`, чтобы избежать конфликтов.</span><span class="sxs-lookup"><span data-stu-id="21cbf-162">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="21cbf-163">(Метку времени добавлять необязательно; можно указать любую уникальную строку для имени приложения.)</span><span class="sxs-lookup"><span data-stu-id="21cbf-163">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="21cbf-164">Целевой регион, которым в данном примере является `westus`.</span><span class="sxs-lookup"><span data-stu-id="21cbf-164">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="21cbf-165">(Полный список см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].)</span><span class="sxs-lookup"><span data-stu-id="21cbf-165">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<javaVersion>` | <span data-ttu-id="21cbf-166">Версия среды выполнения Java для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="21cbf-166">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="21cbf-167">(Полный список см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].)</span><span class="sxs-lookup"><span data-stu-id="21cbf-167">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<deploymentType>` | <span data-ttu-id="21cbf-168">Тип развертывания для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="21cbf-168">Specifies deployment type for your web app.</span></span> <span data-ttu-id="21cbf-169">Значение по умолчанию — `war`.</span><span class="sxs-lookup"><span data-stu-id="21cbf-169">Default is `war`.</span></span> |

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="21cbf-170">Сборка и развертывание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="21cbf-170">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="21cbf-171">После настройки всех параметров в предыдущих разделах этой статьи можно приступать к развертыванию веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="21cbf-171">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="21cbf-172">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="21cbf-172">To do so, use the following steps:</span></span>

1. <span data-ttu-id="21cbf-173">В командной строке или в окне терминала, которые вы использовали ранее, перестройте JAR-файл, используя Maven, если вы внесли изменения в файл *pom.xml*; например:</span><span class="sxs-lookup"><span data-stu-id="21cbf-173">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="21cbf-174">Разверните веб-приложение в Azure с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="21cbf-174">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="21cbf-175">Maven выполнит развертывание веб-приложения в Azure; если веб-приложение еще не существует, оно будет создано.</span><span class="sxs-lookup"><span data-stu-id="21cbf-175">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="21cbf-176">После развертывания веб-приложения вы сможете управлять им с помощью [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="21cbf-176">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="21cbf-177">Веб-приложение будет указано в разделе **Службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="21cbf-177">Your web app will be listed in **App Services**:</span></span>

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* <span data-ttu-id="21cbf-179">URL-адрес веб-приложения будет указан в разделе **Обзор** для вашего веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="21cbf-179">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Определение URL-адреса для веб-приложения][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="21cbf-181">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="21cbf-181">Next steps</span></span>

<span data-ttu-id="21cbf-182">Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="21cbf-182">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="21cbf-183">[Подключаемый модуль Maven для веб-приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="21cbf-183">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="21cbf-184">Вход в Azure из интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="21cbf-184">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="21cbf-185">Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="21cbf-185">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="21cbf-186">Создание субъекта-службы Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="21cbf-186">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="21cbf-187">Справочник по параметрам Maven</span><span class="sxs-lookup"><span data-stu-id="21cbf-187">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[портал Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Подключаемый модуль Maven для веб-приложений Azure]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme
[Maven Plugin for Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
