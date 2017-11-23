---
title: "Развертывание приложения Spring Boot в реестре контейнеров Azure в службе приложений Azure с помощью подключаемого модуля Maven для веб-приложений Azure"
description: "В этом руководстве представлен порядок развертывания приложения Spring Boot в реестре контейнеров Azure в службе приложений Azure с помощью подключаемого модуля Maven."
services: container-registry
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Maven
ms.assetid: 
ms.service: multiple
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 548c294bd576b00b62994c09d82ec21ad72f4dbd
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a><span data-ttu-id="9a3e9-104">Развертывание приложения Spring Boot в реестре контейнеров Azure в службе приложений Azure с помощью подключаемого модуля Maven для веб-приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9a3e9-104">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app in Azure Container Registry to Azure App Service</span></span>

<span data-ttu-id="9a3e9-105">**[Spring Framework]** — это популярная платформа с открытым кодом, которая помогает Java-разработчикам создавать мобильные приложения, веб-приложения и приложения API.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-105">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="9a3e9-106">В этом руководстве для удобства используется пример приложения, созданный с помощью [Spring Boot] — подхода к использованию Spring на основе соглашений.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-106">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="9a3e9-107">В этой статье демонстрируется, как развернуть пример приложения Spring Boot в реестре контейнера Azure, а затем использовать подключаемый модуль Maven для веб-приложений Azure для развертывания приложения в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-107">This article demonstrates how to deploy a sample Spring Boot application to Azure Container Registry, and then use the Maven Plugin for Azure Web Apps to deploy your application to Azure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9a3e9-108">Подключаемый модуль Maven для веб-приложений Azure в настоящее время доступен в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-108">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="9a3e9-109">Сейчас поддерживается только FTP-публикация, но на будущее запланированы дополнительные функции.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-109">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="9a3e9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9a3e9-110">Prerequisites</span></span>

<span data-ttu-id="9a3e9-111">Для работы с этим руководством требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-111">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="9a3e9-112">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="9a3e9-112">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="9a3e9-113">[Интерфейс командной строки Azure (CLI)].</span><span class="sxs-lookup"><span data-stu-id="9a3e9-113">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="9a3e9-114">Актуальный [пакет разработчиков Java (JDK)] версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-114">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="9a3e9-115">Средство сборки [Maven] (версия 3) от Apache.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-115">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="9a3e9-116">Клиент [Git].</span><span class="sxs-lookup"><span data-stu-id="9a3e9-116">A [Git] client.</span></span>
* <span data-ttu-id="9a3e9-117">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="9a3e9-117">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9a3e9-118">С учетом требований виртуализации для этого руководства изложенные здесь инструкции нельзя выполнять на виртуальной машине. Необходимо использовать физический компьютер с включенными функциями виртуализации.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-118">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="9a3e9-119">Клонирование примера "Приложение Spring Boot в веб-приложении Docker"</span><span class="sxs-lookup"><span data-stu-id="9a3e9-119">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="9a3e9-120">В этом разделе представлены сведения о клонировании контейнерного приложения Spring Boot и его тестировании на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-120">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="9a3e9-121">Откройте командную строку или окно терминала и создайте локальный каталог для размещения приложения Spring Boot, после чего перейдите в этот каталог, например:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-121">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="9a3e9-122">-- или --</span><span class="sxs-lookup"><span data-stu-id="9a3e9-122">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="9a3e9-123">Клонируйте образец проекта [Spring Boot on Docker Getting Started] (Запуск Spring Boot в Docker) в созданный каталог, например:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-123">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="9a3e9-124">Перейдите в каталог готового проекта, например:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-124">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="9a3e9-125">Выполните сборку файла JAR с помощью Maven, например:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-125">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="9a3e9-126">При создании веб-приложения запустите веб-приложение с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-126">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="9a3e9-127">Проверьте веб-приложение, перейдя к нему локально с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-127">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="9a3e9-128">Например, если имеется Curl, можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-128">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="9a3e9-129">Должно появиться следующее сообщение: **Hello Docker World**.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-129">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Локальный просмотр образца приложения][SB01]

> [!NOTE]
>
> <span data-ttu-id="9a3e9-131">При локальном использовании Docker может появиться сообщение об ошибке подключения к локальному компьютеру через порт 2375.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-131">When you are using Docker locally, you may see an error which states that you cannot connect to localhost on port 2375.</span></span> <span data-ttu-id="9a3e9-132">В этом случае попробуйте использовать Docker локально без TLS.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-132">If this happens, you may need to enable using Docker locally without TLS.</span></span> <span data-ttu-id="9a3e9-133">Для этого откройте параметры Docker и **предоставьте управляющую программу Docker для TCP://localhost:2375 без TLS**.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-133">To do so, open your Docker settings and check the option to **Expose Docker Daemon on TCP://localhost:2375 without TLS**.</span></span>
>
> ![Предоставление управляющей программы Docker для локального TCP-порта 2375][TL01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="9a3e9-135">Создание субъекта-службы Azure</span><span class="sxs-lookup"><span data-stu-id="9a3e9-135">Create an Azure service principal</span></span>

<span data-ttu-id="9a3e9-136">В этом разделе представлен порядок создания субъекта-службы Azure, которого подключаемый модуль Maven использует при развертывании контейнера в Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-136">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="9a3e9-137">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-137">Open a command prompt.</span></span>

1. <span data-ttu-id="9a3e9-138">Войдите в учетную запись Azure с помощью интерфейса командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-138">Sign into your Azure account by using the Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="9a3e9-139">Для завершения процесса входа следуйте инструкциям.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-139">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="9a3e9-140">Создайте субъект-службу Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-140">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="9a3e9-141">Где `uuuuuuuu` — это имя пользователя и `pppppppp` — пароль для субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-141">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="9a3e9-142">В ответ Azure предоставит код JSON, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-142">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="9a3e9-143">При настройке подключаемого модуля Maven для развертывания контейнера в Azure используйте значения из этого ответа JSON.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-143">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="9a3e9-144">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` и `tttttttt` являются значениями заполнителя, которые используются в этом примере с целью упростить сопоставление этих значений с соответствующими им элементами во время настройки файла Maven `settings.xml` в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-144">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="9a3e9-145">Создание реестра контейнеров Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9a3e9-145">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="9a3e9-146">Откройте окно командной строки.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-146">Open a command prompt.</span></span>

1. <span data-ttu-id="9a3e9-147">Войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-147">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="9a3e9-148">Создайте группу ресурсов Azure, используемых в этой статье.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-148">Create a resource group for the Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="9a3e9-149">Замените `wingtiptoysresources` в этом примере уникальным именем для группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-149">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="9a3e9-150">Создайте частный реестр контейнеров Azure в группе ресурсов для приложения Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-150">Create a private Azure container registry in the resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="9a3e9-151">Замените `wingtiptoysregistry` в этом примере уникальным именем для реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-151">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="9a3e9-152">Получите пароль для реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-152">Retrieve the password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="9a3e9-153">В ответ Azure предоставит пароль, например:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-153">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a><span data-ttu-id="9a3e9-154">Добавление реестра контейнеров Azure и субъекта-службы Azure в настройки Maven</span><span class="sxs-lookup"><span data-stu-id="9a3e9-154">Add your Azure container registry and Azure service principal to your Maven settings</span></span>

1. <span data-ttu-id="9a3e9-155">Откройте файл Maven `settings.xml` в текстовом редакторе; этот файл может находиться по пути, аналогичному указанному в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-155">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="9a3e9-156">Добавьте параметры доступа к реестру контейнеров Azure из предыдущего раздела этой статьи в коллекцию `<servers>` в файле *settings.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-156">Add your Azure Container Registry access settings from the previous section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="9a3e9-157">Описание</span><span class="sxs-lookup"><span data-stu-id="9a3e9-157">Where:</span></span>
   <span data-ttu-id="9a3e9-158">Элемент</span><span class="sxs-lookup"><span data-stu-id="9a3e9-158">Element</span></span> | <span data-ttu-id="9a3e9-159">Описание</span><span class="sxs-lookup"><span data-stu-id="9a3e9-159">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="9a3e9-160">Содержит имя закрытого реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-160">Contains the name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="9a3e9-161">Содержит имя закрытого реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-161">Contains the name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="9a3e9-162">Содержит пароль, полученный в предыдущем разделе этой статьи.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-162">Contains the password you retrieved in the previous section of this article.</span></span>

1. <span data-ttu-id="9a3e9-163">Добавьте параметры субъекта-службы Azure из раздела выше этой статьи в коллекцию `<servers>` в файле *settings.xml*, например:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-163">Add your Azure service principal settings from an earlier section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="9a3e9-164">Описание</span><span class="sxs-lookup"><span data-stu-id="9a3e9-164">Where:</span></span>
   <span data-ttu-id="9a3e9-165">Элемент</span><span class="sxs-lookup"><span data-stu-id="9a3e9-165">Element</span></span> | <span data-ttu-id="9a3e9-166">Описание</span><span class="sxs-lookup"><span data-stu-id="9a3e9-166">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="9a3e9-167">Задает уникальное имя, которое Maven использует для поиска параметров безопасности при развертывании веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-167">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="9a3e9-168">Содержит значение `appId` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-168">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="9a3e9-169">Содержит значение `tenant` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-169">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="9a3e9-170">Содержит значение `password` из субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-170">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="9a3e9-171">Определяет целевую облачную среду Azure, которой в этом примере является `AZURE`.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-171">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="9a3e9-172">(Полный список сред см. в документации по [подключаемому модулю Maven для веб-приложений Azure].)</span><span class="sxs-lookup"><span data-stu-id="9a3e9-172">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="9a3e9-173">Сохраните и закройте файл *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-173">Save and close the *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a><span data-ttu-id="9a3e9-174">Сборка образа контейнера Docker и его передача в реестр контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="9a3e9-174">Build your Docker container image and push it to your Azure container registry</span></span>

1. <span data-ttu-id="9a3e9-175">Перейдите в каталог завершенного проекта для приложения Spring Boot (например, "*C:\SpringBoot\gs-spring-boot-docker\complete*" или "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") и откройте файл *pom.xml* в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-175">Navigate to the completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="9a3e9-176">Обновите коллекцию `<properties>` в файле *pom.xml*, добавив значение сервера входа для реестра контейнеров Azure из предыдущего раздела данного учебника, например:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-176">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="9a3e9-177">Описание</span><span class="sxs-lookup"><span data-stu-id="9a3e9-177">Where:</span></span>
   <span data-ttu-id="9a3e9-178">Элемент</span><span class="sxs-lookup"><span data-stu-id="9a3e9-178">Element</span></span> | <span data-ttu-id="9a3e9-179">Описание</span><span class="sxs-lookup"><span data-stu-id="9a3e9-179">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="9a3e9-180">Задает имя закрытого реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-180">Specifies the name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="9a3e9-181">Задает URL-адрес закрытого реестра контейнеров Azure, который сформирован путем добавления ".azurecr.io" к имени закрытого реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-181">Specifies the URL of your private Azure container registry, which is derived by appending ".azurecr.io" to the name of your private container registry.</span></span>

1. <span data-ttu-id="9a3e9-182">Убедитесь, что в элементе `<plugin>` для подключаемого модуля Docker в файле *pom.xml* содержатся необходимые свойства для адреса сервера входа и имя реестра из предыдущего шага в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-182">Verify that `<plugin>` for the Docker plugin in your *pom.xml* file contains the correct properties for the login server address and registry name from the previous step in this tutorial.</span></span> <span data-ttu-id="9a3e9-183">Например:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-183">For example:</span></span>

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
   <span data-ttu-id="9a3e9-184">Описание</span><span class="sxs-lookup"><span data-stu-id="9a3e9-184">Where:</span></span>
   <span data-ttu-id="9a3e9-185">Элемент</span><span class="sxs-lookup"><span data-stu-id="9a3e9-185">Element</span></span> | <span data-ttu-id="9a3e9-186">Описание</span><span class="sxs-lookup"><span data-stu-id="9a3e9-186">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="9a3e9-187">Задает свойство, которое содержит имя закрытого реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-187">Specifies the property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="9a3e9-188">Задает свойство, которое содержит URL-адрес закрытого реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-188">Specifies the property which contains the URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="9a3e9-189">Перейдите в каталог завершенного проекта для приложения Spring Boot и выполните команду ниже для перестроения приложения и отправки контейнера в реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-189">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="9a3e9-190">НЕОБЯЗАТЕЛЬНО. Перейдите на [портал Azure] и убедитесь, что в реестре контейнеров имеется образ контейнера Docker с именем **gs-spring-boot-docker**.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-190">OPTIONAL: Browse to the [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Проверка контейнера на портале Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a><span data-ttu-id="9a3e9-192">Настройка файла pom.xml и последующие построение и развертывание контейнера в Azure</span><span class="sxs-lookup"><span data-stu-id="9a3e9-192">Customize your pom.xml, then build and deploy your container to Azure</span></span>

<span data-ttu-id="9a3e9-193">Откройте файл `pom.xml` для приложения Spring Boot в текстовом редакторе, а затем найдите элемент `<plugin>` для `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-193">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="9a3e9-194">Этот элемент должен выглядеть примерно следующим образом.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-194">This element should resemble the following example:</span></span>

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

<span data-ttu-id="9a3e9-195">Существует несколько значений, которые можно изменить для подключаемого модуля Maven. Подробное описание каждого из этих элементов см. в документации по [подключаемому модулю Maven для веб-приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="9a3e9-195">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="9a3e9-196">Существует ряд значений, на которые следует обратить внимание в этой статье.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-196">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="9a3e9-197">Элемент</span><span class="sxs-lookup"><span data-stu-id="9a3e9-197">Element</span></span> | <span data-ttu-id="9a3e9-198">Описание</span><span class="sxs-lookup"><span data-stu-id="9a3e9-198">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="9a3e9-199">Версия [подключаемому модулю Maven для веб-приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="9a3e9-199">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="9a3e9-200">Обратитесь к списку версий в [центральном репозитории Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22), чтобы убедиться, что вы используете актуальную версию.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-200">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="9a3e9-201">Сведения для проверки подлинности для Azure, в которых в данном примере содержится элемент `<serverId>`, который, в свою очередь, содержит `azure-auth`; Maven использует это значение для поиска значений субъекта-службы Azure в файле Maven *settings.xml*, который вы определили в предыдущем разделе этой статьи.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-201">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="9a3e9-202">Целевая группа ресурсов, которой в этом примере является `wingtiptoysresources`.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-202">Specifies the target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="9a3e9-203">Если эта группа ресурсов не существует, она будет создана во время развертывания.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-203">The resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="9a3e9-204">Целевое имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-204">Specifies the target name for your web app.</span></span> <span data-ttu-id="9a3e9-205">В этом примере целевое имя — `maven-linux-app-${maven.build.timestamp}`, к которому в этом примере добавлен суффикс `${maven.build.timestamp}`, чтобы избежать конфликтов.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-205">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="9a3e9-206">(Метку времени добавлять необязательно; можно указать любую уникальную строку для имени приложения.)</span><span class="sxs-lookup"><span data-stu-id="9a3e9-206">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="9a3e9-207">Целевой регион, которым в данном примере является `westus`.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-207">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="9a3e9-208">(Полный список см. в документации по [подключаемому модулю Maven для веб-приложений Azure].)</span><span class="sxs-lookup"><span data-stu-id="9a3e9-208">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="9a3e9-209">Свойства, которые содержат имя и URL-адрес контейнера.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-209">Specifies the properties which contain the name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="9a3e9-210">Любые уникальные настройки для Maven, которые следует использовать при развертывании веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-210">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="9a3e9-211">В этом примере элемент `<property>` содержит пару "имя/значение" дочерних элементов, которая задает порт для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-211">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9a3e9-212">Параметры для изменения номера порта в этом примере необходимы только в случае, если требуется изменить порт по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-212">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

1. <span data-ttu-id="9a3e9-213">В командной строке или в окне терминала, которые вы использовали ранее, перестройте JAR-файл, используя Maven, если вы внесли изменения в файл *pom.xml*; например:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-213">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="9a3e9-214">Разверните веб-приложение в Azure с помощью Maven; например:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-214">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="9a3e9-215">Maven выполнит развертывание веб-приложения в Azure; если веб-приложение еще не существует, оно будет создано.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-215">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9a3e9-216">Если при запуске развертывания в регионе, который задан в элементе `<region>` в файле *pom.xml*, нет достаточного количества доступных серверов, может появиться сообщение об ошибке, аналогичное приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-216">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
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
> <span data-ttu-id="9a3e9-217">В этом случае можно указать другой регион и повторно выполнить команду Maven для развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-217">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="9a3e9-218">После развертывания веб-приложения вы сможете управлять им с помощью [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="9a3e9-218">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="9a3e9-219">Веб-приложение будет указано в разделе **Службы приложений**:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-219">Your web app will be listed in **App Services**:</span></span>

   ![Веб-приложение в разделе "Службы приложений" на портале Azure][AP01]

* <span data-ttu-id="9a3e9-221">URL-адрес веб-приложения будет указан в разделе **Обзор** для вашего веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="9a3e9-221">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Определение URL-адреса для веб-приложения][AP02]

## <a name="next-steps"></a><span data-ttu-id="9a3e9-223">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a3e9-223">Next steps</span></span>

<span data-ttu-id="9a3e9-224">Дополнительные сведения о различных технологиях, рассматриваемых в данной статье, см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="9a3e9-224">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="9a3e9-225">[подключаемому модулю Maven для веб-приложений Azure]</span><span class="sxs-lookup"><span data-stu-id="9a3e9-225">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="9a3e9-226">Вход в Azure из интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="9a3e9-226">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="9a3e9-227">Создание субъекта-службы Azure с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9a3e9-227">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="9a3e9-228">Справочник по параметрам Maven</span><span class="sxs-lookup"><span data-stu-id="9a3e9-228">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="9a3e9-229">[Подключаемый модуль Docker для Maven]</span><span class="sxs-lookup"><span data-stu-id="9a3e9-229">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Интерфейс командной строки Azure (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[портал Azure]: https://portal.azure.com/
[подключаемому модулю Maven для веб-приложений Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service/containers/tutorial-custom-docker-image
[Docker]: https://www.docker.com/
[Подключаемый модуль Docker для Maven]: https://github.com/spotify/docker-maven-plugin
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP02.png
[TL01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/TL01.png
