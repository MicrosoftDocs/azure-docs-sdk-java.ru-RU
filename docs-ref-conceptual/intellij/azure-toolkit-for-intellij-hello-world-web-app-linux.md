---
title: "Запуск веб-приложения Hello World в контейнере Linux с помощью набора средств Azure для IntelliJ"
description: "Узнайте, как создать базовое веб-приложение Hello World в контейнере Linux и опубликовать его в Azure с помощью набора средств Azure для IntelliJ."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm
ms.openlocfilehash: c3c6339bb5a8415854253701d0ac340d42587509
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/24/2017
---
# <a name="run-a-hello-world-web-app-in-a-linux-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="32127-103">Запуск веб-приложения Hello World в контейнере Linux с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="32127-103">Run a Hello World web app in a Linux container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="32127-104">Контейнеры [Docker] широко используются при развертывании веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="32127-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="32127-105">При этом разработчики могут объединить все зависимости и файлы проекта в одном пакете, а затем развернуть его на сервере.</span><span class="sxs-lookup"><span data-stu-id="32127-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="32127-106">Набор средств Azure для IntelliJ упрощает этот процесс для разработчиков на языке Java, предоставляя функции для развертывания контейнеров в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="32127-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="32127-107">В этой статье показаны действия, необходимые для создания базового веб-приложения Hello World и его публикации в контейнере Linux в Azure с помощью набора средств Azure для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="32127-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* <span data-ttu-id="32127-108">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="32127-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="32127-109">Для работы с этим руководством необходимо настроить [Docker], чтобы он имел возможность предоставить управляющую программу на порте 2375 без протокола TLS.</span><span class="sxs-lookup"><span data-stu-id="32127-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="32127-110">Этот параметр можно настроить при установке Docker или с помощью меню параметров Docker.</span><span class="sxs-lookup"><span data-stu-id="32127-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Меню параметров Docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="32127-112">Создание проекта веб-приложения</span><span class="sxs-lookup"><span data-stu-id="32127-112">Create a new web app project</span></span>

1. <span data-ttu-id="32127-113">Запустите IntelliJ и войдите в свою учетную запись Azure, следуя инструкциям из статьи "Инструкции по входу для набора средств Azure для IntelliJ".</span><span class="sxs-lookup"><span data-stu-id="32127-113">Start IntelliJ and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="32127-114">Щелкните меню **File** (Файл), выберите команду **New** (Создать), а затем — **Project** (Проект).</span><span class="sxs-lookup"><span data-stu-id="32127-114">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Создание проекта][file-new-project]

1. <span data-ttu-id="32127-116">В диалоговом окне **New Project** (Новый проект) выберите **Maven**, а затем **maven-archetype-webapp** и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="32127-116">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Выбор веб-приложения архетипа Maven][maven-archetype-webapp]
   
1. <span data-ttu-id="32127-118">Укажите значение **GroupId** (Идентификатор группы) и **ArtifactId** (Идентификатор артефакта) для веб-приложения и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="32127-118">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Указание идентификатора группы и артефакта][groupid-and-artifactid]

1. <span data-ttu-id="32127-120">Настройте любые параметры Maven или примите значения по умолчанию и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="32127-120">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Указание параметров Maven][maven-options]

1. <span data-ttu-id="32127-122">Укажите имя и расположение проекта, а затем щелкните **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="32127-122">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Указание имени проекта][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="32127-124">Создание реестра контейнеров Azure для использования в качестве частного реестра Docker</span><span class="sxs-lookup"><span data-stu-id="32127-124">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="32127-125">Ниже рассмотрена процедура использования портала Azure для создания реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="32127-125">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="32127-126">Если вы хотите использовать Azure CLI, а не портал Azure, выполните процедуру, описанную в статье [Создание частного реестра контейнеров Docker с помощью Azure CLI 2.0][Create Docker Registry using Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="32127-126">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="32127-127">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="32127-127">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="32127-128">После входа в свою учетную запись на портале Azure можно выполнить процедуру, описанную в статье [Создание частного реестра контейнеров Docker с помощью портала Azure], которую здесь полезно представить еще раз.</span><span class="sxs-lookup"><span data-stu-id="32127-128">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="32127-129">Щелкните значок меню **+ Создать**, нажмите кнопку **Контейнеры**, а затем нажмите кнопку **Реестр контейнеров Azure**.</span><span class="sxs-lookup"><span data-stu-id="32127-129">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Создание нового реестра контейнеров Azure][AR01]

1. <span data-ttu-id="32127-131">При появлении страницы сведений о шаблоне реестра контейнеров Azure нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="32127-131">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Создание нового реестра контейнеров Azure][AR02]

1. <span data-ttu-id="32127-133">При появлении страницы **Создать реестр контейнеров** введите данные в поля **Имя реестра** и **Группа ресурсов**, выберите **Включить** для параметра **Пользователь-администратор** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="32127-133">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Настройка параметров реестра контейнеров Azure][AR03]

1. <span data-ttu-id="32127-135">После создания реестра контейнеров перейдите в реестр контейнеров на портале Azure и нажмите кнопку **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="32127-135">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="32127-136">Запишите имя пользователя и пароль для последующих шагов.</span><span class="sxs-lookup"><span data-stu-id="32127-136">Take note of the username and password for the next steps.</span></span>

   ![Ключи доступа к реестру контейнеров Azure][AR04]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="32127-138">Развертывание веб-приложения в контейнере Docker</span><span class="sxs-lookup"><span data-stu-id="32127-138">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="32127-139">Щелкните правой кнопкой мыши проект в обозревателе проектов, выберите **Azure**, а затем — **Add Docker Support** (Добавление поддержки Docker).</span><span class="sxs-lookup"><span data-stu-id="32127-139">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="32127-140">Файл Docker будет автоматически создан с конфигурацией по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="32127-140">This will automatically create a Docker file with a default configuration.</span></span>

   ![Добавление поддержки Docker][add-docker-support]

1. <span data-ttu-id="32127-142">Добавив поддержку Docker, щелкните правой кнопкой мыши проект в обозревателе проектов, выберите **Azure**, а затем — **Run on Web App (Linux)** (Выполнить веб-приложение (Linux)).</span><span class="sxs-lookup"><span data-stu-id="32127-142">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Run on Web App (Linux)**.</span></span>

   ![Выполнение веб-приложения (Linux)][run-on-web-app-linux]

1. <span data-ttu-id="32127-144">Когда отобразится диалоговое окно **Run on Web App (Linux)** (Выполнение веб-приложения (Linux)), введите необходимые сведения:</span><span class="sxs-lookup"><span data-stu-id="32127-144">When the **Run on Web App (Linux)** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="32127-145">**Name** (Имя) — понятное имя, отображаемое в наборе средств Azure.</span><span class="sxs-lookup"><span data-stu-id="32127-145">**Name**: This specifies the friendly name which is displayed in the Azure Toolkit.</span></span> 

   * <span data-ttu-id="32127-146">**Server URL** (URL-адрес сервера) — URL-адрес реестра контейнеров из предыдущего раздела этой статьи. Обычно используется следующий синтаксис *registry*.azurecr.io.</span><span class="sxs-lookup"><span data-stu-id="32127-146">**Server URL**: This specifies the URL for your container registry from the previous section of this article; typically this will use the following syntax: "*registry*.azurecr.io".</span></span> 

   * <span data-ttu-id="32127-147">**Username** (Имя пользователя) и **Password** (Пароль) — ключи доступа для реестра контейнеров из предыдущего раздела этой статьи.</span><span class="sxs-lookup"><span data-stu-id="32127-147">**Username** and **Password**: Specifies the access keys for your container registry from the previous section of this article.</span></span> 

   * <span data-ttu-id="32127-148">**Image and tag** (Образ и тег) — название образа контейнера. Обычно используется следующий синтаксис: *registry*.azurecr.io/*appname*:latest, где:</span><span class="sxs-lookup"><span data-stu-id="32127-148">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="32127-149">*registry* — это реестр контейнеров из предыдущего раздела этой статьи;</span><span class="sxs-lookup"><span data-stu-id="32127-149">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="32127-150">*appname* — это имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="32127-150">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="32127-151">**Use Existing Web App** (Использовать имеющееся веб-приложение) или **Create New Web App** (Создать веб-приложение) — указывает, будете ли вы развертывать контейнер в имеющемся веб-приложении или создадите веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="32127-151">**Use Existing Web App** or **Create New Web App**: Specifies whether you will deploy your container to an existing web app or create a new web app.</span></span> 

   * <span data-ttu-id="32127-152">**Resource Group** (Группа ресурсов) — указывает, создадите ли вы группу ресурсов или будете использовать имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="32127-152">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="32127-153">**App Service Plan** (План службы приложений) — указывает, создадите ли вы план службы приложений или будете использовать имеющийся.</span><span class="sxs-lookup"><span data-stu-id="32127-153">**App Service Plan**: Specifies whether you willuse an existing or create a new app service plan.</span></span> 

1. <span data-ttu-id="32127-154">Настроив перечисленные выше параметры, нажмите кнопку **Run** (Выполнить).</span><span class="sxs-lookup"><span data-stu-id="32127-154">When you have finished configuring the settings listed above, click **Run**.</span></span>

   ![Создание веб-приложения][create-web-app]

1. <span data-ttu-id="32127-156">После публикации веб-приложения параметры будут сохранены в качестве параметров по умолчанию. Приложение можно запустить в Azure, щелкнув значок зеленой стрелки на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="32127-156">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="32127-157">Вы можете изменить параметры, щелкнув раскрывающееся меню для веб-приложения, а затем — **Edit Configurations** (Изменить конфигурации).</span><span class="sxs-lookup"><span data-stu-id="32127-157">You can modify these settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Пункт меню Edit configuration (Изменить конфигурацию)][edit-configuration-menu]

1. <span data-ttu-id="32127-159">При отображении диалогового окна **Run/Debug Configurations** (Конфигурации выполнения и отладки) можно изменить любые параметры по умолчанию, а затем нажать кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="32127-159">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Диалоговое окно Edit configuration (Изменение конфигурации)][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="32127-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32127-161">Next steps</span></span>

<span data-ttu-id="32127-162">Дополнительные материалы по Docker доступны на официальном [веб-сайте Docker][Docker].</span><span class="sxs-lookup"><span data-stu-id="32127-162">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[портал Azure]: https://portal.azure.com/
[Создание частного реестра контейнеров Docker с помощью портала Azure]: /azure/container-registry/container-registry-get-started-portal
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[AR01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR01.png
[AR02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR02.png
[AR03]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR03.png
[AR04]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR04.png

[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[create-web-app]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-web-app.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
