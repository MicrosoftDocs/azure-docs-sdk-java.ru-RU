---
title: "Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure"
description: "Сведения о развертываний приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 1ab19a4805884773239c4d99090b9e117b3859cd
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/06/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-containerized-spring-boot-app-to-azure"></a><span data-ttu-id="cfae8-103">Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="cfae8-103">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>

<span data-ttu-id="cfae8-104">В этой статье описано, как использовать [подключаемый модуль Maven для веб-приложений Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) для развертывания примера приложения Spring Boot в контейнере Docker в службах приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="cfae8-104">This article demonstrates using the [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) to deploy a sample Spring Boot application in a Docker container to Azure App Services.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="cfae8-105">Подключаемый модуль Maven для веб-приложений Azure для [Apache Maven](http://maven.apache.org/) обеспечивает эффективную интеграцию службы приложений Azure в проекты Maven и упрощает процесс развертывания веб-приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="cfae8-105">The Maven Plugin for Azure Web Apps for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="cfae8-106">Подключаемый модуль Maven для веб-приложений Azure в настоящее время доступен в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="cfae8-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="cfae8-107">Сейчас поддерживается только FTP-публикация, но на будущее запланированы дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="cfae8-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="cfae8-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cfae8-108">Prerequisites</span></span>

<span data-ttu-id="cfae8-109">Для работы с этим руководством требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="cfae8-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="cfae8-110">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="cfae8-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="cfae8-111">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="cfae8-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="cfae8-112">Актуальный [пакет разработчиков Java (JDK)] версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="cfae8-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="cfae8-113">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="cfae8-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="cfae8-114">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="cfae8-114">A [Git] client.</span></span>
* <span data-ttu-id="cfae8-115">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="cfae8-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cfae8-116">С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="cfae8-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="cfae8-117">Клонирование примера "Приложение Spring Boot в веб-приложении Docker"</span><span class="sxs-lookup"><span data-stu-id="cfae8-117">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="cfae8-118">В этом разделе представлены сведения о клонировании контейнерного приложения Spring Boot и его тестировании на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="cfae8-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="cfae8-119">Откройте командную строку или окно терминала и создайте локальный каталог для размещения приложения Spring Boot, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="cfae8-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="cfae8-120">-- или --</span><span class="sxs-lookup"><span data-stu-id="cfae8-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="cfae8-121">Клонируйте образец проекта [Spring Boot on Docker Getting Started] (Запуск Spring Boot в Docker) в созданный каталог, например:</span><span class="sxs-lookup"><span data-stu-id="cfae8-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="cfae8-122">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="cfae8-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="cfae8-123">Выполните сборку файла JAR с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="cfae8-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="cfae8-124">При создании веб-приложения запустите веб-приложение с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="cfae8-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="cfae8-125">Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="cfae8-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="cfae8-126">Например, если имеется Curl, можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cfae8-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="cfae8-127">Должно появиться следующее сообщение: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="cfae8-127">You should see the following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="cfae8-128">Создание субъекта-службы Azure</span><span class="sxs-lookup"><span data-stu-id="cfae8-128">Create an Azure service principal</span></span>

<span data-ttu-id="cfae8-129">В этом разделе представлен порядок создания субъекта-службы Azure, которого подключаемый модуль Maven использует при развертывании контейнера в Azure.</span><span class="sxs-lookup"><span data-stu-id="cfae8-129">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="cfae8-130">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="cfae8-130">Open a command prompt.</span></span>

1. <span data-ttu-id="cfae8-131">Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="cfae8-131">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="cfae8-132">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="cfae8-132">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="cfae8-133">Создайте субъект-службу Azure.</span><span class="sxs-lookup"><span data-stu-id="cfae8-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="cfae8-134">Где `uuuuuuuu` — это имя пользователя и `pppppppp` — пароль для субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="cfae8-134">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="cfae8-135">В ответ Azure предоставит код JSON, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="cfae8-135">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="cfae8-136">При настройке подключаемого модуля Maven для развертывания контейнера в Azure используйте значения из этого ответа JSON.</span><span class="sxs-lookup"><span data-stu-id="cfae8-136">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="cfae8-137">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` и `tttttttt` являются значениями заполнителя, которые используются в этом примере с целью упростить сопоставление этих значений с соответствующими им элементами во время настройки файла Maven `settings.xml` в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="cfae8-137">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="cfae8-138">Настройка Maven для использования субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="cfae8-138">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="cfae8-139">В этом разделе с помощью значений из субъекта службы Azure выполняется настройка проверки подлинности, используемой Maven при развертывании контейнера в Azure.</span><span class="sxs-lookup"><span data-stu-id="cfae8-139">In this section, you use the values from your Azure service principal to configure the authentication that Maven will use when deploying your container to Azure.</span></span>

1. <span data-ttu-id="cfae8-140">Откройте файл Maven `settings.xml` в текстовом редакторе; этот файл может находиться по пути, аналогичному указанному в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="cfae8-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="cfae8-141">Добавьте параметры субъекта-службы Azure из предыдущего раздела этого учебника в коллекцию `<servers>` в файле *settings.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="cfae8-141">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="cfae8-142">Описание</span><span class="sxs-lookup"><span data-stu-id="cfae8-142">Where:</span></span>
   <span data-ttu-id="cfae8-143">Элемент</span><span class="sxs-lookup"><span data-stu-id="cfae8-143">Element</span></span> | <span data-ttu-id="cfae8-144">Описание</span><span class="sxs-lookup"><span data-stu-id="cfae8-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="cfae8-145">Задает уникальное имя, которое Maven использует для поиска параметров безопасности при развертывании веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="cfae8-145">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="cfae8-146">Содержит значение `appId` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="cfae8-146">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="cfae8-147">Содержит значение `tenant` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="cfae8-147">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="cfae8-148">Содержит значение `password` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="cfae8-148">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="cfae8-149">Определяет целевую облачную среду Azure, которой в этом примере является `AZURE`.</span><span class="sxs-lookup"><span data-stu-id="cfae8-149">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="cfae8-150">(Полный список сред см. в документации по [подключаемому модулю Maven для веб-приложений Azure].)</span><span class="sxs-lookup"><span data-stu-id="cfae8-150">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="cfae8-151">Сохраните и закройте файл *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="cfae8-151">Save and close the *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-to-docker-hub"></a><span data-ttu-id="cfae8-152">НЕОБЯЗАТЕЛЬНО. Развертывание локального файла Docker в центр Docker</span><span class="sxs-lookup"><span data-stu-id="cfae8-152">OPTIONAL: Deploy your local Docker file to Docker Hub</span></span>

<span data-ttu-id="cfae8-153">При наличии учетной записи Docker образ контейнера Docker можно создать локально и принудительно отправить его в центр Docker.</span><span class="sxs-lookup"><span data-stu-id="cfae8-153">If you have a Docker account, you can build your Docker container image locally and push it to Docker Hub.</span></span> <span data-ttu-id="cfae8-154">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cfae8-154">To do so, use the following steps.</span></span>

1. <span data-ttu-id="cfae8-155">Откройте файл `pom.xml` для приложения Spring Boot в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="cfae8-155">Open the `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="cfae8-156">Найдите дочерний элемент `<imageName>` элемента `<containerSettings>`.</span><span class="sxs-lookup"><span data-stu-id="cfae8-156">Locate the `<imageName>` child element of the `<containerSettings>` element.</span></span>

1. <span data-ttu-id="cfae8-157">Обновите значение `${docker.image.prefix}`, указав имя учетной записи Docker:</span><span class="sxs-lookup"><span data-stu-id="cfae8-157">Update the `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="cfae8-158">Выберите один из следующих способов развертывания.</span><span class="sxs-lookup"><span data-stu-id="cfae8-158">Choose one of the following deployment methods:</span></span>

   * <span data-ttu-id="cfae8-159">Создайте образ контейнера локально с помощью Maven, а затем используйте Docker для принудительной отправки контейнера в центр Docker.</span><span class="sxs-lookup"><span data-stu-id="cfae8-159">Build your container image locally with Maven, and then use Docker to push your container to Docker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="cfae8-160">Если установлен [подключаемый модуль Docker для Maven], можно автоматически создать и отправить образа контейнера в центр Docker с помощью параметра `-DpushImage`.</span><span class="sxs-lookup"><span data-stu-id="cfae8-160">If you have the [Docker plugin for Maven] installed, you can automatically build and your container image to Docker Hub by using the `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-to-azure"></a><span data-ttu-id="cfae8-161">НЕОБЯЗАТЕЛЬНО. Настройка pom.xml перед развертыванием веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="cfae8-161">OPTIONAL: Customize your pom.xml before deploying your container to Azure</span></span>

<span data-ttu-id="cfae8-162">Откройте файл `pom.xml` для приложения Spring Boot в текстовом редакторе, а затем найдите элемент `<plugin>` для `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="cfae8-162">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="cfae8-163">Этот элемент должен выглядеть примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="cfae8-163">This element should resemble the following example:</span></span>

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
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="cfae8-164">Существует несколько значений, которые можно изменить для подключаемого модуля Maven. Подробное описание каждого из этих элементов см. в документации по [подключаемому модулю Maven для веб-приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="cfae8-164">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="cfae8-165">Существует ряд значений, на которые следует обратить внимание в этой статье.</span><span class="sxs-lookup"><span data-stu-id="cfae8-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="cfae8-166">Элемент</span><span class="sxs-lookup"><span data-stu-id="cfae8-166">Element</span></span> | <span data-ttu-id="cfae8-167">Описание</span><span class="sxs-lookup"><span data-stu-id="cfae8-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="cfae8-168">Версия [подключаемому модулю Maven для веб-приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="cfae8-168">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="cfae8-169">Обратитесь к списку версий в [центральном репозитории Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22), чтобы убедиться, что вы используете актуальную версию.</span><span class="sxs-lookup"><span data-stu-id="cfae8-169">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="cfae8-170">Сведения для проверки подлинности для Azure, в которых в данном примере содержится элемент `<serverId>`, который, в свою очередь, содержит `azure-auth`; Maven использует это значение для поиска значений субъекта-службы Azure в файле Maven *settings.xml*, который вы определили в предыдущем разделе этой статьи.</span><span class="sxs-lookup"><span data-stu-id="cfae8-170">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="cfae8-171">Целевая группа ресурсов, которой в этом примере является `maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="cfae8-171">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="cfae8-172">Если эта группа ресурсов не существует, она будет создана во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="cfae8-172">The resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="cfae8-173">Целевое имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cfae8-173">Specifies the target name for your web app.</span></span> <span data-ttu-id="cfae8-174">В этом примере целевое имя — `maven-linux-app-${maven.build.timestamp}`, к которому в этом примере добавлен суффикс `${maven.build.timestamp}`, чтобы избежать конфликтов.</span><span class="sxs-lookup"><span data-stu-id="cfae8-174">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="cfae8-175">(Метку времени добавлять необязательно; можно указать любую уникальную строку для имени приложения.)</span><span class="sxs-lookup"><span data-stu-id="cfae8-175">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="cfae8-176">Целевой регион, которым в данном примере является `westus`.</span><span class="sxs-lookup"><span data-stu-id="cfae8-176">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="cfae8-177">(Полный список см. в документации по [подключаемому модулю Maven для веб-приложений Azure].)</span><span class="sxs-lookup"><span data-stu-id="cfae8-177">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="cfae8-178">Любые уникальные настройки для Maven, которые следует использовать при развертывании веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="cfae8-178">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="cfae8-179">В этом примере элемент `<property>` содержит пару "имя/значение" дочерних элементов, которая задает порт для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="cfae8-179">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cfae8-180">Параметры для изменения номера порта в этом примере необходимы только в случае, если требуется изменить порт по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cfae8-180">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

## <a name="build-and-deploy-your-container-to-azure"></a><span data-ttu-id="cfae8-181">Создание и развертывание контейнера в Azure</span><span class="sxs-lookup"><span data-stu-id="cfae8-181">Build and deploy your container to Azure</span></span>

<span data-ttu-id="cfae8-182">После настройки всех параметров в предыдущих разделах этой статьи можно приступать к развертыванию контейнера в Azure.</span><span class="sxs-lookup"><span data-stu-id="cfae8-182">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your container to Azure.</span></span> <span data-ttu-id="cfae8-183">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cfae8-183">To do so, use the following steps:</span></span>

1. <span data-ttu-id="cfae8-184">В командной строке или в окне терминала, которые вы использовали ранее, перестройте JAR-файл, используя Maven, если вы внесли изменения в файл *pom.xml*; например:</span><span class="sxs-lookup"><span data-stu-id="cfae8-184">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="cfae8-185">Разверните веб-приложение в Azure с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="cfae8-185">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="cfae8-186">Maven выполнит развертывание веб-приложения в Azure; если веб-приложение еще не существует, оно будет создано.</span><span class="sxs-lookup"><span data-stu-id="cfae8-186">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="cfae8-187">Если при запуске развертывания в регионе, который задан в элементе `<region>` в файле *pom.xml*, нет достаточного количества доступных серверов, может появиться сообщение об ошибке, аналогичное приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="cfae8-187">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="cfae8-188">В этом случае можно указать другой регион и повторно выполнить команду Maven для развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="cfae8-188">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="cfae8-189">После развертывания веб-приложения вы сможете управлять им с помощью [портала Azure].</span><span class="sxs-lookup"><span data-stu-id="cfae8-189">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="cfae8-190">Веб-приложение будет указано в разделе **Службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="cfae8-190">Your web app will be listed in **App Services**:</span></span>

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* <span data-ttu-id="cfae8-192">URL-адрес веб-приложения будет указан в разделе **Обзор** для вашего веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="cfae8-192">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cfae8-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cfae8-194">Next steps</span></span>

<span data-ttu-id="cfae8-195">Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="cfae8-195">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="cfae8-196">[подключаемому модулю Maven для веб-приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="cfae8-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="cfae8-197">Вход в Azure из интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="cfae8-197">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="cfae8-198">Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="cfae8-198">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure App Service </span></span>](deploy-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="cfae8-199">Создание субъекта-службы Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cfae8-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="cfae8-200">Справочник по параметрам Maven</span><span class="sxs-lookup"><span data-stu-id="cfae8-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="cfae8-201">[подключаемый модуль Docker для Maven]</span><span class="sxs-lookup"><span data-stu-id="cfae8-201">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[портала Azure]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[подключаемый модуль Docker для Maven]: https://github.com/spotify/docker-maven-plugin
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[подключаемому модулю Maven для веб-приложений Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP02.png
