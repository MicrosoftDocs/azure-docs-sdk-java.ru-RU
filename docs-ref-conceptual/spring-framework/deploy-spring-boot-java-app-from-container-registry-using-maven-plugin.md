---
title: Развертывание приложения Spring Boot в реестре контейнеров Azure в службе приложений Azure с помощью подключаемого модуля Maven для веб-приложений Azure
description: В этом руководстве представлен порядок развертывания приложения Spring Boot в реестре контейнеров Azure в службе приложений Azure с помощью подключаемого модуля Maven.
services: container-registry
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: e84960ebf79b89b2430924016a429518a935d086
ms.sourcegitcommit: 9d9e2fa97ebd95a699adcb58e82c3fc0882f0a24
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/15/2018
ms.locfileid: "49315938"
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a><span data-ttu-id="be590-103">Развертывание приложения Spring Boot в реестре контейнеров Azure в службе приложений Azure с помощью подключаемого модуля Maven для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="be590-103">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app in Azure Container Registry to Azure App Service</span></span>

<span data-ttu-id="be590-104">В этой статье описано, как развернуть пример приложения [Spring Boot] в реестре контейнера Azure, а затем использовать подключаемый модуль Maven для веб-приложений Azure для развертывания приложения в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-104">This article demonstrates how to deploy a sample [Spring Boot] application to Azure Container Registry, and then use the Maven Plugin for Azure Web Apps to deploy your application to Azure App Service.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="be590-105">Подключаемый модуль Maven для веб-приложений Azure для [Apache Maven](http://maven.apache.org/) обеспечивает эффективную интеграцию службы приложений Azure в проекты Maven и упрощает процесс развертывания веб-приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-105">The Maven Plugin for Azure Web Apps for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="be590-106">Подключаемый модуль Maven для веб-приложений Azure в настоящее время доступен в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="be590-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="be590-107">Сейчас поддерживается только FTP-публикация, но на будущее запланированы дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="be590-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="be590-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="be590-108">Prerequisites</span></span>

<span data-ttu-id="be590-109">Для работы с этим руководством требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="be590-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="be590-110">Подписка Azure. Если у вас ее еще нет, вы можете активировать [Преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="be590-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="be590-111">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="be590-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="be590-112">Актуальный [пакет разработчиков Java (JDK)] версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="be590-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="be590-113">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="be590-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="be590-114">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="be590-114">A [Git] client.</span></span>
* <span data-ttu-id="be590-115">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="be590-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="be590-116">С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="be590-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="be590-117">Клонирование примера "Приложение Spring Boot в веб-приложении Docker"</span><span class="sxs-lookup"><span data-stu-id="be590-117">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="be590-118">В этом разделе представлены сведения о клонировании контейнерного приложения Spring Boot и его тестировании на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="be590-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="be590-119">Откройте командную строку или окно терминала и создайте локальный каталог для размещения приложения Spring Boot, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="be590-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="be590-120">-- или --</span><span class="sxs-lookup"><span data-stu-id="be590-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="be590-121">Клонируйте образец проекта [Spring Boot on Docker Getting Started] (Запуск Spring Boot в Docker) в созданный каталог, например:</span><span class="sxs-lookup"><span data-stu-id="be590-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone -b https://github.com/spring-guides/gs-spring-boot-docker
   ```

1. <span data-ttu-id="be590-122">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="be590-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="be590-123">Выполните сборку файла JAR с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="be590-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="be590-124">При создании веб-приложения запустите веб-приложение с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="be590-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="be590-125">Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="be590-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="be590-126">Например, если имеется Curl, можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="be590-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="be590-127">Должно появиться следующее сообщение: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="be590-127">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Локальный просмотр образца приложения][SB01]

> [!NOTE]
>
> <span data-ttu-id="be590-129">При локальном использовании Docker может появиться сообщение об ошибке подключения к локальному компьютеру через порт 2375.</span><span class="sxs-lookup"><span data-stu-id="be590-129">When you are using Docker locally, you may see an error which states that you cannot connect to localhost on port 2375.</span></span> <span data-ttu-id="be590-130">В этом случае попробуйте использовать Docker локально без TLS.</span><span class="sxs-lookup"><span data-stu-id="be590-130">If this happens, you may need to enable using Docker locally without TLS.</span></span> <span data-ttu-id="be590-131">Для этого откройте параметры Docker и **предоставьте управляющую программу для TCP://localhost:2375 без TLS**.</span><span class="sxs-lookup"><span data-stu-id="be590-131">To do so, open your Docker settings and check the option to **Expose daemon on TCP://localhost:2375 without TLS**.</span></span>
>
> ![Предоставление управляющей программы Docker для локального TCP-порта 2375][TL01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="be590-133">Создание субъекта-службы Azure</span><span class="sxs-lookup"><span data-stu-id="be590-133">Create an Azure service principal</span></span>

<span data-ttu-id="be590-134">В этом разделе представлен порядок создания субъекта-службы Azure, которого подключаемый модуль Maven использует при развертывании контейнера в Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-134">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="be590-135">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="be590-135">Open a command prompt.</span></span>

2. <span data-ttu-id="be590-136">Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-136">Sign into your Azure account by using the Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="be590-137">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="be590-137">Follow the instructions to complete the sign-in process.</span></span>

3. <span data-ttu-id="be590-138">Создайте субъект-службу Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-138">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="be590-139">Описание</span><span class="sxs-lookup"><span data-stu-id="be590-139">Where:</span></span>

   | <span data-ttu-id="be590-140">Параметр</span><span class="sxs-lookup"><span data-stu-id="be590-140">Parameter</span></span>  |                    <span data-ttu-id="be590-141">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="be590-141">Description</span></span>                     |
   |------------|----------------------------------------------------|
   | `uuuuuuuu` | <span data-ttu-id="be590-142">Определяет имя пользователя для субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="be590-142">Specifies the user name for the service principal.</span></span> |
   | `pppppppp` | <span data-ttu-id="be590-143">Определяет пароль для субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="be590-143">Specifies the password for the service principal.</span></span>  |


4. <span data-ttu-id="be590-144">В ответ Azure предоставит код JSON, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="be590-144">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="be590-145">При настройке подключаемого модуля Maven для развертывания контейнера в Azure используйте значения из этого ответа JSON.</span><span class="sxs-lookup"><span data-stu-id="be590-145">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="be590-146">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` и `tttttttt` являются значениями заполнителя, которые используются в этом примере с целью упростить сопоставление этих значений с соответствующими им элементами во время настройки файла Maven `settings.xml` в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="be590-146">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="be590-147">Создание реестра контейнеров Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="be590-147">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="be590-148">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="be590-148">Open a command prompt.</span></span>

1. <span data-ttu-id="be590-149">Войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-149">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="be590-150">Создайте группу ресурсов Azure, используемых в этой статье.</span><span class="sxs-lookup"><span data-stu-id="be590-150">Create a resource group for the Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="be590-151">Замените `wingtiptoysresources` в этом примере уникальным именем для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="be590-151">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="be590-152">Создайте частный реестр контейнеров Azure в группе ресурсов для приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="be590-152">Create a private Azure container registry in the resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="be590-153">Замените `wingtiptoysregistry` в этом примере уникальным именем для реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="be590-153">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="be590-154">Получите пароль для реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="be590-154">Retrieve the password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="be590-155">В ответ Azure предоставит пароль, например:</span><span class="sxs-lookup"><span data-stu-id="be590-155">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a><span data-ttu-id="be590-156">Добавление реестра контейнеров Azure и субъекта-службы Azure в настройки Maven</span><span class="sxs-lookup"><span data-stu-id="be590-156">Add your Azure container registry and Azure service principal to your Maven settings</span></span>

1. <span data-ttu-id="be590-157">Откройте файл Maven `settings.xml` в текстовом редакторе; этот файл может находиться по пути, аналогичному указанному в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="be590-157">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

2. <span data-ttu-id="be590-158">Добавьте параметры доступа к реестру контейнеров Azure из предыдущего раздела этой статьи в коллекцию `<servers>` в файле *settings.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="be590-158">Add your Azure Container Registry access settings from the previous section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="be590-159">Описание</span><span class="sxs-lookup"><span data-stu-id="be590-159">Where:</span></span>

   |   <span data-ttu-id="be590-160">Элемент</span><span class="sxs-lookup"><span data-stu-id="be590-160">Element</span></span>    |                                 <span data-ttu-id="be590-161">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="be590-161">Description</span></span>                                  |
   |--------------|------------------------------------------------------------------------------|
   |    `<id>`    |         <span data-ttu-id="be590-162">Содержит имя закрытого реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-162">Contains the name of your private Azure container registry.</span></span>          |
   | `<username>` |         <span data-ttu-id="be590-163">Содержит имя закрытого реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-163">Contains the name of your private Azure container registry.</span></span>          |
   | `<password>` | <span data-ttu-id="be590-164">Содержит пароль, полученный в предыдущем разделе этой статьи.</span><span class="sxs-lookup"><span data-stu-id="be590-164">Contains the password you retrieved in the previous section of this article.</span></span> |


3. <span data-ttu-id="be590-165">Добавьте параметры субъекта-службы Azure из раздела выше этой статьи в коллекцию `<servers>` в файле *settings.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="be590-165">Add your Azure service principal settings from an earlier section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="be590-166">Описание</span><span class="sxs-lookup"><span data-stu-id="be590-166">Where:</span></span>

   |     <span data-ttu-id="be590-167">Элемент</span><span class="sxs-lookup"><span data-stu-id="be590-167">Element</span></span>     |                                                                                   <span data-ttu-id="be590-168">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="be590-168">Description</span></span>                                                                                   |
   |-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `<id>`      |                                <span data-ttu-id="be590-169">Задает уникальное имя, которое Maven использует для поиска параметров безопасности при развертывании веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-169">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>                                |
   |   `<client>`    |                                                             <span data-ttu-id="be590-170">Содержит значение `appId` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="be590-170">Contains the `appId` value from your service principal.</span></span>                                                             |
   |   `<tenant>`    |                                                            <span data-ttu-id="be590-171">Содержит значение `tenant` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="be590-171">Contains the `tenant` value from your service principal.</span></span>                                                             |
   |     `<key>`     |                                                           <span data-ttu-id="be590-172">Содержит значение `password` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="be590-172">Contains the `password` value from your service principal.</span></span>                                                            |
   | `<environment>` | <span data-ttu-id="be590-173">Определяет целевую облачную среду Azure, которой в этом примере является `AZURE`.</span><span class="sxs-lookup"><span data-stu-id="be590-173">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="be590-174">(Полный список сред см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].)</span><span class="sxs-lookup"><span data-stu-id="be590-174">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span> |


4. <span data-ttu-id="be590-175">Сохраните и закройте файл *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="be590-175">Save and close the *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a><span data-ttu-id="be590-176">Сборка образа контейнера Docker и его передача в реестр контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="be590-176">Build your Docker container image and push it to your Azure container registry</span></span>

1. <span data-ttu-id="be590-177">Перейдите в каталог завершенного проекта для приложения Spring Boot (например, "*C:\SpringBoot\gs-spring-boot-docker\complete*" или "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="be590-177">Navigate to the completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

2. <span data-ttu-id="be590-178">Обновите коллекцию `<properties>` в файле *pom.xml*, добавив значение сервера входа для реестра контейнеров Azure из предыдущего раздела данного учебника, например:</span><span class="sxs-lookup"><span data-stu-id="be590-178">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="be590-179">Описание</span><span class="sxs-lookup"><span data-stu-id="be590-179">Where:</span></span>

   |           <span data-ttu-id="be590-180">Элемент</span><span class="sxs-lookup"><span data-stu-id="be590-180">Element</span></span>           |                                                                       <span data-ttu-id="be590-181">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="be590-181">Description</span></span>                                                                       |
   |-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
   | `<azure.containerRegistry>` |                                              <span data-ttu-id="be590-182">Задает имя закрытого реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-182">Specifies the name of your private Azure container registry.</span></span>                                               |
   |   `<docker.image.prefix>`   | <span data-ttu-id="be590-183">Задает URL-адрес закрытого реестра контейнеров Azure, который сформирован путем добавления ".azurecr.io" к имени закрытого реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="be590-183">Specifies the URL of your private Azure container registry, which is derived by appending ".azurecr.io" to the name of your private container registry.</span></span> |


3. <span data-ttu-id="be590-184">Убедитесь, что в элементе `<plugin>` для подключаемого модуля Docker в файле *pom.xml* содержатся необходимые свойства для адреса сервера входа и имя реестра из предыдущего шага в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="be590-184">Verify that `<plugin>` for the Docker plugin in your *pom.xml* file contains the correct properties for the login server address and registry name from the previous step in this tutorial.</span></span> <span data-ttu-id="be590-185">Например: </span><span class="sxs-lookup"><span data-stu-id="be590-185">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="be590-186">Описание</span><span class="sxs-lookup"><span data-stu-id="be590-186">Where:</span></span>

   |     <span data-ttu-id="be590-187">Элемент</span><span class="sxs-lookup"><span data-stu-id="be590-187">Element</span></span>     |                                       <span data-ttu-id="be590-188">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="be590-188">Description</span></span>                                       |
   |-----------------|-----------------------------------------------------------------------------------------|
   |  `<serverId>`   |  <span data-ttu-id="be590-189">Задает свойство, которое содержит имя закрытого реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-189">Specifies the property which contains name of your private Azure container registry.</span></span>   |
   | `<registryUrl>` | <span data-ttu-id="be590-190">Задает свойство, которое содержит URL-адрес закрытого реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-190">Specifies the property which contains the URL of your private Azure container registry.</span></span> |


4. <span data-ttu-id="be590-191">Перейдите в каталог завершенного проекта для приложения Spring Boot и выполните команду ниже для перестроения приложения и отправки контейнера в реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-191">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

5. <span data-ttu-id="be590-192">НЕОБЯЗАТЕЛЬНО. Перейдите на [портал Azure] и убедитесь, что в реестре контейнеров имеется образ контейнера Docker с именем **gs-spring-boot-docker**.</span><span class="sxs-lookup"><span data-stu-id="be590-192">OPTIONAL: Browse to the [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Проверка контейнера на портале Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a><span data-ttu-id="be590-194">Настройка файла pom.xml и последующие построение и развертывание контейнера в Azure</span><span class="sxs-lookup"><span data-stu-id="be590-194">Customize your pom.xml, then build and deploy your container to Azure</span></span>

<span data-ttu-id="be590-195">Откройте файл `pom.xml` для приложения Spring Boot в текстовом редакторе, а затем найдите элемент `<plugin>` для `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="be590-195">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="be590-196">Этот элемент должен выглядеть примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="be590-196">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
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

<span data-ttu-id="be590-197">Существует несколько значений, которые можно изменить для подключаемого модуля Maven. Подробное описание каждого из этих элементов см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="be590-197">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="be590-198">Существует ряд значений, на которые следует обратить внимание в этой статье.</span><span class="sxs-lookup"><span data-stu-id="be590-198">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="be590-199">Элемент</span><span class="sxs-lookup"><span data-stu-id="be590-199">Element</span></span> | <span data-ttu-id="be590-200">ОПИСАНИЕ</span><span class="sxs-lookup"><span data-stu-id="be590-200">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="be590-201">Версия [Подключаемый модуль Maven для веб-приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="be590-201">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="be590-202">Обратитесь к списку версий в [центральном репозитории Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22), чтобы убедиться, что вы используете актуальную версию.</span><span class="sxs-lookup"><span data-stu-id="be590-202">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<authentication>` | <span data-ttu-id="be590-203">Сведения для проверки подлинности для Azure, в которых в данном примере содержится элемент `<serverId>`, который, в свою очередь, содержит `azure-auth`; Maven использует это значение для поиска значений субъекта-службы Azure в файле Maven *settings.xml*, который вы определили в предыдущем разделе этой статьи.</span><span class="sxs-lookup"><span data-stu-id="be590-203">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="be590-204">Целевая группа ресурсов, которой в этом примере является `wingtiptoysresources`.</span><span class="sxs-lookup"><span data-stu-id="be590-204">Specifies the target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="be590-205">Если эта группа ресурсов не существует, она будет создана во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="be590-205">The resource group will be created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="be590-206">Целевое имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="be590-206">Specifies the target name for your web app.</span></span> <span data-ttu-id="be590-207">В этом примере целевое имя — `maven-linux-app-${maven.build.timestamp}`, к которому в этом примере добавлен суффикс `${maven.build.timestamp}`, чтобы избежать конфликтов.</span><span class="sxs-lookup"><span data-stu-id="be590-207">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="be590-208">(Метку времени добавлять необязательно; можно указать любую уникальную строку для имени приложения.)</span><span class="sxs-lookup"><span data-stu-id="be590-208">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="be590-209">Целевой регион, которым в данном примере является `westus`.</span><span class="sxs-lookup"><span data-stu-id="be590-209">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="be590-210">(Полный список см. в документации по [Подключаемый модуль Maven для веб-приложений Azure].)</span><span class="sxs-lookup"><span data-stu-id="be590-210">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<containerSettings>` | <span data-ttu-id="be590-211">Свойства, которые содержат имя и URL-адрес контейнера.</span><span class="sxs-lookup"><span data-stu-id="be590-211">Specifies the properties which contain the name and URL of your container.</span></span> |
| `<appSettings>` | <span data-ttu-id="be590-212">Любые уникальные настройки для Maven, которые следует использовать при развертывании веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="be590-212">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="be590-213">В этом примере элемент `<property>` содержит пару "имя/значение" дочерних элементов, которая задает порт для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="be590-213">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span> |

> [!NOTE]
>
> <span data-ttu-id="be590-214">Параметры для изменения номера порта в этом примере необходимы только в случае, если требуется изменить порт по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="be590-214">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

1. <span data-ttu-id="be590-215">В командной строке или в окне терминала, которые вы использовали ранее, перестройте JAR-файл, используя Maven, если вы внесли изменения в файл *pom.xml*; например:</span><span class="sxs-lookup"><span data-stu-id="be590-215">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="be590-216">Разверните веб-приложение в Azure с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="be590-216">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="be590-217">Maven выполнит развертывание веб-приложения в Azure; если веб-приложение еще не существует, оно будет создано.</span><span class="sxs-lookup"><span data-stu-id="be590-217">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="be590-218">Если при запуске развертывания в регионе, который задан в элементе `<region>` в файле *pom.xml*, нет достаточного количества доступных серверов, может появиться сообщение об ошибке, аналогичное приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="be590-218">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
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
> <span data-ttu-id="be590-219">В этом случае можно указать другой регион и повторно выполнить команду Maven для развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="be590-219">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="be590-220">После развертывания веб-приложения вы сможете управлять им с помощью [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="be590-220">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="be590-221">Веб-приложение будет указано в разделе **Службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="be590-221">Your web app will be listed in **App Services**:</span></span>

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* <span data-ttu-id="be590-223">URL-адрес веб-приложения будет указан в разделе **Обзор** для вашего веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="be590-223">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Определение URL-адреса для веб-приложения][AP02]

## <a name="next-steps"></a><span data-ttu-id="be590-225">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="be590-225">Next steps</span></span>

<span data-ttu-id="be590-226">Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="be590-226">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="be590-227">[Подключаемый модуль Maven для веб-приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="be590-227">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="be590-228">Вход в Azure из интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="be590-228">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="be590-229">Создание субъекта-службы Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be590-229">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="be590-230">Справочник по параметрам Maven</span><span class="sxs-lookup"><span data-stu-id="be590-230">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="be590-231">[Подключаемый модуль Docker для Maven]</span><span class="sxs-lookup"><span data-stu-id="be590-231">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[портал Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Подключаемый модуль Maven для веб-приложений Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service/containers/tutorial-custom-docker-image
[Docker]: https://www.docker.com/
[Подключаемый модуль Docker для Maven]: https://github.com/spotify/docker-maven-plugin
[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[Преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP02.png
[TL01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/TL01.png
