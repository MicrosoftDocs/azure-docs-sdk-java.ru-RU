---
title: Создание веб-приложения Hello World для Службы приложений Azure с помощью Eclipse
description: В этом учебнике показано, как с помощью набора средств Azure для Eclipse создать веб-приложение Hello World для Azure.
services: app-service
keywords: java, eclipse, web app, azure app service, hello world, quick start
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 7e88298afaf0b4601d85d6063b7096c79e677421
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65625862"
---
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-eclipse"></a><span data-ttu-id="ce6db-104">Создание веб-приложения Hello World для Службы приложений Azure с помощью Eclipse</span><span class="sxs-lookup"><span data-stu-id="ce6db-104">Create a Hello World web app for Azure App Service using Eclipse</span></span>

<span data-ttu-id="ce6db-105">С помощью модуля с открытым кодом [Azure Toolkit for Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse) всего за несколько минут можно создать и развернуть в Службе приложений Azure базовое приложение Hello World в качестве веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ce6db-105">Using open sourced [Azure Toolkit for Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse) plugin, creating and deploying a basic Hello World application to Azure App Service as a web app can be done in a few minutes.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ce6db-106">Если вы предпочитаете использовать IntelliJ IDEA, ознакомьтесь с нашим [аналогичным учебником для IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="ce6db-106">If you prefer using IntelliJ IDEA, check out our [similar tutorial for IntelliJ][intellij-hello-world].</span></span>
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> <span data-ttu-id="ce6db-107">Обязательно очистите ресурсы после выполнения действий из этого учебника.</span><span class="sxs-lookup"><span data-stu-id="ce6db-107">Don't forget to clean up the resources after you complete this tutorial.</span></span> <span data-ttu-id="ce6db-108">В этом случае работа с этим учебником не приведет к превышению квоты бесплатной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ce6db-108">In that case, running this guide will not exceed your free account quota.</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a><span data-ttu-id="ce6db-109">Установка и вход</span><span class="sxs-lookup"><span data-stu-id="ce6db-109">Installation and sign-in</span></span>

1. <span data-ttu-id="ce6db-110">Перетащите следующую кнопку в запущенную рабочую область Eclipse, чтобы установить подключаемый модуль Azure Toolkit for Eclipse ([другие варианты установки](azure-toolkit-for-eclipse-installation.md)).</span><span class="sxs-lookup"><span data-stu-id="ce6db-110">Drag the following button to your running Eclipse workspace to install the Azure Toolkit for Eclipse plugin ([other installation options](azure-toolkit-for-eclipse-installation.md)).</span></span>

    <span data-ttu-id="ce6db-111">[![Перетащите в запущенную рабочую область Eclipse*. * Требуется клиент Eclipse Marketplace](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Перетащите в запущенную рабочую область Eclipse*. * Требуется клиент Eclipse Marketplace")</span><span class="sxs-lookup"><span data-stu-id="ce6db-111">[![Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client")</span></span>

1. <span data-ttu-id="ce6db-112">Чтобы войти в учетную запись Azure, щелкните **Tools** (Средства), выберите **Azure** и **Sign In** (Вход).</span><span class="sxs-lookup"><span data-stu-id="ce6db-112">To sign in to your Azure account, click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="ce6db-113">![Меню Eclipse для входа в систему Azure][I01]</span><span class="sxs-lookup"><span data-stu-id="ce6db-113">![Eclipse Menu for Azure Sign In][I01]</span></span>

1. <span data-ttu-id="ce6db-114">В окне **Azure Sign In** (Вход в Azure) выберите **Device Login** (Имя пользователя устройства) и щелкните **Sign in** (Вход) ([другие варианты входа](azure-toolkit-for-eclipse-sign-in-instructions.md)).</span><span class="sxs-lookup"><span data-stu-id="ce6db-114">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in** ([other sign-in options](azure-toolkit-for-eclipse-sign-in-instructions.md)).</span></span>

   ![Окно Azure Sign In (Вход в Azure) с выбранным именем пользователя устройства][I02]

1. <span data-ttu-id="ce6db-116">В диалоговом окне **Azure Device Login** (Вход в систему устройства Azure) щелкните **Copy&Open** (Копировать и открыть).</span><span class="sxs-lookup"><span data-stu-id="ce6db-116">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![Диалоговое окно входа Azure][I03]

1. <span data-ttu-id="ce6db-118">В браузере вставьте код устройства (скопированный при нажатии **Copy&Open** (Копировать и открыть) на последнем шаге), а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ce6db-118">In the browser, paste your device code (which has been copied when you clicked **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Вход в систему устройства в браузере][I04]

1. <span data-ttu-id="ce6db-120">Наконец, в диалоговом окне **Select Subscriptions** (Выбор подписок) выберите нужные подписки и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ce6db-120">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][I05]

## <a name="creating-web-app-project"></a><span data-ttu-id="ce6db-122">Создание проекта веб-приложения</span><span class="sxs-lookup"><span data-stu-id="ce6db-122">Creating web app project</span></span>

1. <span data-ttu-id="ce6db-123">Выберите **File** (Файл), **New** (Создать), а затем — **Dynamic Web Project** (Динамический веб-проект).</span><span class="sxs-lookup"><span data-stu-id="ce6db-123">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="ce6db-124">(Если элемента **Динамический веб-проект** нет в списке доступных проектов после выбора пунктов **Файл** и **Создать**, сделайте следующее: последовательно щелкните **Файл**, **Создать**, **Проект...** , разверните узел **Интернет**, щелкните **Dynamic Web Project** (Динамический веб-проект) и нажмите кнопку **Далее**.)</span><span class="sxs-lookup"><span data-stu-id="ce6db-124">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

   ![Создание динамического веб-проекта][file-new-dynamic-web-project]

2. <span data-ttu-id="ce6db-126">Для целей данного учебника присвойте проекту имя **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="ce6db-126">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="ce6db-127">Экран будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ce6db-127">Your screen will appear similar to the following:</span></span>
   
   ![Свойства нового динамического веб-проекта][dynamic-web-project-properties]

3. <span data-ttu-id="ce6db-129">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="ce6db-129">Click **Finish**.</span></span>

4. <span data-ttu-id="ce6db-130">В представлении обозревателя проектов в Eclipse разверните узел **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="ce6db-130">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="ce6db-131">Щелкните правой кнопкой мыши **WebContent**, выберите **Создать**, затем щелкните **JSP File** (JSP-файл).</span><span class="sxs-lookup"><span data-stu-id="ce6db-131">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

   ![Создание файла JSP][create-new-jsp-file]

5. <span data-ttu-id="ce6db-133">В диалоговом окне **New JSP File** (Новый JSP-файл) укажите имя файла **index.jsp**, оставьте родительскую папку **MyWebApp/WebContent** без изменений, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ce6db-133">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

   ![Диалоговое окно New JSP File (Создание JSP-файла)][new-jsp-file-dialog]

6. <span data-ttu-id="ce6db-135">Для нашего примера в диалоговом окне **Select JSP Template** (Выбор шаблона JSP) щелкните **New JSP File (html)** (Создать JSP-файл (html)) и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="ce6db-135">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

   ![Выбор шаблона JSP][select-jsp-template]

7. <span data-ttu-id="ce6db-137">При открытии в Eclipse файла index.jsp добавьте код для динамического отображения фразы **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="ce6db-137">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="ce6db-138">в существующий элемент `<body>`.</span><span class="sxs-lookup"><span data-stu-id="ce6db-138">within the existing `<body>` element.</span></span> <span data-ttu-id="ce6db-139">Обновленное содержимое элемента `<body>` должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="ce6db-139">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="ce6db-140">Сохраните index.jsp.</span><span class="sxs-lookup"><span data-stu-id="ce6db-140">Save index.jsp.</span></span>

## <a name="deploying-web-app-to-azure"></a><span data-ttu-id="ce6db-141">Развертывание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="ce6db-141">Deploying web app to Azure</span></span>

1. <span data-ttu-id="ce6db-142">В представлении обозревателя проектов Eclipse щелкните правой кнопкой мыши проект, выберите **Azure**, а затем — **Publish as Azure Web App** (Опубликовать как веб-приложение Azure).</span><span class="sxs-lookup"><span data-stu-id="ce6db-142">Within Eclipse's Project Explorer view, right-click your project, choose **Azure**, and then choose **Publish as Azure Web App**.</span></span>
   
   ![Опубликовать как веб-приложение Azure][publish-as-azure-web-app]

1. <span data-ttu-id="ce6db-144">В диалоговом окне **Deploy Web App** (Развертывание веб-приложения) можно выбрать один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="ce6db-144">When the **Deploy Web App** dialog box appears, you can choose one of the following options:</span></span>

   * <span data-ttu-id="ce6db-145">Выберите существующее веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="ce6db-145">Select an existing web app if one exists.</span></span>

      ![Выбор службы приложения][select-app-service]

   * <span data-ttu-id="ce6db-147">Щелкните **Create New Web App** (Создать веб-приложение).</span><span class="sxs-lookup"><span data-stu-id="ce6db-147">Click **Create New Web App**.</span></span>

      ![Создание службы приложений][create-app-service]

      <span data-ttu-id="ce6db-149">В диалоговом окне **Create App Service** (Создание службы приложений) укажите требуемую информацию для веб-приложения и нажмите кнопку **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="ce6db-149">Specify the requisite information for your web app in the **Create App Service** dialog box, and then click **Create**.</span></span>

      <span data-ttu-id="ce6db-150">Здесь вы можете настроить среду выполнения, параметры приложения, план службы и группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ce6db-150">Here you can configure the runtime environment, app settings, service plan and resource group.</span></span>

      ![Диалоговое окно "Создание службы приложений"][create-app-service-dialog]

1. <span data-ttu-id="ce6db-152">Выберите веб-приложение и щелкните **Deploy** (Развернуть).</span><span class="sxs-lookup"><span data-stu-id="ce6db-152">Select your web app and then click **Deploy**.</span></span>

   ![Развертывание службы приложений][deploy-app-service]

1. <span data-ttu-id="ce6db-154">Набор средств отобразит сообщение о состоянии (**Опубликовано**) на вкладке **Журнал действий Azure** при успешном развертывании веб-приложения, где будет содержаться гиперссылка с URL-адресом развернутого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="ce6db-154">The toolkit will display a **Published** status under the **Azure Activity Log** tab when it has successfully deployed your web app, which is a hyperlink for the URL of your deployed web app.</span></span>

   ![Состояние публикации][publish-status]

1. <span data-ttu-id="ce6db-156">Перейти к своему веб-приложению можно с помощью ссылки, предоставленной в сообщении о состоянии.</span><span class="sxs-lookup"><span data-stu-id="ce6db-156">You can browse to your web app using the link provided in the status message.</span></span>

   ![Просмотр веб-приложения][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="cleaning-up-resources"></a><span data-ttu-id="ce6db-158">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="ce6db-158">Cleaning up resources</span></span>

1. <span data-ttu-id="ce6db-159">Опубликовав веб-приложение в Azure, вы можете управлять им, щелкнув его правой кнопкой мыши в Azure Explorer и выбрав один из параметров контекстного меню.</span><span class="sxs-lookup"><span data-stu-id="ce6db-159">After you have published your web app to Azure, you can manage it by right-clicking in Azure Explorer and selecting one of the options in the context menu.</span></span> <span data-ttu-id="ce6db-160">Например, вы можете **удалить** веб-приложение здесь, чтобы очистить ресурс для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="ce6db-160">For example, you can **Delete** your web app here to clean up the resource for this tutorial.</span></span>

   ![Управление службой приложений][manage-app-service]

## <a name="next-steps"></a><span data-ttu-id="ce6db-162">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="ce6db-162">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="ce6db-163">Дополнительные сведения о создании веб-приложений Azure см. в разделе [Обзор веб-приложений].</span><span class="sxs-lookup"><span data-stu-id="ce6db-163">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Обзор веб-приложений]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->
[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

[browse-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/browse-web-app.png
[file-new-dynamic-web-project]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/file-new-dynamic-web-project.png
[dynamic-web-project-properties]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/dynamic-web-project-properties.png
[create-new-jsp-file]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-new-jsp-file.png
[new-jsp-file-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/new-jsp-file-dialog.png
[select-jsp-template]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-jsp-template.png
[publish-as-azure-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-as-azure-web-app.png
[deploy-web-app-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-web-app-dialog.png
[select-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-app-service.png
[create-app-service-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service-dialog.png
[publish-status]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-status.png
[create-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service.png
[deploy-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-app-service.png
[manage-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/manage-app-service.png
