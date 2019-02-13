---
title: Развертывание веб-приложения Hello World, выполняющегося в контейнере Linux, в облаке с помощью набора средств Azure для IntelliJ
description: Запуск веб-приложения Hello World в контейнере Linux и его развертывание в облаке с помощью набора средств Azure для IntelliJ.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/20/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: fdff8dc2bd7a29473314d5c0bc99b7bcda369156
ms.sourcegitcommit: 54e7f077d694a5b1dd7fa6c8870b7d476af9829c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2019
ms.locfileid: "55648728"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="4d548-103">Развертывание веб-приложения Hello World в контейнере Linux в облаке с помощью набора средств Azure для IntelliJ</span><span class="sxs-lookup"><span data-stu-id="4d548-103">Deploy a Hello World web app to a Linux container in the cloud using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="4d548-104">Контейнеры [Docker] широко используются при развертывании веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="4d548-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="4d548-105">При этом разработчики могут объединить все зависимости и файлы проекта в одном пакете, а затем развернуть его на сервере.</span><span class="sxs-lookup"><span data-stu-id="4d548-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="4d548-106">Набор средств Azure для IntelliJ упрощает этот процесс для разработчиков на языке Java, предоставляя функции для развертывания контейнеров в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4d548-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="4d548-107">В этой статье показаны действия, необходимые для создания базового веб-приложения Hello World и его публикации в контейнере Linux в Azure с помощью набора средств Azure для IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="4d548-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* <span data-ttu-id="4d548-108">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="4d548-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="4d548-109">Для работы с этим руководством необходимо настроить [Docker], чтобы он имел возможность предоставить управляющую программу на порте 2375 без протокола TLS.</span><span class="sxs-lookup"><span data-stu-id="4d548-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="4d548-110">Этот параметр можно настроить при установке Docker или с помощью меню параметров Docker.</span><span class="sxs-lookup"><span data-stu-id="4d548-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Меню параметров Docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="4d548-112">Создание проекта веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4d548-112">Create a new web app project</span></span>

1. <span data-ttu-id="4d548-113">Запустите IntelliJ и войдите в свою учетную запись Azure, следуя инструкциям по [входу для набора средств Azure для IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="4d548-113">Start IntelliJ and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions) article.</span></span>

1. <span data-ttu-id="4d548-114">Щелкните меню **File** (Файл), выберите команду **New** (Создать), а затем — **Project** (Проект).</span><span class="sxs-lookup"><span data-stu-id="4d548-114">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Создание проекта][file-new-project]

1. <span data-ttu-id="4d548-116">В диалоговом окне **New Project** (Новый проект) выберите **Maven**, а затем **maven-archetype-webapp** и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="4d548-116">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Выбор веб-приложения архетипа Maven][maven-archetype-webapp]
   
1. <span data-ttu-id="4d548-118">Укажите значение **GroupId** (Идентификатор группы) и **ArtifactId** (Идентификатор артефакта) для веб-приложения и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="4d548-118">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Указание идентификатора группы и артефакта][groupid-and-artifactid]

1. <span data-ttu-id="4d548-120">Настройте любые параметры Maven или примите значения по умолчанию и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="4d548-120">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Указание параметров Maven][maven-options]

1. <span data-ttu-id="4d548-122">Укажите имя и расположение проекта, а затем щелкните **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="4d548-122">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Указание имени проекта][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="4d548-124">Создание реестра контейнеров Azure для использования в качестве частного реестра Docker</span><span class="sxs-lookup"><span data-stu-id="4d548-124">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="4d548-125">Ниже рассмотрена процедура использования портала Azure для создания реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="4d548-125">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="4d548-126">Если вы хотите использовать Azure CLI, а не портал Azure, выполните процедуру, описанную в статье [Создание частного реестра контейнеров Docker с помощью Azure CLI 2.0][Create Docker Registry using Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="4d548-126">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="4d548-127">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="4d548-127">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="4d548-128">После входа в свою учетную запись на портале Azure можно выполнить процедуру, описанную в статье [Создание частного реестра контейнеров Docker с помощью портала Azure], которую здесь полезно представить еще раз.</span><span class="sxs-lookup"><span data-stu-id="4d548-128">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="4d548-129">Щелкните значок меню **+ Создать ресурс**, а затем последовательно выберите **Контейнеры** и **Реестр контейнеров**.</span><span class="sxs-lookup"><span data-stu-id="4d548-129">Click the menu icon for **+ Create a resource**, then click **Containers**, and then click **Container Registry**.</span></span>
   
   ![Создание нового реестра контейнеров Azure][create-container-registry-01]

1. <span data-ttu-id="4d548-131">При появлении страницы **Создать реестр контейнеров** введите данные в поля **Имя реестра** и **Группа ресурсов**, выберите **Включить** для параметра **Пользователь-администратор** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="4d548-131">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Настройка параметров реестра контейнеров Azure][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="4d548-133">Развертывание веб-приложения в контейнере Docker</span><span class="sxs-lookup"><span data-stu-id="4d548-133">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="4d548-134">Щелкните правой кнопкой мыши проект в обозревателе проектов, выберите **Azure**, а затем — **Add Docker Support** (Добавление поддержки Docker).</span><span class="sxs-lookup"><span data-stu-id="4d548-134">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="4d548-135">Файл Docker будет автоматически создан с конфигурацией по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4d548-135">This will automatically create a Docker file with a default configuration.</span></span>

   ![Добавление поддержки Docker][add-docker-support]

1. <span data-ttu-id="4d548-137">Добавив поддержку Docker, щелкните проект правой кнопкой мыши в обозревателе проектов, выберите **Azure**, а затем — **Run on Web App for Containers** (Выполнить в веб-приложении для контейнеров).</span><span class="sxs-lookup"><span data-stu-id="4d548-137">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Run on Web App for Containers**.</span></span>

   ![Выполнение в веб-приложении для контейнеров][run-on-web-app-for-containers]

1. <span data-ttu-id="4d548-139">Когда отобразится диалоговое окно **Run on Web App for Containers** (Выполнение в веб-приложении для контейнеров), введите необходимые сведения:</span><span class="sxs-lookup"><span data-stu-id="4d548-139">When the **Run on Web App for Containers** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="4d548-140">**Имя.** Понятное имя, отображаемое в наборе средств Azure.</span><span class="sxs-lookup"><span data-stu-id="4d548-140">**Name**: This specifies the friendly name which is displayed in the Azure Toolkit.</span></span> 

   * <span data-ttu-id="4d548-141">**Container Registry** (Реестр контейнеров). Выберите в раскрывающемся меню реестр контейнеров, который вы создали в предыдущем разделе этой статьи.</span><span class="sxs-lookup"><span data-stu-id="4d548-141">**Container Registry**: Choose the container registry from the drop-down menu that you created in the previous section of this article.</span></span> <span data-ttu-id="4d548-142">Поля **Server URL** (URL-адрес сервера), **Username** (Имя пользователя) и **Password** (Пароль) будут заполнены автоматически.</span><span class="sxs-lookup"><span data-stu-id="4d548-142">The fields for **Server URL**, **Username**, and **Password** will be automatically populated.</span></span>

   * <span data-ttu-id="4d548-143">**Image and tag** (Образ и тег). Имя образа контейнера. Обычно используется следующий синтаксис: *registry*.azurecr.io/*appname*:latest, где:</span><span class="sxs-lookup"><span data-stu-id="4d548-143">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="4d548-144">*registry* — это реестр контейнеров из предыдущего раздела этой статьи;</span><span class="sxs-lookup"><span data-stu-id="4d548-144">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="4d548-145">*appname* — это имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="4d548-145">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="4d548-146">**Use Existing Web App** (Использовать существующее веб-приложение) или **Create New Web App** (Создать веб-приложение). Указывает, будете ли вы развертывать контейнер в существующем веб-приложении или создадите новое.</span><span class="sxs-lookup"><span data-stu-id="4d548-146">**Use Existing Web App** or **Create New Web App**: Specifies whether you will deploy your container to an existing web app or create a new web app.</span></span> <span data-ttu-id="4d548-147">С помощью указанного вами **имени приложения** будет создан URL-адрес для вашего веб-приложения, например: *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="4d548-147">The **App name** that you specify will create the URL for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   * <span data-ttu-id="4d548-148">**Группа ресурсов**. Указывает, создадите ли вы группу ресурсов или будете использовать существующую.</span><span class="sxs-lookup"><span data-stu-id="4d548-148">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="4d548-149">**App Service Plan** (План службы приложений). Указывает, создадите ли вы план службы приложений или будете использовать существующий.</span><span class="sxs-lookup"><span data-stu-id="4d548-149">**App Service Plan**: Specifies whether you will use an existing or create a new app service plan.</span></span> 

   ![Выполнение в веб-приложении для контейнеров][run-on-web-app-linux]

1. <span data-ttu-id="4d548-151">Настроив перечисленные выше параметры, нажмите кнопку **Run** (Выполнить).</span><span class="sxs-lookup"><span data-stu-id="4d548-151">When you have finished configuring the settings listed above, click **Run**.</span></span> <span data-ttu-id="4d548-152">После успешного развертывания веб-приложения его состояние будет отображаться в окне **Run** (Выполнение).</span><span class="sxs-lookup"><span data-stu-id="4d548-152">When your web app has been successfully deployed, the status will be displayed in the **Run** window.</span></span>

   ![Веб-приложение успешно развернуто][successfully-deployed]

1. <span data-ttu-id="4d548-154">После публикации веб-приложения вы можете перейти к указанному для него ранее URL-адресу, например *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="4d548-154">After your web app has been published, you can browse to the URL that specifed earlier for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   ![Переход к веб-приложению][browsing-to-web-app]

## <a name="optional-modify-your-web-app-publish-settings"></a><span data-ttu-id="4d548-156">Необязательно: Изменение параметров для публикации веб-приложения</span><span class="sxs-lookup"><span data-stu-id="4d548-156">Optional: Modify your web app publish settings</span></span>

1. <span data-ttu-id="4d548-157">После публикации веб-приложения параметры будут сохранены в качестве параметров по умолчанию. Приложение можно запустить в Azure, щелкнув значок зеленой стрелки на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="4d548-157">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="4d548-158">Вы можете изменить параметры, щелкнув раскрывающееся меню для веб-приложения, а затем — **Edit Configurations** (Изменить конфигурации).</span><span class="sxs-lookup"><span data-stu-id="4d548-158">You can modify these settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Пункт меню Edit configuration (Изменить конфигурацию)][edit-configuration-menu]

1. <span data-ttu-id="4d548-160">При отображении диалогового окна **Run/Debug Configurations** (Конфигурации выполнения и отладки) можно изменить любые параметры по умолчанию, а затем нажать кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4d548-160">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Диалоговое окно Edit configuration (Изменение конфигурации)][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="4d548-162">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="4d548-162">Next steps</span></span>

<span data-ttu-id="4d548-163">Дополнительные материалы по Docker доступны на официальном [веб-сайте Docker][Docker].</span><span class="sxs-lookup"><span data-stu-id="4d548-163">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[портал Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Создание частного реестра контейнеров Docker с помощью портала Azure]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-intellij-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
