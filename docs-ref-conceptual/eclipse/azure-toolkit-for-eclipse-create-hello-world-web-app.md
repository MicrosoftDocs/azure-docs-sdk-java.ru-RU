---
title: Создание веб-приложения Hello World для Azure в Eclipse
description: В этом учебнике показано, как с помощью набора средств Azure для Eclipse создать веб-приложение Hello World для Azure.
services: app-service
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
ms.openlocfilehash: c98f966eb17e3fbde877451c8f8fefb21e6bf686
ms.sourcegitcommit: dca98b953fa3149fb2e6aa49e27e843b6df0c6c2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57786893"
---
# <a name="create-a-hello-world-web-app-for-azure-using-eclipse"></a><span data-ttu-id="e1a13-103">Создание веб-приложения Hello World для Azure в Eclipse</span><span class="sxs-lookup"><span data-stu-id="e1a13-103">Create a Hello World web app for Azure using Eclipse</span></span>

<span data-ttu-id="e1a13-104">В этом руководстве показано, как создать базовое приложение Hello World для Azure и развернуть его как веб-приложение с помощью [Набор средств Azure для Eclipse].</span><span class="sxs-lookup"><span data-stu-id="e1a13-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for Eclipse].</span></span>

> [!NOTE]
>
> <span data-ttu-id="e1a13-105">Дополнительные сведения о версии, в которой используются [Набор средств Azure для IntelliJ], см. в статье [Создание веб-приложения Azure (цен. категория "Базовый") с помощью IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="e1a13-105">For a version of this article that uses the [Azure Toolkit for IntelliJ], see [Create a Hello World web app for Azure using IntelliJ][intellij-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="e1a13-106">Набор средств Azure для Eclipse обновлен в августе 2017 года. В него добавлен другой рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="e1a13-106">The Azure Toolkit for Eclipse was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="e1a13-107">В этой статье описывается, как создать веб-приложение Hello World с помощью набора средств Azure для Eclipse версии 3.0.7 (или более поздней).</span><span class="sxs-lookup"><span data-stu-id="e1a13-107">This article illustrates creating a Hello World web app by using version 3.0.7 (or later) of the Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="e1a13-108">Если вы используете набор средств версии 3.0.6 (или более ранней), необходимо выполнить действия, описанные в руководстве по [созданию веб-приложения Hello World для Azure в Eclipse с помощью набора средств предыдущих версий][Legacy Version].</span><span class="sxs-lookup"><span data-stu-id="e1a13-108">If you are using the version 3.0.6 (or earlier) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in Eclipse using the legacy toolkit][Legacy Version].</span></span>
> 

<span data-ttu-id="e1a13-109">После завершения этого учебника приложение при просмотре в веб-браузере будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e1a13-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Предварительный просмотр приложения Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="e1a13-111">Создание проекта веб-приложения</span><span class="sxs-lookup"><span data-stu-id="e1a13-111">Create a new web app project</span></span>

1. <span data-ttu-id="e1a13-112">Запустите Eclipse и войдите в учетную запись Azure, следуя инструкциям из статьи [Инструкции по входу для набора средств Azure для Eclipse][eclipse-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="e1a13-112">Start Eclipse, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="e1a13-113">Выберите **File** (Файл), **New** (Создать), а затем — **Dynamic Web Project** (Динамический веб-проект).</span><span class="sxs-lookup"><span data-stu-id="e1a13-113">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="e1a13-114">(Если элемента **Динамический веб-проект** нет в списке доступных проектов после выбора пунктов **Файл** и **Создать**, сделайте следующее: последовательно щелкните **Файл**, **Создать**, **Проект...**, разверните узел **Интернет**, щелкните **Dynamic Web Project** (Динамический веб-проект) и нажмите кнопку **Далее**.)</span><span class="sxs-lookup"><span data-stu-id="e1a13-114">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

   ![Создание динамического веб-проекта][file-new-dynamic-web-project]

2. <span data-ttu-id="e1a13-116">Для целей данного учебника присвойте проекту имя **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="e1a13-116">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="e1a13-117">Экран будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e1a13-117">Your screen will appear similar to the following:</span></span>
   
   ![Свойства нового динамического веб-проекта][dynamic-web-project-properties]

3. <span data-ttu-id="e1a13-119">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="e1a13-119">Click **Finish**.</span></span>

4. <span data-ttu-id="e1a13-120">В представлении обозревателя проектов в Eclipse разверните узел **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="e1a13-120">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="e1a13-121">Щелкните правой кнопкой мыши **WebContent**, выберите **Создать**, затем щелкните **JSP File** (JSP-файл).</span><span class="sxs-lookup"><span data-stu-id="e1a13-121">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

   ![Создание файла JSP][create-new-jsp-file]

5. <span data-ttu-id="e1a13-123">В диалоговом окне **New JSP File** (Новый JSP-файл) укажите имя файла **index.jsp**, оставьте родительскую папку **MyWebApp/WebContent** без изменений, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e1a13-123">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

   ![Диалоговое окно New JSP File (Создание JSP-файла)][new-jsp-file-dialog]

6. <span data-ttu-id="e1a13-125">Для нашего примера в диалоговом окне **Select JSP Template** (Выбор шаблона JSP) щелкните **New JSP File (html)** (Создать JSP-файл (html)) и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e1a13-125">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

   ![Выбор шаблона JSP][select-jsp-template]

7. <span data-ttu-id="e1a13-127">При открытии в Eclipse файла index.jsp добавьте код для динамического отображения фразы **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="e1a13-127">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="e1a13-128">в существующий элемент `<body>`.</span><span class="sxs-lookup"><span data-stu-id="e1a13-128">within the existing `<body>` element.</span></span> <span data-ttu-id="e1a13-129">Обновленное содержимое элемента `<body>` должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="e1a13-129">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="e1a13-130">Сохраните index.jsp.</span><span class="sxs-lookup"><span data-stu-id="e1a13-130">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="e1a13-131">Развертывание веб-приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="e1a13-131">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="e1a13-132">В представлении обозревателя проектов Eclipse щелкните правой кнопкой мыши проект, выберите **Azure**, а затем — **Publish as Azure Web App** (Опубликовать как веб-приложение Azure).</span><span class="sxs-lookup"><span data-stu-id="e1a13-132">Within Eclipse's Project Explorer view, right-click your project, choose **Azure**, and then choose **Publish as Azure Web App**.</span></span>
   
   ![Опубликовать как веб-приложение Azure][publish-as-azure-web-app]

1. <span data-ttu-id="e1a13-134">В диалоговом окне **Deploy Web App** (Развертывание веб-приложения) можно выбрать один из следующих вариантов:</span><span class="sxs-lookup"><span data-stu-id="e1a13-134">When the **Deploy Web App** dialog box appears, you can choose one of the following options:</span></span>

   * <span data-ttu-id="e1a13-135">Выберите существующее веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="e1a13-135">Select an existing web app if one exists.</span></span>

      ![Выбор службы приложения][select-app-service]

   * <span data-ttu-id="e1a13-137">Щелкните **Create New Web App** (Создать веб-приложение).</span><span class="sxs-lookup"><span data-stu-id="e1a13-137">Click **Create New Web App**.</span></span>

      ![Создание службы приложений][create-app-service]

      <span data-ttu-id="e1a13-139">В диалоговом окне **Create App Service** (Создание службы приложений) укажите требуемую информацию для веб-приложения и нажмите кнопку **Create** (Создать).</span><span class="sxs-lookup"><span data-stu-id="e1a13-139">Specify the requisite information for your web app in the **Create App Service** dialog box, and then click **Create**.</span></span>

      <span data-ttu-id="e1a13-140">Здесь вы можете настроить среду выполнения, параметры приложения, план службы и группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e1a13-140">Here you can configure the runtime environment, app settings, service plan and resource group.</span></span>

      ![Диалоговое окно "Создание службы приложений"][create-app-service-dialog]

1. <span data-ttu-id="e1a13-142">Выберите веб-приложение и щелкните **Deploy** (Развернуть).</span><span class="sxs-lookup"><span data-stu-id="e1a13-142">Select your web app and then click **Deploy**.</span></span>

   ![Развертывание службы приложений][deploy-app-service]

1. <span data-ttu-id="e1a13-144">Набор средств отобразит сообщение о состоянии (**Опубликовано**) на вкладке **Журнал действий Azure** при успешном развертывании веб-приложения, где будет содержаться гиперссылка с URL-адресом развернутого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e1a13-144">The toolkit will display a **Published** status under the **Azure Activity Log** tab when it has successfully deployed your web app, which is a hyperlink for the URL of your deployed web app.</span></span>

   ![Состояние публикации][publish-status]

1. <span data-ttu-id="e1a13-146">Перейти к своему веб-приложению можно с помощью ссылки, предоставленной в сообщении о состоянии.</span><span class="sxs-lookup"><span data-stu-id="e1a13-146">You can browse to your web app using the link provided in the status message.</span></span>

   ![Просмотр веб-приложения][browse-web-app]

1. <span data-ttu-id="e1a13-148">Опубликовав веб-сайт в Azure, вы можете управлять им, щелкнув его правой кнопкой мыши и выбрав один из параметров контекстного меню.</span><span class="sxs-lookup"><span data-stu-id="e1a13-148">After you have published your web to Azure, you can manage your app by right-clicking on it and selecting one of the options on the context menu.</span></span> <span data-ttu-id="e1a13-149">Например, вы можете **запустить**, **остановить** или **удалить** веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="e1a13-149">For example, you can **Start**, **Stop**, or **Delete** your web app.</span></span>

   ![Управление службой приложений][manage-app-service]

## <a name="next-steps"></a><span data-ttu-id="e1a13-151">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="e1a13-151">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="e1a13-152">Дополнительные сведения о создании веб-приложений Azure см. в разделе [Обзор веб-приложений].</span><span class="sxs-lookup"><span data-stu-id="e1a13-152">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Набор средств Azure для Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Обзор веб-приложений]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->

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
