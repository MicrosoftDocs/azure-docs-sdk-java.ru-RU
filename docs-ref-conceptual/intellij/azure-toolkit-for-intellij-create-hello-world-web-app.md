---
title: Создание веб-приложения Hello World для Службы приложений Azure с помощью IntelliJ
description: В этом учебнике показано, как с помощью набора средств Azure для IntelliJ создать веб-приложение Hello World для Azure.
services: app-service
keywords: java, intellij, web app, azure app service, hello world, quick start
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: ae0749ce1ddab971f1a83e2e5e58492fd8ccb287
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/15/2019
ms.locfileid: "65626102"
---
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-intellij"></a><span data-ttu-id="b400f-104">Создание веб-приложения Hello World для Службы приложений Azure с помощью IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b400f-104">Create a Hello World web app for Azure App Service using IntelliJ</span></span>

<span data-ttu-id="b400f-105">С помощью подключаемого модуля с открытым кодом [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) всего за несколько минут можно создать и развернуть в Службе приложений Azure базовое приложение Hello World в качестве веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b400f-105">Using open sourced [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) plugin, creating and deploying a basic Hello World application to Azure App Service as a web app can be done in a few minutes.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b400f-106">Если вы предпочитаете использовать Eclipse, ознакомьтесь с нашим [аналогичным учебником для Eclipse][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="b400f-106">If you prefer using Eclipse, check out our [similar tutorial for Eclipse][eclipse-hello-world].</span></span>
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> <span data-ttu-id="b400f-107">Обязательно очистите ресурсы после выполнения действий из этого учебника.</span><span class="sxs-lookup"><span data-stu-id="b400f-107">Don't forget to clean up the resources after you complete this tutorial.</span></span> <span data-ttu-id="b400f-108">В этом случае работа с этим учебником не приведет к превышению квоты бесплатной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b400f-108">In that case, running this guide will not exceed your free account quota.</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-intellij-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a><span data-ttu-id="b400f-109">Установка и вход</span><span class="sxs-lookup"><span data-stu-id="b400f-109">Installation and Sign-in</span></span>

1. <span data-ttu-id="b400f-110">В диалоговом окне Settings/Preferences (Параметры и предпочтения) в IntelliJ IDEA (CTRL+ALT+S) выберите **Plugins** (Подключаемые модули).</span><span class="sxs-lookup"><span data-stu-id="b400f-110">In IntelliJ IDEA's Settings/Preferences dialog (Ctrl+Alt+S), select **Plugins**.</span></span> <span data-ttu-id="b400f-111">Затем найдите модуль **Azure Toolkit for IntelliJ** в **Marketplace** и щелкните **Install** (Установить).</span><span class="sxs-lookup"><span data-stu-id="b400f-111">Then, find the **Azure Toolkit for IntelliJ** in the **Marketplace** and click **Install**.</span></span> <span data-ttu-id="b400f-112">После установки щелкните **Restart** (Перезапуск), чтобы активировать подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="b400f-112">After installed, click **Restart** to activate the plugin.</span></span> 

   ![Подключаемый модуль Azure Toolkit for IntelliJ в Marketplace][marketplace]

2. <span data-ttu-id="b400f-114">Чтобы войти в учетную запись Azure, откройте боковую панель **Azure Explorer**, а затем щелкните значок **Azure Sign In** (Вход в Azure) в верхней строке (или в меню IDEA **Tools/Azure/Azure Sign in** (Средства/Azure/Вход в Azure)).</span><span class="sxs-lookup"><span data-stu-id="b400f-114">To sign in to your Azure account, open sidebar **Azure Explorer**, and then click the **Azure Sign In** icon in the bar on top (or from IDEA menu **Tools/Azure/Azure Sign in**).</span></span>

   ![Команда Azure Sign In (Вход в Azure) в IntelliJ][I01]

3. <span data-ttu-id="b400f-116">В окне **Azure Sign In** (Вход в Azure) выберите **Device Login** (Имя пользователя устройства) и щелкните **Sign in** (Вход) ([другие варианты входа](azure-toolkit-for-intellij-sign-in-instructions.md)).</span><span class="sxs-lookup"><span data-stu-id="b400f-116">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in** ([other sign in options](azure-toolkit-for-intellij-sign-in-instructions.md)).</span></span>

   ![Окно Azure Sign In (Вход в Azure) с выбранным именем пользователя устройства][I02]

4. <span data-ttu-id="b400f-118">В диалоговом окне **Azure Device Login** (Вход в систему устройства Azure) щелкните **Copy&Open** (Копировать и открыть).</span><span class="sxs-lookup"><span data-stu-id="b400f-118">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![Диалоговое окно входа Azure][I03]

5. <span data-ttu-id="b400f-120">В браузере вставьте код устройства (скопированный при нажатии **Copy&Open** (Копировать и открыть) на последнем шаге), а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b400f-120">In the browser, paste your device code (which has been copied when you click **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Вход в систему устройства в браузере][I04]

6. <span data-ttu-id="b400f-122">В диалоговом окне **Select Subscriptions** (Выбор подписок) выберите нужные подписки и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b400f-122">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Диалоговое окно выбора подписок][I05]

## <a name="creating-web-app-project"></a><span data-ttu-id="b400f-124">Создание проекта веб-приложения</span><span class="sxs-lookup"><span data-stu-id="b400f-124">Creating web app project</span></span>

1. <span data-ttu-id="b400f-125">В IntelliJ щелкните меню **File** (Файл), выберите команду **New** (Создать), а затем — **Project** (Проект).</span><span class="sxs-lookup"><span data-stu-id="b400f-125">In IntelliJ, click the **File** menu, then click **New**, and then click **Project**.</span></span>

   ![Создание проекта][file-new-project]

2. <span data-ttu-id="b400f-127">В диалоговом окне **New Project** (Новый проект) выберите **Maven**, а затем **maven-archetype-webapp** и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="b400f-127">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>

   ![Выбор веб-приложения архетипа Maven][maven-archetype-webapp]

3. <span data-ttu-id="b400f-129">Укажите значение **GroupId** (Идентификатор группы) и **ArtifactId** (Идентификатор артефакта) для веб-приложения и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="b400f-129">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>

   ![Указание идентификатора группы и артефакта][groupid-and-artifactid]

4. <span data-ttu-id="b400f-131">Настройте любые параметры Maven или примите значения по умолчанию и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="b400f-131">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>

   ![Указание параметров Maven][maven-options]

5. <span data-ttu-id="b400f-133">Укажите имя и расположение проекта, а затем щелкните **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="b400f-133">Specify your project name and location, and then click **Finish**.</span></span>

   ![Указание имени проекта][project-name]

6. <span data-ttu-id="b400f-135">В представлении обозревателя проектов откройте и измените файл **src/main/webapp/index.jsp** следующим образом и **сохраните изменения**:</span><span class="sxs-lookup"><span data-stu-id="b400f-135">Under Project Explorer view, open and edit the file **src/main/webapp/index.jsp** as following and **save the changes**:</span></span>

   ```html
   <html>
    <body>
      <b><% out.println("Hello World!"); %></b>
    </body>
   </html>
   ```

   ![Изменение страницы индексов][edit-index-page]

## <a name="deploying-web-app-to-azure"></a><span data-ttu-id="b400f-137">Развертывание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="b400f-137">Deploying web app to Azure</span></span>

1. <span data-ttu-id="b400f-138">В представлении обозревателя проектов щелкните проект правой кнопкой мыши, разверните **Azure** и щелкните **Deploy to Azure** (Развертывание в Azure).</span><span class="sxs-lookup"><span data-stu-id="b400f-138">Under Project Explorer view, right-click your project, expand **Azure**, then click **Deploy to Azure**.</span></span>

   ![Меню развертывания в Azure][deploy-to-azure-menu]

1. <span data-ttu-id="b400f-140">В диалоговом окне развертывания в Azure вы можете напрямую развернуть приложение в существующее веб-приложение Tomcat, если оно у вас есть. В противном случае необходимо создать такое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="b400f-140">In the Deploy to Azure dialog box, you can directly deploy the application to an existing Tomcat webapp if you already have one, otherwise you should create a new one first.</span></span>
   1. <span data-ttu-id="b400f-141">Щелкните ссылку **No Available webapp, click to create a new one** (Нет доступного веб-приложения. Щелкните, чтобы создать), чтобы создать веб-приложение. Если в подписке уже есть веб-приложения, можно выбрать **Create New WebApp** (Создать веб-приложение) из раскрывающегося списка веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="b400f-141">Click the link **No Available webapp, click to create a new one** to crete a new web app, you could choose **Create New WebApp** from WebApp dropdown if there are existing webapps in your subscription.</span></span>

      ![Диалоговое окно развертывания в Azure][deploy-to-azure-dialog]

   1. <span data-ttu-id="b400f-143">Во всплывающем диалоговом окне выберите **TOMCAT 8.5-jre8** как веб-контейнер и укажите другие необходимые сведения, а затем нажмите кнопку **ОК**, чтобы создать веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="b400f-143">In the pop-up dialog box, chose **TOMCAT 8.5-jre8** as Web Container and specify other required information, then click **OK** to create the webapp.</span></span>

      ![Создание веб-приложения][create-new-web-app-dialog]

   1. <span data-ttu-id="b400f-145">Выберите веб-приложение из раскрывающегося списка веб-приложений, а затем щелкните **Run** (Запуск). (Вы можете выполнить запуск отсюда, если хотите выполнить развертывание в существующее веб-приложение.)</span><span class="sxs-lookup"><span data-stu-id="b400f-145">Choose the web app from WebApp drop down, and then click **Run**.(You could start from here if you want deploy to an existing webapp)</span></span>

      ![Развертывание в существующее веб-приложение][deploy-to-existing-webapp]

1. <span data-ttu-id="b400f-147">Набор средств отобразит сообщение о состоянии при успешном развертывании веб-приложения, а также URL-адрес развернутого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="b400f-147">The toolkit will display a status message when it has successfully deployed your web app, along with the URL of your deployed web app if succeed.</span></span>

   ![Развертывание завершено успешно][successfully-deployed]

1. <span data-ttu-id="b400f-149">Перейти к своему веб-приложению можно с помощью ссылки, предоставленной в сообщении о состоянии.</span><span class="sxs-lookup"><span data-stu-id="b400f-149">You can browse to your web app using the link provided in the status message.</span></span>

   ![Просмотр веб-приложения][browse-web-app]

## <a name="managing-deploy-configurations"></a><span data-ttu-id="b400f-151">Управление конфигурациями развертывания</span><span class="sxs-lookup"><span data-stu-id="b400f-151">Managing deploy configurations</span></span>

1. <span data-ttu-id="b400f-152">После публикации веб-приложения параметры будут сохранены в качестве параметров по умолчанию. Развертывание можно запустить, щелкнув значок зеленой стрелки на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="b400f-152">After you have published your web app, your settings will be saved as the default, and you can run the deployment by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="b400f-153">Вы можете изменить параметры, щелкнув раскрывающееся меню для веб-приложения, а затем — **Edit Configurations** (Изменить конфигурации).</span><span class="sxs-lookup"><span data-stu-id="b400f-153">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Пункт меню Edit configuration (Изменить конфигурацию)][edit-configuration-menu]

1. <span data-ttu-id="b400f-155">При отображении диалогового окна **Run/Debug Configurations** (Конфигурации выполнения и отладки) можно изменить любые параметры по умолчанию, а затем нажать кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b400f-155">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Диалоговое окно Edit configuration (Изменение конфигурации)][edit-configuration-dialog]

## <a name="cleaning-up-resources"></a><span data-ttu-id="b400f-157">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="b400f-157">Cleaning up resources</span></span>

1. <span data-ttu-id="b400f-158">Удаление веб-приложений в Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="b400f-158">Deleting Web Apps in Azure Explorer</span></span>

     ![Очистка ресурсов][clean-resources]

## <a name="next-steps"></a><span data-ttu-id="b400f-160">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="b400f-160">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="b400f-161">Дополнительные сведения о создании веб-приложений Azure см. в разделе [Обзор веб-приложений].</span><span class="sxs-lookup"><span data-stu-id="b400f-161">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Обзор веб-приложений]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->
[marketplace]:./media/azure-toolkit-for-intellij-create-hello-world-web-app/marketplace.png
[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[deploy-to-azure-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[deploy-to-azure-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[deploy-to-existing-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/deploy-to-existing-webapp.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
[clean-resources]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/clean-resource.png
[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-intellij-sign-in-instructions/I05.png
