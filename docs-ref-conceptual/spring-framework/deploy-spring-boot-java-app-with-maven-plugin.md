---
title: "Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure"
description: "Сведения о развертываний приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Maven
ms.assetid: 
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 32781b3ee923f4d64d4e1a11df73f077281eee40
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-to-azure"></a><span data-ttu-id="bb9a1-104">Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="bb9a1-104">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure</span></span>

<span data-ttu-id="bb9a1-105">[Подключаемый модуль Maven для веб-приложений Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) для [Apache Maven](http://maven.apache.org/) обеспечивает эффективную интеграцию службы приложений Azure в проекты Maven и упрощает процесс развертывания веб-приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-105">The [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>

<span data-ttu-id="bb9a1-106">В этой статье демонстрируется использование подключаемого модуля Maven для веб-приложений Azure с целью развертывания примера приложения Spring Boot в службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-106">This article demonstrates using the Maven Plugin for Azure Web Apps to deploy a sample Spring Boot application to Azure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="bb9a1-107">Подключаемый модуль Maven для веб-приложений Azure в настоящее время доступен в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-107">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="bb9a1-108">Сейчас поддерживается только FTP-публикация, но на будущее запланированы дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-108">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="bb9a1-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bb9a1-109">Prerequisites</span></span>

<span data-ttu-id="bb9a1-110">Для работы с этим руководством требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-110">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="bb9a1-111">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="bb9a1-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="bb9a1-112">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="bb9a1-112">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="bb9a1-113">Актуальный [пакет разработчиков Java (JDK)] версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="bb9a1-114">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="bb9a1-115">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="bb9a1-115">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="bb9a1-116">Клонирование примера "Веб-приложение Spring Boot"</span><span class="sxs-lookup"><span data-stu-id="bb9a1-116">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="bb9a1-117">В этом разделе представлены сведения о клонировании готового приложения Spring Boot и его тестировании на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-117">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="bb9a1-118">Откройте командную строку или окно терминала и создайте локальный каталог для размещения приложения Spring Boot, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="bb9a1-118">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="bb9a1-119">-- или --</span><span class="sxs-lookup"><span data-stu-id="bb9a1-119">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="bb9a1-120">Клонируйте образец проекта [Spring Boot Getting Started] в созданный каталог, например:</span><span class="sxs-lookup"><span data-stu-id="bb9a1-120">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="bb9a1-121">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="bb9a1-121">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="bb9a1-122">Выполните сборку файла JAR с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="bb9a1-122">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="bb9a1-123">При создании веб-приложения запустите веб-приложение с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="bb9a1-123">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="bb9a1-124">Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-124">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="bb9a1-125">Например, если имеется Curl, можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bb9a1-125">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="bb9a1-126">Должно появиться следующее сообщение: **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="bb9a1-126">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="bb9a1-127">Создание субъекта-службы Azure</span><span class="sxs-lookup"><span data-stu-id="bb9a1-127">Create an Azure service principal</span></span>

<span data-ttu-id="bb9a1-128">В этом разделе представлен порядок создания субъекта-службы Azure, которого подключаемый модуль Maven использует при развертывании веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-128">In this section, you create an Azure service principal that the Maven plugin uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="bb9a1-129">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-129">Open a command prompt.</span></span>

1. <span data-ttu-id="bb9a1-130">Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-130">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="bb9a1-131">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-131">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="bb9a1-132">Создайте субъект-службу Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-132">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="bb9a1-133">Где `uuuuuuuu` — это имя пользователя и `pppppppp` — пароль для субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-133">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="bb9a1-134">В ответ Azure предоставит код JSON, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-134">Azure responds with JSON that resembles the following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="bb9a1-135">При настройке подключаемого модуля Maven для развертывания веб-приложения в Azure используйте значения из этого ответа JSON.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-135">You will use the values from this JSON response when you configure the Maven plugin to deploy your web app to Azure.</span></span> <span data-ttu-id="bb9a1-136">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` и `tttttttt` являются значениями заполнителя, которые используются в этом примере с целью упростить сопоставление этих значений с соответствующими им элементами во время настройки файла Maven `settings.xml` в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-136">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="bb9a1-137">Настройка Maven для использования субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="bb9a1-137">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="bb9a1-138">В этом разделе с помощью значений из субъекта службы Azure выполняется настройка проверки подлинности, используемой Maven при развертывании веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-138">In this section, you use the values from your Azure service principal to configure the authentication that Maven uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="bb9a1-139">Откройте файл Maven `settings.xml` в текстовом редакторе; этот файл может находиться по пути, аналогичному указанному в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-139">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="bb9a1-140">Добавьте параметры субъекта-службы Azure из предыдущего раздела этого учебника в коллекцию `<servers>` в файле *settings.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="bb9a1-140">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="bb9a1-141">Описание</span><span class="sxs-lookup"><span data-stu-id="bb9a1-141">Where:</span></span>
   <span data-ttu-id="bb9a1-142">Элемент</span><span class="sxs-lookup"><span data-stu-id="bb9a1-142">Element</span></span> | <span data-ttu-id="bb9a1-143">Описание</span><span class="sxs-lookup"><span data-stu-id="bb9a1-143">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="bb9a1-144">Задает уникальное имя, которое Maven использует для поиска параметров безопасности при развертывании веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-144">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="bb9a1-145">Содержит значение `appId` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-145">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="bb9a1-146">Содержит значение `tenant` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-146">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="bb9a1-147">Содержит значение `password` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-147">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="bb9a1-148">Определяет целевую облачную среду Azure, которой в этом примере является `AZURE`.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-148">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="bb9a1-149">(Полный список сред см. в документации по [подключаемому модулю Maven для веб-приложений Azure].)</span><span class="sxs-lookup"><span data-stu-id="bb9a1-149">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="bb9a1-150">Сохраните и закройте файл *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-150">Save and close the *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-to-azure"></a><span data-ttu-id="bb9a1-151">НЕОБЯЗАТЕЛЬНО. Перед развертыванием веб-приложения в Azure настройте pom.xml.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-151">OPTIONAL: Customize your pom.xml before deploying your web app to Azure</span></span>

<span data-ttu-id="bb9a1-152">Откройте файл `pom.xml` для приложения Spring Boot в текстовом редакторе, а затем найдите элемент `<plugin>` для `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-152">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="bb9a1-153">Этот элемент должен выглядеть примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-153">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="bb9a1-154">Существует несколько значений, которые можно изменить для подключаемого модуля Maven. Подробное описание каждого из этих элементов см. в документации по [подключаемому модулю Maven для веб-приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="bb9a1-154">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="bb9a1-155">Существует ряд значений, на которые следует обратить внимание в этой статье.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-155">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="bb9a1-156">Элемент</span><span class="sxs-lookup"><span data-stu-id="bb9a1-156">Element</span></span> | <span data-ttu-id="bb9a1-157">Описание</span><span class="sxs-lookup"><span data-stu-id="bb9a1-157">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="bb9a1-158">Версия [подключаемому модулю Maven для веб-приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="bb9a1-158">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="bb9a1-159">Обратитесь к списку версий в [центральном репозитории Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22), чтобы убедиться, что вы используете актуальную версию.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-159">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="bb9a1-160">Сведения для проверки подлинности для Azure, в которых в данном примере содержится элемент `<serverId>`, который, в свою очередь, содержит `azure-auth`; Maven использует это значение для поиска значений субъекта-службы Azure в файле Maven *settings.xml*, который вы определили в предыдущем разделе этой статьи.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-160">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="bb9a1-161">Целевая группа ресурсов, которой в этом примере является `maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-161">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="bb9a1-162">Если эта группа ресурсов не существует, она создается во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-162">The resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="bb9a1-163">Целевое имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-163">Specifies the target name for your web app.</span></span> <span data-ttu-id="bb9a1-164">В этом примере целевое имя — `maven-web-app-${maven.build.timestamp}`, к которому в этом примере добавлен суффикс `${maven.build.timestamp}`, чтобы избежать конфликтов.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-164">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="bb9a1-165">(Метку времени добавлять необязательно; можно указать любую уникальную строку для имени приложения.)</span><span class="sxs-lookup"><span data-stu-id="bb9a1-165">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="bb9a1-166">Целевой регион, которым в данном примере является `westus`.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-166">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="bb9a1-167">(Полный список см. в документации по [подключаемому модулю Maven для веб-приложений Azure].)</span><span class="sxs-lookup"><span data-stu-id="bb9a1-167">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="bb9a1-168">Версия среды выполнения Java для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-168">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="bb9a1-169">(Полный список см. в документации по [подключаемому модулю Maven для веб-приложений Azure].)</span><span class="sxs-lookup"><span data-stu-id="bb9a1-169">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="bb9a1-170">Тип развертывания для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-170">Specifies deployment type for your web app.</span></span> <span data-ttu-id="bb9a1-171">Сейчас поддерживается только `ftp`, хотя поддержка других типов развертывания находится в разработке.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-171">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="bb9a1-172">Ресурсы и целевые назначения, которые Maven использует при развертывании веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-172">Specifies resources and target destinations which Maven uses when deploying your web app to Azure.</span></span> <span data-ttu-id="bb9a1-173">В этом примере два элемента `<resource>` указывают, что Maven развернет JAR-файл для веб-приложения и файл *web.config* из проекта Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-173">In this example, two `<resource>` elements specify that Maven will deploy the JAR file for your web app and the *web.config* file from the Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="bb9a1-174">Сборка и развертывание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="bb9a1-174">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="bb9a1-175">После настройки всех параметров в предыдущих разделах этой статьи можно приступать к развертыванию веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-175">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="bb9a1-176">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-176">To do so, use the following steps:</span></span>

1. <span data-ttu-id="bb9a1-177">В командной строке или в окне терминала, которые вы использовали ранее, перестройте JAR-файл, используя Maven, если вы внесли изменения в файл *pom.xml*; например:</span><span class="sxs-lookup"><span data-stu-id="bb9a1-177">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="bb9a1-178">Разверните веб-приложение в Azure с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="bb9a1-178">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="bb9a1-179">Maven выполнит развертывание веб-приложения в Azure; если веб-приложение еще не существует, оно будет создано.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-179">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="bb9a1-180">После развертывания веб-приложения вы сможете управлять им с помощью [портала Azure].</span><span class="sxs-lookup"><span data-stu-id="bb9a1-180">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="bb9a1-181">Веб-приложение будет указано в разделе **Службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="bb9a1-181">Your web app will be listed in **App Services**:</span></span>

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* <span data-ttu-id="bb9a1-183">URL-адрес веб-приложения будет указан в разделе **Обзор** для вашего веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="bb9a1-183">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="bb9a1-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb9a1-185">Next steps</span></span>

<span data-ttu-id="bb9a1-186">Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="bb9a1-186">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="bb9a1-187">[подключаемому модулю Maven для веб-приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="bb9a1-187">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="bb9a1-188">Вход в Azure из интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="bb9a1-188">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="bb9a1-189">Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="bb9a1-189">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="bb9a1-190">Создание субъекта-службы Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bb9a1-190">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="bb9a1-191">Справочник по параметрам Maven</span><span class="sxs-lookup"><span data-stu-id="bb9a1-191">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[портала Azure]: https://portal.azure.com/
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[подключаемому модулю Maven для веб-приложений Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
