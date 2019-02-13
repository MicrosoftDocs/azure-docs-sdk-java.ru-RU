---
title: Развертывание веб-приложения Hello World, выполняющегося в контейнере Linux, в облаке с помощью Azure Toolkit for Eclipse
description: Запустите базовое веб-приложение Hello World в контейнере Linux и разверните его в облаке с помощью Azure Toolkit for Eclipse.
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
ms.openlocfilehash: 799f21a282956f9a88aa35743157fc1292197569
ms.sourcegitcommit: 54e7f077d694a5b1dd7fa6c8870b7d476af9829c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/02/2019
ms.locfileid: "55649250"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="6edfc-103">Развертывание веб-приложения Hello World в контейнере Linux в облаке с помощью Azure Toolkit for Eclipse</span><span class="sxs-lookup"><span data-stu-id="6edfc-103">Deploy a Hello World web app to a Linux container in the cloud using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="6edfc-104">Контейнеры [Docker] широко используются при развертывании веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="6edfc-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="6edfc-105">При этом разработчики могут объединить все зависимости и файлы проекта в одном пакете, а затем развернуть его на сервере.</span><span class="sxs-lookup"><span data-stu-id="6edfc-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="6edfc-106">Набор средств Azure Toolkit for Eclipse упрощает этот процесс для разработчиков на языке Java, предоставляя функции для развертывания контейнеров в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6edfc-106">The Azure Toolkit for Eclipse simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="6edfc-107">В этой статье показаны действия, необходимые для создания базового веб-приложения Hello World и его публикации в контейнере Linux в Azure с помощью Azure Toolkit for Eclipse.</span><span class="sxs-lookup"><span data-stu-id="6edfc-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]
* <span data-ttu-id="6edfc-108">Клиент [Docker].</span><span class="sxs-lookup"><span data-stu-id="6edfc-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="6edfc-109">Для работы с этим руководством необходимо настроить [Docker], чтобы он имел возможность предоставить управляющую программу на порте 2375 без протокола TLS.</span><span class="sxs-lookup"><span data-stu-id="6edfc-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="6edfc-110">Этот параметр можно настроить при установке Docker или с помощью меню параметров Docker.</span><span class="sxs-lookup"><span data-stu-id="6edfc-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Меню параметров Docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="6edfc-112">Создание проекта веб-приложения</span><span class="sxs-lookup"><span data-stu-id="6edfc-112">Create a new web app project</span></span>

1. <span data-ttu-id="6edfc-113">Запустите Eclipse и войдите в свою учетную запись Azure, следуя [инструкциям по входу для Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="6edfc-113">Start Eclipse and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions) article.</span></span>

1. <span data-ttu-id="6edfc-114">Откройте меню **File** (Файл), выберите **New** (Создать), а затем — **Dynamic Web Project** (Динамический веб-проект).</span><span class="sxs-lookup"><span data-stu-id="6edfc-114">Click the **File** menu, then click **New**, and then click **Dynamic Web Project**.</span></span>
   
   ![Создание проекта][file-new-project]

1. <span data-ttu-id="6edfc-116">В диалоговом окне **New Dynamic Web Project** (Создание динамического веб-проекта) введите имя и расположение проекта, а затем нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="6edfc-116">In the **New Dynamic Web Project** dialog box, specify your project name and location, and then click **Finish**.</span></span>
   
   ![Указание имени проекта][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="6edfc-118">Создание реестра контейнеров Azure для использования в качестве частного реестра Docker</span><span class="sxs-lookup"><span data-stu-id="6edfc-118">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="6edfc-119">Ниже рассмотрена процедура использования портала Azure для создания реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="6edfc-119">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="6edfc-120">Если вы хотите использовать Azure CLI, а не портал Azure, выполните процедуру, описанную в статье [Создание частного реестра контейнеров Docker с помощью Azure CLI 2.0][Create Docker Registry using Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="6edfc-120">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="6edfc-121">Перейдите на [портал Azure] и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="6edfc-121">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="6edfc-122">После входа в свою учетную запись на портале Azure можно выполнить процедуру, описанную в статье [Создание частного реестра контейнеров Docker с помощью портала Azure], которую здесь полезно представить еще раз.</span><span class="sxs-lookup"><span data-stu-id="6edfc-122">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="6edfc-123">Щелкните значок меню **+ Создать ресурс**, а затем последовательно выберите **Контейнеры** и **Реестр контейнеров**.</span><span class="sxs-lookup"><span data-stu-id="6edfc-123">Click the menu icon for **+ Create a resource**, then click **Containers**, and then click **Container Registry**.</span></span>
   
   ![Создание нового реестра контейнеров Azure][create-container-registry-01]

1. <span data-ttu-id="6edfc-125">При появлении страницы **Создать реестр контейнеров** введите данные в поля **Имя реестра** и **Группа ресурсов**, выберите **Включить** для параметра **Пользователь-администратор** и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6edfc-125">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Настройка параметров реестра контейнеров Azure][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="6edfc-127">Развертывание веб-приложения в контейнере Docker</span><span class="sxs-lookup"><span data-stu-id="6edfc-127">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="6edfc-128">Щелкните правой кнопкой мыши проект в обозревателе проектов, выберите **Azure**, а затем — **Add Docker Support** (Добавление поддержки Docker).</span><span class="sxs-lookup"><span data-stu-id="6edfc-128">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="6edfc-129">Файл Docker будет автоматически создан с конфигурацией по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6edfc-129">This will automatically create a Docker file with a default configuration.</span></span>

   ![Добавление поддержки Docker][add-docker-support]

1. <span data-ttu-id="6edfc-131">После добавления поддержки Docker щелкните проект правой кнопкой мыши в обозревателе проектов, выберите **Azure**, а затем — **Publish to Web App for Containers** (Опубликовать в веб-приложении для контейнеров).</span><span class="sxs-lookup"><span data-stu-id="6edfc-131">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Publish to Web App for Containers**.</span></span>

   ![Публикация в веб-приложении для контейнеров][run-on-web-app-for-containers]

1. <span data-ttu-id="6edfc-133">Когда отобразится диалоговое окно **Run on Web App for Containers** (Выполнение в веб-приложении для контейнеров), введите необходимые сведения:</span><span class="sxs-lookup"><span data-stu-id="6edfc-133">When the **Run on Web App for Containers** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="6edfc-134">**Docker File** (Файл Docker). Путь к файлу Docker, который был создан при добавлении поддержки Docker к проекту.</span><span class="sxs-lookup"><span data-stu-id="6edfc-134">**Docker File**: This specifies the path to the Docker file that was created when you added Docker support to your project.</span></span> 

   * <span data-ttu-id="6edfc-135">**Container Registry** (Реестр контейнеров). Выберите в раскрывающемся меню реестр контейнеров, который вы создали в предыдущем разделе этой статьи.</span><span class="sxs-lookup"><span data-stu-id="6edfc-135">**Container Registry**: Choose the container registry from the drop-down menu that you created in the previous section of this article.</span></span> <span data-ttu-id="6edfc-136">Поля **Server URL** (URL-адрес сервера), **Username** (Имя пользователя) и **Password** (Пароль) будут заполнены автоматически.</span><span class="sxs-lookup"><span data-stu-id="6edfc-136">The fields for **Server URL**, **Username**, and **Password** will be automatically populated.</span></span>

   * <span data-ttu-id="6edfc-137">**Image and tag** (Образ и тег). Имя образа контейнера. Обычно используется следующий синтаксис: *registry*.azurecr.io/*appname*:latest, где:</span><span class="sxs-lookup"><span data-stu-id="6edfc-137">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="6edfc-138">*registry* — это реестр контейнеров из предыдущего раздела этой статьи;</span><span class="sxs-lookup"><span data-stu-id="6edfc-138">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="6edfc-139">*appname* — это имя веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6edfc-139">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="6edfc-140">**Web App for Container** (Веб-приложение для контейнера). Выберите **Use Existing** (Использовать существующее) или **Create New** (Создать), чтобы указать, будете ли вы развертывать контейнер в существующем веб-приложении или создадите новое.</span><span class="sxs-lookup"><span data-stu-id="6edfc-140">**Web App for Container**: Choose **Use Existing** or **Create New** to specify whether you will deploy your container to an existing web app or create a new web app.</span></span>  <span data-ttu-id="6edfc-141">С помощью указанного вами **имени приложения** будет создан URL-адрес для вашего веб-приложения, например: *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="6edfc-141">The **App name** that you specify will create the URL for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   * <span data-ttu-id="6edfc-142">**Группа ресурсов**. Указывает, создадите ли вы группу ресурсов или будете использовать существующую.</span><span class="sxs-lookup"><span data-stu-id="6edfc-142">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="6edfc-143">**App Service Plan** (План службы приложений). Указывает, создадите ли вы план службы приложений или будете использовать существующий.</span><span class="sxs-lookup"><span data-stu-id="6edfc-143">**App Service Plan**: Specifies whether you will use an existing or create a new app service plan.</span></span> 

   ![Выполнение в веб-приложении для контейнеров][run-on-web-app-linux]

1. <span data-ttu-id="6edfc-145">Настроив перечисленные выше параметры, нажмите кнопку **OK**, чтобы опубликовать свое веб-приложение в Azure.</span><span class="sxs-lookup"><span data-stu-id="6edfc-145">When you have finished configuring the settings listed above, click **OK** to publish your web app to Azure.</span></span>

1. <span data-ttu-id="6edfc-146">После публикации веб-приложения вы можете перейти к указанному для него ранее URL-адресу, например *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="6edfc-146">After your web app has been published, you can browse to the URL that specifed earlier for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   ![Переход к веб-приложению][browsing-to-web-app]

## <a name="next-steps"></a><span data-ttu-id="6edfc-148">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="6edfc-148">Next steps</span></span>

<span data-ttu-id="6edfc-149">Дополнительные материалы по Docker доступны на официальном [веб-сайте Docker][Docker].</span><span class="sxs-lookup"><span data-stu-id="6edfc-149">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

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

[add-docker-support]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-eclipse-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/file-new-project.png
[project-name]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-linux.png
