---
title: Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure
description: Сведения о развертываний приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: cc14ac8dfd393d60924c39be0870c3caedc9741c
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339088"
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-containerized-spring-boot-app-to-azure"></a><span data-ttu-id="20b7b-103">Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="20b7b-103">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>

<span data-ttu-id="20b7b-104">В этой статье описано, как использовать [подключаемый модуль Maven для веб-приложений Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) для развертывания примера приложения Spring Boot в контейнере Docker в службах приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="20b7b-104">This article demonstrates using the [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) to deploy a sample Spring Boot application in a Docker container to Azure App Services.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="20b7b-105">Подключаемый модуль Maven для веб-приложений Azure для [Apache Maven](http://maven.apache.org/) обеспечивает эффективную интеграцию службы приложений Azure в проекты Maven и упрощает процесс развертывания веб-приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="20b7b-105">The Maven Plugin for Azure Web Apps for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="20b7b-106">Подключаемый модуль Maven для веб-приложений Azure в настоящее время доступен в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="20b7b-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="20b7b-107">Сейчас поддерживается только FTP-публикация, но на будущее запланированы дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="20b7b-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="20b7b-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="20b7b-108">Prerequisites</span></span>

<span data-ttu-id="20b7b-109">Для работы с этим руководством требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="20b7b-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="20b7b-110">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="20b7b-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="20b7b-111">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="20b7b-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="20b7b-112">Поддерживаемая версия Java Development Kit (JDK).</span><span class="sxs-lookup"><span data-stu-id="20b7b-112">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="20b7b-113">Дополнительные сведения о версиях JDK, доступных для разработки в Azure, см. в статье <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="20b7b-113">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="20b7b-114">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="20b7b-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="20b7b-115">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="20b7b-115">A [Git] client.</span></span>
* <span data-ttu-id="20b7b-116">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="20b7b-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="20b7b-117">С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="20b7b-117">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="20b7b-118">Клонирование примера "Приложение Spring Boot в веб-приложении Docker"</span><span class="sxs-lookup"><span data-stu-id="20b7b-118">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="20b7b-119">В этом разделе представлены сведения о клонировании контейнерного приложения Spring Boot и его тестировании на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="20b7b-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="20b7b-120">Откройте командную строку или окно терминала и создайте локальный каталог для размещения приложения Spring Boot, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="20b7b-120">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="20b7b-121">-- или --</span><span class="sxs-lookup"><span data-stu-id="20b7b-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="20b7b-122">Клонируйте образец проекта [Spring Boot on Docker Getting Started] (Запуск Spring Boot в Docker) в созданный каталог, например:</span><span class="sxs-lookup"><span data-stu-id="20b7b-122">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker
   ```

1. <span data-ttu-id="20b7b-123">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="20b7b-123">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="20b7b-124">Выполните сборку файла JAR с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="20b7b-124">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="20b7b-125">При создании веб-приложения запустите веб-приложение с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="20b7b-125">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="20b7b-126">Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="20b7b-126">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="20b7b-127">Например, если имеется Curl, можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="20b7b-127">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="20b7b-128">Должно появиться следующее сообщение: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="20b7b-128">You should see the following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="20b7b-129">Создание субъекта-службы Azure</span><span class="sxs-lookup"><span data-stu-id="20b7b-129">Create an Azure service principal</span></span>

<span data-ttu-id="20b7b-130">В этом разделе представлен порядок создания субъекта-службы Azure, которого подключаемый модуль Maven использует при развертывании контейнера в Azure.</span><span class="sxs-lookup"><span data-stu-id="20b7b-130">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="20b7b-131">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="20b7b-131">Open a command prompt.</span></span>

2. <span data-ttu-id="20b7b-132">Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="20b7b-132">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="20b7b-133">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="20b7b-133">Follow the instructions to complete the sign-in process.</span></span>

3. <span data-ttu-id="20b7b-134">Создайте субъект-службу Azure.</span><span class="sxs-lookup"><span data-stu-id="20b7b-134">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="20b7b-135">Описание</span><span class="sxs-lookup"><span data-stu-id="20b7b-135">Where:</span></span>

   | <span data-ttu-id="20b7b-136">Параметр</span><span class="sxs-lookup"><span data-stu-id="20b7b-136">Parameter</span></span>  |                    <span data-ttu-id="20b7b-137">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="20b7b-137">Description</span></span>                     |
   |------------|----------------------------------------------------|
   | `uuuuuuuu` | <span data-ttu-id="20b7b-138">Определяет имя пользователя для субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="20b7b-138">Specifies the user name for the service principal.</span></span> |
   | `pppppppp` | <span data-ttu-id="20b7b-139">Определяет пароль для субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="20b7b-139">Specifies the password for the service principal.</span></span>  |


4. <span data-ttu-id="20b7b-140">В ответ Azure предоставит код JSON, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="20b7b-140">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="20b7b-141">При настройке подключаемого модуля Maven для развертывания контейнера в Azure используйте значения из этого ответа JSON.</span><span class="sxs-lookup"><span data-stu-id="20b7b-141">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="20b7b-142">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` и `tttttttt` являются значениями заполнителя, которые используются в этом примере с целью упростить сопоставление этих значений с соответствующими им элементами во время настройки файла Maven `settings.xml` в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="20b7b-142">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="20b7b-143">Настройка Maven для использования субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="20b7b-143">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="20b7b-144">В этом разделе с помощью значений из субъекта службы Azure выполняется настройка проверки подлинности, используемой Maven при развертывании контейнера в Azure.</span><span class="sxs-lookup"><span data-stu-id="20b7b-144">In this section, you use the values from your Azure service principal to configure the authentication that Maven will use when deploying your container to Azure.</span></span>

1. <span data-ttu-id="20b7b-145">Откройте файл Maven `settings.xml` в текстовом редакторе; этот файл может находиться по пути, аналогичному указанному в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="20b7b-145">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

2. <span data-ttu-id="20b7b-146">Добавьте параметры субъекта-службы Azure из предыдущего раздела этого учебника в коллекцию `<servers>` в файле *settings.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="20b7b-146">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="20b7b-147">Описание</span><span class="sxs-lookup"><span data-stu-id="20b7b-147">Where:</span></span>

   |     <span data-ttu-id="20b7b-148">Элемент</span><span class="sxs-lookup"><span data-stu-id="20b7b-148">Element</span></span>     |                                                                                   <span data-ttu-id="20b7b-149">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="20b7b-149">Description</span></span>                                                                                   |
   |-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `<id>`      |                                <span data-ttu-id="20b7b-150">Задает уникальное имя, которое Maven использует для поиска параметров безопасности при развертывании веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="20b7b-150">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>                                |
   |   `<client>`    |                                                             <span data-ttu-id="20b7b-151">Содержит значение `appId` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="20b7b-151">Contains the `appId` value from your service principal.</span></span>                                                             |
   |   `<tenant>`    |                                                            <span data-ttu-id="20b7b-152">Содержит значение `tenant` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="20b7b-152">Contains the `tenant` value from your service principal.</span></span>                                                             |
   |     `<key>`     |                                                           <span data-ttu-id="20b7b-153">Содержит значение `password` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="20b7b-153">Contains the `password` value from your service principal.</span></span>                                                            |
   | `<environment>` | <span data-ttu-id="20b7b-154">Определяет целевую облачную среду Azure, которой в этом примере является `AZURE`.</span><span class="sxs-lookup"><span data-stu-id="20b7b-154">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="20b7b-155">(Полный список сред см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].)</span><span class="sxs-lookup"><span data-stu-id="20b7b-155">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span> |


3. <span data-ttu-id="20b7b-156">Сохраните и закройте файл *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="20b7b-156">Save and close the *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-to-docker-hub"></a><span data-ttu-id="20b7b-157">НЕОБЯЗАТЕЛЬНО. Развертывание локального файла Docker в центр Docker</span><span class="sxs-lookup"><span data-stu-id="20b7b-157">OPTIONAL: Deploy your local Docker file to Docker Hub</span></span>

<span data-ttu-id="20b7b-158">При наличии учетной записи Docker образ контейнера Docker можно создать локально и принудительно отправить его в центр Docker.</span><span class="sxs-lookup"><span data-stu-id="20b7b-158">If you have a Docker account, you can build your Docker container image locally and push it to Docker Hub.</span></span> <span data-ttu-id="20b7b-159">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="20b7b-159">To do so, use the following steps.</span></span>

1. <span data-ttu-id="20b7b-160">Откройте файл `pom.xml` для приложения Spring Boot в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="20b7b-160">Open the `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="20b7b-161">Найдите дочерний элемент `<imageName>` элемента `<containerSettings>`.</span><span class="sxs-lookup"><span data-stu-id="20b7b-161">Locate the `<imageName>` child element of the `<containerSettings>` element.</span></span>

1. <span data-ttu-id="20b7b-162">Обновите значение `${docker.image.prefix}`, указав имя учетной записи Docker:</span><span class="sxs-lookup"><span data-stu-id="20b7b-162">Update the `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="20b7b-163">Выберите один из следующих способов развертывания.</span><span class="sxs-lookup"><span data-stu-id="20b7b-163">Choose one of the following deployment methods:</span></span>

   * <span data-ttu-id="20b7b-164">Создайте образ контейнера локально с помощью Maven, а затем используйте Docker для принудительной отправки контейнера в центр Docker.</span><span class="sxs-lookup"><span data-stu-id="20b7b-164">Build your container image locally with Maven, and then use Docker to push your container to Docker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```

   * <span data-ttu-id="20b7b-165">Если установлен [подключаемый модуль Docker для Maven], можно автоматически создать и отправить образа контейнера в центр Docker с помощью параметра `-DpushImage`.</span><span class="sxs-lookup"><span data-stu-id="20b7b-165">If you have the [Docker plugin for Maven] installed, you can automatically build and your container image to Docker Hub by using the `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-to-azure"></a><span data-ttu-id="20b7b-166">НЕОБЯЗАТЕЛЬНО. Настройка pom.xml перед развертыванием веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="20b7b-166">OPTIONAL: Customize your pom.xml before deploying your container to Azure</span></span>

<span data-ttu-id="20b7b-167">Откройте файл `pom.xml` для приложения Spring Boot в текстовом редакторе, а затем найдите элемент `<plugin>` для `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="20b7b-167">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="20b7b-168">Этот элемент должен выглядеть примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="20b7b-168">This element should resemble the following example:</span></span>

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

<span data-ttu-id="20b7b-169">Существует несколько значений, которые можно изменить для подключаемого модуля Maven. Подробное описание каждого из этих элементов см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="20b7b-169">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="20b7b-170">Существует ряд значений, на которые следует обратить внимание в этой статье.</span><span class="sxs-lookup"><span data-stu-id="20b7b-170">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="20b7b-171">Элемент</span><span class="sxs-lookup"><span data-stu-id="20b7b-171">Element</span></span> | <span data-ttu-id="20b7b-172">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="20b7b-172">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="20b7b-173">Версия [Подключаемый модуль Maven для веб-приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="20b7b-173">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="20b7b-174">Обратитесь к списку версий в [центральном репозитории Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22), чтобы убедиться, что вы используете актуальную версию.</span><span class="sxs-lookup"><span data-stu-id="20b7b-174">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<authentication>` | <span data-ttu-id="20b7b-175">Сведения для проверки подлинности для Azure, в которых в данном примере содержится элемент `<serverId>`, который, в свою очередь, содержит `azure-auth`; Maven использует это значение для поиска значений субъекта-службы Azure в файле Maven *settings.xml*, который вы определили в предыдущем разделе этой статьи.</span><span class="sxs-lookup"><span data-stu-id="20b7b-175">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="20b7b-176">Целевая группа ресурсов, которой в этом примере является `maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="20b7b-176">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="20b7b-177">Если эта группа ресурсов не существует, она будет создана во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="20b7b-177">The resource group will be created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="20b7b-178">Целевое имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="20b7b-178">Specifies the target name for your web app.</span></span> <span data-ttu-id="20b7b-179">В этом примере целевое имя — `maven-linux-app-${maven.build.timestamp}`, к которому в этом примере добавлен суффикс `${maven.build.timestamp}`, чтобы избежать конфликтов.</span><span class="sxs-lookup"><span data-stu-id="20b7b-179">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="20b7b-180">(Метку времени добавлять необязательно; можно указать любую уникальную строку для имени приложения.)</span><span class="sxs-lookup"><span data-stu-id="20b7b-180">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="20b7b-181">Целевой регион, которым в данном примере является `westus`.</span><span class="sxs-lookup"><span data-stu-id="20b7b-181">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="20b7b-182">(Полный список см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].)</span><span class="sxs-lookup"><span data-stu-id="20b7b-182">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<appSettings>` | <span data-ttu-id="20b7b-183">Любые уникальные настройки для Maven, которые следует использовать при развертывании веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="20b7b-183">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="20b7b-184">В этом примере элемент `<property>` содержит пару "имя/значение" дочерних элементов, которая задает порт для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="20b7b-184">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span> |

> [!NOTE]
>
> <span data-ttu-id="20b7b-185">Параметры для изменения номера порта в этом примере необходимы только в случае, если требуется изменить порт по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="20b7b-185">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

## <a name="build-and-deploy-your-container-to-azure"></a><span data-ttu-id="20b7b-186">Создание и развертывание контейнера в Azure</span><span class="sxs-lookup"><span data-stu-id="20b7b-186">Build and deploy your container to Azure</span></span>

<span data-ttu-id="20b7b-187">После настройки всех параметров в предыдущих разделах этой статьи можно приступать к развертыванию контейнера в Azure.</span><span class="sxs-lookup"><span data-stu-id="20b7b-187">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your container to Azure.</span></span> <span data-ttu-id="20b7b-188">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="20b7b-188">To do so, use the following steps:</span></span>

1. <span data-ttu-id="20b7b-189">В командной строке или в окне терминала, которые вы использовали ранее, перестройте JAR-файл, используя Maven, если вы внесли изменения в файл *pom.xml*; например:</span><span class="sxs-lookup"><span data-stu-id="20b7b-189">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="20b7b-190">Разверните веб-приложение в Azure с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="20b7b-190">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="20b7b-191">Maven выполнит развертывание веб-приложения в Azure; если веб-приложение еще не существует, оно будет создано.</span><span class="sxs-lookup"><span data-stu-id="20b7b-191">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="20b7b-192">Если при запуске развертывания в регионе, который задан в элементе `<region>` в файле *pom.xml*, нет достаточного количества доступных серверов, может появиться сообщение об ошибке, аналогичное приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="20b7b-192">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
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
> <span data-ttu-id="20b7b-193">В этом случае можно указать другой регион и повторно выполнить команду Maven для развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="20b7b-193">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="20b7b-194">После развертывания веб-приложения вы сможете управлять им с помощью [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="20b7b-194">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="20b7b-195">Веб-приложение будет указано в разделе **Службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="20b7b-195">Your web app will be listed in **App Services**:</span></span>

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* <span data-ttu-id="20b7b-197">URL-адрес веб-приложения будет указан в разделе **Обзор** для вашего веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="20b7b-197">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="20b7b-199">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="20b7b-199">Next steps</span></span>

<span data-ttu-id="20b7b-200">Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="20b7b-200">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="20b7b-201">[Подключаемый модуль Maven для веб-приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="20b7b-201">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="20b7b-202">Вход в Azure из интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="20b7b-202">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="20b7b-203">Развертывание приложения Spring Boot в Azure с помощью подключаемого модуля Maven для веб-приложений Azure в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="20b7b-203">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure App Service </span></span>](deploy-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="20b7b-204">Создание субъекта-службы Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="20b7b-204">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="20b7b-205">Справочник по параметрам Maven</span><span class="sxs-lookup"><span data-stu-id="20b7b-205">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="20b7b-206">[Подключаемый модуль Docker для Maven]</span><span class="sxs-lookup"><span data-stu-id="20b7b-206">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[портал Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[Подключаемый модуль Docker для Maven]: https://github.com/spotify/docker-maven-plugin
[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Подключаемый модуль Maven для веб-приложений Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[AP01]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP02.png
